# When the DS doesn't cover something

When no token, type style or component fits:

1. **Don't pick an approximate raw value silently, and don't add a token locally.**
2. If the work can't wait, use the **closest existing token** (or, if none is even close, keep the design's value) and mark the spot:

   ```
   TODO(ds): <one line: what's missing>. Request: <link or "drafted for designers">
   ```

   Use your language's comment syntax. One marker per spot, so the `TODO(ds)` inventory stays accurate.
3. **Draft a request** for the designers with three facts:

   ```
   DS request: <token | type style | component | state>

   What is needed: <the value or behaviour, e.g. "a left-to-right image overlay gradient, near-black to transparent at 54%">
   Where it goes: <page / block / component, and the design-file node if there is one>
   What I found and why it doesn't work: <the closest token(s) and why they don't fit>
   ```

4. List every new `TODO(ds)` and request in your final report, so the user can send them on.

The same applies to states a component guide doesn't list: ask instead of inventing one.
