Basic syntax
============

PHP tags
--------

[PHP tags][php-tags] are used to let PHP know which part(s) of a file it needs to parse. Because of this we can mix PHP and another language (e.g. HTML). To start the parsing of code in a file you need to add the PHP opening tag `<?php` and to end the parsing of code in a file you need to add a PHP closing tag `?>`. Everything outside of the PHP tags will be left alone by the parser and will just work like normal. A simple example of this using a simple HTML document:

    <html>
      <head>
        <title><?php echo 'This is the page title'; ?></title>
      </head>
      <body>
        <h1><?php echo 'This is the heading of the page'; ?></h1>
        <p>This is a paragraph...</p>
      </body>
    </html>

In the above example we have normal HTML code enhanced with PHP code. As you can see there are two PHP code blocks inside the HTML code (the code enclosed in the PHP opening and closing tags). The result of the above code will be send to the browser (after being parsed):

    <html>
      <head>
        <title>This is the page title</title>
      </head>
      <body>
        <h1>This is the heading of the page</h1>
        <p>This is a paragraph...</p>
      </body>
    </html>

As you can see all the HTML code is left as is and the PHP code is parsed.

Sometimes it is useful to have only a opening tag in your file. If PHP doesn't find a closing tag after an opening tag all other code after the opening tag will be parsed by PHP:

    <?php
    echo 'This is a ';
    echo 'file with a opening tag without ';
    echo 'a closing tag, so all these lines will be parsed by PHP.';

The result of this code will be:

    This is a file with a opening tag without a closing tag, so all these lines will be parsed by PHP.

> **Note:**
> The reason that the previous example results in only one line where we have three lines of code is that PHP will ignore all whitespace characters. So the previous example would be the same as `echo 'This is a ';echo 'file with a opening tag without ';echo 'a closing tag, so all these lines will be parsed by PHP.';`.

Instructions
------------

[PHP instructions][instructions] are ended with a semicolon (;) as can be seen in the previous examples. When you forget to add the semicolon to end an instruction PHP will display an error:

    <?php
    echo 'This instruction isn't ended with a semi colon.'
    echo 'The previous line will result in an error';

The above code will result in the following error:

    Parse error: syntax error, unexpected 'echo' (T_ECHO), expecting ',' or ';' in /example.php on line 3

> **Note:**  
> It looks like there is an error on line 3, but actually the error (missing semicolon) occurred on line 2. For more information about PHP's error reporting see the chapter "Error reporting" of this tutorial.

Comments
--------

It may be useful to add [comments][comments] to you code. Comments are not parsed by PHP and can be a powerful tool to add remarks to parts of your script. Comments in PHP can span over either one or multiple lines.

Single line comments start with `//` and everything after this on the same line will be a comment. Multiline comments start with `/*` and end with `*/`. Everything inside these will be a comment.

    <?php
    // this is a comment on a single line and will not be parsed by PHP

    /*
       this is a comment spanning over multiple lines
       this also will not be parsed by PHP
    */

    echo 'This is a basic instruction'; // comments can be added everywhere even after instructions

The above example will only output `The is a basic instruction`.

[php-tags]:http://php.net/manual/en/language.basic-syntax.phptags.php
[instructions]:http://php.net/manual/en/language.basic-syntax.instruction-separation.php
[comments]:http://php.net/manual/en/language.basic-syntax.comments.php