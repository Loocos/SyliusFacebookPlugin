# Sylius Facebook Plugin

[![Latest Version][ico-version]][link-packagist]
[![Software License][ico-license]](LICENSE)
[![Build Status][ico-github-actions]][link-github-actions]

Track user behavior in Facebook.

## Installation

### Step 1: Download the plugin

Open a command console, enter your project directory and execute the following command to download the latest stable version of this plugin:

```bash
$ composer require setono/sylius-facebook-plugin
```

This command requires you to have Composer installed globally, as explained in the [installation chapter](https://getcomposer.org/doc/00-intro.md) of the Composer documentation.

### Step 2: Enable the plugin

Then, enable the plugin by adding it to the list of registered plugins/bundles
in `config/bundles.php` file of your project before (!) `SyliusGridBundle`:

```php
<?php
$bundles = [
    Setono\BotDetectionBundle\SetonoBotDetectionBundle::class => ['all' => true],
    Setono\SyliusFacebookPlugin\SetonoSyliusFacebookPlugin::class => ['all' => true],
    Sylius\Bundle\GridBundle\SyliusGridBundle::class => ['all' => true],
];
```

If you want to enable consent (i.e. cookie / gdpr) you can install the [consent bundle](https://github.com/Setono/ConsentBundle).

### Step 3: Configure plugin

```yaml
# config/packages/setono_sylius_facebook.yaml
imports:
    - { resource: "@SetonoSyliusFacebookPlugin/Resources/config/app/config.yaml" }
    
    # Uncomment next line if you want to load some example pixels via fixtures
    # - { resource: "@SetonoSyliusFacebookPlugin/Resources/config/app/fixtures.yaml" }
```

### Step 4: Import routing

```yaml
# config/routes/setono_sylius_facebook.yaml
setono_sylius_facebook:
    resource: "@SetonoSyliusFacebookPlugin/Resources/config/routes.yaml"
```

### Step 5: Update your database schema

```bash
$ php bin/console doctrine:migrations:diff
$ php bin/console doctrine:migrations:migrate
```

### Step 6: Create a pixel
When you create a pixel in Facebook you receive a pixel id.

Now create a new pixel in your Sylius shop by navigating to `/admin/pixels/new`.
Remember to enable the pixel and enable the channels you want to track. 

### Step 7: You're ready!
The events that are tracked are located in the [EventSubscriber folder](src/EventSubscriber).

## Related links
- https://developers.facebook.com/docs/marketing-api/audiences/guides/dynamic-product-audiences/#setuppixel
- https://developers.facebook.com/docs/marketing-api/conversions-api
- https://developers.facebook.com/docs/marketing-api/conversions-api/using-the-api
- https://developers.facebook.com/docs/marketing-api/conversions-api/guides/business-sdk-features
- https://github.com/facebook/facebook-php-business-sdk

## Contribute
Ways you can contribute:
* Translate [messages](src/Resources/translations/messages.en.yaml) and [validators](src/Resources/translations/validators.en.yaml) to your mother tongue
* Create Behat tests that verifies the scripts are outputted on the respective pages
* Create new event subscribers that handle [Facebook events](https://developers.facebook.com/docs/facebook-pixel/reference/) which are not implemented

Thank you!

[ico-version]: https://poser.pugx.org/setono/sylius-facebook-plugin/v/stable
[ico-license]: https://poser.pugx.org/setono/sylius-facebook-plugin/license
[ico-github-actions]: https://github.com/Setono/SyliusFacebookPlugin/workflows/build/badge.svg

[link-packagist]: https://packagist.org/packages/setono/sylius-facebook-plugin
[link-github-actions]: https://github.com/Setono/SyliusFacebookPlugin/actions
