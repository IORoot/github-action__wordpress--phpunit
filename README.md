# WP-Github-Action-Workflow

This is a working example of using a github action workflow to test a Wordpress plugin.

It's using the wordpress phpunit test suite.

This example does the following things:

- Install Ubuntu, MySQL, PHP, PHPUnit & Composer
- Download the current repo
- Download a second 'private' repo using a deploy key secret.
- Install your phpunit tests for the current plugin.
- Run PHPUnit 

## Main.yml

This file is commented and explains each part of it. Use it in your `/.github/workflows/main.yml` file within your repository.

## tests/Bootstrap.php

This file contains a little bit of customised code to pull in a second dependent plugin to test the original plugin.

My scenario was that I'm using the ACF plugin on the admin pages and needed to pull it in to test my plugin. 

The slight problem was that on my server, the folder structure will be:

    wp-content/
        plugins/
            advanced-custom-fields/
            my-cool-plugin/

But within the Github action container, the ACF plugin is being pulled into the same directory as the current repo, like this:

    wp-content/
        plugins/
            my-cool-plugin/ 
                advanced-custom-fields/

So the bootstrap.php file will check for the difference and load the approriate one, like this:

```php

    $path = '';
    if (!is_dir(dirname(dirname(__FILE__)) . '/second-plugin-to-add'))
    {
        $path = '../';
    }
    require dirname(dirname(__FILE__)) . '/'.$path.'second-plugin-to-add/my_second_plugin.php';		// ACF

```

Now it will run by pulling in ACF from the right location.

