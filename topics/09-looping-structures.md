Looping structures
==================

Loops can be used to for example iterate over an array or to repeat a specific piece of code. PHP has support for four different looping structures: `foreach`, `for`, `while` and `do while`.

A [`foreach`][foreach] loop can be used to loop through items in an array or an object:

    <?php

    $images = array(
        'Chuck'   => 'chuck-norris.png',
        'Unicorn' => 'unicorn.png',
        'Cat'     => 'cat.png',
    );
    ?>

    <html>
      <head>
        <title>Image gallery</title>
      </head>
      <body>
        <?php
        foreach($images as $title => $image) {
            echo '        <img src="' . $image . '" alt="' . $title . '">';
        }
        ?>
      </body>
    </html>

In the above example we have created a simple HTML page with the three images we have in our array `$images`. First we have added the three images to our array as we have seen in the previous topics. In the body of our HTML page we are looping through our array using a `foreach` loop. The loop consist of three parts: `$images` is the array we want to loop through. In the second part `$title` we assign the key of the current item in the array to a variable. E.g. the key for the first item will be `Chuck`. In the last part we assign the value of the current item to the `$image` variable (for the first item this will be `chuck-norris.png`). Inside the loop we can use those two new variables.

It is not always needed to have the key of the current item in a variable. In this case we can just use the `foreach` loop to only get the current value:

    <?php
    $images = array(
        'Chuck'   => 'chuck-norris.png',
        'Unicorn' => 'unicorn.png',
        'Cat'     => 'cat.png',
    );

    foreach($images as $image) {
        // now we only have the value of the current item
        echo $image;
    }

The next looping structure is the [`for`][for] loop. Using a for loop we can repeat a piece of code a predetermined number of times:

    <?php
    echo 'Lets count to 10: ';

    for($i = 1; $i <= 10; $i++) {
        echo $i;
    }

This example will output: `Lets count to 10: 12345678910`. Instead of looping through an array with items (as in the previous example) we are now defining how many times the code in our loop should get executed. First we create and initialize a variable `$i`. After that we tell PHP until what value it should continue to loop. And finally we tell PHP to add `1` to the current value of `$i`.

> **Note:**  
> The `++` in this example is called the [incrementing operator][incrementing-operator]. It is the same as doing `$i = $i + 1;`.

We can also use the for loop to count down to a value:

    <?php
    echo 'Lets count down: ';

    for($i = 10; $i > 0; $i--) {
        echo $i;
    }

This will display: `Lets count down to 10: 10987654321`.

It is also possible to countdown with other steps than 1:

    <?php
    echo 'Lets count down to 10: ';

    for($i = 10; $i > 0; $i-=2) {
        echo $i;
    }

This will display: `Lets count down: 108642`.

> **Note:**  
> The [assignment operator][assigment-operator] (`$i-=2`) we have used in this example is the same as doing: `$i = $i - 2;`

The next looping structure is the [`while`][while] loop:

    <?php
    echo 'Lets count to 10: ';

    $i = 1;
    while ($i <= 10) {
        echo $i++;
    }

The code in the while loop will keep being executed for as long as the expression evaluates to true. In this example this will display: `Lets count to 10: 12345678910`.

Another similar loop is the [`do while`][do-while] loop:

    <?php
    echo 'Lets count to 10: ';

    $i = 1;
    do {
        echo $i++;
    } while ($i <= 10)

This example will display exactly the same thing as the previous example. As you can see the syntax is slighty different than our `while` example. I.e. the expression is at the end of the loop instead of at the start. This is also the difference between the two. In a "normal" while loop the expression is checked before the first iteration of the loop. In a do while loop it is checked for the first time after the first iteration. What this means is that the code inside a do while will always executed at least once.

An example of this difference:

    <?php
    $isValid = false;

    while($isValid) {
        echo 'Printing text inside the while loop.';
    }

    do {
        echo 'Printing text inside the do while loop.';
    } while($isValid);

In the above example only the text `Printing text inside the do while loop.` will be displayed. Because we are using a variable with a `false` value the while loop doesn´t iterate at all. However since the do while loop only checks the value after the iteration it will display the text (once).

