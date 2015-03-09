Error reporting
===============

Now that we know the basics of PHP it is time to look into error reporting. When you are working with PHP (or any other language for that matter) things may and will go wrong at some point. This may for example be the result of trying to write to a write protected file or perhaps a simple typo in your code. When something goes wrong it is always nice to know what exactly went wrong. For this PHP has error reporting in place. Error reporting will tell you what went wrong and also where in the code (linenumber).

Although PHP provides several different levels of error reporting it is considered best practice to display all possible errors (especially during the development phase of a project). Error reporting can be enabled in two places in PHP.

php.ini
-------

Error reporting can be enabled in the php.ini file. This file contains the "global" settings used by all PHP scripts on the server. To enable error reporting in the `php.ini` file you should find or add the following
lines and change them to the correct values:

    error_reporting = -1
    display_errors On

> **Note:**  
> Please note that changes made to the php.ini file will only be in effect after a restart of the webservice.

Runtime
-------

Error reporting can also be enabled in .php files. To do so we simply have to include two lines to the PHP file we are working on:

    <?php
    error_reporting(-1);
    ini_set('display_errors', 1);

> **Note:**  
> It is advised to always enable error reporting at the top of our file to catch any errors in our script.

> **Note:**  
> Setting the error reporting in a .php file will override the error reporting settings in the php.ini file.*

Once error reporting is enabled and there is an issue in our script PHP will show you what and where something is wrong:

    <?php
    echo 'This will produce an error because of the missing semicolon (;) at the end of the echo statement'
    echo 'This is another echo statement';

The above script will produce the following error:

> Parse error: syntax error, unexpected end of file, expecting ',' or ';' in /test.php on line 3

Production
----------

While it is very useful (if not mandatory) to have errors in our script displayed on the page while we are in the development phase of a project, it is considered bad practice to do so in the production environment. When displaying errors in our production environment some internal information may leak out to an potentional attacker. Because we do want to find out what is happening when something goes wrong we can set PHP up to only log errors instead of displaying them on the page.  This can also be done in either the php.ini file or at runtime by an `ini_set()` directive.

### php.ini

    error_reporting = -1
    display_errors Off
    log_errors On
    error_log /path/to/php-error.log

### runtime

    <?php
    error_reporting(-1);
    ini_set('display_errors', 0);
    ini_set('log_errors', 1);
    ini_set('error_log', '/path/to/php-error.log');

Debugging
=========

Showing and understanding errors outputted by PHP's error reporting is an important part of basic debugging the code you have written. Another important part of debugging your code is knowing what variables contain what data in certain places of your code. Luckily PHP also has built in functions for this purpose.

One way to check what a variable contain at a certain point in your code is by simply echoing the variable:

    <?php
    $name = 'Rasmus';

    echo $name;

Although this works perfectly fine for simple variables containing a single value the `echo` statement is less useful for outputting more complex variables (like for example `array`s):

    <?php
    $names = array(
        'Rasmus',
        'John',
    );

    echo $names;

The above example simply outputs `Array` which tells us the variable is an `array`, but it does not output the contents of the array. So `echo` is not very useful in this case. In case where the variable does not contains a simple (/ single) value we can make use of the built in [`var_dump`][var-dump] function:

    <?php
    $names = array(
        'Rasmus',
        'John',
    );

    var_dump($names);

Using `var_dump` in the example above we get a nice output containing all the contents of our variable:

    array(2) {
      [0]=>
      string(6) "Rasmus"
      [1]=>
      string(4) "John"
    }

As you can see `var_dump` provides us with a lot more useful (debugging) information than our simple `echo` statement. It shows the type of the variable (`array`) and it shows the number of elements in the variable `2`. Also it shows us the individual elements in the variable and at what position in the array (the index) they are found. It also show the type of the texts (`string`) and the length of the texts (`6` and `4`).

`var_dump` can even be used to output more complex structures like for example a menu structure on a website:

    <?php
    $menu = array(
        'home' => array(
            'name'    => 'Home',
            'url'     => '/',
            'active'  => false,
            'created' => new DateTime('2014-03-26 11:34:02'),
            'children' => array(),
        ),
        'productgroups' => array(
            'name'    => 'Productgroups',
            'url'     => '/productgroups',
            'active'  => true,
            'created' => new DateTime('2014-03-26 12:36:13'),
            'children' => array(
                'productgroup-1' => array(
                    'name'    => 'Productgroup 1',
                    'url'     => '/productgroups/productgroup-1',
                    'active'  => false,
                    'created' => new DateTime('2014-04-01 09:14:13'),
                    'children' => array(),
                ),
                'productgroup-2' => array(
                    'name'    => 'Productgroup 2',
                    'url'     => '/productgroups/productgroup-2',
                    'active'  => false,
                    'created' => new DateTime('2014-04-01 09:15:24'),
                    'children' => array(),
                ),
            ),
        ),
    );
    
    var_dump($menu);

Which results in the following output:

    array(2) {
      ["home"]=>
      array(5) {
        ["name"]=>
        string(4) "Home"
        ["url"]=>
        string(1) "/"
        ["active"]=>
        bool(false)
        ["created"]=>
        object(DateTime)#1 (3) {
          ["date"]=>
          string(26) "2014-03-26 11:34:02.000000"
          ["timezone_type"]=>
          int(3)
          ["timezone"]=>
          string(3) "UTC"
        }
        ["children"]=>
        array(0) {
        }
      }
      ["productgroups"]=>
      array(5) {
        ["name"]=>
        string(13) "Productgroups"
        ["url"]=>
        string(14) "/productgroups"
        ["active"]=>
        bool(true)
        ["created"]=>
        object(DateTime)#2 (3) {
          ["date"]=>
          string(26) "2014-03-26 12:36:13.000000"
          ["timezone_type"]=>
          int(3)
          ["timezone"]=>
          string(3) "UTC"
        }
        ["children"]=>
        array(2) {
          ["productgroup-1"]=>
          array(5) {
            ["name"]=>
            string(14) "Productgroup 1"
            ["url"]=>
            string(29) "/productgroups/productgroup-1"
            ["active"]=>
            bool(false)
            ["created"]=>
            object(DateTime)#3 (3) {
              ["date"]=>
              string(26) "2014-04-01 09:14:13.000000"
              ["timezone_type"]=>
              int(3)
              ["timezone"]=>
              string(3) "UTC"
            }
            ["children"]=>
            array(0) {
            }
          }
          ["productgroup-2"]=>
          array(5) {
            ["name"]=>
            string(14) "Productgroup 2"
            ["url"]=>
            string(29) "/productgroups/productgroup-2"
            ["active"]=>
            bool(false)
            ["created"]=>
            object(DateTime)#4 (3) {
              ["date"]=>
              string(26) "2014-04-01 09:15:24.000000"
              ["timezone_type"]=>
              int(3)
              ["timezone"]=>
              string(3) "UTC"
            }
            ["children"]=>
            array(0) {
            }
          }
        }
      }
    }

Although this variable has a much more complex structure the same rule apply as in our previous examples. `var_dump` outputs the contents and the type of every element in our variable.

Xdebug
------

Another useful tool for debugging your PHP code is [Xdebug][xdebug]. Xdebug formats (amongst others) the error and the `var_dump` outputs of PHP. Xdebug is not installed by default on most PHP installation, but can be downloaded from [their site][xdebug]. Xdebug can also be used to step through code (there is also integration with IDEs).

[var-dump]:http://nl1.php.net/manual/en/function.var-dump.php
[xdebug]:http://xdebug.org
