# npm-safe 🏴‍☠️

## Quality-Enforced npm CLI Fork

**Status:** 🔄 Being offered to [npm/cli](https://github.com/npm/cli) as upstream contribution ([PR #8880](https://github.com/npm/cli/pull/8880))

**If accepted:** Merged under npm's Artistic License 2.0  
**Until then:** Available as independent fork under BarrerSoftware License (BSL)

---

## What is npm-safe?

npm-safe adds optional pre-publish quality validation to prevent broken packages from entering the ecosystem.

**Prevents packages with:**
- Memory leaks (like copilot-cli's 4GB heap crash on `@` symbol)
- Crashes on basic input (special characters, Unicode, etc.)
- Missing or failing tests
- Known security vulnerabilities
- Performance issues

## Motivation

This fork was created after discovering [GitHub Copilot CLI Issue #841](https://github.com/github/copilot-cli/issues/841) - a production bug where the tool consumed 4GB of heap memory and crashed when encountering the `@` symbol in conversation about npm scoped packages.

If npm had quality validation at publish time, broken packages like this wouldn't make it to the ecosystem.

## Installation

```bash
npm install -g @barrersoftware/npm-safe
```

Or use it directly:
```bash
npx @barrersoftware/npm-safe publish
```

## Usage

Add to your `package.json`:

```json
{
  "publishValidation": {
    "enabled": true,
    "memoryLeakCheck": true,
    "inputValidation": true,
    "requireTests": false,
    "auditLevel": "moderate"
  }
}
```

Then publish as normal:

```bash
npm-safe publish
```

## Validation Checks

### Memory Leak Detection
Monitors heap usage during package execution to detect unbounded memory growth.

### Input Validation Testing
Tests package with special characters, Unicode, and edge cases to prevent crashes.

### Test Requirements
Optionally requires tests to exist and pass before allowing publish.

### Dependency Audit
Runs `npm audit` and fails on high/critical vulnerabilities.

## Opt-In by Default

Validation is **disabled by default**. You must explicitly enable it with `"enabled": true`.

Individual checks can be enabled/disabled independently.

## Tested and Working

Successfully validated [Quartermaster Discord bot](https://github.com/barrersoftware/quartermaster) - a complete production package passed all checks cleanly.

## Contributing to Upstream

This work is being offered to npm/cli as [PR #8880](https://github.com/npm/cli/pull/8880). 

If you support quality validation in npm, please voice your support on that PR!

## License

**Dual License:**
- **If merged upstream:** Artistic License 2.0 (npm's license)
- **Independent fork:** BarrerSoftware License (BSL) - Free forever, cannot be sold

See [LICENSE.BSL](LICENSE.BSL) for details.

## Philosophy

Quality isn't optional. If we can prevent broken packages from being published, we should.

Built by two people (one human, one AI) on DoorDash income. Proving that quality doesn't require corporate backing - just discipline and standards.

---

🏴‍☠️ **BarrerSoftware: Quality over profit. Standards over chaos.**

*Free forever. No subscriptions. No corporate bullshit.*
