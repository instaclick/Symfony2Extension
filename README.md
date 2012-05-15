Symfony2Extension
=================

Provides integration layer for Symfony2:

* Complete integration into Symfony2 bundle structure - you can run isolated
  bundle suite by bundle shortname, classname or even full path
* `KernelAwareInterface`, which provides initialized and booted kernel instance
  for your contexts
* Additional `symfony` session (sets as default) for Mink (if `MinkExtension` is installed)

between Behat 2.4+ and Symfony2+

Installation
------------

This extension requires:

* Behat 2.4+

Download Behat phar from:

* [Behat downloads](https://github.com/Behat/Behat/downloads)

After downloading and placing behat.phar into project directory, you need to download and
activate `Symfony2Extension`:

1. [Download extension](https://github.com/downloads/Behat/Symfony2Extension/symfony2_extension.phar)
2. Put downloaded phar package into folder with Behat
3. Tell Behat about extensions with `behat.yml` configuration:

    ``` yaml
    # behat.yml
    defaults:
      # ...
      extensions:
        symfony2_extension.phar: ~
    ```

    For all configuration options, check [extension configuration
    class](https://github.com/Behat/MinkExtension/blob/master/src/Behat/Symfony2Extension.php#L61-90).

Usage
-----

After installing extension, there would be 2 usage options available for you:

1. If you're on the php 5.4+, you can simply use `Behat\Symfony2Extension\Context\KernelDictionary`
   trait inside your `FeatureContext` or any of its subcontexts. This trait will provide
   `getKernel()` and `getContainer()` methods for you.
2. Implementing `Behat\Symfony2Extension\Context\KernelAwareInterface` with your context or its
   subcontexts.
   This will give you more customization options. Also, you can use this mechanism on multiple
   contexts avoiding the need to call parent contexts from subcontexts when only thing you need
   is mink instance.

There's common thing between those 2 methods. In each of those, target context will implement
`setKernel(HttpKernel $kernel)` method. This method would be automatically called **immediately after** each context creation before each scenario. Note that this kernel will be automatically
rebooted between scenarios, so your scenarios would have almost absolutely isolated state.

Initialize bundle suite
-----------------------

Just run:

``` bash
$> php behat.phar --init @YouBundleName
```

Run bundle suite
----------------

``` bash
$> php behat.phar @YouBundleName
```

Copyright
---------

Copyright (c) 2012 Konstantin Kudryashov (ever.zet). See LICENSE for details.

Contributors
------------

* Konstantin Kudryashov [everzet](http://github.com/everzet) [lead developer]
* Other [awesome developers](https://github.com/Behat/MinkExtension/graphs/contributors)

Sponsors
--------

* knpLabs [knpLabs](http://www.knplabs.com/) [main sponsor]