Do's and Dont's
===============

The do's and dont's of PHP.

How to store users passwords safely?
------------------------------------

Storing users password in plain-text in the database is a bad idea. Everyone can understand that.
The last couple of years the PHP community best practice has changed alot. The short answer to the question is:
[Use bcrypt](http://codahale.com/how-to-safely-store-a-password/). In PHP 5.5 there is a new [password hashing](https://gist.github.com/3707231) API available.
If you are using older versions you can learn how to use [Bcrypt here](http://xqus.com/blog/how-to-store-passwords).
