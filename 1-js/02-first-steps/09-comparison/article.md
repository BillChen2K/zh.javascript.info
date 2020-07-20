<<<<<<< HEAD
# 值的比较

我们知道，在数学中有很多用于比较大小的运算符。

在 JavaScript 中，它们的编写方式如下：

- 大于 / 小于：<code>a &gt; b</code>，<code>a &lt; b</code>。
- 大于等于 / 小于等于：<code>a &gt;= b</code>，<code>a &lt;= b</code>。
- 检查两个值的相等：`a == b`，请注意双等号 `==` 表示相等性检查，而单等号 `a = b` 表示赋值。
- 检查两个值不相等。不相等在数学中的符号是 <code>&ne;</code>，但在 JavaScript 中写成 <code>a != b</code>。

在本文中，我们将进一步了解不同类型的比较，JavaScript 是如何进行比较的，包括一些重要的特殊性。

在文末给出了一些秘诀，帮助你避免“javascript 陷阱”相关的问题。

## 比较结果为 Boolean 类型

所有比较运算符均返回布尔值：

- `true` —— 表示“yes（是）”，“correct（正确）”或“the truth（真）”。
- `false` ——  表示“no（否）”，“wrong（错误）”或“not the truth（非真）”。

示例：

```js run
alert( 2 > 1 );  // true（正确）
alert( 2 == 1 ); // false（错误）
alert( 2 != 1 ); // true（正确）
```

和其他类型的值一样，比较的结果可以被赋值给任意变量：

```js run
let result = 5 > 4; // 把比较的结果赋值给 result
alert( result ); // true
```

## 字符串比较

在比较字符串的大小时，JavaScript 会使用“字典（dictionary）”或“词典（lexicographical）”顺序进行判定。

换言之，字符串是按字符（母）逐个进行比较的。

例如：
=======
# Comparisons

We know many comparison operators from maths.

In JavaScript they are written like this:

- Greater/less than: <code>a &gt; b</code>, <code>a &lt; b</code>.
- Greater/less than or equals: <code>a &gt;= b</code>, <code>a &lt;= b</code>.
- Equals: `a == b`, please note the double equality sign `==` means the equality test, while a single one `a = b` means an assignment.
- Not equals. In maths the notation is <code>&ne;</code>, but in JavaScript it's written as <code>a != b</code>.

In this article we'll learn more about different types of comparisons, how JavaScript makes them, including important peculiarities. 

At the end you'll find a good recipe to avoid "javascript quirks"-related issues.

## Boolean is the result

All comparison operators return a boolean value:

- `true` -- means "yes", "correct" or "the truth".
- `false` -- means "no", "wrong" or "not the truth".

For example:

```js run
alert( 2 > 1 );  // true (correct)
alert( 2 == 1 ); // false (wrong)
alert( 2 != 1 ); // true (correct)
```

A comparison result can be assigned to a variable, just like any value:

```js run
let result = 5 > 4; // assign the result of the comparison
alert( result ); // true
```

## String comparison

To see whether a string is greater than another, JavaScript uses the so-called "dictionary" or "lexicographical" order.

In other words, strings are compared letter-by-letter.

For example:
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

```js run
alert( 'Z' > 'A' ); // true
alert( 'Glow' > 'Glee' ); // true
alert( 'Bee' > 'Be' ); // true
```

<<<<<<< HEAD
字符串的比较算法非常简单：

1. 首先比较两个字符串的首位字符大小。
2. 如果一方字符较大（或较小），则该字符串大于（或小于）另一个字符串。算法结束。
3. 否则，如果两个字符串的首位字符相等，则继续取出两个字符串各自的后一位字符进行比较。
4. 重复上述步骤进行比较，直到比较完成某字符串的所有字符为止。
5. 如果两个字符串的字符同时用完，那么则判定它们相等，否则未结束（还有未比较的字符）的字符串更大。

在上面的例子中，`'Z' > 'A'` 在算法的第 1 步就得到了返回结果，而字符串 `Glow` 与 `Glee` 则继续逐个字符比较：

