# Lisp Test Runner

![SBCL-Tests](https://github.com/qitab/ace.test/workflows/SBCL-Tests/badge.svg)
[![Gitter](https://badges.gitter.im/qitab/community.svg)](https://gitter.im/qitab/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

This library is a test runner for `lisp_test` rules. To use it, just define a
`lisp_test` rule which has `//lisp/test` in its deps:

```build
load("//lisp/devtools/bazel:rules.bzl", "lisp_library", "lisp_test")

lisp_test(
  name = "foo-test",
  srcs = ["foo-test.lisp"],
  deps = [
    ":foo",
    "//lisp/test",
  ],
)
```

Then use the `ace.test` package. This gives an access to the `deftest` macro
to define a tests and `expect` or `check` to implement test assertions:

```lisp
(defpackage #:foo-test
  (:use #:common-lisp #:ace.test #:foo))

(in-package #:foo-test)

(deftest test-something ()
  (expect (equal (something) expected-value)))
```

When running the tests from Blaze one can limit the execution to specific test
names with the [`--test_filter`](https://docs.bazel.build/versions/master/command-line-reference.html)
option. For Lisp, that takes a value of test function names, comma-separated,
with or without package prefix (go/testfilter).

This is a test

### Disclaimer: This is not an official Google product.
