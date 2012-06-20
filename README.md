php.net Tutorial
================

This repo contains a proposal for the new tutorial on [php.net][tutorial].  
The idea is to create a better introduction tutorial for the language. The goal is to help new  
people getting started using PHP and at the same time educate people in best practices.

The topics of this tutorial should contain all the information neccesary for people to create  
their first project using PHP while considering the level of people who will use it: namely:  
people new to the language.

Contribute
----------

For questions, suggestion or discussions use [the issue tracker][issues].

If you want to contribute you are encouraged to fork this repo and make a push request with your changes.

To keep changes and formatting in line there are some rules in place to guarantee this:

- All topics should be in a separate document.
- The documents should be named as the title in only lowercase characters where spaces are replaced by dashes (`-`) and prefixed with `n-` where `n` is the topic number.
- The documents should be saved using the `.md` extension.
- The documents should use proper markdown formatting.
- When new documents are added the table of contents should be updated accordingly with the filename as entry.
- Always add links to [the English version of the manual][manual] where more information or further  
  explanation is justified. Note that links to the manual should **not** be preceded by a subdomain, e.g.: http://nl.php.net/manual/en/.
- When adding links always use named link instead of numeric links or inline links.
- Notes should be formatted using markdown blockquotes.

    > **Note:**  
    > This is an example of a note

[issues]:https://github.com/PeeHaa/php-net-tutorial/issues
[tutorial]:http://php.net/tut.php
[manual]:http://php.net/manual/en/