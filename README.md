# Interval

A small library that implements the interval iterator function.

## Installation

To install the package, use the [Composer](https://getcomposer.org/doc/).

```bash
composer require serafim/interval
```

## Usage

### Increasing interval

In the second integer argument (to) is greater than the first 
integer argument (from), the interval will be incremented by `1`.

```php
$interval = \interval(1, 6); 
// [1, 2, 3, 4, 5, 6]
```

### Decreasing interval

In the first integer argument (from) is greater than the second 
integer argument (to), the interval will be decremented by `-1`. 

```php
$interval = \interval(6, 1); 
// [6, 5, 4, 3, 2, 1]
```

### Floats interval

If one of the values is float, the step will 
automatically change to `.1` (or `-.1`).

```php
$incremental = \interval(.5, 1); 
// [0.5, 0.6, 0.7, 0.8, 0.9, 1.0]

$decremental = \interval(1, .5); 
// [1.0, 0.9, 0.8, 0.7, 0.6, 0.5]
```

### Step indication

```php
$interval = \interval(1, 1.1)->step(.05); 
// [1.0, 1.05, 1.1]
```

### Infinity increasing interval

```php
$interval = \interval(1); 
// [1, 2, 3, 4 … ∞]
```

### Infinity decreasing interval

```php
$interval = \interval(2)->step(-1); 
// [2, 1, 0, -1, -2 … ∞]
```

### Shortcut definition

Just a little insanity, why not? Just do not ask how it works!
```php
$interval = \interval(1...5);
// [1, 2, 3, 4, 5]
```
