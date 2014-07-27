Sessions and cookies
====================

In the previous topics you have seen that you can save data in variables. Although this is very useful the variables set are only defined per request. This means that when you have set a variable and you refresh the page or navigate to another page the variable will not be set. PHP also provides a way to make data more persistent. One way to accomplish this is by using a database to store information in which is something we will cover in a later topic. For some data you want to store it only has to be persintent for as long as the user is on your site (e.g. for checking whether a user is logged in). Or you want to provide a "remember me" function on your website in which case you would have to store some persistent information on the users computer.

Sessions
--------

Session are used to store data which will stay available for as long as the session is valid. In most cases the session will be valid until the user closes the website in his browser. Session are often used to check whether a specific user is logged in. Consider the following example without sessions:

index.php

    <?php
    if (isset($_POST['submit'])) {
        $username = $_POST['username'];

        // redirect the user to the success page
        header('Location: http://127.0.0.1/success.php');
        exit();
    }
    ?>

    <html>
        <head>
            <title>My awesome site</title>
        </head>
        <body>
            <form action="">
                <input type="text" name="username">
                <input type="submit" name="submit" value="Submit">
            </form>
        </body>
    </html>

success.php

    <html>
        <head>
            <title>Success - My awesome site</title>
        </head>
        <body>
            <p>Welkom <?php echo htmlspecialchars($username, ENT_QUOTES, 'UTF-8'); ?>,</p>
        </body>
    </html>

The above example will result in a notice (`Notice: Undefined variable: username in /path/to/success.php on line 6`), because `$username` is not defined in the current request. In order to store the username during the time the user is on the website we have to store it in a session. Sessions are just like "normal" variables only they don't get deleted for as long as the user is on the site (or the session is manually deleted).

If we take our previous example and add sessions we can display the username on the success page (as well as on other pages).

Using session in PHP is really easy. First we need to tell PHP we want to use session using the [`session_start`][session-start] function. Once we have told PHP we want to use sessions we can simply create a session variable just like any other variable and use it on other pages. All session variables are stored in a specific variable called `$_SESSION`. This is an array containing all session data (for that specific user).

    <?php
    // tell PHP we want to use sessions on this page
    session_start();

    if (isset($_POST['submit'])) {
        // add the username to the session
        $_SESSION['username'] = $_POST['username'];

        // redirect the user to the success page
        header('Location: http://127.0.0.1/success.php');
        exit();
    }
    ?>

    <html>
        <head>
            <title>My awesome site</title>
        </head>
        <body>
            <form action="">
                <input type="text" name="username">
                <input type="submit" name="submit" value="Submit">
            </form>
        </body>
    </html>

success.php

    <?php
    // tell PHP we want to use sessions on this page
    session_start();
    ?>

    <html>
        <head>
            <title>Success - My awesome site</title>
        </head>
        <body>
            <p>Welkom <?php echo htmlspecialchars($_SESSION['username'], ENT_QUOTES, 'UTF-8'); ?>,</p>
        </body>
    </html>

Now the success page show the text "Welkom {username}," where the username is replaced by the actual username filled in in the form.

> **Note:**
> Whenever you want to use sessions (whether you add data to it or simply use it to read data from) you *always* have to start the session by using the `session_start` function.

When using session in PHP the `session_start` functions always has to be the very first thing in your script (before any output). This is a common pitfall when new people start working with sessions in PHP. What this basically means is that you cannot have anything before `session_start` in your script. Not even spaces. Some examples of where the `session_start` function will not work are:

     <?php
    session_start();

Because of the space before `<?php` `session_start` will fail, because the space will be seen as output.

    <html>
        <head>
            <title>My awesome website</title>
        </head>
        <body>
            <?php session_start(); ?>
            <p>Welkom <?php echo $_SESSION['username']; ?>,</p>
        </body>
    </html>

In the above example there has been already HTML outputted which will also prevent `session_start` to run correctly.

