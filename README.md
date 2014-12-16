TzbSendyBundle
===============

[![SensioLabsInsight](https://insight.sensiolabs.com/projects/df46d30d-af90-4e31-b5af-c7dc4f4bd139/mini.png)](https://insight.sensiolabs.com/projects/df46d30d-af90-4e31-b5af-c7dc4f4bd139)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/jkabat/TbzSendyBundle/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/jkabat/TbzSendyBundle/?branch=master)

This bundle is used to integrate the [SendyPHP class from Jacob Bennett](https://github.com/JacobBennett/SendyPHP) into a symfony2 project.

Installation
============

Step 1: Download the Bundle
---------------------------

Open a command console, enter your project directory and execute the
following command to download the latest stable version of this bundle:

```bash
$ composer require tzb/sendy-bundle "~1"
```

This command requires you to have Composer installed globally, as explained
in the [installation chapter](https://getcomposer.org/doc/00-intro.md)
of the Composer documentation.

Step 2: Enable the Bundle
-------------------------

Then, enable the bundle by adding the following line in the `app/AppKernel.php`
file of your project:

```php
<?php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = array(
            // ...

            new Tzb\SendyBundle\TzbSendyBundle(),
        );

        // ...
    }

    // ...
}
```

Step 3: Configure `sendy_manager` Service
-----------------------------------------

```yaml
# app/config/config.yml
tzb_sendy:
    api_key: sendy_api_key
    api_host: http://sendy.installation.url
    list_id: default_list_id
```

Usage
=====

Get count of total active subscribers for default list:

```php
// get service
$sendy = $this->container->get('tzb_sendy.sendy_manager');
$count = $sendy->getSubscriberCount();
```

Get count of total active subscribers for other list:

```php
$sendy = $this->container->get('tzb_sendy.sendy_manager');
$count = $sendy->getSubscriberCount('other_list_id');
```

Get status of subscriber identified by e-mail:

```php
$sendy = $this->container->get('tzb_sendy.sendy_manager');
$status = $sendy->getSubscriberStatus('email@example.com');
```

Subscribe user to default list (other list id can be used as third parameter):

```php
$sendy = $this->container->get('tzb_sendy.sendy_manager');
$status = $sendy->subscribe('Name', 'email@example.com');
```

Unsubscribe user from default list (other list id can be used as second parameter):

```php
$sendy = $this->container->get('tzb_sendy.sendy_manager');
$status = $sendy->unsubscribe('email@example.com');
```

Versions
========

1.0.3 : 2014/12/16

* minor doc enhancements
* new: unit tests coverage

1.0.2 : 2014/12/12

* getError property removal
* new: SendyException

1.0.1 : 2014/12/11

* doc enhancement
* new: badges section

1.0.0 : 2014/12/11

* first release
