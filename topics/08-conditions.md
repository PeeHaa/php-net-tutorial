Conditional Statements
======================

Conditional statements can be used to execute or "exclude" certain parts of the script based on a certain condition. We have several ways of doing this. This simpliest way is based on a single condition. This is done by an `if` statement:

    <?php
    $userAge = 42;

    if ($userAge > 60) {
        echo 'You are over 60.';
    }

This script will not output anything, because the `echo` statement is inside the condition statement. In the above example the `echo` statement will only be executed when the `$userAge` variable contains a value over 60. This is because we are checking using the greater than sign `>` in our conditional statement. An overview of all the comparison operators avaiable will be shown in the next example:

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

Todo:

- strict comparison
- if else
- if elseif else
- switch