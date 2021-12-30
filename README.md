# jsdefinitivenote
Notes for JavaScript Definitive Guide book
Ch.1 Introduction to JavaScript

- JavaScript is a high-level, dynamic, interpreted programming language that is well-suited to object-oriented and functional programming styles.
Ch.2 Lexical Structure

- The lexical structure of a programming language is the set of elementary rules that specifies how you write programs in that language.
	. Case sensitivity, spaces, and line breaks
	. Comments
	.Literals
	.Identifiers and reserved words
	.Unicode
	.Optional semicolons
- This means that language keywords, variables, function names, and other identifiers must always be typed with a consistent capitalization of letters.
-JavaScript ignores spaces. For most part, JavaScript also ignores line breaks.

Comments
- JavaScript supports two styles of comments. Any text between a //
and the end of a line is treated as a comment and is ignored by
JavaScript. Any text between the characters /* and */ is also treated
as a comment; these comments may span multiple lines but may not be
nested.
Literals
- A literal is a data value that appears directly in a program.
Identifiers and Reserved Words
-An identifier is simply an name. In JavaScript, identifiers are used to name constants, variables, properties, functions , and classes and to provide labels for certain loops in JavaScript code.
-A JavaScript identifier must begin with a letter, an underscore (_), or a dollar sign($). Subsequent characters can be letters, digits, underscores, or dollar signs. (Digits are not allowed as the first character so that JavaScript can easily distinguish identifiers from numbers.)

Reserved Words
- The following words are part of the JavaScript language. Many of these (such as if, while, and for) are reserved keywords that must not be used as the names of constants, variables, functions, or classes (though they can all be used as the names of properties within an object).
- JavaScript also reserves or restricts the use of certain keywords that are not currently used by the language but that might be used in future versions:
.enum
.implements
.interface
.package
.private
.protected
.public

Unicode
- JavaScript programs are written using the Unicode character set, and you can use any Unicode characters in strings and comments. For portability and ease of editing, it is common to use only ASCII letters and digits in identifiers. But this is a programming convention only, and the language allows Unicode letters, digits, and ideographs (but not
emojis) in identifiers. This means that programmers can use
mathematical symbols and words from non-English languages as
constants and variables:  
const π = 3.14;
const sí = true;

Optional Semicolons
- Like many programming languages, JavaScript uses the semicolon(;) to separate statements from one another.
- A few details you should understand about optional semicolons in JavaScript.
- Note that JavaScript does not treat every line break as a semicolon: it usually treats line breaks as semicolons only if it can’t parse the code without adding an implicit semicolon. JavaScript treats a line break as a semicolon if the next nonspace character cannot be interpreted as a continuation of the current statement. Consider the following code: 
let a 
a
=
3
console.log(a)
-  JavaScript interprets this code like this:
let a; a = 3; console.log(a);
- JavaScript does treat the first line break as a semicolon because it cannot parse the code let a a without a semicolon. The second a could stand alone as the statement a;, but JavaScript does not treat the second line break as a semicolon because it can continue parsing the longer statement a = 3;.
- These statement termination rules lead to some surprising cases. This
code looks like two separate statements separated with a newline:
	let y = x + f
	(a+b).toString()
- But the parentheses on the second line of code can be interpreted as a
function invocation of f from the first line, and JavaScript interprets
the code like this:- 
	let y = x + f(a+b).toString();
- Some programmers like to put a defensive semicolon at the beginning of any such statement so that it will continue to work correctly even if the statement before it is modified and a previously terminating semicolon removed:
	let x = 0 // Semicolon omitted here 
	;[x,x+1,x+2].forEach(console.log) // Defensive ; keeps this statement separate

- There are three exceptions to the general rule that JavaScript interprets line breaks as semicolons when it cannot parse the second line as a continuation of the statement on the first line. The first exception involves the return, throw, yield, break, and continue statements (see Chapter 5). These statements often stand alone, but they are sometimes followed by an identifier or expression. If a line break appears after any of these words (before any other tokens), JavaScript will always interpret that line break as a semicolon. For example, if you write:
	return
	true;
