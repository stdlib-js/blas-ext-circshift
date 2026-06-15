<!--

@license Apache-2.0

Copyright (c) 2026 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# circshift

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Circularly shift the elements of an input [ndarray][@stdlib/ndarray/ctor] by a specified number of positions along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.



<section class="usage">

## Usage

To use in Observable,

```javascript
circshift = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-circshift@umd/browser.js' )
```

To vendor stdlib functionality and avoid installing dependency trees for Node.js, you can use the UMD server build:

```javascript
var circshift = require( 'path/to/vendor/umd/blas-ext-circshift/index.js' )
```

To include the bundle in a webpage,

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-circshift@umd/browser.js"></script>
```

If no recognized module system is present, access bundle contents via the global scope:

```html
<script type="text/javascript">
(function () {
    window.circshift;
})();
</script>
```

#### circshift( x, k\[, options] )

Circularly shifts the elements of an input [ndarray][@stdlib/ndarray/ctor] by a specified number of positions along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ 1.0, 2.0, 3.0, 4.0, 5.0 ] );
// returns <ndarray>[ 1.0, 2.0, 3.0, 4.0, 5.0 ]

var y = circshift( x, 2 );
// returns <ndarray>[ 4.0, 5.0, 1.0, 2.0, 3.0 ]

var bool = ( x === y );
// returns true
```

The function has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor].
-   **k**: number of positions to shift. May be either an integer scalar value or an [ndarray][@stdlib/ndarray/ctor] having a real-valued or "generic" [data type][@stdlib/ndarray/dtypes]. If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dims`. For example, given the input shape `[2, 3, 4]` and `options.dims=[0]`, an [ndarray][@stdlib/ndarray/ctor] for `k` must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`. Similarly, when performing the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor], an [ndarray][@stdlib/ndarray/ctor] for `k` must be a zero-dimensional [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).

The function accepts the following options:

-   **dims**: list of dimensions over which to perform operation. If not provided, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].

By default, the function circularly shifts all elements. To perform the operation over specific dimensions, provide a `dims` option.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ 1.0, 2.0, 3.0, 4.0 ], {
    'shape': [ 2, 2 ],
    'order': 'row-major'
});
// returns <ndarray>[ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ]

var y = circshift( x, 1, {
    'dims': [ 0 ]
});
// returns <ndarray>[ [ 3.0, 4.0 ], [ 1.0, 2.0 ] ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   The input [ndarray][@stdlib/ndarray/ctor] is shifted **in-place** (i.e., the input [ndarray][@stdlib/ndarray/ctor] is **mutated**).
-   When shifting elements along a single dimension, a positive `k` shifts elements to the right (toward higher indices), and a negative `k` shifts elements to the left (toward lower indices). If `k` is zero, the input [ndarray][@stdlib/ndarray/ctor] is left unchanged.
-   The function iterates over [ndarray][@stdlib/ndarray/ctor] elements according to the memory layout of the input [ndarray][@stdlib/ndarray/ctor]. Accordingly, performance degradation is possible when operating over multiple dimensions of a large non-contiguous multi-dimensional input [ndarray][@stdlib/ndarray/ctor]. In such scenarios, one may want to copy an input [ndarray][@stdlib/ndarray/ctor] to contiguous memory before performing the circular shift.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/random-discrete-uniform@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-circshift@umd/browser.js"></script>
<script type="text/javascript">
(function () {

// Generate an ndarray of random numbers:
var x = discreteUniform( [ 5, 5 ], -20, 20, {
    'dtype': 'generic'
});
console.log( ndarray2array( x ) );

// Perform operation:
circshift( x, 2, {
    'dims': [ 0 ]
});

// Print the results:
console.log( ndarray2array( x ) );

})();
</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-ext-circshift.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-ext-circshift

[test-image]: https://github.com/stdlib-js/blas-ext-circshift/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/blas-ext-circshift/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-ext-circshift/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-ext-circshift?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-ext-circshift.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-ext-circshift/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-ext-circshift/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-ext-circshift/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-ext-circshift/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-ext-circshift/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-ext-circshift/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-ext-circshift/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-ext-circshift/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-ext-circshift/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/umd

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes/tree/umd

[@stdlib/ndarray/base/broadcast-shapes]: https://github.com/stdlib-js/ndarray-base-broadcast-shapes/tree/umd

</section>

<!-- /.links -->
