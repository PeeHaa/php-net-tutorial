Form handling
=============

Up to now we have only seen examples of code without any user interaction. At some point we have to use information submitted by the user. An example of this is by the user filling in an HTML form.

An example of a form (this file will be saved as register.php):

    <?php
    // check whether the form has been submitted by the user
    if (isset($_POST['submit'])) {
        // check whether all fields has been filled in
        if (strlen(trim($_POST['username'])) && strlen(trim($_POST['password'])) && strlen(trim($_POST['password2']))) {
            // check whether the passwords match and has the correct length
            if (strlen($_POST['password']) == 8 && $_POST['password'] == $_POST['password2']) {
                // do stuff with the user info, e.g. add it to a database

                // redirect the user to the success page
                header('Location: http://php.net/success.php');
                exit();
            }
        }
    }
    ?>

    <html>
      <head>
        <title>Registration form</form>
      </head>
      <body>
        <h1>Register for an account</h1>
        <p>Please fill in this form to register for an account.</p>
        <?php if (isset($_POST['submit'])) { ?>
        <p class="error">There is an error submitting the form. Please check whether all fields are filled in and the passwords match.</p>
        <?php } ?>
        ?>
        <form action="/register.php" method="post">
          <table>
            <tr>
              <th>Username: </th>
              <td><input type="text" name="username"></td>
            </tr>
            <tr>
              <th>Password (minimum length is 8): </th>
              <td><input type="password" name="password"></td>
            </tr>
            <tr>
              <th>Retype password: </th>
              <td><input type="password" name="password2"></td>
            </tr>
            <tr>
              <th></th>
              <td><input type="submit" name="submit" value="Signup"></td>
            </tr>
          </table>
        </form>
      </body>
    </html>

In this example we have a basic registration form with fields for: the username, the password, retype the password and a submit button. At the top of our script we are using PHP to do some basic validation on the form data. There are several things going on at the top of our script. As you can see we are using the `$_POST` variable. The [`$_POST`][post-superglobal] variable is an array which contains all the data sent from our form. The first thing we do is check whether the form is submitted. We do this by checking whether the `$_POST` variable contains an item with the key `submit` (this is our submit button). This check is done by the builtin function [`isset()`][isset].

Once we have confirmed the form is submitted we are checking whether all fields in our form are filled in also using the `isset` function. And finally we are checking whether the password contains of at least 8 characters using the [`strlen()`][strlen] function and whether both passwords match.

When the form is submitted and all fields are correctly filled in the user is redirected to a success page. The redirect to the success page is done by the [`header()`][header] function. Also note the [`exit()`][exit] function after the redirect to prevent the further execution of the script.

Above our HTML form we are checking again whether the form has been submitted. If that is the case we will display an error message, because when the form is submitted and not all fields are filled in correctly we will not redirect the user to the success page.

> **Note:**  
> As you can see the form validation gets messy quickly this way. In one of the next topics we will see how to improve this validation code (with all the nested if statements) by creating and using functions.

Now that we have a basic form working we can expand on this a bit, by for example adding error messages at fields which are not correctly filled in. And by filling in the user submitted username when the form validation failed:

When displaying data it is important to prevent so called XSS vulnerabilities in your script. A simple example of such a vulnerability is the following script:

    <?php
    $initialValue = '';
    if (isset($_GET['submit'])) {
        $initialValue = $_GET['keywords'];
    }

    <html>
      <head>
        <title>Example of a XSS vulnerable page</title>
      </head>
      <body>
        <h1>XSS vulnerability</h1>
        <form action="search.php" method="get">
          <input type="text" name="keywords" value="<?php echo $initialValue; ?>">
          <input type="submit" name="submit" value="Search">
        </form>
      </body>
    </html>

This script will allow the user to add keywords into a searchfield. Instead of using the `$_POST` variable we are now using the [`$_GET`][get-superglobal] variable to access out form values. We can access it this way, because set set the method of the form to `get`. When we are using the get method the values of our form will be added to our URL. So when the form gets submitted the resulting URL will be: `http://domain.com/search.php?keywords=keywords%20added%20by%20user&submit=Search`. The get and post methods refer to the [HTTP methods][http-methods]. It depends on what you are trying to do which method you should use when submitting data. Generally when you are sending data to the server in order to be saved you would use the post method (in our example the registration for) and when using form data to retrieve information from the server we would use get (this example where we are getting search results). Also note the when submitting a form using the post method the values of our form don't get appended to the URL.

When the user submits the form the keywords are filled in again in the textfield. This looks fine at first, however consider the following keywords added by the user: `"><script>alert('I\'ve just injected malicious javascript in the page!')</script><input type="hidden`. Because we are filling in the value of the searchbox on submit with the user supplied data the resulting HTML will look like:

    <html>
      <head>
        <title>Example of a XSS vulnerable page</title>
      </head>
      <body>
        <h1>XSS vulnerability</h1>
        <form action="search.php" method="get">
          <input type="text" name="keywords" value=""><script>alert('I\'ve just injected malicious javascript in the page!');</script><input type="hidden">
          <input type="submit" name="submit" value="Search">
        </form>
      </body>
    </html>

As you can see we have now provided the user a way of breaking out of our input field and inject "malicious" HTML into out document. This example doesn't have real malicious code (e.g. it adds a javascript which alerts a message), but this is just a demonstration to show you it is possible to inject any HTML.

