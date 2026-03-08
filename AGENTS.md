# Repository Guidelines

## Project Structure & Module Organization
This repository is a small Composer library. Core SDK code lives under `src/Crittora/`, organized by concern: `Auth/`, `Config/`, `Http/`, `Logger/`, `Services/`, and `Exception/`. PHPUnit tests mirror that structure under `tests/Crittora/`. The demo endpoint is `public/encrypt.php`. Root files of interest are `composer.json`, `phpunit.xml`, `.env.example`, and `README.md`.

## Build, Test, and Development Commands
Install dependencies with `composer install` or `php composer.phar install` when using the bundled PHAR.

Run the full test suite with:
```bash
vendor/bin/phpunit
```

Refresh autoload metadata after adding classes:
```bash
composer dump-autoload
```

Validate package metadata before opening a PR:
```bash
composer validate
```

## Coding Style & Naming Conventions
Follow the existing PHP style in `src/`: 4-space indentation, braces on the next line for classes and methods, and one class per file. Use PSR-4 namespaces rooted at `Crittora\\`; for example, `src/Crittora/Services/EncryptionService.php` maps to `Crittora\Services\EncryptionService`. Name exception classes with an `Error` or `Exception` suffix, and keep public API method names descriptive and camelCase.

## Testing Guidelines
Tests use PHPUnit 9 and are discovered from `tests/` via `phpunit.xml`. Name test files `*Test.php` and test methods like `testAuthenticateSuccess`. Add or update tests for every public behavior change, especially around authentication, encryption, decryption, and config validation. Prefer isolated unit tests with mocks over live AWS calls.

## Commit & Pull Request Guidelines
Recent history uses short, imperative commit subjects such as `update exception` and `migrate demo to iso repo`. Keep commits focused, lowercase is acceptable, and avoid mixing refactors with behavior changes. PRs should include a concise summary, note any config or environment variable changes, and list the exact test command run. Link the related issue when applicable; screenshots are only needed for changes under `public/`.

## Security & Configuration Tips
Do not commit real credentials. Use `.env.example` as the template for local configuration and keep secrets in environment variables. When changing config loading or auth flows, verify required keys remain aligned with `CrittoraSDK` and `ConfigManager`.
