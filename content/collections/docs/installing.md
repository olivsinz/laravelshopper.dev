---
id: 39a2b558-476a-4130-a179-be2265abb408
blueprint: page
title: 'Install Shopper'
intro: 'Quick start guide for installing and configuring Laravel Shopper on your existing Laravel App.'
template: page
---
## Supported Versions of Laravel

**Laravel 8 only is currently supported.** It feels like this section needs more than one sentence but it really doesn't. That first one said all that needs saying.

> Laravel 9 will be support at the next release. See the [release notes](https://github.com/shopperlabs/framework/releases) for more information.

## Install Shopper

Shopper is really easy to install. After creating your new app or in an existing Laravel app \(8+\). There are 2 steps to follow to install Shopper.

1. Run `php artisan config:clear` to make sure your config isn't cached.

2. Install `shopper/framework` with Composer.

    ``` shell
    composer require shopper/framework --with-dependencies
    ```
3. Add the following settings to your Tailwindcss config `tailwind.config.js`.
	```js
    module.exports = {
      ...
      presets: [
        ...
        require('./vendor/wireui/wireui/tailwind.config'), // [tl! focus]
        require('./vendor/shopper/framework/tailwind.config'), // [tl! focus]
      ],
      purge: [
        ...
        './vendor/shopper/framework/resources/**/*.blade.php', // [tl! focus]
        './vendor/wire-elements/modal/resources/views/*.blade.php', // [tl! focus]
        './vendor/rappasoft/laravel-livewire-tables/resources/views/tailwind/**/*.blade.php', // [tl! focus]
        './vendor/wireui/wireui/resources/**/*.blade.php', // [tl! focus]
        './vendor/wireui/wireui/ts/**/*.ts', // [tl! focus]
        './vendor/wireui/wireui/src/View/**/*.php' // [tl! focus]
      ],
      ...
    }
	```

## Write Env Variables

Next make sure to create a new database and add your database credentials to your .env file, you will also want to add your application URL in the `APP_URL` variable

   ```shell
    APP_URL=http://laravelshopper.test
    DB_HOST=localhost
    DB_DATABASE=homestead
    DB_USERNAME=homestead
    DB_PASSWORD=secret
    ```
    
## Automatic Installation

After installing Shopper in your project via compose and configuring the database, now we will automatically install in the project.

  ```shell
   php artisan shopper:install
  ```

This will install shopper, publish vendor files, create shopper and storage symlinks if they don't exist in the public folder, run migrations and seeders classes.


And we're all good to go!

## Update Existing Files

Extend your current User Model \(usually `app/Models/User.php`\) using the `Shopper\Framework\Models\User\User as Authenticatable` alias:

```php
// app/Models/User.php

use Shopper\Framework\Models\User\User as Authenticatable; 

class User extends Authenticatable
{
    // ...
}
```

## Create an Admin user

Now we can create a new superuser and sign into the Dashboard and start creating some content to display on the frontend.

Run the following command to create a user with supreme \(at the moment of creation\) rights:

```shell
php artisan shopper:admin
```

And you will be prompted for the user email, firstname, lastname and password.

    
## New Shopper Directory

After Shopper is installed, you'll have 1 new directory in your project:
- `config/shopper/`

## Publish Vendor Files

If you want to publish again Shopper's vendor files run these commands:

```shell
php artisan shopper:publish
```

To run the project you may use the built-in server: `php artisan serve`

After that, run `composer dump-autoload` to finish your installation!

If your are using Laravel Valet you can easily access with your project name with `.test` at the end when you navigate on you project.

```shell
http://laravelshopper.test/shopper
```