One final caveat when using `session_start` is when saving your source files as UTF-8. Some editors will add some special (and often invisible) character to the start of the file you are working in. This character is called the [Byte Order Mark (or simply BOM)][bom]. The BOM will also been seen as output which prevent `session_start` to function correctly. So when saving PHP files (in UTF-8) *always* verify it doesn't save with the BOM character (every sane editor will have the option to save without this character).

> **Note:**
> If there is output before using the `session_start` function PHP will display a warning (as long as you have enabled error reporting as explained in the Error reporting chapter). The error will look something like `Warning: session_start(): Cannot send session cookie - headers already sent by (output started at /in/g6FKH:2) in /in/g6FKH on line 2`.

In order to delete specific session variables we can simply use PHP's [`unset`][unset] function:

    <?php
    session_start();

    unset($_SESSION['username']);

If we want to completely remove all session data of the current user (useful when a user logs out) we can do the following:

    <?php
    // Initialize the session.
    session_start();

    // Unset all of the session variables.
    $_SESSION = array();

    // If it's desired to kill the session, also delete the session cookie.
    // Note: This will destroy the session, and not just the session data!
    if (ini_get("session.use_cookies")) {
        $params = session_get_cookie_params();
        setcookie(session_name(), '', time() - 42000,
            $params["path"], $params["domain"],
            $params["secure"], $params["httponly"]
        );
    }

    // Finally, destroy the session.
    session_destroy();

Cookies
-------

Cookies (just like session) are used to store data when the user navigates to other pages. However unlike sessions cookies will stay available even when the user closes the browser. This can be useful for example when you have a website where users can choose a language. In order to save the chosen language of the user even after the user closes its browser we can use cookies to store the chosen language. Just like sessions cookies are stored in a specific PHP array (`$_COOKIE`). Now lets see how cookies work:

index.php

    <?php
    if (isset($_COOKIE['lang']) && in_array($_COOKIE['lang'], array('en', 'nl'))) {
        header('Location: http://127.0.0.1/' . $_COOKIE['lang']);
        exit;
    }
    ?>

    <html>
        <head>
            <title>Choose language - My awesome site</title>
        </head>
        <body>
            <p>Choose a language: <a href="/choose-language.php?lang=en">English</a> <a href="/choose-language.php?lang=nl">Dutch</a></p>
        </body>
    </html>

choose-language.php

    <?php
    if (!isset($_GET['lang']) && !in_array($_GET['lang'], array('en', 'nl'))) {
        header('Location: http://127.0.0.1/');
        exit;
    }

    setcookie('lang', $_GET['lang'], time()+60*60*24*30);

    header('Location: http://127.0.0.1/' . $_GET['lang']);
    exit;


What we are doing in the above snippet is that when somebody goes to our homepage (`http://127.0.0.1`) we will first check whether there is already a cookie containing the previously chosen language (`isset($_COOKIE['lang'])`) and whether that language (if any) is in our list of supported languages (using the built in [`in_array`][in-array] function). If the user previously did not choose a language a language picker will be displayed to the user.

Of the user choses a language (by clicking on the link) his choice will be stored in a cookie variable using the [`setcookie`][setcookie] function. The `setcookie` function creates a cookie using a name (the first paramater), a value (second parameter) and an expiration time (the third parameter).

> **Note:**
> Never store sensitive data in cookies. Cookies are stored on the client side (meaning on the machine of the user).

If we want to remove a cookie we cannot simply `unset` the cookie (because the actual cookie is on the user's machine), but we have to make use of `setcookie` again only with tan expiration time in the past:

    setcookie ('lang', '', time() - 3600);

[session-start]:http://php.net/manual/en/function.session-start.php
[bom]:http://en.wikipedia.org/wiki/Byte_order_mark
[unset]:http://nl3.php.net/manual/en/function.unset.php
[in-array]:http://php.net/manual/en/function.in-array.php
[setcookie]:http://nl3.php.net/manual/en/function.setcookie.php
