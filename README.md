Gmp
===

This package provides a drop in replacement for Go's built in
[math/big](http://golang.org/pkg/math/big/) big integer package using
the [GNU Multiprecision Library](http://gmplib.org/) (GMP).

GMP is very much faster than Go's math/big however it is an external C
library with all the problems that entails (cgo, dependencies etc)

This library was made by taking the [cgo example of wrapping
GMP](http://golang.org/misc/cgo/gmp/gmp.go) from the Go source and
doing the following to it

* Copying the implementation from misc/cgo/gmp/gmp.go
* Copying the documentation from src/pkg/math/big/int.go
* Additional implementation of missing methods
* Bug fixes for existing implementations
* Making it passes the test suite from src/pkg/math/big/int_test.go
* Adding memory management
* Fix problems on 32 bit platforms when using `int64` values which don't fit into a `C.long`
* Implementing Rat support making it pass src/pkg/math/big/rat_test.go

See here for package docs

* http://go.pkgdoc.org/github.com/ncw/gmp

Install
-------

This package is intended as full replacement for go math/big package, so installation is a bit harder than "go get":

    cd $GOROOT/src/pkg/math
    rm -rf big
    git clone https://github.com/YuriyNasretdinov/big.git
    cd $GOROOT/src
    ./all.bash # all tests, including encryption and math/big itself should pass

Testing
-------

To run the tests use

    cd $GOROOT/src/pkg/math/big && go test

The tests have been copied from the tests for the math/big library in
the Go source and modified as little as possible so it should be 100%
compatible.

Differences
-----------

Here are the differences between math/big and this package

* `Int.SetBits` not implemented
* `Rat.Num()` and `Rat.Denom()` return a copy not a reference, so
*  If you want to set them use the new methods `Rat.SetNum()` and `Rat.SetDenom()`


License
-------

As this contains a great deal of code copied from the Go source it is
licenced identically to the Go source itself - see the LICENSE file
for details.

Contact and support
-------------------

The project website is at:

* https://github.com/ncw/gmp

There you can file bug reports, ask for help or contribute patches.

Authors
-------

* [The Go team](http://golang.org/AUTHORS)
* Nick Craig-Wood <nick@craig-wood.com>

Contributors
------------

* Yuriy Nasretdinov
