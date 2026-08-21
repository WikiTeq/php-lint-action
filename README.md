# php-lint-action

A composite GitHub Action that lints PHP code with `phpcs` and `phplint`.

## Usage

```yaml
steps:
  - uses: WikiTeq/php-lint-action@main
```

## What it does

1. Sets up PHP 8.1 with `composer`, `phpcs`, and `phplint` via [shivammathur/setup-php](https://github.com/shivammathur/setup-php).
2. Checks out your repository.
3. Runs `composer update` **if a `composer.json` is present** at the repository root.
4. Runs `phplint -w --exclude=vendor` over the repository.
5. Runs `vendor/bin/phpcs -sp --standard=.phpcs.xml .` **only if both `vendor/bin/phpcs` and `.phpcs.xml` exist**.

Steps 3 and 5 are skipped gracefully when their prerequisites are missing, so the action works in plain PHP repositories without Composer or PHP_CodeSniffer setups.

## Requirements

- The repository must contain PHP files to lint.
- `composer update` and `phpcs` only run in Composer-based projects (see above); no other configuration from the consuming repo is required.
