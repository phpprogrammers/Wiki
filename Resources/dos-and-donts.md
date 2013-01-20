Do's and Dont's
===============

The do's and dont's of PHP.

Do use bcrypt to store your passwords
-------------------------------------

Storing users password in plain-text in the database is a bad idea. Everyone can understand that.
The last couple of years the PHP community best practice has changed alot, from unsalted md5 hashes
to more complicated alorithms. But still there are some bad practice going on in the PHP community.
So how should you store passwords? [Use bcrypt](http://codahale.com/how-to-safely-store-a-password/).

In PHP 5.5 there is a new password hashing API, if you have it available you should use it.

```php
// Hashing a password.
$hash = password_hash($password, PASSWORD_DEFAULT);

// Validating a password.
// $password from user, $hash from database
if (password_verify($password, $hash)) {
  // Valid password.
} else {
  // Invalid password.
}
