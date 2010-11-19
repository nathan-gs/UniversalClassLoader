UniversalClassLoader implements a "universal" autoloader for PHP 5.3.
It is able to load classes that use either:

 * The [technical interoperability standards for PHP 5.3 namespaces and
   class names](http://groups.google.com/group/php-standards/web/psr-0-final-proposal).
 * [The PEAR naming convention](http://pear.php.net) for classes.

Classes from a sub-namespace or a sub-hierarchy of PEAR classes can be
looked for in a list of locations to ease the vendoring of a sub-set of
classes for large projects.

Example usage:

    $loader = new UniversalClassLoader();
    
    // register classes with namespaces
    $loader->registerNamespaces(array(
        'Symfony\Component' => __DIR__.'/component',
        'Symfony' => __DIR__.'/framework',
    ));
    
    // register a library using the PEAR naming convention
    $loader->registerPrefixes(array(
        'Swift_' => __DIR__.'/Swift',
    ));
    
    // activate the autoloader
    $loader->register();
    
In this example, if you try to use a class in the Symfony\Component
namespace or one of its children (Symfony\Component\Console for instance),
the autoloader will first look for the class under the component/
directory, and it will then fallback to the framework/ directory if not found before giving up.

###Credits
This UniversalClassLoader is a copy of The [Symfony2 UniversalClassLoader](https://github.com/symfony/symfony/blob/master/src/Symfony/Component/HttpFoundation/UniversalClassLoader.php). It's made
& opensourced by Fabien Potencier of Sensio Labs for the [Symfony2 Framework](http://symfony-reloaded.org),
it can be found on the [Symfony2 github](https://github.com/symfony/symfony) page. 

