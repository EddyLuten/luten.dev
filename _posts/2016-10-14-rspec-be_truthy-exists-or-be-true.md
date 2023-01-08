---
layout: single
title:  "RSpec be_truthy, exist, or be true?"
date:   2016-10-14 00:00:00 -0700
---
The documentation for RSpec is amazingly detailed, but sometimes falls a bit short on when to apply certain matchers. In many of the specs that I've reviewed, incorrect matchers were used to test for pure Boolean values.

<!--more-->

## be_truthy and be_falsey

```ruby
expect(some_evaluation).to be_truthy
expect(some_evaluation).to be_falsey
```

The matcher `be_truthy` should only be used when expecting an evaluation to be *not* `nil` and *not* `false`.

The matcher `be_falsey` should only be used when expecting an evaluation to be `nil` or `false`.

Notice that `be_truthy` does not actually check for the Boolean value `true`.

If you have a method that should only be evaluated into a Boolean, do not use these matchers for your spec.

## be true and be false

```ruby
expect(some_evaluation).to be true
expect(some_evaluation).to be false
```

The matchers `be true` and `be false` expect *only* `true` and `false` returned, respectively. This is a straight up value comparison, so use this if your method or evaluation should only return `true` or `false`.

## exist

```ruby
expect(some_evaluation).to exist
```

The documentation for RSpec lists `exist` right along with `be true` and `be_truthy`, though it's not really related. A spec that matches on `exist` will only pass if the object has implemented the `exists?` or `exist?` methods *and* the result of its evaluation matches the `is_truthy` matcher.

This means that passing in `true`, `false`, or `nil`, will fail the test dramatically since none of them implement `exist?` or `exists?`.

## What's the Big Deal?

`nil`

`nil` is that sneaky value that creeps its way into your code when you don't expect it. It disguises itself as a missing element in a hash or an unexpected API response value and worms its way though your codebase until it hits *that method*. *That method* never expected `nil` and treats it just like any other value, spitting out a result that should be `true` or `false`, but is in actuality `nil`. The spec for *that method* uses `is_falsey` and passes beautifully. Meanwhile, your application breaks and you now have a table column populated with `NULL` values. Whoops. Good luck figuring out where that happened.

This may seem pedantic and unlikely to happen, but entropy increases as your application grows more complex and these types of problems begin rearing their ugly heads. Especially in dynamically typed languages such as Ruby. So, in most cases, use `be true` or `be false` unless you really have a  good reason not to do so.
