# domaintoolsAPI PHP Wrapper #

## Presentation ##

The domaintoolsAPI PHP Wrapper is a simple connector to access all webservices of [domaintools.com](http://domaintools.com "domaintools.com").

## Getting started ##

1- Clone the project with Git by running:

    $ git clone git://github.com/domaintools/domaintoolsAPI_php_wrapper

   Or download the project in either [zip](https://github.com/domaintools/domaintoolsAPI_php_wrapper/zipball/master "Download in zip format") or [tar](https://github.com/domaintools/domaintoolsAPI_php_wrapper/tarball/master "Download in tar format") formats.

2- Rename the **api.ini.default** to **api.ini**

3- Fill **api.ini**  with your domaintools credentials:

    username  = 'your_api_username';
    key        = 'your_api_key';

3-A Create a short PHP file which requires the project domaintoolsAPI PHP wrapper and makes a simple call to a webservice (**whois** for example):

```php
<?php
  // Require domaintoolsAPI PHP wrapper
  require 'domaintoolsAPI_php_wrapper/DomaintoolsAPI_class.inc.php';

  //Make a call to the webservice whois with a xml return
  //type for the domain name : example.com
  $request = new DomaintoolsAPI();

  $request->from("whois") //name of the service (whois, info, availability)
          ->withType("xml") // Return type (JSON or XML)
          ->domain("example.com"); //Domain name

  $response = $request->execute();
  //Display the response
  echo $response;
?>
```

3-B If required you can also override on the fly your configuration :

```php
<?php
  // Require domaintoolsAPI PHP wrapper
  require 'domaintoolsAPI_php_wrapper/DomaintoolsAPI_class.inc.php';

  // we get the default configuration
  $configuration = new DomaintoolsAPIConfiguration();
  // we change some values
  $configuration->set('username','anotherUsername')->
          set('password','anotherPassword');
  //Make a call to the webservice whois with a xml return
  //type for the domain name : example.com
  $request = new DomaintoolsAPI($configuration);
  $request->from("whois")
          ->withType("json")
          ->domain("example.com");
  $response = $request->execute();
  //Display the response
  echo $response;
?>
```

4- Execute the PHP script:

    $ php testDomaintoolsAPI.php

   If everything works fine, you should have a display like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Response>
  <service>whois</service>
  <domain>example.com</domain>
  <timestamp>1296054220</timestamp>
  <content>
    <whois>&lt;![CDATA[
      Whois Server Version 2.0

      Domain names in the .com and .net domains can now be registered
      with many different competing registrars. Go to http://www.internic.net
      for detailed information.

      EXAMPLE.COM.AU
      EXAMPLE.COM

      To single out one record, look it up with "xxx", where xxx is one of the
      of the records displayed above. If the records are the same, look them up
      with "=xxx" to receive a full display for each record.

      &gt;&gt;&gt; Last update of whois database: Tue, 25 Jan 2011 14:37:03 UTC &lt;&lt;&lt;

      NOTICE: The expiration date displayed in this record is the date the
      registrar's sponsorship of the domain name registration in the registry is
      currently set to expire. This date does not necessarily reflect the expiration
      date of the domain name registrant's agreement with the sponsoring
      registrar.  Users may consult the sponsoring registrar's Whois database to
      view the registrar's reported date of expiration for this registration.

      The Registry database contains ONLY .COM, .NET, .EDU domains and
      Registrars.
      ]]&gt;
    </whois>
  </content>
</Response>
```

5- Read the documentation to learn more, and visit [domaintools.com](http://domaintools.com "domaintools.com") to know the list of available services.

## Documentation ##

The domaintoolsAPI PHP Wrapper is a fluent API implemented by using method chaining.

After having instanciate your request like this:

```php
<?php $request = new DomaintoolsAPI(); ?>
```

You can combine methods to specify return type, options, etc.:

```php
<?php $request->from("thumbnail")->where(array("return" => "fullsize"))->withType("xml")->domain("example.com"); ?>
```

### Choose service to call - from ###

```php
<?php $request->from("whois"); ?>
```

You can find the list of available services on [domaintools.com](http://domaintools.com "domaintools.com") .

### Call the service - execute ###

```php
<?php $request->from("whois")->domain("example.com")->execute(); ?>
```

To call the service use the method **execute**, and return the response.

The response is a string with the format of the specify return type (JSON or XML for example).

### Specify options - where ###

```php
<?php $request->from("domain-search")->where(array("query" => "domain tools")); ?>
```

The method **where** allows to specify options of the service. It takes only on parameter, an array of options where the key is the name of the option and value is the value of the option.

The list of options for each service is available on the [domaintoolsAPI documentation](http://domaintools.com/api/docs/ "domaintoolsAPI documentation") .

### Specify return type - withType ###

```php
<?php $request->from("whois")->withType("json"); ?>
```
The method **withType** allows to specify the return type of the response. It takes only one parameter, the **name** of the return type.

The list of return types is available on the [domaintoolsAPI documentation](http://domaintools.com/api/docs/ "domaintoolsAPI documentation") .

By default (If you don't call the method withType) the return type used is **json**.

## Changelog ##

See the CHANGELOG.rdoc file for details.

## License ##

Copyright (C) 2011 by domaintools.com, DomaintoolsAPI PHP Wrapper is released under the MIT license.

See the LICENSE.md file for details.
