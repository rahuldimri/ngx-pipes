# Angular2 Pipes

[![Build Status](https://travis-ci.org/danrevah/ng2-pipes.svg?branch=master)](https://travis-ci.org/danrevah/ng2-pipes)

> Useful pipes for Angular2

## Table of contents

 - [Installation](#installation)
 - [String](#String)
    - [repeat](#repeat)
    - [scan](#scan)
    - [shorten](#shorten)
    - [strip-tags](#strip-tags)
    - [ucfirst](#ucfirst)
    - [ucwords](#ucwords)
    - [trim](#trim)
    - [ltrim](#ltrim)
    - [rtrim](#rtrim)
    - [reverse](#reverse)
 - [Array](#Array)   
    - [diff](#diff)
    - [flatten](#flatten)
    - [initial](#initial)
    - [intersection](#intersection)
    - [reverse](#reverse)
    - [tail](#tail)
    - [truthify](#truthify)
    - [union](#union)
    - [unique](#unique)
    - [without](#without)
 

## Installation


1. Use npm to install the package

```
$ npm install ng2-pipes --save 
```

2. Add into your module `imports` the PipesModule

```typescript
import {NgPipesModule} from 'ng2-pipes';

@NgModule({
 // ...
 imports: [
   // ...
   NgPipesModule
 ]
})

```


## String

### repeat

Repeats a string n times
Api: `string | repeat: times: [separator|optional]`
Example:

```html
<p>{{ 'example' | repeat: 3: '@' }}</p> <!-- Output: "example@example@example" -->
```

### scan

Scans string and replace `{i}` placeholders by equivalent member of the array
Api: `string | scan: [ARRAY]`

```html
<p>{{'Hey {0}, {1}' | scan: ['foo', 'bar']}}</p> <!-- Output: "Hey foo, bar" -->
```

### shorten

Shortening a string by length and providing a custom string to denote an omission

Api: `string | shorten: length: [suffix|optional]: [wordBreak boolean|optional]`

```html
<p>{{'Hey foo bar' | shorten: 3: '...'}}</p> <!-- Output: "Hey..." -->
```

### strip-tags

Strips a HTML tags from string and providing which tags should not be removed
Api: `string | strip-tags: [ARRAY]`

```html
<p>{{'<a href="">foo</a> <p class="foo">bar</p>' | strip-tags }}</p> <!-- Output: "foo bar" -->
<p>{{'<a href="">foo</a> <p class="foo">bar</p>' | strip-tags: ['p']}}</p> <!-- Output: foo <p class="foo">bar</p> -->
```

### ucfirst

Uppercase first letter of first word

```html
<p>{{'foo bar' | ucfirst }}</p> <!-- Output: "Foo bar" -->
```

### ucwords

Uppercase first letter every word

```html
<p>{{'foo bar' | ucwords }}</p> <!-- Output: "Foo Bar" -->
```

### trim

Strips characters from the beginning and end of a string (default character is space).
Api: `string | trim: [characters|optional]`

```html
<p>{{'  foo  ' | trim }}</p> <!-- Output: "foo" -->
<p>{{'foobarfoo' | ltrim: 'foo' }}</p> <!-- Output: "bar" -->
```

### ltrim

Strips characters from the beginning of a string (default character is space).
Api: `string | ltrim: [characters|optional]`

```html
<p>{{'  foo  ' | ltrim }}</p> <!-- Output: "foo  " -->
<p>{{'foobarfoo' | ltrim: 'foo' }}</p> <!-- Output: "barfoo" -->
```

### rtrim

Strips characters from the end of a string (default character is space).
Api: `string | rtrim: [characters|optional]`

```html
<p>{{'  foo  ' | rtrim }}</p> <!-- Output: "  foo" -->
<p>{{'foobarfoo' | rtrim: 'foo' }}</p> <!-- Output: "foobar" -->
```

### reverse

Reverses a string
Api: `string | reverse`

```html
<p>{{'foo bar' | reverse }}</p> <!-- Output: "rab oof" -->
```


## Array

### diff

Returns array of diff between arrays 
Api: `array | diff: [ARRAY]: [ARRAY]: ... : [ARRAY]`

```typescript
this.items = [1, 2, 3, 4];
```

```html
<li *ngFor="let item of items | diff: [[1, 2]]"> <-- Array: [3, 4] -->
```

### flatten

Flattens nested array, passing shallow will mean it will only be flattened a single level
Api: `array | flatten: [shallow|optional]`

```typescript
this.items = [1,2,3,[4,5,6,[7,8,9],[10,11,12,13,[14],[15],[16, [17]]]]];
```

```html
<li *ngFor="let item of items | flatten"> 
<-- Array: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17] -->
```

### initial

Slicing off the end of the array by n elements
Api: `array | initial: n`

```typescript
this.items = [first, second, third];
```

```html
<li *ngFor="let item of items | initial: 1"> <-- Array: [first, second] -->
```

### tail

Slicing off the start of the array by n elements
Api: `array | tail: n`

```typescript
this.items = [first, second, third];
```

```html
<li *ngFor="let item of items | tail: 1"> <-- Array: [second, third] -->
```

### intersection

Returns the intersections of an arrays
Api: `array | intersection: [ARRAY]: [ARRAY]: ... : [ARRAY]`

```typescript
this.items = [1, 2, 3, 4, 5];
```

```html
<li *ngFor="let item of items | intersection: [1, 2]: [3, 6]"> <-- Array: [1, 2, 3] -->
```

### reverse

Reverses an array
Api: `array | reverse`

```typescript
this.items = [1, 2, 3];
```

```html
<li *ngFor="let item of items | reverse"> <-- Array: [3, 2, 1] -->
```

### truthify

Removes un-truthy values from array
Api: `array | truthify`

```typescript
this.items = [null, 1, false, undefined, 2, 0, 3, NaN, 4, ''];
```

```html
<li *ngFor="let item of items | truthify"> <-- Array: [1, 2, 3, 4] -->
```

### union

Removes un-truthy values from array
Api: `array | union: [ARRAY]`

```typescript
this.items = [1, 2, 3];
```

```html
<li *ngFor="let item of items | union: [[4]]"> <-- Array: [1, 2, 3, 4] -->
```

### unique

Removes duplicates from array
Api: `array | unique`

```typescript
this.items = [1, 2, 3, 1, 2, 3];
```

```html
<li *ngFor="let item of items | unique"> <-- Array: [1, 2, 3] -->
```

### unique

Returns array without specific elements
Api: `array | without: [ARRAY]`

```typescript
this.items = [1, 2, 3, 1, 2, 3];
```

```html
<li *ngFor="let item of items | without: [1,3]"> <-- Array: [2, 2] -->
```