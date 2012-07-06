Basic commands and operations
=============================

Printing content
--------------

One of the most common things you want to do is display content. In the previous topics we have already done it. To display a message we can simply do:

    <?php
    echo 'This is the text that is going to be displayed';

On the first line we have started PHP mode by adding the PHP opening tag `<?php`. On the second line we instruct PHP to display the text `This is the text that is going to be displayed`. As you can see the text is encapsulated in quotes. This is mandatory (for strings). We close the `echo` statement with a semi colon (`;`).

> **Note:**
> To do basic printing in PHP we can either use [`echo`][echo] or [`print`][print]. If we would have replaced `echo` with print in the previous example the outcome would have been the same.

Arithmetic
----------

PHP support all kinds of [arithmetic operations][arithmetic]. We can do additions, substractions, multiplications, divisions and modules operations:

    <?php
    echo 5 + 3; // will print 8
    echo 5 - 3; // will print 2
    echo 5 * 3; // will print 15
    echo 5 / 3; // will print 1.6666666666667
    echo 5 % 3; // will print 2

> **Note:**
> In the above example we haven't added quotes around the things we wanted to print, because otherwise PHP would have interpreted it as a string and the result of (for example) the first echo line would have been `5 + 3` instead of the calculated `8`.

PHP has a lot of useful builtin functions for [math operations][math].

Variables
---------

Variables can be used to store information in for later use. [Variable][variables] in PHP always start with a dollar sign (`$`). After the dollar sign comes the name of the variable. The name must begin with either letter or an underscore. A variable name may only contain alpha-numeric characters and underscores (`a-z`, `A-Z`, `0-9`, or `_`).

A simple example of using variables in PHP:

    <?php
    $userAge = 28;

    echo 'Your current age is: ' . $userAge . ', in 10 years your age will be: ' . ($userAge + 10);

This example will display: `You current age is: 28, in 10 years your age will be: 38`. As you can see in this example there are some things going on we haven't seen yet.

What happens on the second line of our script (`$userAge = 28;`) is that we have created a new variable called `userAge` and have assigned a value to it (`28`). Now `$userAge` represents the number 28. In the last line of our script we are using the variable to display the current age of the user and the age after 10 years.

Another thing we can see in our example is that we are using a dot (`.`) to "tie together" the string we want to output. This is called [string concatenation][string-operators]. This enables us to add the contents of our variable to the output. The last thing we see in our previous example is that we do a arithmetics operation on our variable and have enclosed it in parentheses `()`. This way the outcome of the operation (`38`) will be added to our string.

> **Note:**
> Variable names are case sensitive so `$userAge` is not the same as `$userage`.

Quotes
------

Strings in PHP must always be enclosed in quotes. There are two types of quotes which can be used for this. Single quotes (`'`) and double quotes (`"`). A string in single quotes means a literal string in PHP. A string in double quotes is parsed by PHP. If we take the previous (simplified) example again we can see what the difference is between the two:

    <?php
    $userAge = 28;

    echo 'Your current age is: $userAge'; // prints: Your current age is: $userAge
    echo "Your current age is: $userAge"; // prints: Your current age is: 28

As you can see in the first `echo` line it is printed "as is". The reason we have used string concatenation (the dot notation) instead of a double quoted string in our previous example is because PHP doesn't parse the calculation, but only the variable. So if we would have done:

    <?php
    $userAge = 28;

    echo "Your current age is: $userAge , in 10 years your age will be: ($userAge + 10)";

The result would have been: Your current age is: 28 , in 10 years your age will be: (28 + 10)

A benefit of the support of two types of quotes is that we can use the the other type in the string. A good example for this is when printing html using PHP:

    <html>
      <head>
        <title>Quote Example</title>
      </head>
      <body>
        <form action="">
          <?php echo '<input type="text" name="example">'; ?>
          <input type="submit" name="Submit">
        </form>
      </body>
    </html>

In the above example we have used a string in single quotes. Because of this we can use double quotes inside the string for the HTML attributes.

Escaping
--------

It is sometimes neccesary to use a single quote inside a single quoted string or a double quote inside a double quoted string. In order to do this we need to escape the quote inside the string using the escape character (`\`):

    <?php
    echo 'This is an example of an escaped quote (\').'; // prints: This is an example of an escaped quote (').
    echo "This is an example of an escaped quote (\")."; // prints: This is an example of an escaped quote (").

> **Note:**
> If you want to print a backslash you must escape it with a backslash: `echo "This string contains a backslash (\\).";`. This is only needed inside a doublequoted string.

[echo]:http://php.net/manual/en/function.echo.php
[print]:http://php.net/manual/en/function.print.php
[arithmetic]:http://php.net/manual/en/language.operators.arithmetic.php
[math]:http://www.php.net/manual/en/ref.math.php
[variables]:http://www.php.net/manual/en/language.variables.php
[string-operators]:http://php.net/manual/en/language.operators.string.php