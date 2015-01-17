Functions
=========

PHP already has a lot of [built-in functions][builtin-functions]. Besides the built-in functions already provided by PHP it is also possible to define your own functions. Functions can be used to run the same code multiple times without having to add the code multiple times. It can also be used to organize your code. Generally speaking a function is a piece of code with an input, some defined actions based on the input and an output. An example of function that calculates the differences in the age of two people is:

    function getAgeDifference($age1, $age2)
    {
        return abs($age1 - $age2);
    }

    $users = array(
        array(
            'name' => 'John Doe',
            'age'  => 24,
        ),
        array(
            'name' => 'Jane Doe',
            'age'  => 36,
        ),
    );

    echo 'The difference of age in years between ' . $users[0]['name'] . ' and ' . $users[1]['name'] . 'is: ' . getAgeDifference($users[0]['age'], $users[1]['age']) . ' years.';

This example will output: `The difference of age in years between John Doe and Jane Doe is: 12 years.` What happens in this example is that we pass two parameters to the function (i.e. `$age1` and `$age2`) and that the function calculates the differences between the two dates. Also note that in this example we have used the built-in function [`abs()`][abs]. The `abs()` function return an absolute number. If we wouldn't have added that the result of our function would have been `-12` instead of `12`. Also note the [`return`][return] keyword in our function. The `return` keyword in a function ends the execution of the function and returns a value (in our case the number of years in between the two ages).

Now that we have seen a simple example of a function lets have a look at a bit more complex function. Lets create a function which creates an excerpt from a longer text:

    function getExcerpt($text, $numberOfCharacters = 200)
    {
        $excerpt = substr($text, 0, $numberOfCharacters);

        if (strlen($text) > $numberOfCharacters) {
            $excerpt.= '...';
        }

        return $excerpt;
    }

    $articles = array(
        '1' => array(
            'timestamp' => '2012-02-06 16:43:15',
            'title'     => 'Blog example',
            'text'      => 'Morbi viverra lectus sit amet diam feugiat convallis. Fusce ipsum tellus, porta convallis bibendum a, sagittis id arcu. Etiam at enim nisi. Sed luctus aliquet varius. Aenean pharetra tortor ac ipsum mollis quis suscipit lacus porta. Etiam ligula nibh, vestibulum at blandit vel, facilisis eu nulla. Curabitur eget urna lectus, sed accumsan ante. In vestibulum neque ut dui mollis vitae aliquam enim venenatis. Mauris vitae sapien ligula. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Suspendisse potenti. Morbi bibendum molestie elit, non vestibulum risus consequat sagittis. In hac habitasse platea dictumst. Curabitur vehicula tempor lacus lobortis venenatis.',
        ),
        '2' => array(
            'timestamp' => '2012-02-07 14:12:21',
            'title'     => 'Second blog post',
            'text'      => 'Maecenas quis lectus sed tortor consectetur sodales eu sed augue. Curabitur non justo suscipit arcu sollicitudin adipiscing mattis luctus elit. Praesent venenatis pretium justo, eget fringilla urna laoreet sit amet. Donec ullamcorper metus at lacus semper ut rutrum ante sagittis. Suspendisse potenti. Proin et quam justo. Nulla leo arcu, facilisis vitae tempus a, porta ut dolor. Nam diam tortor, tempor eget semper at, viverra at magna. Vivamus sit amet ante ante. Phasellus eu eros orci. Duis tortor velit, aliquet ut vestibulum ut, semper a tellus. Aenean eget metus odio, non vestibulum metus. Fusce eleifend lectus nec elit pellentesque sit amet fringilla nulla accumsan. Aliquam tempor dignissim adipiscing. Nullam laoreet rhoncus justo nec suscipit. Nullam sollicitudin semper massa, quis mattis tortor consectetur euismod.',
        ),
    );

    foreach($articles as $id => $article) {
        $datetime = new DateTime($article['timestamp']);

        echo '<article>';
        echo '  <h1>' . $article['title'] . '</h1>';
        echo '  <p>' . getExcerpt($article['text']) . '</p>';
        echo '  <footer>' . $datetime->format('d-m-Y H:i:s') . '</footer>';
        echo '</article>';
    }

In this example you have created a function which accepts one required parameter and one optional parameter. The required parameter (`$text`) is the text that will be truncated to the maximum number of characters allowed in the excerpt. The maximum number of characters that the excerpt may contain is the `$numberOfCharacters` parameters. As you can see this parameter has a default value of `200`. What does means is that when we don't pass that parameter to the function (as we have done in our example) the default value will be used. By settings up the function this way you can easily use the same function somewhere else where you may want to display a bigger or smaller portion of some text as an excerpt.

What happens when you run this code is that it will display the articles from our array. It will display the title of the article, the excerpt of the full text of the article. And below each article it will format the date and displays it. To format the date we have used PHP's builtin [DateTime][datetime] class.

It is important that you note that variables declared outside of a function cannot be accessed from within a function. This is what is called [variables scope][variables-scope]. Because of this you should always pass the information you need access to in a function as an argument of that function:

    <?php

    $text = 'This is an example text.';

    function verifyMinimumLength()
    {
        if (strlen($text) > 20) {
            return true;
        }

        return false;
    }

    function verifyMinimumLength2($text)
    {
        if (strlen($text) > 20) {
            return true;
        }

        return false;
    }

    // this function call will produce the notice: Notice: Undefined variable: text in /code/8j8gS0 on line 7
    verifyMinimumLength();

    // this function call will work, because you are passing the text as a parameter to the function
    verifyMinimumLength2($text);

[Anonymous functions][anonymous-functions] (also known as closures) are functions created without names. These functions can be assigned to variables and can then be passed to other functions (just like variables).:

    <?php

    $people = array('Mary', 'Job', 'Judas');
    
    $greet = function($name) {
        printf("Hello, %s \n", $name);
    };
    //this is an anonymous function that has been assigned to a variable
    
    array_walk($people, $greet);
    
The above example will output: `Hello Mary \n Hello Job, Hello Judas`. The anonymous function (assigned to `$greet`) has been passed to the [array_walk][array-walk] as the second argument.


[builtin-functions]:http://php.net/manual/en/functions.internal.php
[abs]:http://php.net/manual/en/function.abs.php
[return]:http://php.net/manual/en/function.return.php
[filterval]:http://php.net/manual/en/function.filter-var.php
[pregmatch]:http://php.net/manual/en/function.preg-match.php
[header]:http://php.net/manual/en/function.header.php
[exit]:http://php.net/manual/en/function.exit.php
[datetime]:http://php.net/manual/en/book.datetime.php
[variables-scope]:http://php.net/manual/en/language.variables.scope.php
[anonymous-functions]:http://php.net/manual/en/functions.anonymous.php
[array-walk]:http://php.net/manual/en/function.array-walk.php
