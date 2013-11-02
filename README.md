Scanner for PHP.ini
===========================

[![Build Status](https://secure.travis-ci.org/psecio/iniscan.png?branch=master)](http://travis-ci.org/psecio/iniscan)

The Iniscan is a tool designed to scan the given php.ini file for common security practices
and report back results. Currently it is only for use on the command line and reports the
results back to the display for both Pass and Fail on each test.

*Installation*

Using Composer:

```
{
    "require": {
        "psecio/iniscan": "dev-master"
    }
}
```

The only current dependency is the Symfony console.

*Example usage:*

```
vendor/bin/iniscan scan --path=/path/to/php.ini
```


*Example results:*

```
Results for /private/etc/php.ini:
============
Status | Severity | Key                      | Description
----------------------------------------------------------------------
PASS   | ERROR    | session.use_cookies      : Must use cookies to manage sessions
FAIL   | WARNING  | session.cookie_domain    : It is recommended that you set the default domain for cookies.
FAIL   | WARNING  |                          : Path /tmp is world writeable

1 passing
2 failure(s)
```

#### Command line usage

*Iniscan* offers a few commands for both checking and showing the contents of your php.ini.

##### Scan

The `scan` command will be the most used - it runs the rules checks against the given ini file and reports back the results. For example:

```
vendor/bin/iniscan scan --path=/path/to/php.ini
```

If the path is omitted, *iniscan* will try to find it based off the current configuration (a "php -i" call). By default, this reports back both the pass and fail results of the checks. If you'd like to only return the failures, you can use the `fail-only` argument:

```
vendor/bin/iniscan scan --path=/path/to/php.ini --fail-only
```

The `scan` command will return an exit code based on the results:

- 0: No errors
- 1: Failures found

##### Show

The `show` command lists out the contents of your `php.ini` file with a bit of extra formatting.

```
vendor/bin/iniscan show --path=/path/to/php.ini
```

##### List

The `list` command shows a listing of the current rules being checked and their related php.ini key.

```
vendor/bin/iniscan list
```

#### Output formats

By default *iniscan* will output information directly to the console in a human-readable result. You can also specify other output formats that may be easier to parse programatically (like JSON). Use the `--format` option to change the output:

```
vendor/bin/iniscan show --path=/path/to/php.ini --format=json
```

**NOTE:** Currently, only the `scan` command supports alternate output formats - and only two: console and JSON.


@author Chris Cornutt <ccornutt@phpdeveloper.org>
