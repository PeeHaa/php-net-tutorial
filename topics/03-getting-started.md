Getting started
===============

Once we have a PHP enabled webserver set up we can start writing our first script. Note that .php files are basically just normal text files only with the extension `.php`. Because of this we can simply create a script using a text editor. Although it is possible to write PHP scripts in just about any text editor it is advised to use an specialized IDE (Integrated Development Environments) for this, because this (among others) comes with syntax higlighting. A partial list of these tools is maintained at [PHP Editors List][ide-list].

> **Note:**  
> Word processors such as StarOffice Writer, Microsoft Word and Abiword are not optimal for editing PHP files. Use of these is discouraged.

> **Note:**  
> If you are writing your PHP scripts using Windows Notepad, you will need to ensure that your files are saved with the .php extension. (Notepad adds a .txt extension to files automatically unless you take one of the following steps to prevent it.) When you save the file and are prompted to provide a name for the file, place the filename in quotes (i.e. "hello.php"). Alternatively, you can click on the 'Text Documents' drop-down menu in the 'Save' dialog box and change the setting to "All Files". You can then enter your filename without quotes.

Now let's start writing our first script. Create a file named hello.php and put it in your web server's root directory (DOCUMENT_ROOT) with the following content:

    <?php
    echo 'Hello world';

Once we have created the file we can browse to it using our browser by going to the address: http://127.0.0.1/hello.php. You should see an empty page now with only the text `Hello World`. That's it! You just wrote your first PHP program.

> **Note:**  
> If you tried this example and it did not output anything, it prompted for download, or you see the whole file as text, chances are that the server you are on does not have PHP enabled, or is not configured properly. Ask your administrator to enable it for you using [the Installation chapter][installation] of the manual. If you are developing locally, also read the installation chapter to make sure everything is configured properly. Make sure that you access the file via http with the server providing you the output. If you just call up the file from your file system, then it will not be parsed by PHP. If the problems persist anyway, do not hesitate to use one of the many [PHP support options][support].

Explanation
-----------

The first line of our example script `<?php` tells PHP to parse anything that comes after it until it finds `?>`. This is needed to start PHP mode in a file. The second line `echo 'Hello world';` tells PHP to print the text: Hello world Because we haven't ended PHP mode by using `?>` the entire file will be parsed by PHP.

Let's take a look at another basic example. Create a file named hello2.php and put it in your web server's root directory (DOCUMENT_ROOT) with the following content:

    <html>
      <head>
        <title>Hello world</title>
      </head>
      <body>
        <p><?php echo 'Hello world'; ?></p>
      </body>
    </html>

Once we have created the file we can browse to it using our browser just like the previous example by going to the address: http://127.0.0.1/hello2.php. You should now see a very basic HTML page with the text Hello world. The difference with the previous example is that we have now mixed HTML and PHP by enabling and disabling PHP mode inside the `<p>` tag. You may jump in and out of PHP mode in an HTML file like this anywhere you want.

[ide-list]:http://en.wikipedia.org/wiki/List_of_PHP_editors
[installation]:http://php.net/manual/en/install.php
[support]:http://php.net/support.php