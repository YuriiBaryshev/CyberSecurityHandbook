# JavaScript basic types of variables

### Undefined - typeof return "undefined"

The Undefined type is inhabited by exactly one value: undefined.

### Null - typeof return "object"

The Null type is inhabited by exactly one value: null.

### Boolean - typeof return "boolean"

The Boolean type represents a logical entity and is inhabited by two values: true and false.

### Number - typeof return "number"

The Number type is a [double-precision 64-bit binary format IEEE 754 value](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number#number_encoding). It is capable of storing positive floating-point numbers between 2^-1074 (Number.MIN_VALUE) and 2^1024 (Number.MAX_VALUE) as well as negative floating-point numbers between -2^-1074 and -2^1024, but it can only safely store integers in the range -(2^53 − 1) (Number.MIN_SAFE_INTEGER) to 2^53 − 1 (Number.MAX_SAFE_INTEGER). Outside this range, JavaScript can no longer safely represent integers; they will instead be represented by a double-precision floating point approximation. You can check if a number is within the range of safe integers using Number.isSafeInteger().

### BigInt - typeof return "bigint"

The BigInt type is a numeric primitive in JavaScript that can represent integers with arbitrary magnitude. With BigInts, you can safely store and operate on large integers even beyond the safe integer limit (Number.MAX_SAFE_INTEGER) for Numbers.

### String - typeof return "string"

The String type represents textual data and is encoded as a sequence of 16-bit unsigned integer values representing [UTF-16 code units](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String#utf-16_characters_unicode_codepoints_and_grapheme_clusters). Each element in the string occupies a position in the string. The first element is at index 0, the next at index 1, and so on. The length of a string is the number of UTF-16 code units in it, which may not correspond to the actual number of Unicode characters; see the String reference page for more details.

### Symbol - typeof return "symbol"

A Symbol is a unique and immutable primitive value and may be used as the key of an Object property (see below). In some programming languages, Symbols are called "atoms". The purpose of symbols is to create unique property keys that are guaranteed not to clash with keys from other code.