To prevent this we can replace "dangerous" characters by their html entities to prevent XSS vulnerabilities. To do this we must always use the builtin [`htmlspecialchars()`][htmlspecialchars] function when displaying data in a page which may contain dangerous characters:

    <?php
    $initialValue = '';
    if (isset($_GET['submit'])) {
        $initialValue = $_GET['keywords'];
    }

    <html>
      <head>
        <title>Example of a XSS vulnerable page</title>
      </head>
      <body>
        <h1>XSS vulnerability</h1>
        <form action="search.php" method="get">
          <input type="text" name="keywords" value="<?php echo htmlspecialchars($initialValue, 'UTF-8'); ?>">
          <input type="submit" name="submit" value="Search">
        </form>
      </body>
    </html>

If the same malicious user tries to inject his HTML as in the previous example he wouldn't succeed, because the `<`, `>`, `"` will be replaced by their html entities. So the result would be:

    <html>
      <head>
        <title>Example of a XSS vulnerable page</title>
      </head>
      <body>
        <h1>XSS vulnerability</h1>
        <form action="search.php" method="get">
          <input type="text" name="keywords" value="&quot;&gt;&lt;script&gt;alert('I\'ve just injected malicious javascript in the page!');&lt;/script&gt;&gt;input type=&quot;hidden">
          <input type="submit" name="submit" value="Search">
        </form>
      </body>
    </html>

> **Note:**  
> It is important to always use the `htmlspecialchars()` function before outputting anything which may contain possible dangerous characters. In our example we use it to display values in a form, but also don't forget about other ways for people to inject HTML on a page, e.g. their username.  If a user chooses the username `<script>alert('Injected javascript');</script>` and you are displaying that username somewhere the script will be executed when not using `htmlspecialchars()`.

It is also possible to upload files using a form. To be able to upload files we need to add another attribute (`enctype="multipart/form-data"`) to the form element:

    <?php
    $maxFileSize = 10485760;
    $message = null;
    if (isset($_POST['submit']) && $_FILES['filename']['tmp_name']) {
        $savePath = '/path/to/directory/' . basename($_FILES['filename']['name']);

        if ($_FILES['filename']['size'] > $maxFileSize) {
            $message = 'The file exceeded the maximum file size allowed.';
        } elseif(move_uploaded_file($_FILES['filename']['tmp_name'], $savePath)) {
            header('Location: http://domain.com/upload.php');
            exit();
        } else {
            $message = 'There was an error uploading the file. Please try again.';
        }
    }

    <html>
      <head>
        <title>Upload form example</title>
      </head>
      <body>
        <h1>File upload</h1>
        <?php if ($message !== null) { ?>
        <p><?php echo $message; ?>/p>
        <?php } ?>
        <form enctype="multipart/form-data" action="upload.php" method="post">
          <input type="hidden" name="MAX_FILE_SIZE" value="<?php echo $maxFileSize; ?>">
          Select a file: <input name="filename" type="file">
          <input type="submit" name="submit" value="Upload">
        </form>
      </body>
    </html>

In this example we are first defining a variable which contains the maximum size allowed of files being uploaded. This is the size in bytes. For this example we have defined a maximum filesize of 10Mb. In our HTML form we use this variable to fill a hidden field with the maximum file size.

Once the user has chosen a file and submits the form the file will be uploaded to a temporary directory. Note that for file uploads PHP uses another variable ([`$_FILES`][files-superglobal]) which will contain all the needed information to process the upload. When the form is submitted we are first checking whether the file doesn't exceed the maximum filesize we set. Note that we are not using the `MAX_FILE_SIZE` value coming from the form, because this could easily be changed by the client. When the filesize doesn't exceed the filesize limit we are trying to move the file from the temporary directory to the directory we want to save it in. If that succeeds we are doing a redirect to the same page (upload.php). By doing a redirect we prevent the message in browsers about data being send again when the user refreshes the page.

> **Note:**  
> Note that besides enforcing a maximum size of file uploads through either the HTML form or through a PHP script there are also some PHP configuration option to keep in mind. One of these configuration options is the [`post_max_size`][post-max-size] php.ini directive. And another one is the [`upload_max_filesize`][upload-max-filesize] php.ini directive. When uploading large files another setting that needs to be kept in mind is [`max_input_time`][max-input-time].

> **Note:**  
> A popular way of validating data input by the user is by doing it on the client-side by for example using javascript. Although there is nothing wrong with this it is important that you also always validate the user input on the serverside, because the client can always circumvent the clientside validation.

[post-superglobal]:http://php.net/manual/en/reserved.variables.post.php
[get-superglobal]:http://php.net/manual/en/reserved.variables.get.php
[isset]:http://php.net/manual/en/function.isset.php
[strlen]:http://php.net/manual/en/function.strlen.php
[header]:http://php.net/manual/en/function.header.php
[exit]:http://php.net/manual/en/function.exit.php
[htmlspecialchars]:http://php.net/manual/en/function.htmlspecialchars.php
[http-methods]:http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html
[files-superglobal]:http://php.net/manual/en/reserved.variables.files.php
[post-max-size]:http://php.net/manual/en/ini.core.php#ini.post-max-size
[upload-max-filesize]:http://www.php.net/manual/en/ini.core.php#ini.upload-max-filesize
[max-input-time]:http://www.php.net/manual/en/info.configuration.php#ini.max-input-time