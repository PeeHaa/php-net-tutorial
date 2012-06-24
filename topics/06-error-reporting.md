Error reporting
===============

Now that we know the basics of PHP it is time to look into error reporting. When you are working with PHP (or any other language for that matter) things may and will go wrong at some point. This may for example be the result of trying to write to a write protected file or perhaps a simple typo in your code. When something goes wrong it is always nice to know what exactly went wrong. For this PHP has error reporting in place. Error reporting will tell you what went wrong and also where in the code (linenumber).

Although PHP provides several different levels of error reporting it is considered best practice to display all possible errors (especially during the development phase of a project). Error reporting can be enabled in two places in PHP.

php.ini
-------

Error reporting can be enabled in the php.ini file. This file contains the "global" settings used by all PHP  
scripts on the server. To enable error reporting in the `php.ini` file you should find or add the following  
lines and change them to the correct values:

    error_reporting = -1
    display_errors On

> **Note:**  
> Please note that changes made to the php.ini file will only be in effect after a restart of the webservice.

Runtime
-------

Error reporting can also be enabled in .php files. To do so we simply have to include two lines to the PHP  
file we are working on:

    <?php
    error_reporting(-1);
    ini_set('display_errors', 1);

> **Note:**  
> It is advised to always enable error reporting at the top of our file to catch any errors in our script.

> **Note:**  
> Setting the error reporting in a .php file will override the error reporting settings in the php.ini file.*

Once error reporting is enabled and there is an issue in our script PHP will show you what and where something  
is wrong:

    <?php
    echo 'This will produce an error because of the missing semicolon (;) at the end of the echo statement'
    echo 'This is another echo statement';

The above script will produce the following error:

> Parse error: syntax error, unexpected end of file, expecting ',' or ';' in /test.php on line 3