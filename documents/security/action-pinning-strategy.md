# action-pinning-strategy

## 1. Version Tags vs. Commit Hashes

### Version Tags
**Example:** `v1`

* **Version tags are Mutable.**
* A tag is simply a label (or a "sticky note"). Even if the underlying code is modified, the author can still point the same `v1` tag to the new code.

### Commit Hashes
**Example:** `f2a4c...`

* **Commit hashes are Immutable.**
* A SHA hash is a cryptographic signature generated from the code content.
* If the code content changes, the hash changes. Therefore, specifying a specific SHA ensures that **100% identical code is executed**, regardless of when the workflow is run.

## 2. Security Risks

### Supply Chain Attack (Tag Hijacking)
**Scenario:** The account of a popular action's author (e.g., `awesome-action`) is compromised.

1.  The attacker injects malicious code into the `awesome-action` repository.
2.  The attacker deletes the existing `v1` tag and re-applies the `v1` tag to the new commit containing the malicious code.
3.  If your workflow is configured with `uses: owner/awesome-action@v1`, it remains pointing to the tag `v1`.
4.  **Result:** On your next workflow run, the malicious code is automatically downloaded and executed.

## 3. Implementation Examples

### Not Recommended
```yaml
steps:
  - uses: actions/checkout@v3
Risk: The code that v3 points to can be changed at any time without notice.
```

### Recommended

```yaml
steps:
  - uses: actions/checkout@f43a0e5ff2bd294095638e18286ca9a3d1956744 # v3.6.0
```

* Safety: This guarantees that only the code at this specific point in time is executed.
* Tip: Since hash strings are hard to identify, adding the version number as a comment improves readability.