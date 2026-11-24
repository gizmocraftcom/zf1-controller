# Changelog

## 2.0.0
- Package renamed to `gizmocraft/zendframework1-controller` (fork of `diablomedia/zendframework1-controller`).
- Requires PHP >= 8.5; CI runs on PHP 8.5 and 8.6.
- Depends on the `gizmocraft/zendframework1-*` forks (cache, config, exception, filter, loader, locale, registry, session, translate, uri, view) at `^2.0.0` (config `^3.0.0`, session `^3.0.0`).
- The `suggest` entries for the action helper packages (autocomplete, json, ajaxcontext, contextswitch) now point to the `gizmocraft/` forks.
- Dev dependencies upgraded to PHPUnit 13, PHPStan 2.3, php-cs-fixer 3.95 and GrumPHP 2.27; `composer-require-checker` dropped.
- Tests migrated to PHPUnit 13 (`#[Group]` and `#[DataProvider]` attributes instead of annotations, which PHPUnit 12+ ignores; the data-provider tests errored with an `ArgumentCountError` until converted).

### Fixed
- `Zend_Controller_Router_Route_Module`, `Zend_Controller_Router_Route`, `Zend_Controller_Router_Route_Hostname` and `Zend_Controller_Router_Route_Regex`: `assemble()` passed `null` to `urlencode()` for parameters without a value (for example the last segment of `/a/b/c/d/e`), which is deprecated since PHP 8.1. A `null` value is now encoded as an empty string, as before.
- `Zend_Controller_Request_Http::setBaseUrl()`: casts the request URI to a string before the `strpos()`/`strlen()`/`substr()` calls (the request URI is `null` outside a web request, for example on the CLI). No change in behavior.
