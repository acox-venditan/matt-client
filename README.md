# PHP Client for MATT notifications #

## Getting Started ##

When you need to know if some regular process stops working, do this

```php
MATT::expect('My cron finished OK')->every('15m')->sms('07777123456');
```

If something should never happen, do this

```php
MATT::expect('Some horrible error')->never()->email('bill@microsoft.com');
```

You can used named targets and groups that have been set up too, so in this example 'support' means several people

```php
MATT::expect('Some other horrible error')->never()->email('support');
```

## Event Names ##

The `expect()` singleton factory method takes an event name/identifier as a parameter.  These are limited to 32 characters and will be truncated.

We trigger a `E_USER_WARNING` when we do this.

## Intervals ##

The `every()` method take a string parameter to represent intervals. Supported interval strings are one of

- minute
- hour
- day
- week
- month

OR, one of the following time representations, where N is a number

- Nm
- Nh
- Nd

## Cancellation (stop monitoring) ##

If you need to stop the server monitoring a particular event, use `cancel` like this

```php
MATT::expect('Some other horrible error')->cancel();
```

## API calls with PHP Streams ##

As we don't know what sort of platforms we are going to be deployed on to, we don't use Curl in case it's not installed.

So, HTTP calls are made using PHP native Streams and associated context options.

HTTP calls are made on `__destruct()` of each `MATT` instance. If the call fails, an `E_USER_WARNING` triggered.

If the response from the server includes a textual message, this is pushed out with an `E_USER_NOTICE`.

## PHP Version Support ##

Desired compatibility with PHP 5.3.0 and above.

## Coding Standards ##

Desired adherence to [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md).
