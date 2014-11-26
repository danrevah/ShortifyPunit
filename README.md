#ShortifyPunit &nbsp; [![Build Status](https://travis-ci.org/danrevah/ShortifyPunit.svg?branch=master)](https://travis-ci.org/danrevah/ShortifyPunit)  [![Coverage Status](https://coveralls.io/repos/danrevah/ShortifyPunit/badge.png?branch=master)](https://coveralls.io/repos/danrevah/ShortifyPunit/badge.png?branch=master)
> PHP Simple mocking library, **v0.1**


## Installation

The following instructions outline installation using Composer. If you don't
have Composer, you can download it from [http://getcomposer.org/](http://getcomposer.org/)

 * Run either of the following commands, depending on your environment:

```
$ composer global require danrevah/spu:dev-master
$ php composer.phar global require danrevah/spu:dev-master
```

## Mocking Examples
```php
// Creating a new mock for SimpleClassForMocking
$mock = ShortifyPunit::mock('SimpleClassForMocking');

// returns null, was not stubbed yet
$mock->first_method();
```

Basic mocking example, if a function wasn't stubbed the return value will always be `NULL`.

## Stubbing
```php
// Creating a new mock for SimpleClassForMocking
$mock = ShortifyPunit::mock('SimpleClassForMocking');

// Stubbing first_method() function without arguments
ShortifyPunit::when($mock)->first_method()->returns(1);

// returns 1
$mock->first_method();

// Stubbing first_method() function with arguments
ShortifyPunit::when($mock)->first_method(1,2)->returns(2);

// still returns 1
$mock->first_method();

// returns 2
$mock->first_method(1,2);

// Stubbing throws exception
ShortifyPunit::when($mock)->second_method()->throws(new \Exception);

try {
  // Excpetion will be thrown
  $mock->second_method();
} catch(Exception $e) {
  echo 'Exception Was Caught!';
}
```

## Stubbing Method Chanining
```php
 // Mocking method chaining
 ShortifyPunit::when_concat($mock, array('first_method' => array(1),
                                          'second_method' => array()),
                            'returns', 'some string');
 
 // returns "some string"
 $mock->first_method(1)->second_method();
 
 ShortifyPunit::when_concat($mock, array('first_method' => array(),
                                          'second_method' => array()),
                            'throws', new \Exception);
  
 // throws Exception
 $mock->first_method()->second_method();
 
 // still returns "some string"
 $mock->first_method(1)->second_method();
```
  
  
