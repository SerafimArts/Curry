# Curry

Convenient implementation of function 
currying and partial application.

- [Installation](#installation)
- [Usage](#usage)
    - [Left currying](#left-currying)
    - [Right currying](#right-currying)
    - [Partial application](#partial-application)
- [Api](#api)
    - [Functions](#functions)
    - [Methods of the curried function](#curried)
    

## Installation

To install the package, use [Composer](https://getcomposer.org/doc/) 
(Or [The Force](https://www.youtube.com/watch?v=o2we_B6hDrY) for the Jedi Developers).

```bash
composer require serafim/interval
```

## Usage

### Left currying

The left currying can be perceived as adding arguments to an array. 
And then applying this array of arguments to the function.


The left currying returns the partially applied function 
from the first argument.

```php
// Curried function
$fn = \curry(function(...$args) { return \array_sum($args); });

echo $fn(1)(2)(3)(4)(); 
// (1) + (2) + (3) + (4) = 10

echo $fn(1, 2)(3, 4)(); 
// (1 + 2) + (3 + 4) = 10

echo $fn(1, 2, 3)(4)(); 
// (1 + 2 + 3) + (4) = 10

// Hmmm.... It does not matter in what order you are applying this 
```


### Right currying

At the same time, right-hand currying can be 
perceived as adding arguments to the right.

```php
$fn = \rcurry('\\file_put_contents', 'text');

$fn(__DIR__ . '/file1.txt')(); // Write "text" into file1.txt
$fn(__DIR__ . '/file2.txt')(); // Write "text" into file1.txt
$fn(__DIR__ . '/file2.txt')(); // Write "text" into file1.txt
```

### Partial application

Partial application is when you can specify completely 
random arguments, skipping unnecessary.

```php
$fn = \curry(function($a, $b, $c) { return $a + $b * $c; });

$multiply = $fn(_, 2, 2); // ? + 2 * 2
$result = $multiply(3);   // 3 + 2 * 2 = 7

echo $result; // 7
```


```php
$fn = \curry(function($a, $b, $c) { return $a + $b * $c; });

$sum  = $fn(2, 2);    // 2 + 2 * ?
$mul  = $fn(_, 2, 2); // ? + 2 * 2
$test = $fn(_, 2);    // ? + 2 * ?

$sum(6);          // 2 + 2 * 6 = 14
$mul(6);          // 6 + 2 * 2 = 10
$test(6);         // 6 + 2 * ? = function($c) 6 + 2 * $c 
$test->rcurry(6); // ? + 2 * 6 = function($a) $a + 2 * 6
```

## Api

### Functions

- `lcurry(callable $fn, ...$args): Curried` or `curry`
> Left currying (like array_push arguments)

- `rcurry(callable $fn, ...$args): Curried` 
> Right currying

- `uncurry(callable $fn): mixed`
> Returns result or partially applied function


### Curried

- `$fn->__invoke(...$args)` or `$fn(...$args)`
> The magic method that allows an object to a callable type

- `$fn->lcurry(...$args)`
> A method that returns a new function with left currying

- `$fn->rcurry(...$args)`
> A method that returns a new function with right currying

- `$fn->reduce()`
> Reduction of the composition of functions. Those. bringing the function to a single value - the result of this function.

- `$fn->uncurry()`
> An attempt is made to reduce, or bring the function to another, which will return the result

- `$fn->__toString()`
> Just a function dump
