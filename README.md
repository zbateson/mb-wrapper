# zbateson/mb-wrapper

Charset conversion and string manipulation wrapper with a large defined set of aliases.

[![Tests](https://github.com/zbateson/mb-wrapper.svg/actions/workflows/tests.yml/badge.svg)](https://github.com/zbateson/mb-wrapper.svg/actions/workflows/tests.yml)
[![Code Coverage](https://scrutinizer-ci.com/g/zbateson/mb-wrapper/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/zbateson/mb-wrapper/?branch=master)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/zbateson/mb-wrapper/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/zbateson/mb-wrapper/?branch=master)
[![Total Downloads](https://poser.pugx.org/zbateson/mb-wrapper/downloads)](https://packagist.org/packages/zbateson/mb-wrapper)
[![Latest Stable Version](https://poser.pugx.org/zbateson/mb-wrapper/version)](https://packagist.org/packages/zbateson/mb-wrapper)

The goals of this project are to be:

* Well written
* Tested where possible
* Support as wide a range of charset aliases as possible

To include it for use in your project, please install via composer:

```
composer require zbateson/mb-wrapper
```

## Php 7 Support Dropped

As of mb-wrapper 2.0, support for php 7 has been dropped.

## Requirements

mb-wrapper requires PHP 8.0 or newer.  Tested on PHP 8.0, 8.1, 8.2, 8.3, and 8.4 on GitHub Actions.

## New in 2.0

If converting or performing an operation on a string fails in iconv, an UnsupportedCharsetException is now thrown.

## Description

MbWrapper is intended for use wherever mb_* or iconv_* is used.  It scans supported charsets returned by mb_list_encodings(), and prefers mb_* functions, but will fallback to iconv if a charset isn't supported by the mb_ functions.

A list of aliased charsets is maintained for both mb_* and iconv, where a supported charset exists for an alias.  This is useful for mail and http parsing as other systems may report encodings not recognized by mb_* or iconv.

Charset lookup is done by removing non-alphanumeric characters as well, so UTF8 will always be matched to UTF-8, etc...

## Usage

The following wrapper methods are exposed:
* mb_convert_encoding, iconv with MbWrapper::convert
* mb_substr, iconv_substr with MbWrapper::getSubstr
* mb_strlen, iconv_strlen with MbWrapper::getLength
* mb_check_encoding, iconv (for verification) with MbWrapper::checkEncoding

```php
$mbWrapper = new \ZBateson\MbWrapper\MbWrapper();
$fromCharset = 'ISO-8859-1';
$toCharset = 'UTF-8';

$mbWrapper->convert('data', $fromCharset, $toCharset);
$mbWrapper->getLength('data', 'UTF-8');
$mbWrapper->substr('data', 'UTF-8', 1, 2);

if ($mbWrapper->checkEncoding('data', 'UTF-8')) {
    echo 'Compatible';
}
```

## License

BSD licensed - please see [license agreement](https://github.com/zbateson/mb-wrapper/blob/master/LICENSE).
