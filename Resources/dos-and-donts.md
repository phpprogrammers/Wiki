Do's and Dont's
===============

The do's and dont's of PHP.

Do use bcrypt to store your passwords
-------------------------------------

Storing users password in plain-text in the database is a bad idea. Everyone can understand that.
The last couple of years the PHP community best practice has changed alot, from unsalted md5 hashes
to more complicated algorithms. But still there are some bad practice going on in the PHP world.
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
```

If you are using older PHP versions you have to use [crypt()](http://php.net/crypt). This
process is a bit more complicated and requires some more work from you as a developer. Luckily there are 
some libraries that can take care of this for you in a proper way:
* [phpSec](http://phpseclib.com)
* [PasswordLib](https://github.com/ircmaxell/PHP-PasswordLib)

If this does not suit you you should read this blog post: [How to store passwords securely](http://xqus.com/blog/how-to-store-passwords).

But in essential bcrypt hashing in PHP can be done like this:
```php
$myPassword = 'mySecretPassword'; // This is the password we want to hash.

// The salt is extremely important that is created from an truly random source.
// This is just an example, but we will talk more about generating salts later.
// For now we will read 128 bytes from /dev/urandom
$fp = fopen( '/dev/urandom', 'rb');
if ($fp !== false) {
  $randomSalt = fread($fp, 128);
  fclose($fp);
}

// We need to prepeare the $randomSalt. crypt() expects a 22 character string with a special charset.
$salt = substr(strtr(base64_encode($randomSalt), '+', '.'), 0, 22);

$_work = 14; // Work factor. Higher value makes generating hashes slower.

// The salt parameter we pass to crypt() contains more than just the salt.
// There salt contains of 3 parts separated by a dollarsign ($).
// The first (2y) means that we want to use the bcrypt algorithm.
// The second is the work factor, and the third is the salt itself.
$salt = sprintf('$2y$%s$%s', $_work, $salt);

// Then it's time to compute the hash itself.
$hash = crypt($myPassword, $salt);

// To make sure everything went as planned, we check that the returned $hash is longer than 13 characters.
if(strlen($hash) > 13) {
  /* Hash generation was a success! */
  echo $hash;
  // Will output something like: $2y$14$qWBgI7DhxjrqzkbohKHaa.s2nnG.neALCcO0eIKAhZeSMryIgRE5q
} else {
  echo "Something bad happened!";
}
```
But please do not use this code unless you read the blog post mentioned above since there are several things going on here that
need explanation.
