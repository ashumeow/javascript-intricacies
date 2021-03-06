# JavaScript Intricacies

This is a growing collection of JavaScript intricacies, or things that are not easily understood.

Feel free to submit pull requests :)

## Snippets

Q. What's the result?

```javascript
(function() {
    var foo = new Object();
    var bar = new Object();
    var map = new Object();

    map[foo] = "foo";
    map[bar] = "bar";

    return map[foo];
})();
```

A.

```javascript
"bar"
```

Q. What's the result?

```javascript
function f() {
    return "foo";
}
(function() {
    if (1 == 0) {
        function f() {
            return "bar";
        }
    }
    return f();
})();
```

A. ES5

```javascript
"bar"
```

A. ES6

```javascript
"foo"
```

Q. What's the result?

```javascript
(function() {
    return NaN !== NaN;
})();
```

A.

```javascript
true
```

Q. What's the result?

```javascript
(function() {
    function foo() {
        return "a";
    }

    return foo();

    function foo() {
        return "b";
    }
})();
```

A.

```javascript
"b"
```

Q. What's the result?

```javascript
(function(limit) {
  for (var i = 0; i < limit; i++) {
    setTimeout(function() {
      console.log(i);
    }, 0);
  }
})(3);
```

A.

```javascript
3
3
3
```

Q. What's the result?

```javascript
(function() {
    return ~(-3);
})();
```

A.

```javascript
2
```

Q. What's the result?

```javascript
(function() {
    return ~~(-3.4);
})();
```

A.

```javascript
3
```

Q. What's the result?

```javascript
(function() {
    return (function (a, b) {}).length;
})();
```

A.

```javascript
2
```

Q. What's the result?

```javascript
(function(num) {
    return ~~num;
})(1.5);
```

A.

```javascript
1
```

Q. What's the result?

```javascript
(function(foo) {
    return !!foo
})("a");
```

A.

```javascript
true
```

Q. What's the result?

```javascript
(function() {
    return typeof null === "object";
})();
```

A.

```javascript
true
```

Q. What's the result?

```javascript
(function() {
    this.bar = "a";

    function qux(bar) {
        this.bar = this.bar || bar;
    }

    function foo(bar) {
        return this.bar || bar;
    }

    return (function(bar) {
        return foo.bind(this)(bar);
    }).call(new qux("b"), "c");
})();
```

A.

```javascript
"b"
```

Q. What's the result?

```javascript
(function() {}
    var foo = ["a","b","c","d"];
    var bar = ["z","y","x"];
    foo.splice.apply(foo, [2, 1].concat(bar));
    return foo;
})();
```

A.

```javascript
["a", "b", "z", "y", "x", "d"]
```

Q. What's the result?

```javascript
(function() {
    return +(new Date())
})();
```

A.

```javascript
1393812837139
```

Q. What's the result?

```javascript
(function() {
    return (new Date()).valueOf();
})();
```

A.

```javascript
1393812845834
```

Q. What's the result?

```javascript
(function() {
    return (new Date()).toString();
})();
```

A.

```javascript
"Sun Mar 02 2014 18:14:01 GMT-0800 (PST)"
```

Q. What's the result?

```javascript
(function() {
    var foo = "a";
    (function(foo) {
        foo = "b";
    })(foo);
    return foo;
})();
```

A.

```javascript
"a"
```

Q. What's the result?

```
(function() {
    function foo(qux) {
        return qux || this.foo;
    }

    return (Function.bind.bind(Function.call)(foo))({foo: "foo"}, "qux");
})();
```

A.

```javascript
"qux"
```

Q. What's the result?

```javascript
(function() {
    return arguments.toString();
})();
```

A.

```javascript
"[object Arguments]"
```

Q. What's the result?

```javascript
(function() {
    function always(val) {
        return function() {
            return val;
        };
    }

    var f = always(function(){});
    var g = always(function(){});

    return f() === g();
})();
```

A.

```javascript
false
```

Q. What's the result?

```javascript
(function() {
    var num1 = 10;
    var num2 = new Number('10');
    return num1 === num2;
})();
```