It is also possible to skip a (part of) an iteration using the [`continue`][continue] keyword:

    <?php
    $users = array(
        array(
            'name' => 'John Doe',
            'isAdmin' => false,
        ),
        array(
            'name' => 'John Smith',
            'isAdmin' => true,
        ),
        array(
            'name' => 'James Johnson',
            'isAdmin' => false,
        ),
        array(
            'name' => 'Michael Jones',
            'isAdmin' => true,
        ),
    );

    $adminUsers = array();
    $adminCount = 0;
    foreach($users as $user) {
        if (!$user['isAdmin']) {
            continue;
        }

        $adminCount++;
        $adminUsers[] = $user['name'];
    }

    echo 'There are currently ' . $adminCount . ' administrators;
    if ($adminCount > 0) {
        echo ' (' . implode(', ', $adminUsers) . ')';
    }

There are several things happening in this example which we haven't seen yet. The first thing is the so called multidimensional array. This is nothing more than an array (or arrays) inside another array. As we have seen in the previous example we can access a value from an array by using either the numeric index or the named index (when supplied). If we want to display the name of John Smith we can access it directly by `$users[1]['name']`.

Next thing we do in the example is getting the number of administrators and the names of the administrators in our multidimensional array. Before we are getting this info we are declaring (and initializing) two variables: `$adminUsers` (which will contain the names of the administrators) and `$adminCount` (which will contain the number of administrators).

In our `foreach` loop we are looping through all the users in our array. Because we only need the administrators in this example we first check whether the current user is an administrator. When the user is not an administrator we will skip (`continue`) further execution of the iteration and move on to the next user. However when the user is an administrator we will add 1 to our count and add the name of the user to our array of administrators.

Once the loops is finished we will display the number of administrators. And when there are administrators in our array we will display there names separated by a comma. This is done by the builtin [`implode()`][implode] function. The implode function returns all the items in an array "glued together" by a separator (in our case a comma and a space).

The result of this example would be: `'There are currently 2 administrators (John Smith, Michael Jones)`.

> **Note:**  
> Instead of having a separate counter with the number of administrators (`$adminCount`) like in our example we could also have used the builtin [`count()`][count] function to get the number of elements in our `$adminUsers` array.

In some cases it may be useful to break out of a loop instead of just skipping an iteration. This is done by the [`break`][break] keyword:

    <?php
    $users = array(
        array(
            'name' => 'John Doe',
            'isAdmin' => false,
        ),
        array(
            'name' => 'John Smith',
            'isAdmin' => true,
        ),
        array(
            'name' => 'James Johnson',
            'isAdmin' => false,
        ),
        array(
            'name' => 'Michael Jones',
            'isAdmin' => true,
        ),
        array(
            'name' => 'Matthew Moore',
            'isAdmin' => true,
        ),
    );

    $adminUsers = array();
    $adminCount = 0;
    foreach($users as $user) {
        if (!$user['isAdmin']) {
            continue;
        }

        $adminCount++;
        $adminUsers[] = $user['name'];

        if ($adminCount == 2) {
            break;
        }
    }

    echo 'There are currently ' . $adminCount . ' administrators;
    if ($adminCount > 0) {
        echo ' (' . implode(', ', $adminUsers) . ')';
    }

This example is almost the same as the previous example. Two things we have added is: an extra user (which is an admin) and we added a check at the end of our loop which check whether we already have found two administrators in our users array.

Once we have found two administrators we will break out of the loop (e.g. the iterations stop) by using the `break` keyword.

> **Note:**  
> The `continue` and `break;` keywords work for all looping structures.

[foreach]:http://php.net/manual/en/control-structures.foreach.php
[for]:http://php.net/manual/en/control-structures.for.php
[incrementing-operator]:http://php.net/manual/en/language.operators.increment.php
[assigment-operator]:http://php.net/manual/en/language.operators.assignment.php
[while]:http://php.net/manual/en/control-structures.while.php
[do-while]:http://php.net/manual/en/control-structures.do.while.php
[continue]:http://php.net/manual/en/control-structures.continue.php
[implode]:http://php.net/manual/en/function.implode.php
[count]:http://php.net/manual/en/function.count.php
[break]:http://php.net/manual/en/control-structures.break.php