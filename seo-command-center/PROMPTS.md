# PROMPTS.md — my key prompts log

Keep the handful of prompts that actually moved the build. Not every message — the ones that
mattered: the system/sub-agent prompts, the ones you iterated on, the "this finally worked"
moment. This shows how you direct an AI, which is graded (challenge brief section 08).

Format per entry:
- **Prompt** (paste it)
- **For:** what you were trying to do
- **Revised?** did you have to change it, and why

---

<!-- ## Example (replace with your own)

- **Prompt:** "Extend seo/detector.py to detect redirect chains: build a map of {Address ->
  Redirect URL} for all 3xx rows, then a chain exists when a Redirect URL is itself a key in
  that map. Add a redirect_chain issue (High). Run python seo/detector.py and show counts."
- **For:** adding the redirect-chain detector
- **Revised?** Yes — first version flagged single redirects as chains; added the "target is
  also a redirecting URL" condition. -->

---

## My prompts
1. **Prompt** "You are completing missing SEO detectors in `seo/detector.py`.

## CONSTRAINTS
- Architecture unchanged
- Standard library only
- CSV input only
- Deterministic logic only
- Preserve existing issue output format exactly

---

## STEP 1 — Add helpers (exact signatures)

```python
def val(r, key, default=""):
    return str(r.get(key, default) or "").strip()
```

Improve _int() and _float() to handle: empty string, whitespace-only, decimals, malformed — return 0 / 0.0 on failure.

```python
def normalize_url(url):
    # strip whitespace
    # lowercase scheme and hostname only
    # remove fragment (#...)
    # remove trailing slash UNLESS path is "/"
```

---"
**For** clean retrieval from csv and normalisation and handling of None and exceptions.

**Prompt** Refactor all existing detectors to use val(), _int(), _float(), normalize_url() consistently.

**for** So that the all detectors use the normalised value instead of some using raw csv values

5. **Prompt:** "See the report schema json file which is outside the current directory and make sure it matches report.json which is generated is matched strictly according to it. if it is not matching make all the necessary changes."

**For:** Ensuring report.json output conforms to the schema contract defined in report.schema.json.

**Revised?** Yes — changed run.py output generation to match schema exactly; was missing fields and incorrect nesting.

