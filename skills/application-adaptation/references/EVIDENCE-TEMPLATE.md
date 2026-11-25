# Application Evidence Template

Use one record per claim. Do not combine multiple claims in one record.

```markdown
# Evidence Record

- **Claim:**
- **Application:**
- **Version / build:**
- **Platform (device/OS/desktop):**
- **Evidence type:** Official / Observed in sample / Inferred / Unverified
- **Source:** vendor documentation URL, file name, recording name and timestamp
- **Recorded on:**
- **Recorded by:**
- **Scope:** what this evidence does and does not cover
- **Limitations:**
- **Verification status:** Not tested / Partially verified / Verified
- **Notes:**
```

## Rules

- `Official` requires a vendor source for the named version.
- `Observed in sample` is limited to the supplied sample; do not generalize.
- `Inferred` is a reasoned interpretation, not a confirmed capability.
- Parser-derived results, including reverse-engineered `.aep` inspection, must state the parser name and that it is unofficial.
- Never copy a procedure from Alight Motion to After Effects, or the reverse, without separate evidence.
- Do not record customer project content, credentials, or private media in this repository.
