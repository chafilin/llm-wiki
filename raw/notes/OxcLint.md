# OxcLint
#code
## id-length
```
	/// ### What it does
    ///
    /// This rule enforces a minimum and/or maximum identifier length convention.
    /// This rule counts [graphemes](https://unicode.org/reports/tr29/#Default_Grapheme_Cluster_Table) instead of using [String length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length).
    ///
    /// ### Why is this bad?
    ///
    /// Very short identifier names like e, x, _t or very long ones like
    /// hashGeneratorResultOutputContainerObject can make code harder to
    /// read and potentially less maintainable. To prevent this, one may enforce a
    /// minimum and/or maximum identifier length.
    ///
    /// ### Examples
    ///
    /// Examples of incorrect code for this rule with the default `{ "max": 2 }` option:
    ///
    /// ```javascript
    ///
    /// const x = 5;
    /// obj.e = document.body;
    /// const foo = function (e) { };
    /// try {
    ///     dangerousStuff();
    /// } catch (e) {
    ///     // ignore as many do
    /// }
    /// const myObj = { a: 1 };
    /// (a) => { a * a };
    /// class y { }
    /// class Foo { x() {} }
    /// class Bar { #x() {} }
    /// class Baz { x = 1 }
    /// class Qux { #x = 1 }
    /// function bar(...x) { }
    /// function baz([x]) { }
    /// const [z] = arr;
    /// const { prop: [i]} = {};
    /// function qux({x}) { }
    /// const { j } = {};
    /// const { prop: a} = {};
    /// ({ prop: obj.x } = {});
    /// ```
    ///
    /// Examples of correct code for this rule with the default `{ "max": 2 }` options:
    ///
    /// ```javascript
    /// const num = 5;
    /// function _f() { return 42; }
    /// function _func() { return 42; }
    /// obj.el = document.body;
    /// const foo = function (evt) { /* do stuff */ };
    /// try {
    ///     dangerousStuff();
    /// } catch (error) {
    ///     // ignore as many do
    /// }
    /// const myObj = { apple: 1 };
    /// (num) => { num * num };
    /// function bar(num = 0) { }
    /// class MyClass { }
    /// class Foo { method() {} }
    /// class Bar { #method() {} }
    /// class Baz { field = 1 }
    /// class Qux { #field = 1 }
    /// function baz(...args) { }
    /// function qux([longName]) { }
    /// const { prop } = {};
    /// const { prop: [name] } = {};
    /// const [longName] = arr;
    /// function foobar({ prop }) { }
    /// function foobaz({ a: prop }) { }
    /// const { a: property } = {};
    /// ({ prop: obj.longName } = {});
    /// const data = { "x": 1 };  // excused because of quotes
    /// data["y"] = 3;  // excused because of calculated property access
    /// ```
    ///
    /// ### Options
    /// This rule has an object option:
    ///
    /// - "min" (default: 2) enforces a minimum identifier length
    /// - "max" (default: Infinity) enforces a maximum identifier length
    /// - "properties": always (default) enforces identifier length convention for property names
    /// - "properties": never ignores identifier length convention for property names
    /// - "exceptions" allows an array of specified identifier names
    /// - "exceptionPatterns" array of strings representing regular expression patterns, allows identifiers that match any of the patterns.
    /// TODO: add example for each option
```