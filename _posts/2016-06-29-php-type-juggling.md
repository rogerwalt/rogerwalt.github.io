---
layout: post
title:  "PHP Type Juggling and Comparison Operators"
date:   2016-06-29 11:00:04 +0200
categories: php
---
While working on an object storage to store instances to a MySQL database, I encountered this weird situation using [GUIDs](https://en.wikipedia.org/wiki/Globally_unique_identifier).
I wanted to set the GUID on my object to zero (integer) if it wasn't saved in the database yet.
However, GUIDs are stored as string in the application.
You can already guess what's coming.


So to check if an object was stored yet or not, it seems natural to do the following comparison:
{% highlight php %}
<?php
if ($guid != 0)
    // no need to store the object!
{% endhighlight %}

Beware of such code! Look at this:
{% highlight php %}
<?php
$guid = '152584dc-a842-178c-7d54-57b9e1c39e6b';
var_dump($guid != 0);  // bool(true)

$guid = '099d71e3-4f2e-78d3-b85b-34e01a7ec5f9';
var_dump($guid != 0);  // bool(true)

$guid = 'a31ff3da-b389-9fb0-7b43-18043dcde85d';
var_dump($guid != 0);  // bool(false)
{% endhighlight %}

It's not working as expected! When you have a look at [PHP Comparison Operators](http://php.net/manual/en/language.operators.comparison.php) it states clearly:

`$a != $b	Not equal	TRUE if $a is not equal to $b after type juggling.`

Type juggling kills your expectations for this comparison.

- `$guid != 0` is the inverse of `$guid == 0` (remember, `$guid = 0` is never a comparison!)
- `$guid !== 0` is the inverse of `$guid === 0`

A thing like `$guid !=== 0` doesn't exist.