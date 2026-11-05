# LintKit: TYPO3 Mago Config

Liquid Light base configuration for [Mago](https://mago.carthage.software) - the PHP formatter, linter and analyzer - in TYPO3 projects

## Usage

Install the dependency:

```bash
composer require --dev lintkit/typo3-mago-config
```

This also installs [`typo3/testing-framework`](https://github.com/TYPO3/testing-framework).

Add the scripts:

```json
"scripts": {
    "mago": "mago --config vendor/lintkit/typo3-mago-config/.mago.toml",
    "mago:analyze": "@mago analyze",
    "mago:dry-run": "@mago:fix --check",
    "mago:fix": "@mago fmt",
    "mago:lint": "@mago lint"
},
```

### PHP version

Mago targets PHP 8.4 by default. If the project sets `config.platform.php`, pass that version to Mago instead:

```json
"mago": "MAGO_PHP_VERSION=$(composer config platform.php) mago --config vendor/lintkit/typo3-mago-config/.mago.toml",
```

### TYPO3

The config makes allowances for TYPO3:

- TYPO3 core, `config/system/settings.php` and project `backup/` and `html/` directories are not checked
- `$GLOBALS` is allowed in TCA, `ext_localconf.php`, `ext_tables.php` and `config/system/*.php`
- Extbase models may have many properties and methods
- Exception codes (timestamps) don't need numeric separators
- `ext_emconf.php` doesn't need `declare(strict_types=1)`
- The `defined('TYPO3') || die();` guard is not reported as an unused statement

### Baselines

The linter and analyzer read their baselines from a `.mago/` directory in the project root. If these don't exist, Mago warns and reports every issue.

Generate them with:

```bash
mkdir -p .mago
composer mago:lint -- --generate-baseline
composer mago:analyze -- --generate-baseline
```

Commit the `.mago/` directory.

## Upgrading from `lintkit/mago-config`

This package replaces `lintkit/mago-config`, and the TYPO3 rules are now in `.mago.toml` itself.

1. Swap the package:

    ```bash
    composer remove --dev lintkit/mago-config
    composer require --dev lintkit/typo3-mago-config
    ```

2. Change the `mago` script's config path, whether it pointed at `.mago.toml` or `.typo3.mago.toml`, to `vendor/lintkit/typo3-mago-config/.mago.toml`
