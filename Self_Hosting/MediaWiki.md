---
title: MediaWiki
---

# Configuration
## License

You can change the license for your wiki by configuring the following configuration variables:

* [`$wgRightsIcon`](https://www.mediawiki.org/wiki/Manual:$wgRightsIcon)
* [`$wgRightsText`](https://www.mediawiki.org/wiki/Manual:$wgRightsText)
* [`$wgRightsUrl`](https://www.mediawiki.org/wiki/Manual:$wgRightsUrl)

### Example

```php
$wgRightsIcon = "$wgScriptPath/resources/assets/licenses/cc-by-nc-sa.png";
$wgRightsText = "Creative Commons Attribution-NonCommercial-Sharealike License";
$wgRightsUrl = "https://creativecommons.org/licenses/by-nc-sa/3.0/";
```

## SMTP

MediaWiki has a few examples that got me started: [`$wgSMTP` Examples](https://www.mediawiki.org/wiki/Manual:$wgSMTP#Examples).

Here's a sample configuration for FastMail:

```php
$wgSMTP = [
    'host'      => 'smtp.fastmail.com',
    'IDHost'    => 'YOURDOMAIN',
    'port'      => 587,
    'auth'      => true,
    'username'  => 'USERNAME',
    'password'  => 'PASSWORD'
];
```

# Debugging

Add the following to the top of your `LocalSettings.php`:

```php
error_reporting( -1 );
ini_set( 'display_errors', 1 );
$wgShowExceptionDetails = true;
```