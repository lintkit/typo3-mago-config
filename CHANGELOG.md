# 2.0.0

**5th November 2026**

#### Breaking

- Rename the package to `lintkit/typo3-mago-config`. It replaces `lintkit/mago-config`
- Merge the TYPO3 rules into `.mago.toml` and remove `.typo3.mago.toml`. Point the `mago` script at `vendor/lintkit/typo3-mago-config/.mago.toml`

#### Dependencies

- Require `typo3/testing-framework` `^8.0 || ^9.0`

# 1.1.1

**5th November 2026**

#### Fix

- Ignore the `typo3/class-alias-loader` template PHP files in the TYPO3 config

# 1.1.0

**6th October 2026**

#### Feature

- Ignore the `TYPO3_MODE` die statement in the TYPO3 config

# 1.0.0

**6th October 2026**

#### Feature

- Initial release of shared Mago config