JavaScript assumes you meant:
	return; true;
However, you probably meant:
	return true;
-This means that you must not insert a line break between return, break, or continue and the expression that follows the keyword. If you do insert a line break, your code is likely to fail in a nonobvious way that is difficult to debug. -The second exception involves the ++ and −− operators (§4.8). These operators can be prefix operators that appear before an expression or postfix operators that appear after an expression. If you want to use either of these operators as postfix operators, they must appear on thesame line as the expression they apply to. The third exception involves functions defined using concise “arrow” syntax: the => arrow itself must appear on the same line as the parameter list
Ch-3 Types, Values, and Variables

- JavaScript types can be divided into two categories: primitive types and object types. JavaScript’s primitive types include numbers, strings of text (known as strings), and Boolean truth values (known as booleans).
-  The special JavaScript values null and undefined are primitive values, but they are not numbers, strings, or booleans.Each value is typically considered to be the sole member of its own special type.
- ES6 adds a new special- purpose type, known as Symbol, that enables the definition of language extensions without harming backward compatibility.
- An object (that is, a member of the type object) is a collection of properties where each property has a name and a value (either a primitive value or another object). An ordinary JavaScript object is an unordered collection of named values. The language also defines a special kind of object, known as an array, that represents an ordered collection of numbered values. The JavaScript language includes special syntax for working with arrays, and arrays have some special behavior that distinguishes them from ordinary objects.
- JavaScript differs from more static languages in that functions and classes are not just part of the language syntax: they are themselves values that can be manipulated by JavaScript programs. Like any JavaScript value that is not a primitive value, functions and classes are a specialized kind of object.
- The JavaScript interpreter performs automatic garbage collection for memory management. This means that a JavaScript programmer generally does not need to worry about destruction or deallocation of objects or other values. When a value is no longer reachable—when a program no longer has any way to refer to it—the interpreter knows it can never be used again and automatically reclaims the memory it was occupying. (JavaScript programmers do sometimes need to take care to ensure that values do not inadvertently remain reachable—and therefore nonreclaimable—longer than necessary.)
- JavaScript supports an object-oriented programming style. Loosely, this means that rather than having globally defined functions to operate on values of various types, the types themselves define methods for working with values. To sort the elements of an array a, for example, we don’t pass a to a sort() function. Instead, we invoke the sort() method of a:
	a.sort(); // The object-oriented version of sort(a).
- Technically, it is only JavaScript objects that have methods. But numbers, strings, boolean, and symbol values behave as if they have methods. In JavaScript, null and undefined are the only values that methods cannot be invoked on.

-JavaScript’s object types are mutable and its primitive types are immutable. A value of a mutable type can change: a JavaScript program can change the values of object properties and array elements. Numbers, booleans, symbols, null, and undefined are immutable —it doesn’t even make sense to talk about changing the value of a number, for example. Strings can be thought of as arrays of characters, and you might expect them to be mutable. In JavaScript, however, strings are immutable: you can access the text at any index of a string, but JavaScript provides no way to alter the text of an existing string. The differences between mutable and immutable values are explored further in §3.8. JavaScript liberally converts values from one type to another. If a program expects a string, for example, and you give it a number, it will automatically convert the number to a string for you. And if you use a non-boolean value where a boolean is expected, JavaScript will convert accordingly. The rules for value conversion are explained in §3.9. JavaScript’s liberal value conversion rules affect its definition of equality, and the == equality operator performs type conversions as described in §3.9.1. (In practice, however, the == equality operator is deprecated in favor of the strict equality operator ===, which does no type conversions. See §4.9.1 for more about both operators.)Constants and variables allow you to use names to refer to values in your programs. Constants are declared with const and variables are declared with let (or with var in older JavaScript code). JavaScript constants and variables are untyped: declarations do not specify what kind of values will be assigned. Variable declaration and assignment are covered in §3.10.