1. `G` 和 `G` 相等。
2. `l` 和 `l` 相等。
3. `o` 比 `e` 大，算法停止，第一个字符串大于第二个。

```smart header="非真正的字典顺序，而是 Unicode 编码顺序"
在上面的算法中，比较大小的逻辑与字典或电话簿中的排序很像，但也不完全相同。

比如说，字符串比较对字母大小写是敏感的。大写的 `"A"` 并不等于小写的 `"a"`。哪一个更大呢？实际上小写的 `"a"` 更大。这是因为在 JavaScript 使用的内部编码表中（Unicode），小写字母的字符索引值更大。我们会在 <info:string> 这章讨论更多关于字符串的细节。
```

## 不同类型间的比较

当对不同类型的值进行比较时，JavaScript 会首先将其转化为数字（number）再判定大小。

例如：

```js run
alert( '2' > 1 ); // true，字符串 '2' 会被转化为数字 2
alert( '01' == 1 ); // true，字符串 '01' 会被转化为数字 1
```

对于布尔类型值，`true` 会被转化为 `1`、`false` 转化为 `0`。

例如：
=======
The algorithm to compare two strings is simple:

1. Compare the first character of both strings.
2. If the first character from the first string is greater (or less) than the other string's, then the first string is greater (or less) than the second. We're done.
3. Otherwise, if both strings' first characters are the same, compare the second characters the same way.
4. Repeat until the end of either string.
5. If both strings end at the same length, then they are equal. Otherwise, the longer string is greater.

In the examples above, the comparison `'Z' > 'A'` gets to a result at the first step while the strings `"Glow"` and `"Glee"` are compared character-by-character:

1. `G` is the same as `G`.
2. `l` is the same as `l`.
3. `o` is greater than `e`. Stop here. The first string is greater.

```smart header="Not a real dictionary, but Unicode order"
The comparison algorithm given above is roughly equivalent to the one used in dictionaries or phone books, but it's not exactly the same.

For instance, case matters. A capital letter `"A"` is not equal to the lowercase `"a"`. Which one is greater? The lowercase `"a"`. Why? Because the lowercase character has a greater index in the internal encoding table JavaScript uses (Unicode). We'll get back to specific details and consequences of this in the chapter <info:string>.
```

## Comparison of different types

When comparing values of different types, JavaScript converts the values to numbers.

For example:

```js run
alert( '2' > 1 ); // true, string '2' becomes a number 2
alert( '01' == 1 ); // true, string '01' becomes a number 1
```

For boolean values, `true` becomes `1` and `false` becomes `0`.

For example:
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

```js run
alert( true == 1 ); // true
alert( false == 0 ); // true
```

<<<<<<< HEAD
````smart header="一个有趣的现象"
有时候，以下两种情况会同时发生：

- 若直接比较两个值，其结果是相等的。
- 若把两个值转为布尔值，它们可能得出完全相反的结果，即一个是 `true`，一个是 `false`。

例如：
=======
````smart header="A funny consequence"
It is possible that at the same time:

- Two values are equal.
- One of them is `true` as a boolean and the other one is `false` as a boolean.

For example:
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

```js run
let a = 0;
alert( Boolean(a) ); // false

let b = "0";
alert( Boolean(b) ); // true

alert(a == b); // true!
```

<<<<<<< HEAD
对于 JavaScript 而言，这种现象其实挺正常的。因为 JavaScript 会把待比较的值转化为数字后再做比较（因此 `"0"` 变成了 `0`）。若只是将一个变量转化为 `Boolean` 值，则会使用其他的类型转换规则。
````

## 严格相等

普通的相等性检查 `==` 存在一个问题，它不能区分出 `0` 和 `false`：
=======
From JavaScript's standpoint, this result is quite normal. An equality check converts values using the numeric conversion (hence `"0"` becomes `0`), while the explicit `Boolean` conversion uses another set of rules.
````

## Strict equality

