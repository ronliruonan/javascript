# Airbnb JavaScript 风格指南() {

JavaScript最合理的方法 / *A mostly reasonable approach to JavaScript*

> **注意**：该指南假设你正在使用[Babel](https://babeljs.io)，并且需要你使用[babel-preset-airbnb](https://npmjs.com/babel-preset-airbnb) /或等效的东西。同时假设在你的应用中安装了带有[airbnb-browser-shims](https://npmjs.com/airbnb-browser-shims)的shims/polyfills /或等效的东西。    
> **Note**: this guide assumes you are using [Babel](https://babeljs.io), and requires that you use [babel-preset-airbnb](https://npmjs.com/babel-preset-airbnb) or the equivalent. It also assumes you are installing shims/polyfills in your app, with [airbnb-browser-shims](https://npmjs.com/airbnb-browser-shims) or the equivalent.

[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb.svg)](https://www.npmjs.com/package/eslint-config-airbnb)
[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb-base.svg)](https://www.npmjs.com/package/eslint-config-airbnb-base)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/airbnb/javascript?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

这份指南也有其他语言版本。请看[翻译](#translation)            
This guide is available in other languages too. See [Translation](#translation)

其他风格指南 / Other Style Guides

  - [ES5(已废弃) / ES5 (Deprecated)](https://github.com/airbnb/javascript/tree/es5-deprecated/es5)
  - [React](react/)
  - [CSS-in-JavaScript](css-in-javascript/)
  - [CSS & Sass](https://github.com/airbnb/css)
  - [Ruby](https://github.com/airbnb/ruby)

## 内容目录 / Table of Contents

  1. [类型 / Types](#types)
  1. [引用 / References](#references)
  1. [对象 / Objects](#objects)
  1. [数组 / Arrays](#arrays)
  1. [解构 / Destructuring](#destructuring)
  1. [字符串 / Strings](#strings)
  1. [函数 / Functions](#functions)
  1. [箭头函数 / Arrow Functions](#arrow-functions)
  1. [类&构造函数 / Classes & Constructors](#classes--constructors)
  1. [模块 / Modules](#modules)
  1. [Iterators and Generators](#iterators-and-generators)
  1. [属性 / Properties](#properties)
  1. [变量 / Variables](#variables)
  1. [提升 / Hoisting](#hoisting)
  1. [比较运算符&判等 / Comparison Operators & Equality](#comparison-operators--equality)
  1. [代码块 / Blocks](#blocks)
  1. [控制语句 / Control Statements](#control-statements)
  1. [注释 / Comments](#comments)
  1. [空格 / Whitespace](#whitespace)
  1. [逗号 / Commas](#commas)
  1. [分号 / Semicolons](#semicolons)
  1. [类型?转换 / Type Casting & Coercion](#type-casting--coercion)
  1. [命名规则 / Naming Conventions](#naming-conventions)
  1. [访问器函数 / Accessors](#accessors)
  1. [事件 / Events](#events)
  1. [jQuery](#jquery)
  1. [ES5 兼容性 / ECMAScript 5 Compatibility](#ecmascript-5-compatibility)
  1. [ES6+ (ES2015+) 风格 / ECMAScript 6+ (ES 2015+) Styles](#ecmascript-6-es-2015-styles)
  1. [标准库 / Standard Library](#standard-library)
  1. [测试 / Testing](#testing)
  1. [性能 / Performance](#performance)
  1. [资源 / Resources](#resources)
  1. [在野外？ / In the Wild](#in-the-wild)
  1. [翻译 / Translation](#translation)
  1. [JavaScript风格指南 / The JavaScript Style Guide Guide](#the-javascript-style-guide-guide)
  1. [Chat With Us About JavaScript](#chat-with-us-about-javascript)
  1. [Contributors](#contributors)
  1. [License](#license)
  1. [Amendments](#amendments)

## 类型 / Types

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) **基本类型**: 当你访问基本类型时，你将直接使用他们的值。  
    [1.1](#types--primitives) **Primitives**: When you access a primitive type you work directly on its value.
    
    - `string`
    - `number`
    - `boolean`
    - `null`
    - `undefined`
    - `symbol`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

    - Symbols 不能准确地被polyfill，所以在目标浏览器/环境原生不支持情况下，不应该被使用。
    - Symbols cannot be faithfully polyfilled, so they should not be used when targeting browsers/environments that don’t support them natively.

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **引用类型**: 当你访问一个引用类型时，你使用的是值引用。      
    [1.2](#types--complex)  **Complex**: When you access a complex type you work on a reference to its value.

    - `object`
    - `array`
    - `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ back to top](#table-of-contents)**

## 引用 / References

  <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) 所有引用对象使用`const`，禁止使用`var`。eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)
  - [2.1](#references--prefer-const) Use `const` for all of your references; avoid using `var`. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

    > Why? 这样确保你不会重复赋值给你的应用对象，否则将导致bug和难以理解的代码。
    > Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

    ```javascript
    // bad 不推荐
    var a = 1;
    var b = 2;

    // good 推荐
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) 如果一定要重复赋值，使用`let`代替`var`。eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)
  - [2.2](#references--disallow-var) If you must reassign references, use `let` instead of `var`. eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

    > Why? `let`是块作用域而不是函数作用域（比如`var`）。
    > Why? `let` is block-scoped rather than function-scoped like `var`.

    ```javascript
    // bad 不推荐
    var count = 1;
    if (true) {
      count += 1;
    }

    // good 推荐, use the let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) 注意`let`和`const`都是块级作用域。
  - [2.3](#references--block-scope) Note that both `let` and `const` are block-scoped.

    ```javascript
    // const 和 let 仅存在于他们定义的代码块中。
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

**[⬆ back to top](#table-of-contents)**

## 对象 / Objects

  <a name="objects--no-new"></a><a name="3.1"></a>
  - [3.1](#objects--no-new) 使用字面语法创建对象。 eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)
  - [3.1](#objects--no-new) Use the literal syntax for object creation. eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)

    ```javascript
    // bad 不推荐
    const item = new Object();

    // good 推荐
    const item = {};
    ```

  <a name="es6-computed-properties"></a><a name="3.4"></a>
  - [3.2](#es6-computed-properties) 使用计算属性命名来创建动态属性的对象。
  - [3.2](#es6-computed-properties) Use computed property names when creating objects with dynamic property names.

    > Why? 他们允许你在一个地方定义对象的所有属性。
    > Why? They allow you to define all the properties of an object in one place.

    ```javascript

    function getKey(k) {
      return `a key named ${k}`;
    }

    // bad 不推荐
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // good 推荐 😭😭😭
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand"></a><a name="3.5"></a>
  - [3.3](#es6-object-shorthand) 使用对象方法简写方式。 eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)
  - [3.3](#es6-object-shorthand) Use object method shorthand. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    ```javascript
    // bad 不推荐
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // good 推荐
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  <a name="es6-object-concise"></a><a name="3.6"></a>
  - [3.4](#es6-object-concise) 使用属性简写方式。 eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)
  - [3.4](#es6-object-concise) Use property value shorthand. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    > Why? It is shorter and descriptive.

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // bad 不推荐
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // good 推荐
    const obj = {
      lukeSkywalker,
    };
    ```

  <a name="objects--grouped-shorthand"></a><a name="3.7"></a>
  - [3.5](#objects--grouped-shorthand) 将简写属性放在对象声明的开始位置。
  - [3.5](#objects--grouped-shorthand) Group your shorthand properties at the beginning of your object declaration.

    > Why? I更容易表达哪个属性采用了简写方式。
    > Why? It’s easier to tell which properties are using the shorthand.

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // bad 不推荐
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // good 推荐
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

  <a name="objects--quoted-props"></a><a name="3.8"></a>
  - [3.6](#objects--quoted-props) 仅引用无效标识符的属性。eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props.html)
  - [3.6](#objects--quoted-props) Only quote properties that are invalid identifiers. eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props.html)

    > Why? 通常我们会考虑它主观上更容易阅读。它改进了语法突出显示，并且使得多的JS引擎更容易优化。
    > Why? In general we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.

    ```javascript
    // bad 不推荐
    const bad 不推荐 = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // good 推荐
    const good 推荐 = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };
    ```

  <a name="objects--prototype-builtins"></a>
  - [3.7](#objects--prototype-builtins) 不要直接使用`Object.prototype`方法,比如`hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)
  - [3.7](#objects--prototype-builtins) Do not call `Object.prototype` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)

    > Why? 这些方法可能通过对象属性被隐藏 in question - 考虑到 `{ hasOwnProperty: false }` - 或者, 对象可能是一个null(`Object.create(null)`).
    > Why? These methods may be shadowed by properties on the object in question - consider `{ hasOwnProperty: false }` - or, the object may be a null object (`Object.create(null)`).

    ```javascript
    // bad 不推荐
    console.log(object.hasOwnProperty(key));

    // good 推荐
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // best
    const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope. // 在模块范围内，缓存一个查找。
    console.log(has.call(object, key));
    /* or */
    import has from 'has'; // https://www.npmjs.com/package/has
    console.log(has(object, key));
    ```

  <a name="objects--rest-spread"></a>
  - [3.8](#objects--rest-spread) 首选对象展开运算符，而不是[`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 给浅拷贝对象. 使用对象的解构赋值运算来获取省略的新属性。
  - [3.8](#objects--rest-spread) Prefer the object spread operator over [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted.

    ```javascript
    // very bad 不推荐
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
    delete copy.a; // so does this

    // bad 不推荐
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // good 推荐
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    ```

**[⬆ back to top](#table-of-contents)**

## 数组 / Arrays

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals) 使用字面语法创建数组。eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)
  - [4.1](#arrays--literals) Use the literal syntax for array creation. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)

    ```javascript
    // bad 不推荐
    const items = new Array();

    // good 推荐
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push) 使用[Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) 代替直接给一个数组赋值。
  - [4.2](#arrays--push) Use [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) instead of direct assignment to add items to an array.

    ```javascript
    const someStack = [];

    // bad 不推荐
    someStack[someStack.length] = 'abracadabra';

    // good 推荐
    someStack.push('abracadabra');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) 使用数组的扩展`...`来拷贝数组。
  - [4.3](#es6-array-spreads) Use array spreads `...` to copy arrays.

    ```javascript
    // bad 不推荐
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // good 推荐
    const itemsCopy = [...items];
    ```

  <a name="arrays--from"></a>
  <a name="arrays--from-iterable"></a><a name="4.4"></a>
  - [4.4](#arrays--from-iterable) 将可遍历对象转换为数组,使用扩展运算`...` 代替[`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from).
  - [4.4](#arrays--from-iterable) To convert an iterable object to an array, use spreads `...` instead of [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from).

    ```javascript
    const foo = document.querySelectorAll('.foo');

    // good 推荐
    const nodes = Array.from(foo);

    // best
    const nodes = [...foo];
    ```

  <a name="arrays--from-array-like"></a>
  - [4.5](#arrays--from-array-like) 类数组对象转换成数组，使用[`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)。
  - [4.5](#arrays--from-array-like) Use [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) for converting an array-like object to an array.

    ```javascript
    const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

    // bad 不推荐
    const arr = Array.prototype.slice.call(arrLike);

    // good 推荐
    const arr = Array.from(arrLike);
    ```

  <a name="arrays--mapping"></a>
  - [4.6](#arrays--mapping) 使用[`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) 代替扩展运算`...`来map迭代,因为它避免了创建中间数组。
  - [4.6](#arrays--mapping) Use [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) instead of spread `...` for mapping over iterables, because it avoids creating an intermediate array.

    ```javascript
    // bad 不推荐
    const baz = [...foo].map(bar);

    // good 推荐
    const baz = Array.from(foo, bar);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.7](#arrays--callback-return) 在数组方法回调中使用返回语句。如果函数体包含一个返回没有副作用的表达式的语句，则可以忽略返回,following [8.2](#arrows--implicit-return). eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)
  - [4.7](#arrays--callback-return) Use return statements in array method callbacks. It’s ok to omit the return if the function body consists of a single statement returning an expression without side effects, following [8.2](#arrows--implicit-return). eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

    ```javascript
    // good 推荐
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // good 推荐
    [1, 2, 3].map((x) => x + 1);

    // bad 不推荐 - no returned value means `acc` becomes undefined after the first iteration
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
    });

    // good 推荐
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      return flatten;
    });

    // bad 不推荐
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // good 推荐
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

  <a name="arrays--bracket-newline"></a>
  - [4.8](#arrays--bracket-newline) 如果数组有多行，则在打开后和关闭数组括号之前使用换行符。
  - [4.8](#arrays--bracket-newline) Use line breaks after open and before close array brackets if an array has multiple lines

    ```javascript
    // bad 不推荐
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];

    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];

    const numberInArray = [
      1, 2,
    ];

    // good 推荐
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];

    const numberInArray = [
      1,
      2,
    ];
    ```

**[⬆ back to top](#table-of-contents)**

## 解构 / Destructuring

  <a name="destructuring--object"></a><a name="5.1"></a>
  - [5.1](#destructuring--object) 访问和使用对象的多个属性时，使用对象结构语法。eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)
  - [5.1](#destructuring--object) Use object destructuring when accessing and using multiple properties of an object. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > Why? 解构会保存您为这些属性创建的临时引用。
    > Why? Destructuring saves you from creating temporary references for those properties.

    ```javascript
    // bad 不推荐
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // good 推荐
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // best
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

  <a name="destructuring--array"></a><a name="5.2"></a>
  - [5.2](#destructuring--array) 使用数组解构。 eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)
  - [5.2](#destructuring--array) Use array destructuring. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // bad 不推荐
    const first = arr[0];
    const second = arr[1];

    // good 推荐
    const [first, second] = arr;
    ```

  <a name="destructuring--object-over-array"></a><a name="5.3"></a>
  - [5.3](#destructuring--object-over-array) 对于多返回值，使用对象解构，而不是数组解构。
  - [5.3](#destructuring--object-over-array) Use object destructuring for multiple return values, not array destructuring.

    > Why? 随着时间推移，你可以添加新属性/或更改顺序，而不破坏站点调用。
    > Why? You can add new properties over time or change the order of things without breaking call sites.

    ```javascript
    // bad 不推荐
    function processInput(input) {
      // then a miracle occurs
      return [left, right, top, bottom];
    }

    // the caller needs to think about the order of return data
    // 调用方需要考虑返回数据的顺序
    const [left, __, top] = processInput(input);

    // good 推荐
    function processInput(input) {
      // then a miracle occurs
      return { left, right, top, bottom };
    }

    // the caller selects only the data they need
    const { left, top } = processInput(input);
    ```

**[⬆ back to top](#table-of-contents)**

## 字符串 / Strings

  <a name="strings--quotes"></a><a name="6.1"></a>
  - [6.1](#strings--quotes) 字符串使用 `''`。eslint: [`quotes`](https://eslint.org/docs/rules/quotes.html)
  - [6.1](#strings--quotes) Use single quotes `''` for strings. eslint: [`quotes`](https://eslint.org/docs/rules/quotes.html)

    ```javascript
    // bad 不推荐
    const name = "Capt. Janeway";

    // bad 不推荐 - template literals should contain interpolation or newlines
    // 模板字符串应该包含插值/或换行。
    const name = `Capt. Janeway`;

    // good 推荐
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length"></a><a name="6.2"></a>
  - [6.2](#strings--line-length) 行字符超过100个的字符串不应该使用字符串串联跨多行书写。
  - [6.2](#strings--line-length) Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.

    > Why? 破碎的字符串很难使用，并且使用代码的可搜索性降低。
    > Why? Broken strings are painful to work with and make code less searchable.

    ```javascript
    // bad 不推荐
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // bad 不推荐
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // good 推荐
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  - [6.3](#es6-template-literals) 以编程方式构建字符串时，请使用字符串模板而不是串联。eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)
  - [6.3](#es6-template-literals) When programmatically building up strings, use template strings instead of concatenation. eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

    > Why? 模板字符串提供了可读、简洁的语法，并具有正确的行和字符串插值功能。
    > Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

    ```javascript
    // bad 不推荐
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // bad 不推荐
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // bad 不推荐
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // good 推荐
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval"></a><a name="6.5"></a>
  - [6.4](#strings--eval) 不要在字符串上使用`eval()`，他会有太多漏洞。eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)
  - [6.4](#strings--eval) Never use `eval()` on a string, it opens too many vulnerabilities. eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)

  <a name="strings--escaping"></a>
  - [6.5](#strings--escaping) 不要不必要的转义字符。 eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)
  - [6.5](#strings--escaping) Do not unnecessarily escape characters in strings. eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

    > Why? 反斜杠降低可读性，因此仅在必要时使用。
    > Why? Backslashes harm readability, thus they should only be present when necessary.

    ```javascript
    // bad 不推荐
    const foo = '\'this\' \i\s \"quoted\"';

    // good 推荐
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

**[⬆ back to top](#table-of-contents)**

## 方法 / Functions

  <a name="functions--declarations"></a><a name="7.1"></a>
  - [7.1](#functions--declarations) 使用命名函数表达式，而不是函数声明。eslint: [`func-style`](https://eslint.org/docs/rules/func-style)
  - [7.1](#functions--declarations) Use named function expressions instead of function declarations. eslint: [`func-style`](https://eslint.org/docs/rules/func-style)

    > Why? 函数声明被提升，这意味着在文件中定义函数之前引用函数很容易-太容易了。这有损可读性和可维护性。如果发现函数的定义足够大/或足够复杂，以至于干扰了对文件其余部分的理解，那么也许是时候将其提取到自己的模块了。不要忘记显式命名表达式，无论是否从包含变量推断出该名称（这在现代浏览器中通常是这样，或者当使用编译器（如Babel）时）。这消除了对错误调用堆栈所做的任何假设。 ([Discussion](https://github.com/airbnb/javascript/issues/794))
    > Why? Function declarations are hoisted, which means that it’s easy - too easy - to reference the function before it is defined in the file. This harms readability and maintainability. If you find that a function’s definition is large or complex enough that it is interfering with understanding the rest of the file, then perhaps it’s time to extract it to its own module! Don’t forget to explicitly name the expression, regardless of whether or not the name is inferred from the containing variable (which is often the case in modern browsers or when using compilers such as Babel). This eliminates any assumptions made about the Error’s call stack. ([Discussion](https://github.com/airbnb/javascript/issues/794))

    ```javascript
    // bad 不推荐
    function foo() {
      // ...
    }

    // bad 不推荐
    const foo = function () {
      // ...
    };

    // good 推荐
    // lexical name distinguished from the variable-referenced invocation(s)
    // 与变量引用调用区别开来的词法名称。
    const short = function longUniqueMoreDescriptiveLexicalFoo() {
      // ...
    };
    ```

  <a name="functions--iife"></a><a name="7.2"></a>
  - [7.2](#functions--iife) 在括号中调用立即函数表达式。eslint: [`wrap-iife`](https://eslint.org/docs/rules/wrap-iife.html)
  - [7.2](#functions--iife) Wrap immediately invoked function expressions in parentheses. eslint: [`wrap-iife`](https://eslint.org/docs/rules/wrap-iife.html)

    > Why? 立即函数表达式是一个单体-包装他，请注意，在一个模块无处不在的世界，您几乎不需要IIFE。
    > Why? An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.

    ```javascript
    // immediately-invoked function expression (IIFE)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  - [7.3](#functions--in-blocks) 切勿在非函数快中声明函数（`if`,`while`等）。而是将函数分配给变量。浏览器将允许您这样做，但是他们都以不同的方式解释他，这是坏消息。eslint: [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func.html)
  - [7.3](#functions--in-blocks) Never declare a function in a non-function block (`if`, `while`, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad 不推荐 news bears. eslint: [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func.html)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) **Note:** ECMA-262 将`block`定义为语句列表。函数声明不是语句。
  - [7.4](#functions--note-on-blocks) **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement.

    ```javascript
    // bad 不推荐
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good 推荐
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow"></a><a name="7.5"></a>
  - [7.5](#functions--arguments-shadow) 永远不要将参数命名为`arguments`。这将优先于每个函数作用域内的自有`arguments`对象。
  - [7.5](#functions--arguments-shadow) Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    // bad 不推荐
    function foo(name, options, arguments) {
      // ...
    }

    // good 推荐
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - [7.6](#es6-rest) 永远不要使用`arguments`参数来代替对象解构语法 `...`。eslint: [`prefer-rest-params`](https://eslint.org/docs/rules/prefer-rest-params)

    > Why? `...` 是明确又换要提取的参数。此外，剩余参数是一个真正的数组，而不仅仅是类数组对象。
    > Why? `...` is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like `arguments`.

    ```javascript
    // bad 不推荐
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // good 推荐
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) 使用默认参数语法。
  - [7.7](#es6-default-parameters) Use default parameter syntax rather than mutating function arguments.

    ```javascript
    // really bad 不推荐
    function handleThings(opts) {
      // No! We shouldn’t mutate function arguments.
      // Double bad 不推荐: if opts is falsy it'll be set to an object which may
      // be what you want but it can introduce subtle bugs.
      opts = opts || {};
      // ...
    }

    // still bad 不推荐
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // good 推荐
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) 避免使用默认参数的副作用。
  - [7.8](#functions--default-side-effects) Avoid side effects with default parameters.

    > Why? 他们混淆了推理。
    > Why? They are confusing to reason about.

    ```javascript
    var b = 1;
    // bad 不推荐
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  - [7.9](#functions--defaults-last) 始终将默认参数放到最后。
  - [7.9](#functions--defaults-last) Always put default parameters last.

    ```javascript
    // bad 不推荐
    function handleThings(opts = {}, name) {
      // ...
    }

    // good 推荐
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) 永远不要使用Function构造函数创一个新函数。eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)
  - [7.10](#functions--constructor) Never use the Function constructor to create a new function. eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

    > Why? 这种方式创建一个函数相当于字符串的`eval()`，会打开漏洞。
    > Why? Creating a function in this way evaluates a string similarly to `eval()`, which opens vulnerabilities.

    ```javascript
    // bad 不推荐
    var add = new Function('a', 'b', 'return a + b');

    // still bad 不推荐
    var subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) 保持函数签名间隔。eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)
  - [7.11](#functions--signature-spacing) Spacing in a function signature. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    > Why? 一致性是好的，在添加/或删除名称时，您不必添加/或删除空格。
    > Why? Consistency is good 推荐, and you shouldn’t have to add or remove a space when adding or removing a name.

    ```javascript
    // bad 不推荐
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // good 推荐
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) 永远不要转变参数。 eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)
  - [7.12](#functions--mutate-params) Never mutate parameters. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.
    > Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

    ```javascript
    // bad 不推荐
    function f1(obj) {
      obj.key = 1;
    }

    // good 推荐
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) 永不给参数赋值。 eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)
  - [7.13](#functions--reassign-params) Never reassign parameters. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

    ```javascript
    // bad 不推荐
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // good 推荐
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) 首选使用扩展运算符`...`来调用可变方法。eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)
  - [7.14](#functions--spread-vs-apply) Prefer the use of the spread operator `...` to call variadic functions. eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

    > Why? 这样更清晰，你不需要提供上下文，并且你不能轻易的将`new`与`apply`组合。
    > Why? It’s cleaner, you don’t need to supply a context, and you can not easily compose `new` with `apply`.

    ```javascript
    // bad 不推荐
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // good 推荐
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // bad 不推荐
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // good 推荐
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) 具有多行签名或调用的函数应缩进，就像本指南种所有其他多行列表一样：每个项都位于一行上，最后一个项上带有尾随逗号。 eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)
  - [7.15](#functions--signature-invocation-indentation) Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item. eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

    ```javascript
    // bad 不推荐
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // good 推荐
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // bad 不推荐
    console.log(foo,
      bar,
      baz);

    // good 推荐
    console.log(
      foo,
      bar,
      baz,
    );
    ```

**[⬆ back to top](#table-of-contents)**

## 箭头函数 / Arrow Functions

  <a name="arrows--use-them"></a><a name="8.1"></a>
  - [8.1](#arrows--use-them) 当必须使用匿名函数时（如传递内联回调函数），请使用箭头函数表示法。 eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing.html)
  - [8.1](#arrows--use-them) When you must use an anonymous function (as when passing an inline callback), use arrow function notation. eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing.html)

    > Why? 它会保留当前的上下文，这通常是你想要的，是一个更简洁的语法。
    > Why? It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

    > Why not? 如果你有一个相当复杂的函数，则可以将该逻辑移到其自己的命名函数表达式中。
    > Why not? If you have a fairly complicated function, you might move that logic out into its own named function expression.

    ```javascript
    // bad 不推荐
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // good 推荐
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return"></a><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) If the function body consists of a single statement returning an [expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) without side effects, omit the braces and use the implicit return. Otherwise, keep the braces and use a `return` statement. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](https://eslint.org/docs/rules/arrow-body-style.html)

    > Why? Syntactic sugar. It reads well when multiple functions are chained together.

    ```javascript
    // bad 不推荐
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // good 推荐
    [1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

    // good 推荐
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // good 推荐
    [1, 2, 3].map((number, index) => ({
      [index]: number,
    }));

    // No implicit return with side effects
    function foo(callback) {
      const val = callback();
      if (val === true) {
        // Do something if callback returns true
      }
    }

    let bool = false;

    // bad 不推荐
    foo(() => bool = true);

    // good 推荐
    foo(() => {
      bool = true;
    });
    ```

  <a name="arrows--paren-wrap"></a><a name="8.3"></a>
  - [8.3](#arrows--paren-wrap) In case the expression spans over multiple lines, wrap it in parentheses for better readability.

    > Why? It shows clearly where the function starts and ends.

    ```javascript
    // bad 不推荐
    ['get', 'post', 'put'].map((httpMethod) => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    );

    // good 推荐
    ['get', 'post', 'put'].map((httpMethod) => (
      Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    ));
    ```

  <a name="arrows--one-arg-parens"></a><a name="8.4"></a>
  - [8.4](#arrows--one-arg-parens) Always include parentheses around arguments for clarity and consistency. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html)

    > Why? Minimizes diff churn when adding or removing arguments.

    ```javascript
    // bad 不推荐
    [1, 2, 3].map(x => x * x);

    // good 推荐
    [1, 2, 3].map((x) => x * x);

    // bad 不推荐
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // good 推荐
    [1, 2, 3].map((number) => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // bad 不推荐
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // good 推荐
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing"></a><a name="8.5"></a>
  - [8.5](#arrows--confusing) Avoid confusing arrow function syntax (`=>`) with comparison operators (`<=`, `>=`). eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

    ```javascript
    // bad 不推荐
    const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

    // bad 不推荐
    const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

    // good 推荐
    const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

    // good 推荐
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height <= 256 ? largeSize : smallSize;
    };
    ```

  <a name="whitespace--implicit-arrow-linebreak"></a>
  - [8.6](#whitespace--implicit-arrow-linebreak) Enforce the location of arrow function bodies with implicit returns. eslint: [`implicit-arrow-linebreak`](https://eslint.org/docs/rules/implicit-arrow-linebreak)

    ```javascript
    // bad 不推荐
    (foo) =>
      bar;

    (foo) =>
      (bar);

    // good 推荐
    (foo) => bar;
    (foo) => (bar);
    (foo) => (
       bar
    )
    ```

**[⬆ back to top](#table-of-contents)**

## 类&构造函数 / Classes & Constructors

  <a name="constructors--use-class"></a><a name="9.1"></a>
  - [9.1](#constructors--use-class) Always use `class`. Avoid manipulating `prototype` directly.

    > Why? `class` syntax is more concise and easier to reason about.

    ```javascript
    // bad 不推荐
    function Queue(contents = []) {
      this.queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    };

    // good 推荐
    class Queue {
      constructor(contents = []) {
        this.queue = [...contents];
      }
      pop() {
        const value = this.queue[0];
        this.queue.splice(0, 1);
        return value;
      }
    }
    ```

  <a name="constructors--extends"></a><a name="9.2"></a>
  - [9.2](#constructors--extends) Use `extends` for inheritance.

    > Why? It is a built-in way to inherit prototype functionality without breaking `instanceof`.

    ```javascript
    // bad 不推荐
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this.queue[0];
    };

    // good 推荐
    class PeekableQueue extends Queue {
      peek() {
        return this.queue[0];
      }
    }
    ```

  <a name="constructors--chaining"></a><a name="9.3"></a>
  - [9.3](#constructors--chaining) Methods can return `this` to help with method chaining.

    ```javascript
    // bad 不推荐
    Jedi.prototype.jump = function () {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function (height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // good 推荐
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```

  <a name="constructors--tostring"></a><a name="9.4"></a>
  - [9.4](#constructors--tostring) It’s okay to write a custom `toString()` method, just make sure it works successfully and causes no side effects.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return `Jedi - ${this.getName()}`;
      }
    }
    ```

  <a name="constructors--no-useless"></a><a name="9.5"></a>
  - [9.5](#constructors--no-useless) Classes have a default constructor if one is not specified. An empty constructor function or one that just delegates to a parent class is unnecessary. eslint: [`no-useless-constructor`](https://eslint.org/docs/rules/no-useless-constructor)

    ```javascript
    // bad 不推荐
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    // bad 不推荐
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }

    // good 推荐
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
        this.name = 'Rey';
      }
    }
    ```

  <a name="classes--no-duplicate-members"></a>
  - [9.6](#classes--no-duplicate-members) Avoid duplicate class members. eslint: [`no-dupe-class-members`](https://eslint.org/docs/rules/no-dupe-class-members)

    > Why? Duplicate class member declarations will silently prefer the last one - having duplicates is almost certainly a bug.

    ```javascript
    // bad 不推荐
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // good 推荐
    class Foo {
      bar() { return 1; }
    }

    // good 推荐
    class Foo {
      bar() { return 2; }
    }
    ```

**[⬆ back to top](#table-of-contents)**

## 模块 / Modules

  <a name="modules--use-them"></a><a name="10.1"></a>
  - [10.1](#modules--use-them) 在一个非标准模块系统中，要使用模块 (`import`/`export`)。也可以用到你倾向的模块系统中。
    [10.1](#modules--use-them) Always use modules (`import`/`export`) over a non-standard module system. You can always transpile to your preferred module system.

    > Why? 模块是今后必需品，让我们现在开始使用
    > Why? Modules are the future, let’s start using the future now.

    ```javascript
    // bad 不推荐 
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // ok 推荐
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // best 极力推荐
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-wildcard"></a><a name="10.2"></a>
  - [10.2](#modules--no-wildcard) 不用使用import通配符。
  - [10.2](#modules--no-wildcard) Do not use wildcard imports.

    > Why? 这样能确保你有单一的默认export
    > Why? This makes sure you have a single default export.

    ```javascript
    // bad 不推荐 
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // good 推荐
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import"></a><a name="10.3"></a>
  - [10.3](#modules--no-export-from-import) 并且不用直接将import的项export。
  - [10.3](#modules--no-export-from-import) And do not export directly from an import.

    > Why? 尽管简短写法是推荐的，但使用一个清晰的方式来import和export，可以确保代码一致性。
    > Why? Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.

    ```javascript
    // bad 不推荐 
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // good 推荐
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  - [10.4](#modules--no-duplicate-imports) 同一路径的import仅出现一次。
  - [10.4](#modules--no-duplicate-imports) Only import from a path in one place.
 eslint: [`no-duplicate-imports`](https://eslint.org/docs/rules/no-duplicate-imports)

    > Why? 同一路径多行import，会导致代码难维护。
    > Why? Having multiple lines that import from the same path can make code harder to maintain.

    ```javascript
    // bad 不推荐 
    import foo from 'foo';
    // … some other imports … //
    import { named1, named2 } from 'foo';

    // good 推荐
    import foo, { named1, named2 } from 'foo';

    // good 推荐
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  <a name="modules--no-mutable-exports"></a>
  - [10.5](#modules--no-mutable-exports) 不要export可变绑定。
  - [10.5](#modules--no-mutable-exports) Do not export mutable bindings.
 eslint: [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)
    
    > Why? 一般情况下，应该避免Mutation，特出情况除外（当export可变绑定时）。可变绑定需要在特殊场景支持，通常仅export 常量。
    > Why? Mutation should be avoided in general, but in particular when exporting mutable bindings. While this technique may be needed for some special cases, in general, only constant references should be exported.

    ```javascript
    // bad 不推荐 
    let foo = 3;
    export { foo };

    // good 推荐
    const foo = 3;
    export { foo };
    ```

  <a name="modules--prefer-default-export"></a>
  - [10.6](#modules--prefer-default-export) 在仅export单个时，使用default导出比named导出要好。
  - [10.6](#modules--prefer-default-export) In modules with a single export, prefer default export over named export.
 eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)
    
    > Why? 鼓励采用多文件（一个文件仅一个export）方式，有利于可读性、可维护性。
    > Why? To encourage more files that only ever export one thing, which is better for readability and maintainability.

    ```javascript
    // bad 不推荐 
    export function foo() {}

    // good 推荐
    export default function foo() {}
    ```

  <a name="modules--imports-first"></a>
  - [10.7](#modules--imports-first) 将所有的`import`放在非`import`语句上。
  - [10.7](#modules--imports-first) Put all `import`s above non-import statements.
 eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)
    
    > Why? 将`import`放在顶部后，保持他们在顶部可以防止令人惊讶的行为发生。
    > Why? Since `import`s are hoisted, keeping them all at the top prevents surprising behavior.

    ```javascript
    // bad 不推荐 
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // good 推荐
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```

  <a name="modules--multiline-imports-over-newlines"></a>
  - [10.8](#modules--multiline-imports-over-newlines) 多行import应该缩进，就像多行字面的数组和对象。
  - [10.8](#modules--multiline-imports-over-newlines) Multiline imports should be indented just like multiline array and object literals.

    > Why? 大括号遵循与风格指南种所有其他大括号块相同的缩进规则，尾随逗号也是如此。
    > Why? The curly braces follow the same indentation rules as every other curly brace block in the style guide, as do the trailing commas.

    ```javascript
    // bad 不推荐 
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // good 推荐
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```

  <a name="modules--no-webpack-loader-syntax"></a>
  - [10.9](#modules--no-webpack-loader-syntax) 在模块引入语法中，禁止使用webpack loader语法。
  - [10.9](#modules--no-webpack-loader-syntax) Disallow Webpack loader syntax in module import statements.
 eslint: [`import/no-webpack-loader-syntax`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-webpack-loader-syntax.md)

    > Why? 由于在导入中使用了webpack语法，将代码耦合到模块。推荐在`webpack.configi.js`使用loader语法。 
    > Why? Since using Webpack syntax in the imports couples the code to a module bundler. Prefer using the loader syntax in `webpack.config.js`.
    

    ```javascript
    // bad 不推荐 
    import fooSass from 'css!sass!foo.scss';
    import barCss from 'style!css!bar.css';

    // good 推荐
    import fooSass from 'foo.scss';
    import barCss from 'bar.css';
    ```

**[⬆ back to top](#table-of-contents)**

## 迭代器 和 Generator / Iterators and Generators

  <a name="iterators--nope"></a><a name="11.1"></a> 
  - [11.1](#iterators--nope) 不要使用迭代器。优先使用高阶方法来代替`for-in` or `for-of`。eslint: [`no-iterator`](https://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](https://eslint.org/docs/rules/no-restricted-syntax)
  - [11.1](#iterators--nope) Don’t use iterators. Prefer JavaScript’s higher-order functions instead of loops like `for-in` or `for-of`. eslint: [`no-iterator`](https://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](https://eslint.org/docs/rules/no-restricted-syntax)

    > Why? 这将强制我们使用不变的规则。处理返回值的纯函数比其副作用更容易推理。
    > Why? This enforces our immutable rule. Dealing with pure functions that return values is easier to reason about than side effects.

    > 使用 `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... 来遍历数组，使用`Object.keys()` / `Object.values()` / `Object.entries()` 生产数组，以便遍历对象。
    > Use `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... to iterate over arrays, and `Object.keys()` / `Object.values()` / `Object.entries()` to produce arrays so you can iterate over objects.

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // bad 不推荐 
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;

    // good 推荐
    let sum = 0;
    numbers.forEach((num) => {
      sum += num;
    });
    sum === 15;

    // best (use the functional force)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;

    // bad 不推荐 
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }

    // good 推荐
    const increasedByOne = [];
    numbers.forEach((num) => {
      increasedByOne.push(num + 1);
    });

    // best (keeping it functional)
    const increasedByOne = numbers.map((num) => num + 1);
    ```

  <a name="generators--nope"></a><a name="11.2"></a>
  - [11.2](#generators--nope) 现在不要使用generator。
  - [11.2](#generators--nope) Don’t use generators for now.

    > Why? 他们不能更好的转换为ES5。
    > Why? They don’t transpile well to ES5.

  <a name="generators--spacing"></a>
  - [11.3](#generators--spacing) 如果一定要使用generator，或者忽略[我们的建议](#generators--nope), 请确保他们的函数签名要保持适当间隔。eslint: [`generator-star-spacing`](https://eslint.org/docs/rules/generator-star-spacing)
  - [11.3](#generators--spacing) If you must use generators, or if you disregard [our advice](#generators--nope), make sure their function signature is spaced properly. eslint: [`generator-star-spacing`](https://eslint.org/docs/rules/generator-star-spacing)

    > Why? `function` 和 `*` 是相同的概念关键字的一部分 - `*` 不是`function`的修饰符, `function*` 是唯一的构造函数，与`function`不同。
    > Why? `function` and `*` are part of the same conceptual keyword - `*` is not a modifier for `function`, `function*` is a unique construct, different from `function`.

    ```javascript
    // bad 不推荐 
    function * foo() {
      // ...
    }

    // bad 不推荐 
    const bar = function * () {
      // ...
    };

    // bad 不推荐 
    const baz = function *() {
      // ...
    };

    // bad 不推荐 
    const quux = function*() {
      // ...
    };

    // bad 不推荐 
    function*foo() {
      // ...
    }

    // bad 不推荐 
    function *foo() {
      // ...
    }

    // very bad 不推荐 
    function
    *
    foo() {
      // ...
    }

    // very bad 不推荐 
    const wat = function
    *
    () {
      // ...
    };

    // good 推荐
    function* foo() {
      // ...
    }

    // good 推荐
    const foo = function* () {
      // ...
    };
    ```

**[⬆ back to top](#table-of-contents)**

## 属性 / Properties

  <a name="properties--dot"></a><a name="12.1"></a>
  - [12.1](#properties--dot) 使用点语法访问属性。eslint: [`dot-notation`](https://eslint.org/docs/rules/dot-notation.html)
  - [12.1](#properties--dot) Use dot notation when accessing properties. eslint: [`dot-notation`](https://eslint.org/docs/rules/dot-notation.html)

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // bad 不推荐 
    const isJedi = luke['jedi'];

    // good 推荐
    const isJedi = luke.jedi;
    ```

  <a name="properties--bracket"></a><a name="12.2"></a>
  - [12.2](#properties--bracket) 使用变量访问属性时，请使用中括号 `[]` 语法。
  - [12.2](#properties--bracket) Use bracket notation `[]` when accessing properties with a variable.

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```
  <a name="es2016-properties--exponentiation-operator"></a>
  - [12.3](#es2016-properties--exponentiation-operator) 运算指数时，请使用指数运算符 `**` 。eslint: [`no-restricted-properties`](https://eslint.org/docs/rules/no-restricted-properties).
  - [12.3](#es2016-properties--exponentiation-operator) Use exponentiation operator `**` when calculating exponentiations. eslint: [`no-restricted-properties`](https://eslint.org/docs/rules/no-restricted-properties).

    ```javascript
    // bad 不推荐 
    const binary = Math.pow(2, 10);

    // good 推荐
    const binary = 2 ** 10;
    ```

**[⬆ back to top](#table-of-contents)**

## 变量 / Variables

  <a name="variables--const"></a><a name="13.1"></a>
  - [13.1](#variables--const) 始终使用 `const` or `let` 来声明变量。不要对全局变量这样做。我们希望避免污染全局命名空间。...地球超人警告我们注意它们。eslint: [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)
  - [13.1](#variables--const) Always use `const` or `let` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that. eslint: [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)

    ```javascript
    // bad 不推荐 
    superPower = new SuperPower();

    // good 推荐
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  - [13.2](#variables--one-const) 使用一个`const` or `let` 来声明每一个变量/或任务。eslint: [`one-var`](https://eslint.org/docs/rules/one-var.html)
  - [13.2](#variables--one-const) Use one `const` or `let` declaration per variable or assignment. eslint: [`one-var`](https://eslint.org/docs/rules/one-var.html)

    > Why? 这种方式更容易添加一个新的变量声明，并且你永远不会担心将 `;` 敲成 `,` 或者引入唯一标点的差异。你也可以对每个变量进行调试，避免一次性跳过他们。
    > Why? It’s easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs. You can also step through each declaration with the debugger, instead of jumping through all of them at once.

    ```javascript
    // bad 不推荐 
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // bad 不推荐 
    // (compare to above, and try to spot the mistake)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // good 推荐
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group"></a><a name="13.3"></a>
  - [13.3](#variables--const-let-group) 先将 `const` 组织到一起，然后再将`let`组织到一起。
  - [13.3](#variables--const-let-group) Group all your `const`s and then group all your `let`s.

    > Why? 对于以后你可能将赋值之前声明的那些变量，有帮助。
    > Why? This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

    ```javascript
    // bad 不推荐 
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad 不推荐 
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // good 推荐
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used"></a><a name="13.4"></a>
  - [13.4](#variables--define-where-used) 将变量赋值到需要的地方，但请放在合理的位置😀。
  - [13.4](#variables--define-where-used) Assign variables where you need them, but place them in a reasonable place.

    > Why? `let` and `const` 是块作用域，而不是函数作用域。
    > Why? `let` and `const` are block scoped and not function scoped.

    ```javascript
    // bad 不推荐  - unnecessary function call
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // good 推荐
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```
  <a name="variables--no-chain-assignment"></a><a name="13.5"></a>
  - [13.5](#variables--no-chain-assignment) 不要连接变量赋值。eslint: [`no-multi-assign`](https://eslint.org/docs/rules/no-multi-assign)
  - [13.5](#variables--no-chain-assignment) Don’t chain variable assignments. eslint: [`no-multi-assign`](https://eslint.org/docs/rules/no-multi-assign)

    > Why? 链接变量赋值会创建隐式全局变量。
    > Why? Chaining variable assignments creates implicit global variables.

    ```javascript
    // bad 不推荐 
    (function example() {
      // JavaScript interprets this as
      // let a = ( b = ( c = 1 ) );
      // The let keyword only applies to variable a; variables b and c become
      // global variables.
      let a = b = c = 1;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // 1
    console.log(c); // 1

    // good 推荐
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // throws ReferenceError
    console.log(c); // throws ReferenceError

    // the same applies for `const`
    ```

  <a name="variables--unary-increment-decrement"></a><a name="13.6"></a>
  - [13.6](#variables--unary-increment-decrement) 避免使用一元递增和递减语法 (`++`, `--`). eslint [`no-plusplus`](https://eslint.org/docs/rules/no-plusplus)
  - [13.6](#variables--unary-increment-decrement) Avoid using unary increments and decrements (`++`, `--`). eslint [`no-plusplus`](https://eslint.org/docs/rules/no-plusplus)

    > Why? 根据eslint文档, 一元递增和递减语句受到自动分号插入的约束，并可能导致程序中值增加或递减的无声错误。用`num += 1`而不是`num++`/或`num ++`语句来改变值也更具表现力。禁用一元递增和递减语句也能防止无意识中预增量/或预递减值，这也能程序中出现意外行为。
    > Why? Per the eslint documentation, unary increment and decrement statements are subject to automatic semicolon insertion and can cause silent errors with incrementing or decrementing values within an application. It is also more expressive to mutate your values with statements like `num += 1` instead of `num++` or `num ++`. Disallowing unary increment and decrement statements also prevents you from pre-incrementing/pre-decrementing values unintentionally which can also cause unexpected behavior in your programs.

    ```javascript
    // bad 不推荐 

    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }

    // good 推荐

    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

<a name="variables--linebreak"></a>
  - [13.7](#variables--linebreak) Avoid linebreaks before or after `=` in an assignment. If your assignment violates [`max-len`](https://eslint.org/docs/rules/max-len.html), surround the value in parens. eslint [`operator-linebreak`](https://eslint.org/docs/rules/operator-linebreak.html).

    > Why? Linebreaks surrounding `=` can obfuscate the value of an assignment.

    ```javascript
    // bad 不推荐 
    const foo =
      superLongLongLongLongLongLongLongLongFunctionName();

    // bad 不推荐 
    const foo
      = 'superLongLongLongLongLongLongLongLongString';

    // good 推荐
    const foo = (
      superLongLongLongLongLongLongLongLongFunctionName()
    );

    // good 推荐
    const foo = 'superLongLongLongLongLongLongLongLongString';
    ```

<a name="variables--no-unused-vars"></a>
  - [13.8](#variables--no-unused-vars) 禁止使用的变量. eslint: [`no-unused-vars`](https://eslint.org/docs/rules/no-unused-vars)
  - [13.8](#variables--no-unused-vars) Disallow unused variables. eslint: [`no-unused-vars`](https://eslint.org/docs/rules/no-unused-vars)

    > Why? 由于重构不完整，在代码任何位置，声明且未使用的变量很可能是错误。这些变量占用了代码空间，并可能导致读者的混淆。
    > Why? Variables that are declared and not used anywhere in the code are most likely an error due to incomplete refactoring. Such variables take up space in the code and can lead to confusion by readers.

    ```javascript
    // bad 不推荐 

    var some_unused_var = 42;

    // 只写变量不被使用
    // Write-only variables are not considered as used.
    var y = 10;
    y = 5;

    // 修改自身的读取不被视为已使用
    // A read for a modification of itself is not considered as used.
    var z = 0;
    z = z + 1;

    // 未使用的方法参数
    // Unused function arguments.
    function getX(x, y) {
        return x;
    }

    // good 推荐

    function getXPlusY(x, y) {
      return x + y;
    }

    var x = 1;
    var y = a + 2;

    alert(getXPlusY(x, y));

    // 及时未使用'type'也会被忽略，因为它具有一个同级的休息属性。
    // 'type' is ignored even if unused because it has a rest property sibling.
    // 这是提取胜率指定键的对象的一种形式。
    // This is a form of extracting an object that omits the specified keys.
    var { type, ...coords } = data;
    // ‘coords’ 就是没有'type'属性的“数据”对象。
    // 'coords' is now the 'data' object without its 'type' property.
    ```

**[⬆ back to top](#table-of-contents)**

## 提升 / Hoisting

  <a name="hoisting--about"></a><a name="14.1"></a>
  - [14.1](#hoisting--about) `var` 声明被提升到其最接近的封闭函数的顶部，但他们的赋值不会。`const` and `let` 声明有一个新概念，叫做[暂时性死区 (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone). 有必要知晓为什么 [typeof 已经不再安全](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).
  - [14.1](#hoisting--about) `var` declarations get hoisted to the top of their closest enclosing function scope, their assignment does not. `const` and `let` declarations are blessed with a new concept called [Temporal Dead Zones (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone). It’s important to know why [typeof is no longer safe](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).

    ```javascript
    // 我们知道它不会生效（假设没有未定义的全局变量）
    // we know this wouldn’t work (assuming there
    // is no notDefined global variable)
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    // 由于变量提升，你可以在使用变量后再声明它。
    // 注意：‘true’的赋值不会提升。
    // creating a variable declaration after you
    // reference the variable will work due to
    // variable hoisting. Note: the assignment
    // value of `true` is not hoisted.
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // the interpreter is hoisting the variable
    // declaration to the top of the scope,
    // which means our example could be rewritten as:
    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // using const and let
    function example() {
      console.log(declaredButNotAssigned); // => throws a ReferenceError
      console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  <a name="hoisting--anon-expressions"></a><a name="14.2"></a>
  - [14.2](#hoisting--anon-expressions) 匿名函数表达式提升他的变量名称，但不提升函数赋值。
  - [14.2](#hoisting--anon-expressions) Anonymous function expressions hoist their variable name, but not the function assignment.

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function () {
        console.log('anonymous function expression');
      };
    }
    ```

  <a name="hoisting--named-expresions"></a><a name="hoisting--named-expressions"></a><a name="14.3"></a>
  - [14.3](#hoisting--named-expressions) 命名函数表达式提升变量名称，不提升函数名称和函数体。
  - [14.3](#hoisting--named-expressions) Named function expressions hoist the variable name, not the function name or the function body.

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // the same is true when the function name
    // is the same as the variable name.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      };
    }
    ```

  <a name="hoisting--declarations"></a><a name="14.4"></a>
  - [14.4](#hoisting--declarations) 函数声明提升他们的函数名和函数体。
  - [14.4](#hoisting--declarations) Function declarations hoist their name and the function body.

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - 更多信息请参考[JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/) by [Ben Cherry](http://www.adequatelygood.com/).
  - For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/) by [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ back to top](#table-of-contents)**

## 比较运算符和判等 / Comparison Operators & Equality

  <a name="comparison--eqeqeq"></a><a name="15.1"></a>
  - [15.1](#comparison--eqeqeq) 使用 `===` 和 `!==` 超过 `==` 和 `!=`. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq.html)
  - [15.1](#comparison--eqeqeq) Use `===` and `!==` over `==` and `!=`. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq.html)

  <a name="comparison--if"></a><a name="15.2"></a>
  - [15.2](#comparison--if) 条件语句（如`if`语句）使用`ToBoolean`抽象方法使用强制计算表达式，并始终遵循以下简单规则：
  - [15.2](#comparison--if) Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

    - **Objects** 计算为：**true**
    - **Undefined** 计算为：**false**
    - **Null** 计算为：**false**
    - **Booleans** 计算为：**布尔变量本身**
    - **Numbers** 计算为：值为**+0, -0, NaN**将计算为**false**, 其他情况将计算为**true**
    - **Strings** 计算为：空字符串`''`将计算为**false**，其他情况将计算为**true**

    ```javascript
    if ([0] && []) {
      // true
      // 一个数组（甚至空数组）是一个对象，对象将计算为true
      // an array (even an empty one) is an object, objects will evaluate to true
    }
    ```

  <a name="comparison--shortcuts"></a><a name="15.3"></a>
  - [15.3](#comparison--shortcuts) 对于布尔值使用快捷方式，但对字符串和数字进行显示比较。
  - [15.3](#comparison--shortcuts) Use shortcuts for booleans, but explicit comparisons for strings and numbers.

    ```javascript
    // bad 不推荐 
    if (isValid === true) {
      // ...
    }

    // good 推荐
    if (isValid) {
      // ...
    }

    // bad 不推荐 
    if (name) {
      // ...
    }

    // good 推荐
    if (name !== '') {
      // ...
    }

    // bad 不推荐 
    if (collection.length) {
      // ...
    }

    // good 推荐
    if (collection.length > 0) {
      // ...
    }
    ```

  <a name="comparison--moreinfo"></a><a name="15.4"></a>
  - [15.4](#comparison--moreinfo) 更多信息请参考 [Truth Equality and JavaScript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

  <a name="comparison--switch-blocks"></a><a name="15.5"></a>
  - [15.5](#comparison--switch-blocks) 使用大括号包含词法声明的 `case` and `default`字句中创建块（例如：`let`, `const`, `function`, and `class`）。eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations.html)
  - [15.5](#comparison--switch-blocks) Use braces to create blocks in `case` and `default` clauses that contain lexical declarations (e.g. `let`, `const`, `function`, and `class`). eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations.html)

    > Why? 词法声明在整个`switch`块中可见，但只有在分配时才初始化，这仅在达到`case`时发生。当多了个`case`子句尝试定义同一个事儿时，这会导致问题发生。
    > Why? Lexical declarations are visible in the entire `switch` block but only get initialized when assigned, which only happens when its `case` is reached. This causes problems when multiple `case` clauses attempt to define the same thing.

    ```javascript
    // bad 不推荐 
    switch (foo) {
      case 1:
        let x = 1;
        break;
      case 2:
        const y = 2;
        break;
      case 3:
        function f() {
          // ...
        }
        break;
      default:
        class C {}
    }

    // good 推荐
    switch (foo) {
      case 1: {
        let x = 1;
        break;
      }
      case 2: {
        const y = 2;
        break;
      }
      case 3: {
        function f() {
          // ...
        }
        break;
      }
      case 4:
        bar();
        break;
      default: {
        class C {}
      }
    }
    ```

  <a name="comparison--nested-ternaries"></a><a name="15.6"></a>
  - [15.6](#comparison--nested-ternaries) 三元表达式不应该嵌套，通常应该是单行表达式。eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary.html)
  - [15.6](#comparison--nested-ternaries) Ternaries should not be nested and generally be single line expressions. eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary.html)

    ```javascript
    // bad 不推荐 
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // split into 2 separated ternary expressions
    const maybeNull = value1 > value2 ? 'baz' : null;

    // better
    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // best
    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="15.7"></a>
  - [15.7](#comparison--unneeded-ternary) 避免不必要的三元表达式😀。eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary.html)
  - [15.7](#comparison--unneeded-ternary) Avoid unneeded ternary statements. eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary.html)

    ```javascript
    // bad 不推荐 
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // good 推荐
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

  <a name="comparison--no-mixed-operators"></a>
  - [15.8](#comparison--no-mixed-operators) 当混合运算时，使用小括号括起来。 只有一种例外就是标准运算符：`+`, `-`, 和 `**`，因为他们的优先级大家都懂。我们建议将 `/` and `*`括起来，因为他们在混合使用的时候，优先级会模棱两可。
  - [15.8](#comparison--no-mixed-operators) When mixing operators, enclose them in parentheses. The only exception is the standard arithmetic operators: `+`, `-`, and `**` since their precedence is broadly understood. We recommend enclosing `/` and `*` in parentheses because their precedence can be ambiguous when they are mixed.
  eslint: [`no-mixed-operators`](https://eslint.org/docs/rules/no-mixed-operators.html)

    > Why? 这提高了可读性和阐明了开发人员的意图。
    > Why? This improves readability and clarifies the developer’s intention.

    ```javascript
    // bad 不推荐
    const foo = a && b < 0 || c > 0 || d + 1 === 0;

    // bad 不推荐
    const bar = a ** b - 5 % d;

    // bad 不推荐
    // one may be confused into thinking (a || b) && c
    if (a || b && c) {
      return d;
    }

    // bad 不推荐
    const bar = a + b / c * d;

    // good 推荐
    const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

    // good 推荐
    const bar = a ** b - (5 % d);

    // good 推荐
    if (a || (b && c)) {
      return d;
    }

    // good 推荐
    const bar = a + (b / c) * d;
    ```

**[⬆ back to top](#table-of-contents)**

## 块 / Blocks

  <a name="blocks--braces"></a><a name="16.1"></a>
  - [16.1](#blocks--braces) 多行块使用大括号。eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)
  - [16.1](#blocks--braces) Use braces with all multi-line blocks. eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)

    ```javascript
    // bad 不推荐
    if (test)
      return false;

    // good 推荐
    if (test) return false;

    // good 推荐
    if (test) {
      return false;
    }

    // bad 不推荐
    function foo() { return false; }

    // good 推荐
    function bar() {
      return false;
    }
    ```

  <a name="blocks--cuddled-elses"></a><a name="16.2"></a>
  - [16.2](#blocks--cuddled-elses) 如果你使用`if``else`代码块，将`else`放在`if`代码块的结束行。 eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style.html)
  - [16.2](#blocks--cuddled-elses) If you’re using multi-line blocks with `if` and `else`, put `else` on the same line as your `if` block’s closing brace. eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style.html)

    ```javascript
    // bad 不推荐
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // good 推荐
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

  <a name="blocks--no-else-return"></a><a name="16.3"></a>
  - [16.3](#blocks--no-else-return) 如果`if`代码块始终执行`return`语句，那么之后的`else`代码块不是必须的。包含的`return`语句的`if`代码块之后的`else if`的`return`语句可以分割为多个`if`代码块。eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)
  - [16.3](#blocks--no-else-return) If an `if` block always executes a `return` statement, the subsequent `else` block is unnecessary. A `return` in an `else if` block following an `if` block that contains a `return` can be separated into multiple `if` blocks. eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)

    ```javascript
    // bad 不推荐
    function foo() {
      if (x) {
        return x;
      } else {
        return y;
      }
    }

    // bad 不推荐
    function cats() {
      if (x) {
        return x;
      } else if (y) {
        return y;
      }
    }

    // bad 不推荐
    function dogs() {
      if (x) {
        return x;
      } else {
        if (y) {
          return y;
        }
      }
    }

    // good 推荐
    function foo() {
      if (x) {
        return x;
      }

      return y;
    }

    // good 推荐
    function cats() {
      if (x) {
        return x;
      }

      if (y) {
        return y;
      }
    }

    // good 推荐
    function dogs(x) {
      if (x) {
        if (z) {
          return y;
        }
      } else {
        return z;
      }
    }
    ```

**[⬆ back to top](#table-of-contents)**

## 控制语句 / Control Statements

  <a name="control-statements"></a>
  - [17.1](#control-statements) 如果你的控制语句(`if`, `while` etc.) 太长/或者超过单行最大长度， 每个（分组）条件可以放入新行中。逻辑运算应该在行起始位置。
  - [17.1](#control-statements) In case your control statement (`if`, `while` etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. The logical operator should begin the line.

    > Why? 要求在行开头的运算保持运算符对齐，并尊选类似于方法链式。这提高了可读性，是视觉上更容易遵循复杂的逻辑。
    > Why? Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.

    ```javascript
    // bad 不推荐
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
      thing1();
    }

    // bad 不推荐
    if (foo === 123 &&
      bar === 'abc') {
      thing1();
    }

    // bad 不推荐
    if (foo === 123
      && bar === 'abc') {
      thing1();
    }

    // bad 不推荐
    if (
      foo === 123 &&
      bar === 'abc'
    ) {
      thing1();
    }

    // good 推荐
    if (
      foo === 123
      && bar === 'abc'
    ) {
      thing1();
    }

    // good 推荐
    if (
      (foo === 123 || bar === 'abc')
      && doesItLookGoodWhenItBecomesThatLong()
      && isThisReallyHappening()
    ) {
      thing1();
    }

    // good 推荐
    if (foo === 123 && bar === 'abc') {
      thing1();
    }
    ```

  <a name="control-statement--value-selection"></a><a name="control-statements--value-selection"></a>
  - [17.2](#control-statements--value-selection) 不要在控制语句中使用选择运算符。😀😀
  - [17.2](#control-statements--value-selection) Don't use selection operators in place of control statements.

    ```javascript
    // bad 不推荐
    !isRunning && startRunning();

    // good 推荐
    if (!isRunning) {
      startRunning();
    }
    ```

**[⬆ back to top](#table-of-contents)**

## 注释 / Comments

  <a name="comments--multiline"></a><a name="17.1"></a>
  - [18.1](#comments--multiline) 多行注释使用：`/** ... */`。
  - [18.1](#comments--multiline) Use `/** ... */` for multi-line comments.

    ```javascript
    // bad 不推荐
    // make() returns a new element 
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // good 推荐
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--singleline"></a><a name="17.2"></a>
  - [18.2](#comments--singleline) 单行注释使用 `//`。将单行注释放在注释主体上方。除非注释位于代码块的第一行上，否则在注释前空置一行。
  - [18.2](#comments--singleline) Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it’s on the first line of a block.

    ```javascript
    // bad 不推荐
    const active = true;  // is current tab

    // good 推荐
    // is current tab
    const active = true;

    // bad 不推荐
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // good 推荐
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // also good 推荐
    function getType() {
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }
    ```

  <a name="comments--spaces"></a>
  - [18.3](#comments--spaces) 在所有注释前添加一个空格，方便阅读。 eslint: [`spaced-comment`](https://eslint.org/docs/rules/spaced-comment)
  - [18.3](#comments--spaces) Start all comments with a space to make it easier to read. eslint: [`spaced-comment`](https://eslint.org/docs/rules/spaced-comment)

    ```javascript
    // bad 不推荐
    //is current tab
    const active = true;

    // good 推荐
    // is current tab
    const active = true;

    // bad 不推荐
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }

    // good 推荐
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--actionitems"></a><a name="17.3"></a>
  - [18.4](#comments--actionitems) 在注释前加上`FIXME` or `TODO`，帮助其他开发人员更快地了解 你是否在指明一个需要回顾的问题/或者是否在提出一个解决办法需要被实施。这些与常规注释不同，因为他们是可操作性的。操作是：`FIXME: -- 需要解决` or `TODO: --需要实现`。
  - [18.4](#comments--actionitems) Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you’re pointing out a problem that needs to be revisited, or if you’re suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME: -- need to figure this out` or `TODO: -- need to implement`.

  <a name="comments--fixme"></a><a name="17.4"></a>
  - [18.5](#comments--fixme) 使用 `// FIXME:` 来注释问题。
  - [18.5](#comments--fixme) Use `// FIXME:` to annotate problems.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: shouldn’t use a global here // FIXME: 不应该在这儿使用一个全局变量
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="17.5"></a>
  - [18.6](#comments--todo) 使用 `// TODO:` 来注释问题的解决办法。
  - [18.6](#comments--todo) Use `// TODO:` to annotate solutions to problems.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param // TODO: total应该是可配置的可选参数
        this.total = 0;
      }
    }
    ```

**[⬆ back to top](#table-of-contents)**

## 空格 / Whitespace

  <a name="whitespace--spaces"></a><a name="18.1"></a>
  - [19.1](#whitespace--spaces) 使用软Tab（空格符）设置为2个空格。 eslint: [`indent`](https://eslint.org/docs/rules/indent.html)
  - [19.1](#whitespace--spaces) Use soft tabs (space character) set to 2 spaces. eslint: [`indent`](https://eslint.org/docs/rules/indent.html)

    ```javascript
    // bad 不推荐
    function foo() {
    ∙∙∙∙let name;
    }

    // bad 不推荐
    function bar() {
    ∙let name;
    }

    // good 推荐
    function baz() {
    ∙∙let name;
    }
    ```

  <a name="whitespace--before-blocks"></a><a name="18.2"></a>
  - [19.2](#whitespace--before-blocks) 在大括号之前保留一个空格。 eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks.html)
  - [19.2](#whitespace--before-blocks) Place 1 space before the leading brace. eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks.html)

    ```javascript
    // bad 不推荐
    function test(){
      console.log('test');
    }

    // good 推荐
    function test() {
      console.log('test');
    }

    // bad 不推荐
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // good 推荐
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  <a name="whitespace--around-keywords"></a><a name="18.3"></a>
  - [19.3](#whitespace--around-keywords) 在控制语句之前保留一个空格 (`if`, `while` etc.)。在调用和声明方法时，参数列表和方法名之间不要空格。 eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing.html)
  - [19.3](#whitespace--around-keywords) Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space between the argument list and the function name in function calls and declarations. eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing.html)

    ```javascript
    // bad 不推荐
    if(isJedi) {
      fight ();
    }

    // good 推荐
    if (isJedi) {
      fight();
    }

    // bad 不推荐
    function fight () {
      console.log ('Swooosh!');
    }

    // good 推荐
    function fight() {
      console.log('Swooosh!');
    }
    ```

  <a name="whitespace--infix-ops"></a><a name="18.4"></a>
  - [19.4](#whitespace--infix-ops) 使用空格分隔运算符。eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops.html)
  - [19.4](#whitespace--infix-ops) Set off operators with spaces. eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops.html)

    ```javascript
    // bad 不推荐
    const x=y+5;

    // good 推荐
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end"></a><a name="18.5"></a>
  - [19.5](#whitespace--newline-at-end) 使用单个字符结束文件。eslint: [`eol-last`](https://github.com/eslint/eslint/blob/master/docs/rules/eol-last.md)
  - [19.5](#whitespace--newline-at-end) End files with a single newline character. eslint: [`eol-last`](https://github.com/eslint/eslint/blob/master/docs/rules/eol-last.md)

    ```javascript
    // bad 不推荐
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;
    ```

    ```javascript
    // bad 不推荐
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ↵
    ```

    ```javascript
    // good 推荐
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ```

  <a name="whitespace--chains"></a><a name="18.6"></a>
  - [19.6](#whitespace--chains) 采用首行缩进，当使用长方法链接时（超过2个方法链接）。使用前导点，强调是方法调用，而不是新语句。 eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)
  - [19.6](#whitespace--chains) Use indentation when making long method chains (more than 2 method chains). Use a leading dot, which
    emphasizes that the line is a method call, not a new statement. eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)

    ```javascript
    // bad 不推荐
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // bad 不推荐
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // good 推荐
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad 不推荐
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // good 推荐
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // good 推荐
    const leds = stage.selectAll('.led').data(data);
    ```

  <a name="whitespace--after-blocks"></a><a name="18.7"></a>
  - [19.7](#whitespace--after-blocks) 在代码块之后，下一条语句之前，保留一条空白行。
  - [19.7](#whitespace--after-blocks) Leave a blank line after blocks and before the next statement.

    ```javascript
    // bad 不推荐
    if (foo) {
      return bar;
    }
    return baz;

    // good 推荐
    if (foo) {
      return bar;
    }

    return baz;

    // bad 不推荐
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // good 推荐
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // bad 不推荐
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // good 推荐
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  <a name="whitespace--padded-blocks"></a><a name="18.8"></a>
  - [19.8](#whitespace--padded-blocks) 不要使用空白行填充代码块。eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks.html)
  - [19.8](#whitespace--padded-blocks) Do not pad your blocks with blank lines. eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks.html)

    ```javascript
    // bad 不推荐
    function bar() {

      console.log(foo);

    }

    // bad 不推荐
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // bad 不推荐
    class Foo {

      constructor(bar) {
        this.bar = bar;
      }
    }

    // good 推荐
    function bar() {
      console.log(foo);
    }

    // good 推荐
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

  <a name="whitespace--no-multiple-blanks"></a>
  - [19.9](#whitespace--no-multiple-blanks) 不用使用多个空白行来填充你的代码。eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)
  - [19.9](#whitespace--no-multiple-blanks) Do not use multiple blank lines to pad your code. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // bad 不推荐
    class Person {
      constructor(fullName, email, birthday) {
        this.fullName = fullName;


        this.email = email;


        this.setAge(birthday);
      }


      setAge(birthday) {
        const today = new Date();


        const age = this.getAge(today, birthday);


        this.age = age;
      }


      getAge(today, birthday) {
        // ..
      }
    }

    // good 推荐
    class Person {
      constructor(fullName, email, birthday) {
        this.fullName = fullName;
        this.email = email;
        this.setAge(birthday);
      }

      setAge(birthday) {
        const today = new Date();
        const age = getAge(today, birthday);
        this.age = age;
      }

      getAge(today, birthday) {
        // ..
      }
    }
    ```

  <a name="whitespace--in-parens"></a><a name="18.9"></a>
  - [19.10](#whitespace--in-parens) 不要在小括号内添加空格。eslint: [`space-in-parens`](https://eslint.org/docs/rules/space-in-parens.html)
  - [19.10](#whitespace--in-parens) Do not add spaces inside parentheses. eslint: [`space-in-parens`](https://eslint.org/docs/rules/space-in-parens.html)

    ```javascript
    // bad 不推荐
    function bar( foo ) {
      return foo;
    }

    // good 推荐
    function bar(foo) {
      return foo;
    }

    // bad 不推荐
    if ( foo ) {
      console.log(foo);
    }

    // good 推荐
    if (foo) {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-brackets"></a><a name="18.10"></a>
  - [19.11](#whitespace--in-brackets) 不要在方括号中添加空格。eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing.html)
  - [19.11](#whitespace--in-brackets) Do not add spaces inside brackets. eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing.html)

    ```javascript
    // bad 不推荐
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // good 推荐
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  <a name="whitespace--in-braces"></a><a name="18.11"></a>
  - [19.12](#whitespace--in-braces) 在花括号内添加空格。eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing.html)
  - [19.12](#whitespace--in-braces) Add spaces inside curly braces. eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing.html)

    ```javascript
    // bad 不推荐
    const foo = {clark: 'kent'};

    // good 推荐
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len"></a><a name="18.12"></a>
  - [19.13](#whitespace--max-len) 禁止代码行超过100个字符（含空格）。注意：每个[above](#strings--line-length), 长字符串不受此限制，且不应该被打断。 eslint: [`max-len`](https://eslint.org/docs/rules/max-len.html)
  - [19.13](#whitespace--max-len) Avoid having lines of code that are longer than 100 characters (including whitespace). Note: per [above](#strings--line-length), long strings are exempt from this rule, and should not be broken up. eslint: [`max-len`](https://eslint.org/docs/rules/max-len.html)

    > Why? 确保了可读性和可维护性。
    > Why? This ensures readability and maintainability.

    ```javascript
    // bad 不推荐
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // bad 不推荐
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // good 推荐
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // good 推荐
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

  <a name="whitespace--block-spacing"></a>
  - [19.14](#whitespace--block-spacing) 要求在打开的块Token内保持一致的间距，在同一行上需要下一个标记。此规则还在同一行上的闭合块Token和上一个标记内强制一致的间距。 eslint: [`block-spacing`](https://eslint.org/docs/rules/block-spacing)
  - [19.14](#whitespace--block-spacing) Require consistent spacing inside an open block token and the next token on the same line. This rule also enforces consistent spacing inside a close block token and previous token on the same line. eslint: [`block-spacing`](https://eslint.org/docs/rules/block-spacing)

    ```javascript
    // bad 不推荐
    function foo() {return true;}
    if (foo) { bar = 0;}

    // good 推荐
    function foo() { return true; }
    if (foo) { bar = 0; }
    ```

  <a name="whitespace--comma-spacing"></a>
  - [19.15](#whitespace--comma-spacing) 禁止在逗号之前添加空格，在逗号之后需要一个空格。eslint: [`comma-spacing`](https://eslint.org/docs/rules/comma-spacing)
  - [19.15](#whitespace--comma-spacing) Avoid spaces before commas and require a space after commas. eslint: [`comma-spacing`](https://eslint.org/docs/rules/comma-spacing)

    ```javascript
    // bad 不推荐
    var foo = 1,bar = 2;
    var arr = [1 , 2];

    // good 推荐
    var foo = 1, bar = 2;
    var arr = [1, 2];
    ```

  <a name="whitespace--computed-property-spacing"></a>
  - [19.16](#whitespace--computed-property-spacing) 强制计算属性括号内的间距。eslint: [`computed-property-spacing`](https://eslint.org/docs/rules/computed-property-spacing)
  - [19.16](#whitespace--computed-property-spacing) Enforce spacing inside of computed property brackets. eslint: [`computed-property-spacing`](https://eslint.org/docs/rules/computed-property-spacing)

    ```javascript
    // bad 不推荐
    obj[foo ]
    obj[ 'foo']
    var x = {[ b ]: a}
    obj[foo[ bar ]]

    // good 推荐
    obj[foo]
    obj['foo']
    var x = { [b]: a }
    obj[foo[bar]]
    ```

  <a name="whitespace--func-call-spacing"></a>
  - [19.17](#whitespace--func-call-spacing) 禁止在方法和调用之间的空格。eslint: [`func-call-spacing`](https://eslint.org/docs/rules/func-call-spacing)
  - [19.17](#whitespace--func-call-spacing) Avoid spaces between functions and their invocations. eslint: [`func-call-spacing`](https://eslint.org/docs/rules/func-call-spacing)

    ```javascript
    // bad 不推荐
    func ();

    func
    ();

    // good 推荐
    func();
    ```

  <a name="whitespace--key-spacing"></a>
  - [19.18](#whitespace--key-spacing) 在对象的文字属性中，强制键值对的间距。 eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing)
  - [19.18](#whitespace--key-spacing) Enforce spacing between keys and values in object literal properties. eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing)

    ```javascript
    // bad 不推荐
    var obj = { "foo" : 42 };
    var obj2 = { "foo":42 };

    // good 推荐
    var obj = { "foo": 42 };
    ```

  <a name="whitespace--no-trailing-spaces"></a>
  - [19.19](#whitespace--no-trailing-spaces) 禁止行后尾随的空格。eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)
  - [19.19](#whitespace--no-trailing-spaces) Avoid trailing spaces at the end of lines. eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)

  <a name="whitespace--no-multiple-empty-lines"></a>
  - [19.20](#whitespace--no-multiple-empty-lines) 禁止多行空行,只允许文件结尾出现一个新行，且禁止文件开头出现空行。eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)
  - [19.20](#whitespace--no-multiple-empty-lines) Avoid multiple empty lines, only allow one newline at the end of files, and avoid a newline at the beginning of files. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    ```javascript
    // bad 不推荐 - multiple empty lines
    var x = 1;


    var y = 2;

    // bad 不推荐 - 2+ newlines at end of file
    var x = 1;
    var y = 2;


    // bad 不推荐 - 1+ newline(s) at beginning of file

    var x = 1;
    var y = 2;

    // good 推荐
    var x = 1;
    var y = 2;

    ```
    <!-- markdownlint-enable MD012 -->

**[⬆ back to top](#table-of-contents)**

## 逗号 / Commas

  <a name="commas--leading-trailing"></a><a name="19.1"></a>
  - [20.1](#commas--leading-trailing) 前导逗号：**Nope.** eslint: [`comma-style`](https://eslint.org/docs/rules/comma-style.html)
  - [20.1](#commas--leading-trailing) Leading commas: **Nope.** eslint: [`comma-style`](https://eslint.org/docs/rules/comma-style.html)

    ```javascript
    // bad 不推荐
    const story = [
        once
      , upon
      , aTime
    ];

    // good 推荐
    const story = [
      once,
      upon,
      aTime,
    ];

    // bad 不推荐
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // good 推荐
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  <a name="commas--dangling"></a><a name="19.2"></a>
  - [20.2](#commas--dangling) 附加尾随逗号: **Yup.** eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle.html)
  - [20.2](#commas--dangling) Additional trailing comma: **Yup.** eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle.html)

    > Why? 这将触发更清洁的git差异。 此外, 想Bable这样的转移其将删除转码代码中的附加尾随逗号，这意味着您不必担心在旧版浏览器的 [尾随逗号问题](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas)。
    > Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don’t have to worry about the [trailing comma problem](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas) in legacy browsers.

    ```diff
    // bad 不推荐 - git diff without trailing comma
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // good 推荐 - git diff with trailing comma
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    // bad 不推荐
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // good 推荐
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];

    // bad 不推荐
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // does nothing
    }

    // good 推荐
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // does nothing
    }

    // good 推荐 (note that a comma must not appear after a "rest" element)
    function createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    ) {
      // does nothing
    }

    // bad 不推荐
    createHero(
      firstName,
      lastName,
      inventorOf
    );

    // good 推荐
    createHero(
      firstName,
      lastName,
      inventorOf,
    );

    // good 推荐 (note that a comma must not appear after a "rest" element)
    createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    );
    ```

**[⬆ back to top](#table-of-contents)**

## 分号 / Semicolons

  <a name="semicolons--required"></a><a name="20.1"></a>
  - [21.1](#semicolons--required) **Yup.** eslint: [`semi`](https://eslint.org/docs/rules/semi.html)

    > Why? 当JavaScript遇到一行没有分号的换行时，它使用一个规则配置叫 [自动分号插入](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) 来确定是否将换行符视为语句的结尾，且 (顾名思义)在换行符之前将分号放入代码中，如果它认为如此。但是，ASI包含一些古怪的行为，如果JavaScript误解了换行符，您的代码就会中断。随着新功能成为JavaScript的一部分，这些规则将变得更加复杂。显式终止语句并配置linter一不过缺少的分号有呼吁防止遇到问题。
    > Why? When JavaScript encounters a line break without a semicolon, it uses a set of rules called [Automatic Semicolon Insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) to determine whether or not it should regard that line break as the end of a statement, and (as the name implies) place a semicolon into your code before the line break if it thinks so. ASI contains a few eccentric behaviors, though, and your code will break if JavaScript misinterprets your line break. These rules will become more complicated as new features become a part of JavaScript. Explicitly terminating your statements and configuring your linter to catch missing semicolons will help prevent you from encountering issues.

    ```javascript
    // bad 不推荐 - raises exception
    const luke = {}
    const leia = {}
    [luke, leia].forEach((jedi) => jedi.father = 'vader')

    // bad 不推荐 - raises exception
    const reaction = "No! That’s impossible!"
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    // bad 不推荐 - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    // good 推荐
    const luke = {};
    const leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    // good 推荐
    const reaction = "No! That’s impossible!";
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }());

    // good 推荐
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

    [Read more](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214#7365214).

**[⬆ back to top](#table-of-contents)**

## 类型转换&强制 / Type Casting & Coercion

  <a name="coercion--explicit"></a><a name="21.1"></a>
  - [22.1](#coercion--explicit) 在语句的开头执行类型强制。
  - [22.1](#coercion--explicit) Perform type coercion at the beginning of the statement.

  <a name="coercion--strings"></a><a name="21.2"></a>
  - [22.2](#coercion--strings) Strings: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    // => this.reviewScore = 9;

    // bad 不推荐
    const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

    // bad 不推荐
    const totalScore = this.reviewScore + ''; // invokes/执行 this.reviewScore.valueOf()

    // bad 不推荐
    const totalScore = this.reviewScore.toString(); // isn’t guaranteed to return a string // 不保证返回一个字符串

    // good 推荐
    const totalScore = String(this.reviewScore);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  - [22.3](#coercion--numbers) Numbers: 使用`Number`做类型转换，使用带有基数的`parseInt`转换字符串。eslint: [`radix`](https://eslint.org/docs/rules/radix) [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)
  - [22.3](#coercion--numbers) Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings. eslint: [`radix`](https://eslint.org/docs/rules/radix) [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const inputValue = '4';

    // bad 不推荐
    const val = new Number(inputValue);

    // bad 不推荐 😀😀😀
    const val = +inputValue;

    // bad 不推荐
    const val = inputValue >> 0;

    // bad 不推荐
    const val = parseInt(inputValue);

    // good 推荐
    const val = Number(inputValue);

    // good 推荐
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations"></a><a name="21.4"></a>
  - [22.4](#coercion--comment-deviations) 不论出于任何原因，您正在做一些疯狂的事情，`parseInt`是你的瓶颈，出于[性能的原因]需要使用位移运算(https://jsperf.com/coercion-vs-casting/3), 留下评论解释你在做什么。
  - [22.4](#coercion--comment-deviations) If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](https://jsperf.com/coercion-vs-casting/3), leave a comment explaining why and what you’re doing.

    ```javascript
    // good 推荐
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise"></a><a name="21.5"></a>
  - [22.5](#coercion--bitwise) **Note:** 使用位运算符时要当心。Numbers 代表的是[64位值](https://es5.github.io/#x4.3.19), 但是位移运算符总是返回32位整数 ([source](https://es5.github.io/#x11.7))。位移对于大于32位的整数值经发生不期望的行为。[Discussion](https://github.com/airbnb/javascript/issues/109). 最大签名的32为Int值是 2,147,483,647:
  - [22.5](#coercion--bitwise) **Note:** Be careful when using bitshift operations. Numbers are represented as [64-bit values](https://es5.github.io/#x4.3.19), but bitshift operations always return a 32-bit integer ([source](https://es5.github.io/#x11.7)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](https://github.com/airbnb/javascript/issues/109). Largest signed 32-bit Int is 2,147,483,647:

    ```javascript
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

  <a name="coercion--booleans"></a><a name="21.6"></a>
  - [22.6](#coercion--booleans) Booleans: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const age = 0;

    // bad 不推荐
    const hasAge = new Boolean(age);

    // good 推荐
    const hasAge = Boolean(age);

    // best 极力推荐
    const hasAge = !!age;
    ```

**[⬆ back to top](#table-of-contents)**

## 命名规则 / Naming Conventions

  <a name="naming--descriptive"></a><a name="22.1"></a>
  - [23.1](#naming--descriptive) 禁止单字符命名，让你的命名具有自我描述性。eslint: [`id-length`](https://eslint.org/docs/rules/id-length)
  - [23.1](#naming--descriptive) Avoid single letter names. Be descriptive with your naming. eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

    ```javascript
    // bad 不推荐
    function q() {
      // ...
    }

    // good 推荐
    function query() {
      // ...
    }
    ```

  <a name="naming--camelCase"></a><a name="22.2"></a>
  - [23.2](#naming--camelCase) 使用驼峰格式来命名对象、方法和实例。eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase.html)
  - [23.2](#naming--camelCase) Use camelCase when naming objects, functions, and instances. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase.html)

    ```javascript
    // bad 不推荐
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // good 推荐
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase"></a><a name="22.3"></a>
  - [23.3](#naming--PascalCase) 仅在命名构造函数和类时，采用PascalCase命名方式。eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap.html)
  - [23.3](#naming--PascalCase) Use PascalCase only when naming constructors or classes. eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap.html)

    ```javascript
    // bad 不推荐
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // good 推荐
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore"></a><a name="22.4"></a>
  - [23.4](#naming--leading-underscore) 不要使用尾随/或前导下划线。eslint: [`no-underscore-dangle`](https://eslint.org/docs/rules/no-underscore-dangle.html)
  - [23.4](#naming--leading-underscore) Do not use trailing or leading underscores. eslint: [`no-underscore-dangle`](https://eslint.org/docs/rules/no-underscore-dangle.html)

    > Why? JavaScript的属性和方法没有隐私的概念。 尽管前导下划线是“私有”的常见约定，但实际上，这些属性是完全公开的，因此，这些属性是公共API协定的一部分。此约定可能导致开发人员错误地认为更改不会算作中断，或者不需要测试。如果你想要私有化一些东西，它一定不能明显存在。
    > Why? JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean “private”, in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won’t count as breaking, or that tests aren’t needed. tl;dr: if you want something to be “private”, it must not be observably present.

    ```javascript
    // bad 不推荐
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // good 推荐
    this.firstName = 'Panda';

    // good 推荐, in environments where WeakMaps are available
    // see https://kangax.github.io/compat-table/es6/#test-WeakMap
    const firstNames = new WeakMap();
    firstNames.set(this, 'Panda');
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  - [23.5](#naming--self-this) 不要保存`this`引用，使用箭头函数/或[函数的bind语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).
  - [23.5](#naming--self-this) Don’t save references to `this`. Use arrow functions or [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

    ```javascript
    // bad 不推荐
    function foo() {
      const self = this;
      return function () {
        console.log(self);
      };
    }

    // bad 不推荐
    function foo() {
      const that = this;
      return function () {
        console.log(that);
      };
    }

    // good 推荐
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

  <a name="naming--filename-matches-export"></a><a name="22.6"></a>
  - [23.6](#naming--filename-matches-export) 基本文件名应与其默认导出的名称完全匹配。
  - [23.6](#naming--filename-matches-export) A base filename should exactly match the name of its default export.

    ```javascript
    // file 1 contents
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // file 2 contents
    export default function fortyTwo() { return 42; }

    // file 3 contents
    export default function insideDirectory() {}

    // in some other file
    // bad 不推荐
    import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
    import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
    import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

    // bad 不推荐
    import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
    import forty_two from './forty_two'; // snake_case import/filename, camelCase export
    import inside_directory from './inside_directory'; // snake_case import, camelCase export
    import index from './inside_directory/index'; // requiring the index file explicitly
    import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

    // good 推荐
    import CheckBox from './CheckBox'; // PascalCase export/import/filename
    import fortyTwo from './fortyTwo'; // camelCase export/import/filename
    import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
    // ^ supports both insideDirectory.js and insideDirectory/index.js
    ```

  <a name="naming--camelCase-default-export"></a><a name="22.7"></a>
  - [23.7](#naming--camelCase-default-export) 导出默认函数时，使用小驼峰命名规范。文件名应该与函数的名称相同。
  - [23.7](#naming--camelCase-default-export) Use camelCase when you export-default a function. Your filename should be identical to your function’s name.

    ```javascript
    function makeStyleGuide() {
      // ...
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton"></a><a name="22.8"></a>
  - [23.8](#naming--PascalCase-singleton) 导出 构造函数 / 类 / 单例 / 函数库 / 基础对象时，使用大驼峰命名规范。
  - [23.8](#naming--PascalCase-singleton) Use PascalCase when you export a constructor / class / singleton / function library / bare object.

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      },
    };

    export default AirbnbStyleGuide;
    ```

  <a name="naming--Acronyms-and-Initialisms"></a>
  - [23.9](#naming--Acronyms-and-Initialisms) 缩写和首字母缩写应该始终保持 全部大写/或小写。
  - [23.9](#naming--Acronyms-and-Initialisms) Acronyms and initialisms should always be all uppercased, or all lowercased.

    > Why? 名称用于可读性，而不是安抚计算机语法。
    > Why? Names are for readability, not to appease a computer algorithm.

    ```javascript
    // bad 不推荐
    import SmsContainer from './containers/SmsContainer';

    // bad 不推荐
    const HttpRequests = [
      // ...
    ];

    // good 推荐
    import SMSContainer from './containers/SMSContainer';

    // good 推荐
    const HTTPRequests = [
      // ...
    ];

    // also good 推荐
    const httpRequests = [
      // ...
    ];

    // best
    import TextMessageContainer from './containers/TextMessageContainer';

    // best
    const requests = [
      // ...
    ];
    ```

  <a name="naming--uppercase"></a>
  - [23.10](#naming--uppercase) 仅当常量(1)导出时，(2)是“const”（无法重新分配），以及（3）程序猿可以信任他（及其嵌套属性）永远不会更改，则可以选择对常量进行大写。
  - [23.10](#naming--uppercase) You may optionally uppercase a constant only if it (1) is exported, (2) is a `const` (it can not be reassigned), and (3) the programmer can trust it (and its nested properties) to never change.

    > Why? 这是一个额外的工具，以帮助在程序猿不确定变量是否会改变的情况下。大写变量让程序猿知道他们可以新人变量（机器属性）不会更改。
    > Why? This is an additional tool to assist in situations where the programmer would be unsure if a variable might ever change. UPPERCASE_VARIABLES are letting the programmer know that they can trust the variable (and its properties) not to change.
    - 所有“const”变量呢？这是不必要的，因此不赢将大写用于文件中的常量，但是，他应用于导出常量。
    - What about all `const` variables? - This is unnecessary, so uppercasing should not be used for constants within a file. It should be used for exported constants however.
    - 导出的对象呢？在定级导出（例如“导出”）大写，并维护所有嵌套属性不会更改。
    - What about exported objects? - Uppercase at the top level of export (e.g. `EXPORTED_OBJECT.key`) and maintain that all nested properties do not change.

    ```javascript
    // bad 不推荐
    const PRIVATE_VARIABLE = 'should not be unnecessarily uppercased within a file';
    const PRIVATE_VARIABLE = '不应在文件中不必要地大写';

    // bad 不推荐
    export const THING_TO_BE_CHANGED = 'should obviously not be uppercased';
    export const THING_TO_BE_CHANGED = '显然不应该大写';

    // bad 不推荐
    export let REASSIGNABLE_VARIABLE = 'do not use let with uppercase variables';
    export let REASSIGNABLE_VARIABLE = '不要使用大写变量let';

    // ---

    // allowed but does not supply semantic value
    export const apiKey = 'SOMEKEY';

    // better in most cases
    export const API_KEY = 'SOMEKEY';

    // ---

    // bad 不推荐 - unnecessarily uppercases key while adding no semantic value
    // 不必要的大写键名，同事不添加语义值。
    export const MAPPING = {
      KEY: 'value'
    };

    // good 推荐
    export const MAPPING = {
      key: 'value'
    };
    ```

**[⬆ back to top](#table-of-contents)**

## 访问器函数 / Accessors

  <a name="accessors--not-required"></a><a name="23.1"></a>
  - [24.1](#accessors--not-required) 属性的访问器函数不是必需的。
  - [24.1](#accessors--not-required) Accessor functions for properties are not required.

  <a name="accessors--no-getters-setters"></a><a name="23.2"></a>
  - [24.2](#accessors--no-getters-setters) 不要使用JavaScript的getters/setters，因为他们会导致意外的副作用，并且难测试、难维护、难推断。相反，如果您确实使用访问器函数，请使用`getVal()` 和 `setVal('hello')`。
  - [24.2](#accessors--no-getters-setters) Do not use JavaScript getters/setters as they cause unexpected side effects and are harder to test, maintain, and reason about. Instead, if you do make accessor functions, use `getVal()` and `setVal('hello')`.

    ```javascript
    // bad 不推荐
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }

    // good 推荐
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```

  <a name="accessors--boolean-prefix"></a><a name="23.3"></a>
  - [24.3](#accessors--boolean-prefix) 如果属性/方法是`boolean`,使用 `isVal()` /或 `hasVal()`.
  - [24.3](#accessors--boolean-prefix) If the property/method is a `boolean`, use `isVal()` or `hasVal()`.

    ```javascript
    // bad 不推荐
    if (!dragon.age()) {
      return false;
    }

    // good 推荐
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  <a name="accessors--consistent"></a><a name="23.4"></a>
  - [24.4](#accessors--consistent) 可以创建`get()` 和 `set()` 函数,但请保持一致。
  - [24.4](#accessors--consistent) It’s okay to create `get()` and `set()` functions, but be consistent.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

**[⬆ back to top](#table-of-contents)**

## 事件 / Events

  <a name="events--hash"></a><a name="24.1"></a>
  - [25.1](#events--hash) 将数据负载附加到事件（无论是DOM事件还是更专业的事件，如Backbone事件）时，传递文本对象（也叫“hash”）而不是原始值。这允许后续参与者向事件负载添加更多数据，而无需查找和更新事件的每个处理程序。例如，
  - [25.1](#events--hash) When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass an object literal (also known as a "hash") instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```javascript
    // bad 不推荐
    $(this).trigger('listingUpdated', listing.id);

    // ...

    $(this).on('listingUpdated', (e, listingID) => {
      // do something with listingID
    });
    ```

    prefer:

    ```javascript
    // good 推荐
    $(this).trigger('listingUpdated', { listingID: listing.id });

    // ...

    $(this).on('listingUpdated', (e, data) => {
      // do something with data.listingID
    });
    ```

  **[⬆ back to top](#table-of-contents)**

## jQuery

  <a name="jquery--dollar-prefix"></a><a name="25.1"></a>
  - [26.1](#jquery--dollar-prefix) jQuery对象变量的前缀是`$`.
  - [26.1](#jquery--dollar-prefix) Prefix jQuery object variables with a `$`.

    ```javascript
    // bad 不推荐
    const sidebar = $('.sidebar');

    // good 推荐
    const $sidebar = $('.sidebar');

    // good 推荐
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache"></a><a name="25.2"></a>
  - [26.2](#jquery--cache) 缓存jQuery查找项。
  - [26.2](#jquery--cache) Cache jQuery lookups.

    ```javascript
    // bad 不推荐
    function setSidebar() {
      $('.sidebar').hide();

      // ...

      $('.sidebar').css({
        'background-color': 'pink',
      });
    }

    // good 推荐
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...

      $sidebar.css({
        'background-color': 'pink',
      });
    }
    ```

  <a name="jquery--queries"></a><a name="25.3"></a>
  - [26.3](#jquery--queries) 对于DOM查询，请使用级联`$('.sidebar ul')`或 `$('.sidebar > ul') // 父元素 > 子元素`。 [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
  - [26.3](#jquery--queries) For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)

  <a name="jquery--find"></a><a name="25.4"></a>
  - [26.4](#jquery--find) 对于作用域的jQuery对象查询使用`find`。
  - [26.4](#jquery--find) Use `find` with scoped jQuery object queries.

    ```javascript
    // bad 不推荐
    $('ul', '.sidebar').hide();

    // bad 不推荐
    $('.sidebar').find('ul').hide();

    // good 推荐
    $('.sidebar ul').hide();

    // good 推荐
    $('.sidebar > ul').hide();

    // good 推荐
    $sidebar.find('ul').hide();
    ```

**[⬆ back to top](#table-of-contents)**

## ECMAScript 5 兼容性/Compatibility

  <a name="es5-compat--kangax"></a><a name="26.1"></a>
  - [27.1](#es5-compat--kangax) Refer to [Kangax](https://twitter.com/kangax/)’s ES5 [compatibility table](https://kangax.github.io/es5-compat-table/).

**[⬆ back to top](#table-of-contents)**

<a name="ecmascript-6-styles"></a>
## ES6+ (ES 2015+)风格 / ECMAScript 6+ (ES 2015+) Styles

  <a name="es6-styles"></a><a name="27.1"></a>
  - [28.1](#es6-styles) 这里有各种ES6+的功能链接。
  - [28.1](#es6-styles) This is a collection of links to the various ES6+ features.

1. [Arrow Functions](#arrow-functions)
1. [Classes](#classes--constructors)
1. [Object Shorthand](#es6-object-shorthand)
1. [Object Concise](#es6-object-concise)
1. [Object Computed Properties](#es6-computed-properties)
1. [Template Strings](#es6-template-literals)
1. [Destructuring](#destructuring)
1. [Default Parameters](#es6-default-parameters)
1. [Rest](#es6-rest)
1. [Array Spreads](#es6-array-spreads)
1. [Let and Const](#references)
1. [Exponentiation Operator](#es2016-properties--exponentiation-operator)
1. [Iterators and Generators](#iterators-and-generators)
1. [Modules](#modules)

  <a name="tc39-proposals"></a>
  - [28.2](#tc39-proposals) Do not use [TC39 proposals](https://github.com/tc39/proposals) that have not reached stage 3.

    > Why? [They are not finalized](https://tc39.github.io/process-document/), and they are subject to change or to be withdrawn entirely. We want to use JavaScript, and proposals are not JavaScript yet.

**[⬆ back to top](#table-of-contents)**

## 标准库 / Standard Library

  The [Standard Library](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects)
  contains utilities that are functionally broken but remain for legacy reasons.

  <a name="standard-library--isnan"></a>
  - [29.1](#standard-library--isnan) 使用`Number.isNaN`代替全局的`isNaN`。
  - [29.1](#standard-library--isnan) Use `Number.isNaN` instead of global `isNaN`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > Why? 全局的`isNaN`强制非数值转换为数值，任何强制转换的NaN都会返回true。
    > Why? The global `isNaN` coerces non-numbers to numbers, returning true for anything that coerces to NaN.
    > 如果需要此行为，那么显式使用。/If this behavior is desired, make it explicit.

    ```javascript
    // bad 不推荐
    isNaN('1.2'); // false
    isNaN('1.2.3'); // true

    // good 推荐
    Number.isNaN('1.2.3'); // false
    Number.isNaN(Number('1.2.3')); // true
    ```

  <a name="standard-library--isfinite"></a>
  - [29.2](#standard-library--isfinite) 使用`Number.isFinite`替代全局的`isFinite`。
  - [29.2](#standard-library--isfinite) Use `Number.isFinite` instead of global `isFinite`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > Why? 全局的`isFinite`强制非数值转换为数值，任何强制转换的finite数值都会返回true。
    > Why? The global `isFinite` coerces non-numbers to numbers, returning true for anything that coerces to a finite number.
    > 如果需要此行为，那么显式使用。/ If this behavior is desired, make it explicit.

    ```javascript
    // bad 不推荐
    isFinite('2e3'); // true

    // good 推荐
    Number.isFinite('2e3'); // false
    Number.isFinite(parseInt('2e3', 10)); // true
    ```

**[⬆ back to top](#table-of-contents)**

## 测试 / Testing

  <a name="testing--yup"></a><a name="28.1"></a>
  - [30.1](#testing--yup) **Yup.**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real"></a><a name="28.2"></a>
  - [30.2](#testing--for-real) **不是必须的，但很严肃**:
  - [30.2](#testing--for-real) **No, but seriously**:
    - Whichever testing framework you use, you should be writing tests!
    - Strive to write many small pure functions, and minimize where mutations occur.
    - Be cautious about stubs and mocks - they can make your tests more brittle.
    - We primarily use [`mocha`](https://www.npmjs.com/package/mocha) and [`jest`](https://www.npmjs.com/package/jest) at Airbnb. [`tape`](https://www.npmjs.com/package/tape) is also used occasionally for small, separate modules.
    - 100% test coverage is a good 推荐 goal to strive for, even if it’s not always practical to reach it.
    - Whenever you fix a bug, _write a regression test_. A bug fixed without a regression test is almost certainly going to break again in the future.

**[⬆ back to top](#table-of-contents)**

## 性能 / Performance

  - [On Layout & Web Performance](https://www.kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](https://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](https://jsperf.com/try-catch-in-loop-cost/12)
  - [Bang Function](https://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](https://jsperf.com/jquery-find-vs-context-sel/164)
  - [innerHTML vs textContent for script text](https://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](https://jsperf.com/ya-string-concat/38)
  - [Are JavaScript functions like `map()`, `reduce()`, and `filter()` optimized for traversing arrays?](https://www.quora.com/JavaScript-programming-language-Are-Javascript-functions-like-map-reduce-and-filter-already-optimized-for-traversing-array/answer/Quildreen-Motta)
  - Loading...

**[⬆ back to top](#table-of-contents)**

## 资源 / Resources

**Learning ES6+**

  - [Latest ECMA spec](https://tc39.github.io/ecma262/)
  - [ExploringJS](http://exploringjs.com/)
  - [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
  - [Comprehensive Overview of ES6 Features](http://es6-features.org/)

**推荐阅读 / Read This**

  - [Standard ECMA-262](http://www.ecma-international.org/ecma-262/6.0/index.html)

**工具 / Tools**

  - Code Style Linters
    - [ESlint](https://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    - [JSHint](http://jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
  - Neutrino Preset - [@neutrinojs/airbnb](https://neutrinojs.org/packages/airbnb/)

**其他风格指南 / Other Style Guides**

  - [Google JavaScript风格指南](https://google.github.io/styleguide/jsguide.html)
  - [Google JavaScript风格指南 (Old)](https://google.github.io/styleguide/javascriptguide.xml)
  - [jQuery 核心风格指南](https://contribute.jquery.org/style-guide/js/)
  - [编写原则一致, 惯用的JavaScript / Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)
  - [StandardJS](https://standardjs.com)

**其他风格 / Other Styles**

  - [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [Popular JavaScript Coding Conventions on GitHub](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**更多读物 / Further Reading**

  - [弄懂JavaScript关闭? / Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [针对浮躁码农的基础JavaScript / Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [你可能不需要jQuery / You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 功能 / ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
  - [前端指南 / Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**书籍 / Books**

  - [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](https://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](https://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X) - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](https://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](https://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](https://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](https://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](https://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](http://jsbooks.revolunet.com/) - Julien Bouquillon
  - [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
  - [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](http://amzn.com/0321812182) - David Herman
  - [Eloquent JavaScript](http://eloquentjavascript.net/) - Marijn Haverbeke
  - [You Don’t Know JS: ES6 & Beyond](http://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson

**博客 / Blogs**

  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](https://bocoup.com/weblog)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](https://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [nettuts](http://code.tutsplus.com/?s=javascript)

**Podcasts**

  - [JavaScript Air](https://javascriptair.com/)
  - [JavaScript Jabber](https://devchat.tv/js-jabber/)

**[⬆ back to top](#table-of-contents)**

##  / In the Wild

  This is a list of organizations that are using this style guide. Send us a pull request and we'll add you to the list.

  - **123erfasst**: [123erfasst/javascript](https://github.com/123erfasst/javascript)
  - **3blades**: [3Blades](https://github.com/3blades)
  - **4Catalyzer**: [4Catalyzer/javascript](https://github.com/4Catalyzer/javascript)
  - **Aan Zee**: [AanZee/javascript](https://github.com/AanZee/javascript)
  - **Adult Swim**: [adult-swim/javascript](https://github.com/adult-swim/javascript)
  - **Airbnb**: [airbnb/javascript](https://github.com/airbnb/javascript)
  - **AltSchool**: [AltSchool/javascript](https://github.com/AltSchool/javascript)
  - **Apartmint**: [apartmint/javascript](https://github.com/apartmint/javascript)
  - **Ascribe**: [ascribe/javascript](https://github.com/ascribe/javascript)
  - **Avalara**: [avalara/javascript](https://github.com/avalara/javascript)
  - **Avant**: [avantcredit/javascript](https://github.com/avantcredit/javascript)
  - **Axept**: [axept/javascript](https://github.com/axept/javascript)
  - **BashPros**: [BashPros/javascript](https://github.com/BashPros/javascript)
  - **Billabong**: [billabong/javascript](https://github.com/billabong/javascript)
  - **Bisk**: [bisk](https://github.com/Bisk/)
  - **Bonhomme**: [bonhommeparis/javascript](https://github.com/bonhommeparis/javascript)
  - **Brainshark**: [brainshark/javascript](https://github.com/brainshark/javascript)
  - **CaseNine**: [CaseNine/javascript](https://github.com/CaseNine/javascript)
  - **Cerner**: [Cerner](https://github.com/cerner/)
  - **Chartboost**: [ChartBoost/javascript-style-guide](https://github.com/ChartBoost/javascript-style-guide)
  - **Coeur d'Alene Tribe**: [www.cdatribe-nsn.gov](https://www.cdatribe-nsn.gov)
  - **ComparaOnline**: [comparaonline/javascript](https://github.com/comparaonline/javascript-style-guide)
  - **Compass Learning**: [compasslearning/javascript-style-guide](https://github.com/compasslearning/javascript-style-guide)
  - **DailyMotion**: [dailymotion/javascript](https://github.com/dailymotion/javascript)
  - **DoSomething**: [DoSomething/eslint-config](https://github.com/DoSomething/eslint-config)
  - **Digitpaint** [digitpaint/javascript](https://github.com/digitpaint/javascript)
  - **Drupal**: [www.drupal.org](https://www.drupal.org/project/drupal)
  - **Ecosia**: [ecosia/javascript](https://github.com/ecosia/javascript)
  - **Evernote**: [evernote/javascript-style-guide](https://github.com/evernote/javascript-style-guide)
  - **Evolution Gaming**: [evolution-gaming/javascript](https://github.com/evolution-gaming/javascript)
  - **EvozonJs**: [evozonjs/javascript](https://github.com/evozonjs/javascript)
  - **ExactTarget**: [ExactTarget/javascript](https://github.com/ExactTarget/javascript)
  - **Expensify** [Expensify/Style-Guide](https://github.com/Expensify/Style-Guide/blob/master/javascript.md)
  - **Flexberry**: [Flexberry/javascript-style-guide](https://github.com/Flexberry/javascript-style-guide)
  - **Gawker Media**: [gawkermedia](https://github.com/gawkermedia/)
  - **General Electric**: [GeneralElectric/javascript](https://github.com/GeneralElectric/javascript)
  - **Generation Tux**: [GenerationTux/javascript](https://github.com/generationtux/styleguide)
  - **GoodData**: [gooddata/gdc-js-style](https://github.com/gooddata/gdc-js-style)
  - **GreenChef**: [greenchef/javascript](https://github.com/greenchef/javascript)
  - **Grooveshark**: [grooveshark/javascript](https://github.com/grooveshark/javascript)
  - **Grupo-Abraxas**: [Grupo-Abraxas/javascript](https://github.com/Grupo-Abraxas/javascript)
  - **Happeo**: [happeo/javascript](https://github.com/happeo/javascript)
  - **Honey**: [honeyscience/javascript](https://github.com/honeyscience/javascript)
  - **How About We**: [howaboutwe/javascript](https://github.com/howaboutwe/javascript-style-guide)
  - **Huballin**: [huballin](https://github.com/huballin/)
  - **HubSpot**: [HubSpot/javascript](https://github.com/HubSpot/javascript)
  - **Hyper**: [hyperoslo/javascript-playbook](https://github.com/hyperoslo/javascript-playbook/blob/master/style.md)
  - **InterCity Group**: [intercitygroup/javascript-style-guide](https://github.com/intercitygroup/javascript-style-guide)
  - **Jam3**: [Jam3/Javascript-Code-Conventions](https://github.com/Jam3/Javascript-Code-Conventions)
  - **JeopardyBot**: [kesne/jeopardy-bot](https://github.com/kesne/jeopardy-bot/blob/master/STYLEGUIDE.md)
  - **JSSolutions**: [JSSolutions/javascript](https://github.com/JSSolutions/javascript)
  - **Kaplan Komputing**: [kaplankomputing/javascript](https://github.com/kaplankomputing/javascript)
  - **KickorStick**: [kickorstick](https://github.com/kickorstick/)
  - **Kinetica Solutions**: [kinetica/javascript](https://github.com/kinetica/Javascript-style-guide)
  - **LEINWAND**: [LEINWAND/javascript](https://github.com/LEINWAND/javascript)
  - **Lonely Planet**: [lonelyplanet/javascript](https://github.com/lonelyplanet/javascript)
  - **M2GEN**: [M2GEN/javascript](https://github.com/M2GEN/javascript)
  - **Mighty Spring**: [mightyspring/javascript](https://github.com/mightyspring/javascript)
  - **MinnPost**: [MinnPost/javascript](https://github.com/MinnPost/javascript)
  - **MitocGroup**: [MitocGroup/javascript](https://github.com/MitocGroup/javascript)
  - **ModCloth**: [modcloth/javascript](https://github.com/modcloth/javascript)
  - **Money Advice Service**: [moneyadviceservice/javascript](https://github.com/moneyadviceservice/javascript)
  - **Muber**: [muber](https://github.com/muber/)
  - **National Geographic**: [natgeo](https://github.com/natgeo/)
  - **Nimbl3**: [nimbl3/javascript](https://github.com/nimbl3/javascript)
  - **NullDev**: [NullDevCo/JavaScript-Styleguide](https://github.com/NullDevCo/JavaScript-Styleguide)
  - **Nulogy**: [nulogy/javascript](https://github.com/nulogy/javascript)
  - **Orange Hill Development**: [orangehill/javascript](https://github.com/orangehill/javascript)
  - **Orion Health**: [orionhealth/javascript](https://github.com/orionhealth/javascript)
  - **OutBoxSoft**: [OutBoxSoft/javascript](https://github.com/OutBoxSoft/javascript)
  - **Peerby**: [Peerby/javascript](https://github.com/Peerby/javascript)
  - **Pier 1**: [Pier1/javascript](https://github.com/pier1/javascript)
  - **Qotto**: [Qotto/javascript-style-guide](https://github.com/Qotto/javascript-style-guide)
  - **Razorfish**: [razorfish/javascript-style-guide](https://github.com/razorfish/javascript-style-guide)
  - **reddit**: [reddit/styleguide/javascript](https://github.com/reddit/styleguide/tree/master/javascript)
  - **React**: [facebook.github.io/react/contributing/how-to-contribute.html#style-guide](https://facebook.github.io/react/contributing/how-to-contribute.html#style-guide)
  - **REI**: [reidev/js-style-guide](https://github.com/rei/code-style-guides/)
  - **Ripple**: [ripple/javascript-style-guide](https://github.com/ripple/javascript-style-guide)
  - **Sainsbury’s Supermarkets**: [jsainsburyplc](https://github.com/jsainsburyplc)
  - **SeekingAlpha**: [seekingalpha/javascript-style-guide](https://github.com/seekingalpha/javascript-style-guide)
  - **Shutterfly**: [shutterfly/javascript](https://github.com/shutterfly/javascript)
  - **Sourcetoad**: [sourcetoad/javascript](https://github.com/sourcetoad/javascript)
  - **Springload**: [springload](https://github.com/springload/)
  - **StratoDem Analytics**: [stratodem/javascript](https://github.com/stratodem/javascript)
  - **SteelKiwi Development**: [steelkiwi/javascript](https://github.com/steelkiwi/javascript)
  - **StudentSphere**: [studentsphere/javascript](https://github.com/studentsphere/guide-javascript)
  - **SwoopApp**: [swoopapp/javascript](https://github.com/swoopapp/javascript)
  - **SysGarage**: [sysgarage/javascript-style-guide](https://github.com/sysgarage/javascript-style-guide)
  - **Syzygy Warsaw**: [syzygypl/javascript](https://github.com/syzygypl/javascript)
  - **Target**: [target/javascript](https://github.com/target/javascript)
  - **Terra**: [terra](https://github.com/cerner?utf8=%E2%9C%93&q=terra&type=&language=)
  - **TheLadders**: [TheLadders/javascript](https://github.com/TheLadders/javascript)
  - **The Nerdery**: [thenerdery/javascript-standards](https://github.com/thenerdery/javascript-standards)
  - **Tomify**: [tomprats](https://github.com/tomprats)
  - **Traitify**: [traitify/eslint-config-traitify](https://github.com/traitify/eslint-config-traitify)
  - **T4R Technology**: [T4R-Technology/javascript](https://github.com/T4R-Technology/javascript)
  - **UrbanSim**: [urbansim](https://github.com/urbansim/)
  - **VoxFeed**: [VoxFeed/javascript-style-guide](https://github.com/VoxFeed/javascript-style-guide)
  - **WeBox Studio**: [weboxstudio/javascript](https://github.com/weboxstudio/javascript)
  - **Weggo**: [Weggo/javascript](https://github.com/Weggo/javascript)
  - **Zillow**: [zillow/javascript](https://github.com/zillow/javascript)
  - **ZocDoc**: [ZocDoc/javascript](https://github.com/ZocDoc/javascript)

**[⬆ back to top](#table-of-contents)**

## 翻译 / Translation

  This style guide is also available in other languages:

  - ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [armoucar/javascript-style-guide](https://github.com/armoucar/javascript-style-guide)
  - ![bg](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bulgaria.png) **Bulgarian**: [borislavvv/javascript](https://github.com/borislavvv/javascript)
  - ![ca](https://raw.githubusercontent.com/fpmweb/javascript-style-guide/master/img/catala.png) **Catalan**: [fpmweb/javascript-style-guide](https://github.com/fpmweb/javascript-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [lin-123/javascript](https://github.com/lin-123/javascript)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [jigsawye/javascript](https://github.com/jigsawye/javascript)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [nmussy/javascript-style-guide](https://github.com/nmussy/javascript-style-guide)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [timofurrer/javascript-style-guide](https://github.com/timofurrer/javascript-style-guide)
  - ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [sinkswim/javascript-style-guide](https://github.com/sinkswim/javascript-style-guide)
  - ![jp](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/javascript-style-guide](https://github.com/mitsuruog/javascript-style-guide)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [ParkSB/javascript-style-guide](https://github.com/ParkSB/javascript-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [leonidlebedev/javascript-airbnb](https://github.com/leonidlebedev/javascript-airbnb)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [paolocarrasco/javascript-style-guide](https://github.com/paolocarrasco/javascript-style-guide)
  - ![th](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Thailand.png) **Thai**: [lvarayut/javascript-style-guide](https://github.com/lvarayut/javascript-style-guide)
  - ![tr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Turkey.png) **Turkish**: [eraycetinay/javascript](https://github.com/eraycetinay/javascript)
  - ![ua](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Ukraine.png) **Ukrainian**: [ivanzusko/javascript](https://github.com/ivanzusko/javascript)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnam**: [dangkyokhoang/javascript-style-guide](https://github.com/dangkyokhoang/javascript-style-guide)

## JavaScript风格指南 / The JavaScript Style Guide Guide

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

## Chat With Us About JavaScript

  - Find us on [gitter](https://gitter.im/airbnb/javascript).

## Contributors

  - [View Contributors](https://github.com/airbnb/javascript/graphs/contributors)

## License

(The MIT License)

Copyright (c) 2012 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**

## Amendments

We encourage you to fork this guide and change the rules to fit your team’s style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };
