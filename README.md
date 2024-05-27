# Setup HaoKe

Setup HaoKe in your GitHub Actions pipeline to run tests.

## Usage

### Inputs:

- `haoke-version` (default: `v6.6.2.0`) - The HaoKe version to install.
- `php-version` (default: `8.1`) - The PHP version to use. The `php-version` can be any PHP version supported by [setup-php](https://github.com/shivammathur/setup-php).
- `php-extensions` (default: `pcov`) - A comma-separated list of PHP extensions to install. See setup-php project
- `env` (default: `test`) - The environment for the setup. Should be `test` for PHPUnit or `e2e` for E2E tests.
- `install` (default: `false`) - Whether to install HaoKe or not. If set to `false`, the action will only install PHP, MySQL, Composer packages.
- `install-locale` (default: `en-GB`) - The locale to install HaoKe with.
- `install-currency` (default: `EUR`) - The currency to install HaoKe with.
- `mysql-version` (default: `builtin` - Uses by default the bundled MySQL version of GitHub Actions this is MySQL 8) - Specify any docker image to use instead like `mariadb:11` or `mysql:5.7`.

```yaml
- name: Setup HaoKe
  uses: haokeyingxiao/setup-haoke@v1
  with:
    haoke-version: v6.5.3.2
    php-version: 8.1
```

## Example pipeline to run PHPUnit tests

```yaml
jobs:
    phpunit:
        runs-on: ubuntu-latest
        steps:
            - name: Setup HaoKe
              uses: haokeyingxiao/setup-haoke@v1
              with:
                haoke-version: '6.5.7.3'
                php-version: 8.1

            - name: Checkout
              uses: actions/checkout@v3
              with:
                  path: custom/plugins/FroshPlatformTemplateMail

            - name: Run Tests
              run: |
                  cd custom/plugins/FroshPlatformTemplateMail/
                  php -d pcov.enabled=1 ../../../vendor/bin/phpunit --coverage-clover clover.xml

```