A regular equality check `==` has a problem. It cannot differentiate `0` from `false`:
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

```js run
alert( 0 == false ); // true
```

<<<<<<< HEAD
也同样无法区分空字符串和 `false`：
=======
The same thing happens with an empty string:
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

```js run
alert( '' == false ); // true
```

<<<<<<< HEAD
这是因为在比较不同类型的值时，处于相等判断符号 `==` 两侧的值会先被转化为数字。空字符串和 `false` 也是如此，转化后它们都为数字 0。

如果我们需要区分 `0` 和 `false`，该怎么办？

**严格相等运算符 `===` 在进行比较时不会做任何的类型转换。**

换句话说，如果 `a` 和 `b` 属于不同的数据类型，那么 `a === b` 不会做任何的类型转换而立刻返回 `false`。

让我们试试：

```js run
alert( 0 === false ); // false，因为被比较值的数据类型不同
```

同样的，与“不相等”符号 `!=` 类似，“严格不相等”表示为 `!==`。

严格相等的运算符虽然写起来稍微长一些，但是它能够很清楚地显示代码意图，降低你犯错的可能性。

## 对 null 和 undefined 进行比较

当使用 `null` 或 `undefined` 与其他值进行比较时，其返回结果常常出乎你的意料。

当使用严格相等 `===` 比较二者时 
: 它们不相等，因为它们属于不同的类型。
=======
This happens because operands of different types are converted to numbers by the equality operator `==`. An empty string, just like `false`, becomes a zero.

What to do if we'd like to differentiate `0` from `false`?

**A strict equality operator `===` checks the equality without type conversion.**

In other words, if `a` and `b` are of different types, then `a === b` immediately returns `false` without an attempt to convert them.

Let's try it:

```js run
alert( 0 === false ); // false, because the types are different
```

There is also a "strict non-equality" operator `!==` analogous to `!=`.

The strict equality operator is a bit longer to write, but makes it obvious what's going on and leaves less room for errors.

## Comparison with null and undefined

There's a non-intuitive behavior when `null` or `undefined` are compared to other values.

For a strict equality check `===`
: These values are different, because each of them is a different type.
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

    ```js run
    alert( null === undefined ); // false
    ```

<<<<<<< HEAD
当使用非严格相等 `==` 比较二者时
: JavaScript 存在一个特殊的规则，会判定它们相等。他们俩就像“一对恋人”，仅仅等于对方而不等于其他任何的值（只在非严格相等下成立）。
=======
For a non-strict check `==`
: There's a special rule. These two are a "sweet couple": they equal each other (in the sense of `==`), but not any other value.
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

    ```js run
    alert( null == undefined ); // true
    ```

<<<<<<< HEAD
当使用数学式或其他比较方法 `< > <= >=` 时：
: `null/undefined` 会被转化为数字：`null` 被转化为 `0`，`undefined` 被转化为 `NaN`。

下面让我们看看，这些规则会带来什么有趣的现象。同时更重要的是，我们需要从中学会如何远离这些特性带来的“陷阱”。

### 奇怪的结果：null vs 0

通过比较 `null` 和 0 可得：
=======
For maths and other comparisons `< > <= >=`
: `null/undefined` are converted to numbers: `null` becomes `0`, while `undefined` becomes `NaN`.

Now let's see some funny things that happen when we apply these rules. And, what's more important, how to not fall into a trap with them.

### Strange result: null vs 0

Let's compare `null` with a zero:
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

```js run
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) *!*true*/!*
```

<<<<<<< HEAD
是的，上面的结果完全打破了你对数学的认识。在最后一行代码显示“`null` 大于等于 0”的情况下，前两行代码中一定会有一个是正确的，然而事实表明它们的结果都是 false。

为什么会出现这种反常结果，这是因为相等性检查 `==` 和普通比较符 `> < >= <=` 的代码逻辑是相互独立的。进行值的比较时，`null` 会被转化为数字，因此它被转化为了 `0`。这就是为什么（3）中 `null >= 0` 返回值是 true，（1）中 `null > 0` 返回值是 false。

