Data types
==========

[Data types][data-types] in PHP are categorized in two groups, namely: scalar types and compound types. Scalar types can hold only one value, while compound types can hold several values.

Scalar types
------------

PHP is a loose typed language which means that the type of a variable is not predetermined and can change during its lifetime (although not always recommended). The data type of the variable is determined when assigning it a value. The four scalar data types are: [integer][int], [float][float], [string][string], [boolean][bool].

    <?php
    $someString = 'This is a string';
    $someInteger = 42;
    $someFloat = 3.14159265;
    $someBoolean = FALSE;

As you can see a string value consist of text and should always be enclosed in quotes (either single or double quotes). An integer value is is a whole number (without decimals). A float value (or double) is a number with decimals. A boolean value is either `true` or `false`.

> **Note:**
> As in most programming languages the decimal separator is a dot (`.`).

Compound types
--------------

PHP has two compound types: [array][array] and [object][object]. The object data type will be introduced in a later topic. An array can be seen as a list of values. These values can consist of all the different data types PHP offers. Instead of creating separate variables as in the previous example we could have also created an array to hold these values:

    <?php
    $someArray = array(
        'This is a string',
        42,
        3.14159265,
        FALSE,
    );

Once we have created our array we can access the different values by using an index. The indexes of arrays in PHP start with `0`. This index gets incremented when a new item is added. If we want to echo the number `3.14159265` from our array we have to access it by it's index (2):

    <?php
    $someArray = array(
        'This is a string',
        42,
        3.14159265,
        FALSE,
    );

    echo 'This is pi: ' . $someArray[2]; // this will output: This is pi: 3.14159265

It is also possible to initialize an empty array and add items to it later in the script:

    <?php
    $anotherArray = array();

    // let's add an item to the array
    $anotherArray[] = 'This item will be added at index 0';

    // let's add another item to the array
    $anotherArray[] = 'This is another item added to our array at index 1';

    echo 'This is the value of index 0 of our array: ' . $anotherArray[0]; // this will output: This is the value of index 0 of our array: This item will be added at index 0

PHP also supports named (or associative) arrays. This can be useful when storing specific data:

    <?php
    $user = array(
        'username' => 'PHP Dave',
        'fullname' => 'Dave Doe',
        'age'      => 42,
    );

    echo 'Welcome back ' . $user['username']; // will output: Welcome back PHP Dave

Instead of just adding values to our array (which would have gotten a numeric index starting at 0) we have now added name / value pairs to our array. Just like with arrays with numeric indexes it is possible to initialize an empty array and add items to it later:

    <?php
    $user = array();

    $user['username'] = 'PHP Dave';
    $user['fullname'] = 'Dave Doe';
    $user['age'] = 42;

It is not possible to simply display all the contents of an array by `echo`ing it:

    <?php
    $myArray = array(
        'First item',
        'Second item',
        'Third item',
    );

    echo $myArray;

This example will print the text `Array` rather than the contents of the array.

> **Note:**
> When debugging code it may be useful to see what an array (or any other variable for that matter) contains. To display all the contents of a variable we can use the builtin [`var_dump()` function][vardump]. E.g. in our previous example we could do: `var_dump($user);` to display the contents of our array (including the data types).

> **Note:**
> Since PHP 5.4 there is also support for a [short syntax][array-short] for arrays. An example for this is: `$user = ['username' => 'PHP Dave']`.

Loose typing
------------

PHP is a loose (or weak) typed language. This means that data types can change in their lifetime. This is easiest to see with an example:

    <?php
    $value1 = '13'; // this variable contains the string 13 (it's a string because it is enclosed in quotes)
    $value2 = 37; // this variable contains the integer 37

    echo $value1 + $value2; // this will output: 50

Because we are doing an addition of the two variables, PHP converts the first value into an integer to do the calculation. This is called [type juggling][type-juggling].

> **Note:**
> Although the value used in the calculation is converted in a string the original value in the variable `$value1` will still be a string.

[data-types]:http://php.net/manual/en/language.types.intro.php
[int]:http://php.net/manual/en/language.types.integer.php
[float]:http://php.net/manual/en/language.types.float.php
[string]:http://php.net/manual/en/language.types.string.php
[bool]:http://php.net/manual/en/language.types.boolean.php
[array]:http://php.net/manual/en/language.types.array.php
[array-short]:http://php.net/manual/en/language.types.array.php#language.types.array.syntax.modifying
[vardump]:http://php.net/manual/en/function.var-dump.php
[object]:http://php.net/manual/en/language.types.object.php
[type-juggling]:http://php.net/manual/en/language.types.type-juggling.php