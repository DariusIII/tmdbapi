# AGENTS.md

## Project scope
- Library: `php-tmdb/api`
- Runtime floor: PHP `8.3+`
- Current package line: `5.x` (`composer.json`, `lib/Tmdb/Client.php`)
- Upgrade notes currently live in `UPGRADE-6.0.md`
- Main source lives in `lib/Tmdb`
- Tests live in `test/Tmdb/Tests`
- Usage examples live in `examples/`

## Supported dependency branches
- Keep Symfony component constraints on maintained branches: `^6.4 || ^7.0`
- PHPUnit is intentionally pinned to `^9.6.23`
- Do not upgrade PHPUnit to 10+ without also migrating XML config and legacy test-helper patterns
- Monolog dev support is `^3.0`

## Local development commands
- Install/update dependencies:
  - `composer update --no-interaction --no-progress --prefer-dist`
- Run tests:
  - `vendor/bin/phpunit`
  - `composer test`
- Run coverage build:
  - `composer test-ci`
- Run static analysis:
  - `vendor/bin/phpstan analyse`
  - `composer test-phpstan`
- Run coding standards:
  - `vendor/bin/phpcs`
  - `composer test-cs`

## CI parity
- PHPUnit matrix in `.github/workflows/continuous-integration.yml` targets:
  - PHP `8.3` with `normal`, `low`, and `dev` dependencies
  - PHP `8.4` with `normal` dependencies
  - PHP `8.5` with `dev` dependencies
- PHPStan runs on PHP `8.3` and `8.5`
- Coding standards run on PHP `8.3`
- Prefer matching these workflows when changing dependency constraints or tooling

## Testing conventions
- Shared test setup is in `test/Tmdb/Tests/TestCase.php`
- Mock HTTP clients should use PSR-7/PSR-18 objects, not legacy Guzzle 5/6 request abstractions
- Default mocked successful responses use a real JSON body (`{}`) to avoid empty-body decode failures
- API/repository request assertions are based on generated PSR-7 requests from `getRequest()` in the shared test base
- If you change request construction, re-run the full PHPUnit suite because many tests assert path, query, headers, and body behavior indirectly

## Static analysis and coding standards
- PHPStan config is `phpstan.neon.dist` and includes `phpstan-baseline.neon`
- If PHPStan findings change intentionally, regenerate or edit the baseline carefully; keep paths repository-relative
- PHPCS uses `phpcs.xml.dist` with `PSR12` on `lib/`
- `build.xml` and `build/phpunit.xml` are still used as auxiliary build configs; keep them aligned with root Composer/PHPUnit settings

## Release-line notes
- Version 5 intentionally drops PHP `7.x`, `8.0`, `8.1`, and `8.2`
- Empty successful response bodies are treated as empty payloads in `lib/Tmdb/Api/AbstractApi.php`
- Keep `Tmdb\Client::VERSION` aligned with the active package major version

