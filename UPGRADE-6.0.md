Upgrading to 6.0
----------------

Version 6 raises the minimum supported PHP version to `8.3`.

What changed
============

- Support for PHP `7.x`, `8.0`, `8.1`, and `8.2` has been removed.
- Composer constraints were updated to target actively maintained dependency branches.
- CI and static-analysis workflows now validate only supported PHP versions.
- Test helpers were refreshed for current PSR-7/PSR-18 behavior and modern PHPUnit 9.6 APIs.
- Empty successful response bodies are now treated as an empty payload instead of failing JSON decoding.

What you need to do
===================

1. Upgrade your runtime to PHP `8.3` or newer.
2. Update your dependencies:

```shell script
composer update php-tmdb/api --with-all-dependencies
```

3. If you pin Symfony components alongside this package, use supported maintained lines (`6.4` or `7.x`).
4. Re-run your test suite and static analysis after upgrading.

Notes
=====

This release does not change the public TMDB API surface intentionally; the breaking change is the supported PHP/dependency floor.


