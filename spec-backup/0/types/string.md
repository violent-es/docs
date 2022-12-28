# String Type

The `String` data type is UTF-8 encoded. Use `iterate` for fast code point iteration and UTF-8 specific methods for fast manipulation. Methods that take `StringIndex` should be efficient since `StringIndex` contains an UTF-8 index within itself.

```
var s = 'foo\u{1F602}foo';
s.length; // 7
s.charCodeAt(3); // 0x1F_602
s.slice(3, 4); // '\u{1F602}'

// several String methods also accept StringIndex as parameter,
// which is faster than Int. Int corresponds to a code point index that is
// dynamically converted to an UTF-8 index by internally iterating the UTF-8 content.
// A StringIndex object contains an UTF-8 index within itself,
// so methods like charCodeAt() and slice() do not need to
// internally iterate the UTF-8 content.

var i = s.lastIndexOf('foo'); // StringIndex?
i?.default; // index in code points
i?.utf8; // index in UTF-8 octets

// left-to-right iterator

var it = s.iterate;
it.hasRemaining;
it.index; // StringIndex
it.peek(); // it[0]
it.peek(1); // it[1]
it.peekSequence(3);
it.next();
it.skipSequence(3);

// right-to-left iterator

var it = s.iterateRightToLeft;
it[0]; // last character

// for special cases: UTF-8 specific operations

s.lengthUTF8; // number of octets
s.octetAtUTF8(0);
s.charCodeAtUTF8(0); // takes UTF-8 index and returns code point

// for special cases: index conversion

s.indexToUTF8Index(someIndex); // code point index to UTF-8 index
s.utf8IndexToIndex(someIndex); // UTF-8 index to code point index
```