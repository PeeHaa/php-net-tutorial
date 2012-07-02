Conditional Statements
======================

Conditional statements can be used to execute or "exclude" certain parts of the script based on a certain condition. We have several ways of doing this. This simpliest way is based on a single condition. This is done by an [`if`][if] statement:

    <?php
    $userAge = 42;

    if ($userAge > 60) {
        echo 'You are over 60.';
    }

This script will not output anything, because the `echo` statement is inside the condition statement. In the above example the `echo` statement will only be executed when the `$userAge` variable contains a value over 60. This is because we are checking using the greater than sign `>` in our conditional statement. An overview of all the [comparison operators[operator-comparison] avaiable will be shown in the next example:

    <?php
    $userAge = 42;

    // check whether age equals 42
    if ($userAge == 42) {
        echo 'You are 42.';
    }

    // check whether age doesn't equal 42
    if ($userAge != 42) {
        echo 'You are not 42.';
    }

    // check whether age is smaller than 42
    if ($userAge < 42) {
        echo 'You are younger than 42.';
    }

    // check whether age is greater than 42
    if ($userAge > 42) {
        echo 'You are over 42.';
    }

    // check whether age is smaller than or equal to 42
    if ($userAge <= 42) {
        echo 'You are either 42 or younger.';
    }

    // check whether age is greater than or equal to 42
    if ($userAge >= 42) {
        echo 'You are either 42 or older.';
    }

In the previous example we have only checked for one single condition. It is also possible to check multiple conditions in the same `if` statement:

    <?php
    $userAge = 42;
    $isAdmin = TRUE;

    if ($userAge > 60 && $isAdmin) {
        echo 'You are a grumpy old administrator.';
    }

In this example we are checking for two things. The first thing is whether the user is over 60 and the second thing is whether the user is an admin. Only if both conditions are met the `echo` statement will be displayed. This is because we have use the "and" operator `&&`. We can also check whether one of the two conditions is met:

    <?php
    $userAge = 42;
    $isAdmin = TRUE;

    if ($userAge > 60 || $isAdmin) {
        echo 'You are a either old or an administrator.';
    }

In the above example we have used the "or" operator `||`.

Another useful "trick" is grouping. With grouping we can group multiple conditions inside other conditions:

    <?php
    $user = array(
        'length' => '1.82',
        'gender' => 'male',
    );

    if (($user['length'] > 1.76 && $user['gender'] == 'female') || ($user['length'] > 1.8 && $user['gender'] == 'male')) {
        echo 'You are taller than the average person.';
    }

In this example we have grouped two conditions. Grouping conditions is done by wrapping the conditions in extra parentheses (`()`). The reason we have used grouping in this example is because the average length of women is smaller than the average length of men. The example check whether the user is a woman taller than 1.76 feet OR the user is a man taller than 1.8 feet. If one of these conditions are met the text will be displayed.

Now that we have seen the simplest form of conditional statements we can take it a bit further:

    <?php
    $movies = array(
        'Pulp Fiction',
        'Hackers',
    );

    if (count($movies) < 5) {
        echo 'You have a small collection of movies.';
    } else {
        echo 'You have a decent number of movies on your collection.';
    }

In this conditional statement we have introduced two new things. The first is the builtin function [`count()`][count]. Count returns the number of items in an array (or object). In our case it will return `2`. The second thing we see in this example is that besides `if` we have also used [`else`][else]. We happens in our statement is the we check whether our movie collection has less than 5 movies in it and if that is the case we display the text `You have a small collection of movies.`, but otherwise the text `You have a decent number of movies on your collection.` will be displayed.

We can even take this example one step further by adding an [`elseif`][elseif] statement:

    <?php
    $movies = array(
        'Pulp Fiction',
        'Hackers',
    );

    if (count($movies) == 0) {
        echo 'Don't you like movies?';
    } elseif (count($movies) < 5) {
        echo 'You have a small collection of movies.';
    } else {
        echo 'You have a decent number of movies on your collection.';
    }

In this example we are first checking whether there are any movies in our array. When the number of movies is greater than 0 it goes further to the next statement which checks whether out movie collection contains less then 5 movies. And otherwise the text `You have a decent number of movies on your collection.` will be displayed. Not that when we would have 0 movies in our collection only the text `Don't you like movies?` would be displayed although 0 is also less than 5. This is because PHP stops checking for the other conditions once a condition is met. You can have as many `elseif` statement as you like / need.

    <?php
    $movies = array(
        'Pulp Fiction',
        'Hackers',
    );

    if (count($movies) == 0) {
        echo 'Don't you like movies?';
    } elseif (count($movies) < 5) {
        echo 'You have a small collection of movies.';
    } elseif (count($movies) < 20) {
        echo 'You have a decent number of movies on your collection.';
    } else {
        echo 'I heard you like movies.';
    }

Another form of a conditional statement is a [`switch`][switch] statement:

    <?php
    $animal = array(
        'name' => 'Elephant',
        'type' => 'land',
    );

    switch($animal['type']) {
        case 'land':
            echo $animal['name'] . ' is an animal living on the land.';
            break;

        case 'air':
            echo $animal['name'] . ' is an animal flying though the air.';
            break;

        case 'water':
            echo $animal['name'] . ' is an animal swimming through the water.';
            break;
    }

What happens here is that we "feed" the `switch` statement a value. In our case this is `$animal['type']` (land). Below that we have three condition blocks. Such a block start with `case {the value}:` and ends with `break;` Everything inside that will be executed when the condition is met. The break keyword ensure that the other conditions aren't tested once a condition is met.

> **Note:**
> The last `break;` in our example is not mandatory, because there are no other condition after it. But it is considered good pratice to still include it for consistency.

Lets have a look at a bit more complex example of a `switch` statement:

    <?php
    $color = 'pink';

    switch($color) {
        case 'red':
        case 'yellow':
        case 'blue':
            echo $color . ' is a primary color.';
            break;

        case 'black':
        case 'white':
            echo $color . ' is a monochrome color.';
            break;

        default:
            echo $color . ' is a secondary color.';
            break;
    }

In this example instead of checking for one condition we are checking for multiple conditions. When the color is either: red, yellow or blue the text `{color} is a primary color.` will be displayed displayed. When the color is either: black or white the text `{color} is a monochrome color.` is displayed. All other colors will display `{color} is a secondary color.`.

It is important to note that because PHP is a loose typed language `1` validates as `TRUE`:

    <?php
    $count = 1;

    if ($count == TRUE) {
        // this will be displayed
        echo 'Count is true';
    }

    // count is now 2
    $count++;

    if ($count == TRUE) {
        // this will also be displayed
        echo 'Count is still true';
    }

    if ('Some string' == TRUE) {
        // a string also evaluates to true
        echo 'A string also equals true';
    }

To enable strict comparisons in our conditions we can make use of the following:

    <?php
    $count = 1;

    if ($count === TRUE) {
        echo '$count contains a boolean value true.';
    }

    if ($count !== '1') {
        echo '$count contains the string 1.';
    }

In the first conditional statement we have used the strict equals operator (`===`). This checks both the type and the value. The text in that statement will not be displayed, because the variable `$count` contain a value of type integer and `TRUE` is of type boolean. The second conditional statement uses the strict not equal operator. The text in this statement will be displayed, because the type of the value of the variable (integer) doesn't equal the type of the text (string).

> **Note:**
> For a complete overview of type comparisons please see [the manual][type-comparison].

[if]:http://php.net/manual/en/control-structures.if.php
[else]:http://php.net/manual/en/control-structures.else.php
[count]:http://php.net/manual/en/function.count.php
[elseif]:http://php.net/manual/en/control-structures.elseif.php
[switch]:http://php.net/manual/en/control-structures.switch.php
[operator-comparison]:http://php.net/manual/en/language.operators.comparison.php
[type-comparison]:http://php.net/manual/en/types.comparisons.php