A.

```javascript
false
```

Q. What's the result?

```
(function() {
    return [1+1] === [2];
})()
```

A.

```
false
```

Q. What's the result?

```javascript
(function() {
    var obj1 = { foo: 'bar' };
    var obj2 = { foo: 'bar' };
    return obj1 === obj2;
})();
```

A.

```javascript
false
```

Q. What's the result?

```javascript
    ["10","10","10","10"].map(parseInt);
```

A.

```javascript
[10, NaN, 2, 3]
```

Q. What's the result?

```javascript
(function() {
    var o = {
        toString: function() {
            return "a";
        },
        valueOf: function () {
            return 1;
        }
    };

    return o+o;
})();
```

A.

```javascript
2
```

Q. What's the result?

```javascript
(function() {
    function Foo() {}

    function Bar() {}
    Bar.prototype.constructor = Bar;

    Bar.prototype = new Foo();

    return (new Bar()).constructor;
})();
```

A.

```javascript
function Foo() {}
```

Q. What's the result?

```javascript
(function() {

  var f = function g() {
    return 1;
  };

  return g();

})();
```

A.

```javascript
ReferenceError: g is not defined
```

[JSBin](http://jsbin.com/pibob/1/edit)

Q. What's the result?

```javascript
(function() {

  return void (1+1);

})();
```

A.

```javascript
undefined
```

[JSBin](http://jsbin.com/cawiro/1/edit)

Q. What's the result?

```javascript
(function() {

  var a = [1,2];
  var b = a;

  a = [1,2];

  return a === b;

})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/kucob/1/edit)

Q. What's the result?

```javascript
(function() {
    return {foo: 'bar'} === {foo: 'bar'};
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/meyet/1/edit)

Q. What's the result?

```javascript
(function() {
    var questionable = 'outer';

    return (function () {
        return questionable;

    var questionable = 'inner'
    })();
})();
```

A.

```javascript
undefined
```

[JSBin](http://jsbin.com/kesori/1/edit)

Q. What's the result?

```javascript
(function() {
    return new String('foo') === 'foo';
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/femeto/1/edit)

Q. What's the result?

```javascript
(function(n) {
    var even = function (num) {
        return (num === 0) || !(even(num - 1))
    };

    var _even = even;

    even = void 0;

    return _even(n);
})(2);
```

A.

```javascript
TypeError: undefined is not a function
```

[JSBin](http://jsbin.com/mopab/1/edit)

Q. What's the result?

```javascript
(function() {
    var n;

    function name() {
        return this.name
    };

    n = name.bind({name: 'foo'});
    n.bind({name: 'bar'})

    return n();
})();
```

A.

```javascript
"foo"
```

[JSBin](http://jsbin.com/mohuf/1/edit)

Q. What's the result? (assuming window scope)

```javascript
var declared = 1;
Object.getOwnPropertyDescriptor(window, "declared").configurable;
```

A.

```javascript
false
```

Q. What's the result? (assuming window scope)

```javascript
declared = 1;
Object.getOwnPropertyDescriptor(window, "declared").configurable;
```

A.

```javascript
true
```

### Weird parts of JavaScript

Q. What's the result?

```
(function() {
    return ![];
})();
```

A.

```javascript
false
```

Q. What's the result?

```
(function() {
    return +[];
})();
```

A.

```javascript
0
```

Q. What's the result?

```
(function() {
    return +[![]];
})();
```

A.

```javascript
NaN
```

Q. What's the result?

```
(function() {
    return [][[]];
})();
```

A.

```javascript
undefined
```

Q. What's the result?

```
(function() {
    return +!+[];
})();
```

A.

```javascript
1
```

Q. What's the result?

```
(function() {
    return []+[];
})();
```

A.

```javascript
""
```

Q. What's the result?

```
(function() {
    return true + 1;
})();
```

A.

```javascript
2
```

Q. What's the result?

```
(function() {
    return (parseInt("10000000000000000", 10) <
            parseInt("10000000000000001", 10)
    );
})();
```

A.

```javascript
false
```

## License

Released under the MIT License.