另一方面，`undefined` 和 `null` 在相等性检查 `==` 中不会进行任何的类型转换，它们有自己独立的比较规则，所以除了它们之间互等外，不会等于任何其他的值。这就解释了为什么（2）中 `null == 0` 会返回 false。

### 特立独行的 undefined

`undefined` 不应该被与其他值进行比较：
=======
Mathematically, that's strange. The last result states that "`null` is greater than or equal to zero", so in one of the comparisons above it must be `true`, but they are both false.

The reason is that an equality check `==` and comparisons `> < >= <=` work differently. Comparisons convert `null` to a number, treating it as `0`. That's why (3) `null >= 0` is true and (1) `null > 0` is false.

On the other hand, the equality check `==` for `undefined` and `null` is defined such that, without any conversions, they equal each other and don't equal anything else. That's why (2) `null == 0` is false.

### An incomparable undefined

The value `undefined` shouldn't be compared to other values:
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc

```js run
alert( undefined > 0 ); // false (1)
alert( undefined < 0 ); // false (2)
alert( undefined == 0 ); // false (3)
```

<<<<<<< HEAD
为何它看起来如此厌恶 0？返回值都是 false！

原因如下：

- `(1)` 和 `(2)` 都返回 `false` 是因为 `undefined` 在比较中被转换为了 `NaN`，而 `NaN` 是一个特殊的数值型值，它与任何值进行比较都会返回 `false`。
- `(3)` 返回 `false` 是因为这是一个相等性检查，而 `undefined` 只与 `null` 相等，不会与其他值相等。

### 避免问题

我们为何要研究上述示例？我们需要时刻记得这些古怪的规则吗？不，其实不需要。虽然随着代码写得越来越多，我们对这些规则也都会烂熟于胸，但是我们需要更为可靠的方法来避免潜在的问题：

- 除了严格相等 `===` 外，其他但凡是有 `undefined/null` 参与的比较，我们都需要格外小心。
- 除非你非常清楚自己在做什么，否则永远不要使用 `>= > < <=` 去比较一个可能为 `null/undefined` 的变量。对于取值可能是 `null/undefined` 的变量，请按需要分别检查它的取值情况。

## 总结

- 比较运算符始终返回布尔值。
- 字符串的比较，会按照“词典”顺序逐字符地比较大小。
- 当对不同类型的值进行比较时，它们会先被转化为数字（不包括严格相等检查）再进行比较。
- 在非严格相等 `==` 下，`null` 和 `undefined` 相等且各自不等于任何其他的值。
- 在使用 `>` 或 `<` 进行比较时，需要注意变量可能为 `null/undefined` 的情况。比较好的方法是单独检查变量是否等于 `null/undefined`。
=======
Why does it dislike zero so much? Always false!

We get these results because:

- Comparisons `(1)` and `(2)` return `false` because `undefined` gets converted to `NaN` and `NaN` is a special numeric value which returns `false` for all comparisons.
- The equality check `(3)` returns `false` because `undefined` only equals `null`, `undefined`, and no other value.

### Avoid problems

Why did we go over these examples? Should we remember these peculiarities all the time? Well, not really. Actually, these tricky things will gradually become familiar over time, but there's a solid way to avoid problems with them:

- Treat any comparison with `undefined/null` except the strict equality `===` with exceptional care.
- Don't use comparisons `>= > < <=` with a variable which may be `null/undefined`, unless you're really sure of what you're doing. If a variable can have these values, check for them separately.

## Summary

- Comparison operators return a boolean value.
- Strings are compared letter-by-letter in the "dictionary" order.
- When values of different types are compared, they get converted to numbers (with the exclusion of a strict equality check).
- The values `null` and `undefined` equal `==` each other and do not equal any other value.
- Be careful when using comparisons like `>` or `<` with variables that can occasionally be `null/undefined`. Checking for `null/undefined` separately is a good idea.
>>>>>>> ae1171069c2e50b932d030264545e126138d5bdc
