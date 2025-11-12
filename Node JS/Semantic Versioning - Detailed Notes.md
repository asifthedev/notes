# Semantic Versioning - Detailed Notes

## Basic Format

**MAJOR.MINOR.PATCH** (e.g., 2.4.1)

---

## Version Number Rules

### MAJOR (X.0.0)

- Increment when making **incompatible/breaking changes**
- Resets MINOR and PATCH to 0
- Examples:
  - Removing a public function
  - Changing function signatures
  - Removing/renaming parameters
  - Any change that breaks existing code

### MINOR (0.X.0)

- Increment when adding **backward-compatible functionality**
- Resets PATCH to 0
- Examples:
  - Adding new features
  - Adding new methods/functions
  - Deprecating functionality (but not removing)
  - Substantial new functionality in private code

### PATCH (0.0.X)

- Increment for **backward-compatible bug fixes**
- Internal changes that fix incorrect behavior
- No new features, only fixes

---

## Special Symbols & Notations

### Pre-release Versions

Use **hyphen (-)** to denote pre-release:

- `1.0.0-alpha`
- `1.0.0-alpha.1`
- `1.0.0-beta`
- `1.0.0-beta.2`
- `1.0.0-rc.1` (release candidate)

**Precedence:** 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-beta < 1.0.0-rc.1 < 1.0.0

### Build Metadata

Use **plus (+)** to append build metadata:

- `1.0.0+20130313144700`
- `1.0.0+exp.sha.5114f85`
- `1.0.0-beta+exp.sha.5114f85`

**Note:** Build metadata is IGNORED when determining version precedence

### Combined Example

`2.1.5-rc.1+build.123` = Major 2, Minor 1, Patch 5, Release Candidate 1, Build 123

---

## Dependency Range Symbols (npm/package managers)

### Caret (^) - Compatible updates

- `^1.2.3` → Allows >=1.2.3 and <2.0.0
- Updates MINOR and PATCH only
- Most common for production

### Tilde (~) - Patch updates only

- `~1.2.3` → Allows >=1.2.3 and <1.3.0
- Updates PATCH only
- More conservative

### Exact Version (=)

- `1.2.3` or `=1.2.3` → Only version 1.2.3
- No flexibility

### Greater Than/Less Than

- `>1.2.3` → Greater than 1.2.3
- `>=1.2.3` → Greater than or equal
- `<2.0.0` → Less than 2.0.0
- `<=1.2.3` → Less than or equal

### Range (-)

- `1.2.3 - 2.3.4` → Between versions (inclusive)

### Wildcard (x or *)

- `1.2.x` → Any patch version of 1.2
- `1.*` → Any minor/patch of major 1
- `*` → Any version

---

## Initial Development

### Version 0.x.y

- **0.1.0** - Initial development start
- Anything MAY change at any time
- Public API not stable
- **0.y.z** format: y = minor changes, z = patches

### Moving to 1.0.0

- Declare when your API is production-ready
- First stable public API
- After this, follow semver rules strictly

---

## Important Rules

1. **Once published, NEVER modify** that version's contents
2. **Must increment** at least one number for any changes
3. **MAJOR version 0** (0.y.z) is for initial development
4. **Version 1.0.0** defines the public API
5. **Deprecate** rather than remove (until next MAJOR)
6. Pre-release versions have **lower precedence** than normal versions

---

## Practical Examples

| Change                   | From  | To    | Reason |
| ------------------------ | ----- | ----- | ------ |
| Bug fix                  | 1.2.3 | 1.2.4 | PATCH  |
| New feature (compatible) | 1.2.4 | 1.3.0 | MINOR  |
| Breaking change          | 1.3.0 | 2.0.0 | MAJOR  |
| Security patch           | 2.0.0 | 2.0.1 | PATCH  |
| Multiple new features    | 2.0.1 | 2.1.0 | MINOR  |
| Remove deprecated API    | 2.1.0 | 3.0.0 | MAJOR  |
