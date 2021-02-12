# Omnipay: EpayNC 

**EpayNC driver for the Omnipay PHP payment processing library**

[Omnipay](https://github.com/omnipay/omnipay) is a framework agnostic, multi-gateway payment
processing library for PHP 5.3+. This package implements SecurePay support for Omnipay.

## Installation

Omnipay is installed via [Composer](http://getcomposer.org/). To install, simply add it
to your `composer.json` file:

```json
{
    "require": {
        "oneshot-nc/omnipay-epaync": "dev-master"
    }
}
```

And run composer to update your dependencies:

    $ curl -s http://getcomposer.org/installer | php
    $ php composer.phar update

## Basic Usage

The following gateways are provided by this package:

* EpayNC

For general usage instructions, please see the main [Omnipay](https://github.com/omnipay/omnipay)
repository.

### Advanced Usage

#### Saving Cards

##### Creating a token during payment

```php
$paymentParams = array(
    ...
    'createCard' => true,
    'ownerReference' => 'an owner reference',
));
$purchaseRequest = $gateway->purchase($paymentParams);
$redirectResponse = $purchaseRequest->send();
```

##### Creating a token without payment

```php
$paymentParams = array(
    ...
    'ownerReference' => 'an owner reference',
));
$createCardRequest = $gateway->createCard($paymentParams);
$redirectResponse = $createCardRequest->send();
```

##### Retrieve a token in the purchase payzen callback reponse

```php
$paymentParams = array(
    ...
));
$completePurchaseRequest = $gateway->completePurchase($paymentParams);
$callbackResponse = $completePurchaseRequest->send();
if ($callbackResponse->hasCreatedCard()) {
    $cardReference = $callbackResponse->getCardReference();
    $ownerReference = $callbackResponse->getOwnerReference();
}
```

#### Paying using saved Cards

```php
$paymentParams = array(
    ...
    'cardReference' => 'XXXXXXXXXX',
));
$purchaseRequest = $gateway->purchase($paymentParams);
$redirectResponse = $purchaseRequest->send();
```

## Support

If you are having general issues with Omnipay, we suggest posting on
[Stack Overflow](http://stackoverflow.com/). Be sure to add the
[omnipay tag](http://stackoverflow.com/questions/tagged/omnipay) so it can be easily found.

If you want to keep up to date with release anouncements, discuss ideas for the project,
or ask more detailed questions, there is also a [mailing list](https://groups.google.com/forum/#!forum/omnipay) which
you can subscribe to.

If you believe you have found a bug, please report it using the [GitHub issue tracker](https://github.com/omnipay/securepay/issues),
or better yet, fork the library and submit a pull request.
