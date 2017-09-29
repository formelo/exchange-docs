# Introduction

## Overview {#overview}

## Authentication {#auth}

{% method %}
## Types {#types}

| Tag           | Description           |
| ----:         | :----                 |
| `string`      | A sequence of characters from the Unicode and [ISO 10646](https://en.wikipedia.org/wiki/ISO_10646) character sets |
| `alphanum`    | A `string` value that consists of numeric digits, and characters in the [ISO basic Latin alphabet](https://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet). |
| `uri`         | A URI in conformance with [RFC 3986](https://www.ietf.org/rfc/rfc3986.txt). Unless specified otherwise, the only valid schemes are `http` and `https`. |
| `imageuri`    | A `uri` value that is also valid with [RFC 2397](https://www.ietf.org/rfc/rfc2397.txt). The supported media types include `image/jpg`, `image/gif`, and `image/png`. |
| `date`        | A date represented in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format e.g. `2017-03-31`|
| `datetime`    | A date and time represented in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format e.g. `2017-03-31T19:28:55Z`. It defaults to UTC or the time zone of the account |
| `timestamp`   | A time represented as an `int64`. Measured in seconds since the Unix epoch.|
| `int8`        | A whole number in the range −128 to +127. The unsigned form is the range 0 and 255. |
| `int16`       | A whole number in the range −32,768 to +32,767. The unsigned form is the range 0 and 65,535. |
| `int32`       | A whole number in the range −2,147,483,647 to +2,147,483,64. The unsigned form is the range 0 and 4,294,967,295. |
| `int64`       | A whole number in the range −9,223,372,036,854,775,808 to +9,223,372,036,854,775,807. The unsigned form is the range 0 and 18,446,744,073,709,551,615.|
| `float`       | A floating precision number in the range ±3.40282347E+38F (6-7 significant decimal digits) . |
| `double`      | A floating precision number in the range ±1.79769313486231570E+308 (15 significant decimal digits). |
| `numeric`     | Any whole or floating precision number type. |
| `unsigned`    | Denotes the unsigned form of a `numeric` type. |
| `minlen=x`    | A `string` value with at least `x` characters |
| `maxlen=x`    | A `string` value with at most `x` characters |
| `minval=x`    | A `numeric` value that is greater than or equal to `x` |
| `maxval=x`    | A `numeric` value that is less than or equal to `x` |

{% common %}


{% endmethod %}

## Errors {#errors}

## Idempotency {#idempotency}

## Pagination {#pagination}

## Versioning {#versioning}

## Patching {#patch}