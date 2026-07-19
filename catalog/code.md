# Code slop catalog

Phase 3 raw material for the code surface: tells mined from six vetted phase 2 sources plus field observations from working with generated code directly, each with one bad and one good example. This feeds the phase 4 rule distillation, and the bad/good pairs double as phase 6 eval fixtures. Evidence quality varies widely here, from a 623-million-commit industry dataset down to a single maintainer's annotated bug reports, so check the Sources line on an entry before treating it as gospel.

Sources mined:
- gitclear: GitClear Maintainability Gap 2026
- ai-smells: AI-Generated Smells (Zhu, Tsantalis, Rigby, 2026)
- curl-slop: Death by a thousand slops (Stenberg, curl, 2025)
- anti-slop-action: peakoss/anti-slop GitHub Action
- test-slop: AI-Generated Tests are Lying to You (Adamo, 2025)
- osmani-review: AI writes code faster; prove it works (Osmani, 2026)

Tags: scope is always (wrong wherever it appears) or contextual (a tell as an unmotivated default or in aggregate); currency is current (typical of 2025-2026 models) or fading (mostly 2023-2024 era, rarer now).

Two notes on what didn't make the cut. anti-slop-action ships 34 checks, but most of them (source branch, account age, fork rate, profile completeness, merge ratio, spam usernames, blocked commit authors, and every commit-message and PR-description rule) gate contributor trustworthiness or git/PR metadata, not generated content; the project's plan explicitly puts commits and PR descriptions out of scope for now, and account signals were never in scope. Only the three checks that measure the shape of a diff or its comments survive into this catalog. Separately, ai-smells flags its own Feature Envy and Shotgun Surgery detectors as noisy, producing false positives on ordinary code (including Python's built-in `range()`), so those two smells are mentioned as caveats below rather than cataloged as reliable tells, and its Temporal Field finding describes something absent from AI output, not a slop pattern, so it is left out entirely. Its Lack of Cohesion finding (classes whose methods share little semantic unity) isn't excluded, just folded into "Branchy methods and god classes" below as a further symptom of the same God Class Syndrome, since the paper reports it at lower frequency than the other structural smells and doesn't treat it as a distinct pattern.

## Duplication and the shape of change

### Duplication over reuse

Tags: contextual, current. Sources: gitclear, ai-smells, osmani-review, own.

GitClear's 623-million-commit dataset shows duplicated code blocks up 81% since 2023 (to 73.0 per million changed lines, "highest level on record"), copy-pasted lines up from 9.4% to 15.7% of changes, cross-file function calls down 35%, and developers now roughly 5x more likely to copy-paste than refactor, a full reversal of the 2022 baseline. Osmani's review checklist flags this as "a common AI flaw," and ai-smells separately finds agents inlining the same API-call-plus-retry sequence at every call site instead of writing one wrapper, "suggesting agents lack local abstraction capabilities."

Bad (constructed):

```python
# checkout.py
def format_price(cents):
    dollars = cents / 100
    return f"${dollars:.2f}"

# invoice.py
def format_price(cents):
    dollars = cents / 100
    return f"${dollars:.2f}"
```

Good (constructed):

```python
# money.py
def format_price(cents):
    return f"${cents / 100:.2f}"

# checkout.py and invoice.py
from money import format_price
```

### New files instead of updating what's there

Tags: contextual, current. Sources: gitclear, own.

GitClear finds moved/refactored code collapsed from 21% of changes (2022) to 3.8% (2026 YTD), and updates to legacy code fell from 1.7% to 0.46% over the same period: generated changes increasingly add something new beside the old code rather than touching it. The recognizable shape of this is the sibling file, `auth.py` next to a fresh `auth_v2.py` that duplicates most of the original's logic for the sake of one new function.

Bad (constructed):

```text
src/auth.py       (unchanged, still imported by 6 callers)
src/auth_v2.py    (new file, copies login()/logout() almost verbatim, adds refresh_token())
```

Good (constructed):

```text
src/auth.py       (login()/logout() unchanged, refresh_token() added directly)
```

### Diffs sized past what review can absorb

Tags: contextual, current. Sources: ai-smells, anti-slop-action, osmani-review, own.

ai-smells found total lines of generated code correlates almost perfectly with architectural smells (rho=0.94); Osmani cites PRs growing ~18% larger as AI adoption rises, with incidents per PR up ~24% and change failure rate up ~30%; anti-slop-action's default gates (50 changed files, 10,000 changed lines) exist specifically because oversized diffs are a slop signal worth auto-flagging. The giveaway is a diff whose size has no relationship to the size of the task.

Bad (constructed):

```text
Task: fix incorrect tax rounding in checkout.
47 files changed, 3,214 insertions(+), 187 deletions(-)
  (touches: auth, billing, search, admin, notifications, CLI, 3 unrelated modules)
```

Good (constructed):

```text
Task: fix incorrect tax rounding in checkout.
2 files changed, 14 insertions(+), 3 deletions(-)
  (touches: checkout/tax.py, tests/test_tax.py)
```

### Rushed churn: same code re-edited within days

Tags: contextual, current. Sources: gitclear.

GitClear measures two-week code churn (code changed, then changed again almost immediately) up 15% versus 2022 levels, consistent with generated code landing half-baked and needing a string of quick follow-up fixes rather than getting it right, or reviewed properly, the first time.

Bad (constructed):

```text
Jul 2  feat: add retry logic to fetchOrders
Jul 6  fix: fetchOrders retry loop never terminates
Jul 9  fix: fetchOrders retry fix broke timeout handling
```

Good (constructed):

```text
Jul 2  feat: add retry logic to fetchOrders (bounded attempts, explicit timeout, reviewed)
```

## Over-engineered structure

### Long, comprehensive methods instead of focused ones

Tags: contextual, current. Sources: ai-smells.

ai-smells found Long Method is the dominant defect in single-file algorithmic generation (11 zero-shot and 13 few-shot instances from Qwen-Coder-480b versus 1 in the human baseline), and named the "reasoning-complexity paradox": more capable models write more procedurally bloated code precisely because they try to handle every edge case comprehensively in one place instead of decomposing the problem.

Bad (constructed):

```python
def process_order(order):
    if not order.items:
        raise ValueError("empty order")
    total = 0
    for item in order.items:
        if item.quantity <= 0:
            raise ValueError("bad quantity")
        price = item.price
        if order.customer.tier == "gold":
            price *= 0.9
        elif order.customer.tier == "silver":
            price *= 0.95
        total += price * item.quantity
    if order.customer.country in EU_COUNTRIES:
        total *= 1.2
    # ...continues for another 140 lines: inventory checks, email
    # formatting, analytics logging, loyalty points, all inline
    return total
```

Good (constructed):

```python
def process_order(order):
    validate(order)
    subtotal = price_items(order)
    subtotal = apply_tier_discount(subtotal, order.customer)
    return apply_tax(subtotal, order.customer.country)
```

### Branchy methods and god classes

Tags: contextual, current. Sources: ai-smells.

Too Many Branches was "the most prevalent smell" across all scenarios in ai-smells' multi-file agent experiment, and it co-occurs with High Response for a Class to form what the paper calls "God Class Syndrome," a single class accumulating both branch logic and unrelated responsibilities. The same syndrome shows up as Lack of Cohesion too: a class whose methods share no semantic unity, mixing unrelated concerns under one name, though the paper reports it at lower frequency than the branch-heavy and dependency symptoms above. (The paper's Feature Envy and Shotgun Surgery detectors are noted as unreliable, throwing false positives on ordinary single-file code, so they aren't cataloged here as tells in their own right.)

Bad (constructed):

```python
class RequestManager:
    def handle(self, request):
        if request.type == "create":
            ...
        elif request.type == "update":
            ...
        elif request.type == "delete":
            ...
        # ...40 branches total; this class also owns
        # logging, auth checks, and the database connection
```

Good (constructed):

```python
HANDLERS = {"create": CreateHandler(), "update": UpdateHandler(), "delete": DeleteHandler()}

class RequestRouter:
    def handle(self, request):
        return HANDLERS[request.type].run(request)
```

### Modular mirage: files that look separate but aren't

Tags: contextual, current. Sources: ai-smells.

ai-smells describes a "Modular Mirage": functionality scattered across files that look modular on the surface while Unstable Dependency ties them together underneath, each file quietly reaching into another's internals. The effect strongly correlates with total code volume (rho=0.72), meaning it gets worse the bigger the agent-generated system gets, not better.

Bad (constructed):

```text
features/checkout/
  step1.py   # imports features/checkout/step3.py internals directly
  step2.py   # reaches into step1.py's private _cart dict
  step3.py   # duplicates step2.py's tax logic inline
```

Good (constructed):

```text
features/checkout/
  checkout.py    # public run(cart) is the only entry point
  _internal.py   # private helpers, not imported elsewhere
```

### Ignores the existing architecture

Tags: contextual, current. Sources: osmani-review.

Osmani's review checklist asks "is the approach maintainable?" and calls out "roadmap alignment and institutional context that AI can't grasp" as something a reviewer has to check for explicitly, because working code that bypasses the codebase's established patterns will pass tests while still being wrong for the codebase it lands in.

Bad (constructed):

```python
def get_user_orders(user_id):
    conn = sqlite3.connect("app.db")
    return conn.execute(
        "SELECT * FROM orders WHERE user_id = ?", (user_id,)
    ).fetchall()
# every other feature in this codebase goes through OrderRepository
```

Good (constructed):

```python
def get_user_orders(user_id):
    return OrderRepository.find_by_user(user_id)
```

### Unnecessary abstraction and layering

Tags: contextual, current. Sources: own.

An interface, factory, or strategy layer shows up for a case that has exactly one implementation and no second one on the horizon. It reads as thorough, but it's indirection with nothing behind it, and the next person has to trace through three files to find one line of actual behavior.

Bad (constructed):

```python
class PaymentProcessor(ABC):
    @abstractmethod
    def charge(self, amount): ...

class StripeProcessor(PaymentProcessor):
    def charge(self, amount):
        stripe.Charge.create(amount=amount)

class PaymentProcessorFactory:
    @staticmethod
    def create(kind: str) -> PaymentProcessor:
        if kind == "stripe":
            return StripeProcessor()
        raise ValueError(kind)
# only one processor exists, and none are on the roadmap
```

Good (constructed):

```python
def charge(amount):
    stripe.Charge.create(amount=amount)
```

## Defensive and speculative bloat

### Backwards-compat shims nobody asked for

Tags: contextual, current. Sources: own.

Legacy parameter aliases, deprecated-but-kept branches, and version-negotiation code show up for an API that has no external consumers and no deprecation anyone requested. It looks careful; it's actually just surface area to maintain for a caller that doesn't exist.

Bad (constructed):

```python
def create_user(name, email, legacy_username=None, old_email_field=None):
    email = email or old_email_field  # kept for a caller that no longer exists
    username = legacy_username or name
    ...
```

Good (constructed):

```python
def create_user(name, email):
    ...
```

### Config options and feature flags nobody requested

Tags: contextual, current. Sources: own.

A settings knob, env var, or boolean flag appears for a behavior nobody asked to make configurable, for a feature request that was just "send the user a message when their order ships." Every unused option is a path through the code nobody tests and everybody has to reason about.

Bad (constructed):

```python
def send_notification(user, message, use_legacy_formatter=False,
                       retry_strategy="exponential", max_retries=5, dry_run=False):
    ...
```

Good (constructed):

```python
def send_notification(user, message):
    ...
```

### Dead defensive branches

Tags: contextual, current. Sources: own.

A function guards against a state its caller already made impossible: null checks on a value that was just validated, type checks on a parameter the type system already constrains, empty-list handling for a list that can't be empty at that call site. The guard can never fire; it just sits there as noise.

Bad (constructed):

```python
def get_first_item(items: list[str]) -> str:
    if items is None:
        return ""
    if not isinstance(items, list):
        return ""
    if len(items) == 0:
        return ""
    return items[0]
# called only with a validated, non-empty list from one call site
```

Good (constructed):

```python
def get_first_item(items: list[str]) -> str:
    return items[0]
# emptiness is handled once, at the boundary where data enters the system
```

### Broad try/except that swallows errors

Tags: always, current. Sources: gitclear.

GitClear measures a 47% rise in error-masking constructs since 2022. Catching broadly and logging is sometimes reasonable; catching broadly and doing nothing with it is never reasonable, it just converts a bug into a silent one.

Bad (constructed):

```python
try:
    process_payment(order)
except Exception:
    pass
```

Good (constructed):

```python
try:
    process_payment(order)
except PaymentError as e:
    logger.error("payment failed for order %s: %s", order.id, e)
    raise
```

## Comments and in-code hygiene

### Over-commenting the obvious

Tags: contextual, current. Sources: anti-slop-action, own.

anti-slop-action gates PRs on a comment count (default ceiling 10 added comments) specifically because, in the tool's words, "AI-generated code tends to add excessive comments explaining obvious logic." A comment restating exactly what the next line already says isn't documentation, it's noise a reader has to read past.

Bad (constructed):

```python
# create an empty list to store results
results = []
# loop through each item in the items list
for item in items:
    # add the item to the results list
    results.append(item)
```

Good (constructed):

```python
results = []
for item in items:
    results.append(item)
```

### Comments that narrate the change, not the code

Tags: always, current. Sources: own.

The comment describes the edit ("added this check", "changed this to use a dict") instead of describing what the code does or why. It's the model narrating its own diff for a reader who will never see that diff, and it goes stale the moment the code changes again.

Bad (constructed):

```python
# Added this check to handle the new edge case the user mentioned
if user is None:
    return None
# Changed this to use a dict instead of a list for O(1) lookup
lookup = {u.id: u for u in users}
```

Good (constructed):

```python
if user is None:
    return None
lookup = {u.id: u for u in users}  # id -> user, O(1) lookup
```

### Docstrings that restate the signature

Tags: contextual, current. Sources: own.

The docstring repeats the function name and parameter names back in prose, and adds nothing a reader couldn't already see by looking at the signature: no units, no invariants, no explanation of what's non-obvious.

Bad (constructed):

```python
def calculate_discount(price: float, percentage: float) -> float:
    """
    Calculates the discount.

    Args:
        price (float): The price.
        percentage (float): The percentage.

    Returns:
        float: The discount.
    """
    return price * (percentage / 100)
```

Good (constructed):

```python
def calculate_discount(price: float, percentage: float) -> float:
    """Discount amount, not the discounted price. percentage is 0-100, not 0-1."""
    return price * (percentage / 100)
```

### Leftover debug output

Tags: always, current. Sources: own.

Print statements, `console.log`, commented-out old implementations, and self-referential TODOs from the generation process itself get left in place, never meant to ship and never cleaned up before the diff is presented as done.

Bad (constructed):

```python
def calculate_total(items):
    print("DEBUG: items =", items)  # TODO: remove before merging
    # old implementation, keeping just in case
    # total = sum(i.price for i in items)
    total = sum(i.price * i.qty for i in items)
    print("DEBUG: total =", total)
    return total
```

Good (constructed):

```python
def calculate_total(items):
    return sum(i.price * i.qty for i in items)
```

### Success theater in CLI and log output

Tags: contextual, current. Sources: own.

Scripts print a checkmark and "All done!" or "Success! 🎉" regardless of whether anything meaningful happened, standing in for output that would actually tell the reader what occurred.

Bad (constructed):

```python
def run_migration():
    apply_schema_changes()
    print("✅ All done! 🎉 Migration completed successfully!")
```

Good (constructed):

```python
def run_migration():
    changes = apply_schema_changes()
    print(f"Applied {len(changes)} schema changes.")
```

## Hallucination and unearned confidence

### Acting on a hallucinated picture of the codebase

Tags: always, current. Sources: curl-slop, own.

Stenberg's curl writeup documents this directly: report #2819666 named a nonexistent `curl_mfprintf` function, report #3100073 invented an `IPFS_PATH` environment variable curl doesn't have, other reports invented an "MQTT Test Server" and an "HTTP/3 Stream Dependency" for components that don't work that way, and report #2199174 re-reported CVE-2023-38545 as a new finding years after it had shipped fixed. Same mechanism in generated code: a call into a function, module, or config key that was never in this codebase, or a fix for a bug some later commit already fixed.

Bad (constructed):

```python
from myapp.utils.formatting import currency_format  # this module doesn't exist here

def render_price(cents):
    return currency_format(cents)
```

Good (constructed):

```python
from myapp.money import format_price

def render_price(cents):
    return format_price(cents)
```

### Claims of correctness or completeness with nothing to back them

Tags: always, current. Sources: curl-slop, own.

curl's slop reports announce severity ("Critical", "Exploitable") with total certainty and zero proof of concept; report #2823554 claimed a generic "buffer overflow in strcpy" with no code path or reproduction at all; reporters could not produce a repro when maintainers pressed them. The code-level version is a comment or docstring asserting a guarantee ("thread-safe", "handles all edge cases", "fully tested") that nothing in the change actually establishes.

Bad (constructed):

```python
def parse_config(raw: str) -> dict:
    """Thread-safe. Handles all malformed input gracefully. Fully tested."""
    return json.loads(raw)
# no thread-safety mechanism, no error handling, no tests in this diff
```

Good (constructed):

```python
def parse_config(raw: str) -> dict:
    """Raises json.JSONDecodeError on malformed input; caller decides how to handle it."""
    return json.loads(raw)
```

### Placeholder stubs presented as finished work

Tags: always, fading. Sources: own.

2023-2024 era models routinely left a `# TODO: implement this` or a hardcoded placeholder value inside code presented as a complete solution. Sharply less common in 2025-2026 frontier models, which tend to either finish the implementation or say plainly what's missing, but still worth watching for from weaker or budget-tier models.

Bad (constructed):

```python
def calculate_shipping_cost(order):
    # TODO: implement actual shipping calculation
    return 9.99
# presented as "shipping cost calculation is implemented"
```

Good (constructed):

```python
def calculate_shipping_cost(order):
    return SHIPPING_RATES[order.destination_zone] * order.weight_kg
```

### Security-critical code merged without extra scrutiny

Tags: always, current. Sources: osmani-review.

Osmani cites logic errors at 1.75x the rate of human-written code, XSS vulnerabilities at 2.74x higher frequency, and roughly 45% of AI-generated code containing some security flaw, and recommends treating AI output touching auth, payments, secrets, or untrusted input as a high-speed intern's work: it needs an explicit human threat-model pass, not a routine review. This only applies to security-sensitive code paths, not code in general, but wherever it does apply there's no context where skipping the extra scrutiny is fine.

Bad (constructed):

```javascript
function renderComment(comment) {
    container.innerHTML = `<p>${comment.text}</p>`;
}
```

Good (constructed):

```javascript
function renderComment(comment) {
    const p = document.createElement("p");
    p.textContent = comment.text;
    container.appendChild(p);
}
```

## Tests

### Tautological tests written from the code, not the spec

Tags: always, current. Sources: test-slop.

Adamo's clearest example: a `divide` function that silently returns 0 instead of raising on division by zero, and a generated test that asserts exactly that buggy return value, because the test was written by observing the implementation rather than the intended contract. As the article puts it, "your tests now validate the implementation, not the intention", and post-hoc test generation from finished code breaks the intent-observation loop that would otherwise catch this.

Bad:

```python
def divide(a, b):
    if b == 0:
        return 0  # bug: should raise an error
    return a / b

def test_divide_by_zero():
    assert divide(10, 0) == 0
```

Good (constructed):

```python
def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)
```

### Happy-path-only tests, no edge cases

Tags: contextual, current. Sources: test-slop.

Adamo notes generated suites aren't "exploring edge cases, enforcing contracts, or asserting business rules": they check the one input everyone thinks of and stop there.

Bad (constructed):

```python
def test_divide():
    assert divide(10, 2) == 5
```

Good (constructed):

```python
def test_divide():
    assert divide(10, 2) == 5
    assert divide(-10, 2) == -5
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)
    with pytest.raises(TypeError):
        divide("10", 2)
```

### Weak assertions

Tags: contextual, current. Sources: own.

The test checks that a call didn't crash, or returned "something", instead of checking the actual value the spec requires. It passes today and would keep passing after most regressions.

Bad (constructed):

```python
def test_get_user():
    result = get_user(42)
    assert result is not None
```

Good (constructed):

```python
def test_get_user():
    result = get_user(42)
    assert result == User(id=42, name="Ada Lovelace", active=True)
```

### Mock-everything tests that only verify calls happened

Tags: contextual, current. Sources: own.

Every collaborator gets mocked, including pure functions and dependencies that don't need isolating, until the only thing left to assert is that a mock was invoked. That proves the code called something; it proves nothing about what it produced.

Bad (constructed):

```python
def test_process_order():
    mock_repo = Mock()
    mock_calculator = Mock()
    mock_notifier = Mock()
    process_order(mock_repo, mock_calculator, mock_notifier, order_id=1)
    mock_calculator.compute.assert_called_once()
```

Good (constructed):

```python
def test_process_order():
    repo = FakeOrderRepository(orders=[Order(id=1, items=[Item(price=10, qty=2)])])
    result = process_order(repo, RealCalculator(), NullNotifier(), order_id=1)
    assert result.total == 20
```

### Instant suspicious coverage

Tags: contextual, current. Sources: test-slop, own.

Adamo: "you see 90% coverage in seconds... it's all an illusion." A suite generated in the same commit as the code it tests can hit a high coverage number while every assertion just mirrors whatever the code happened to output, with no reference to any actual requirement.

Bad (constructed):

```text
$ pytest --cov=pricing
pricing.py    94%   (40 tests, generated in the same commit as pricing.py)
```
```python
def test_apply_discount():
    assert apply_discount(100, "VIP") == 85  # value copied from a debug print
```

Good (constructed):

```python
def test_apply_discount():
    # VIP tier gets 15% off per pricing policy doc, section 3.2
    assert apply_discount(100, "VIP") == 85
```

### Tests missing, skipped, or deleted instead of fixed

Tags: always, current. Sources: osmani-review, own.

Osmani's review contract calls for enforcing coverage above 70% as a gate, implying its absence is a known way generated changes slip through; in practice this shows up as a failing test getting `@skip`ped, commented out, or deleted in the same change that introduced the bug it was catching, rather than the bug getting fixed.

Bad (constructed):

```python
@pytest.mark.skip(reason="flaky, fix later")
def test_concurrent_writes():
    ...
# added in the same PR that introduced the race condition this test catches
```

Good (constructed):

```python
def test_concurrent_writes():
    with Lock():
        ...
# the race condition is fixed; the test stays enabled
```
