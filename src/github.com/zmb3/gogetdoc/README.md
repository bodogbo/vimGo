gogetdoc
========

[![Build Status](https://travis-ci.org/zmb3/gogetdoc.svg?branch=master)](https://travis-ci.org/zmb3/gogetdoc)

Retrieve documentation for items in Go source code.

Go has a variety of tools that make it easy to lookup documentation.
There's the `godoc` HTTP server, the `go doc` command line tool, and https://godoc.org.

These tools are great, but in many cases one may find it valuable to lookup
documentation right from their editor.  The problem with all of these tools
is that they are all meant to be used by a person who knows what they are
looking for.  This makes editor integration difficult, as there isn't an easy way
to say "get me the documentation for this item here."

The `gogetdoc` tool aims to make it easier for editors to provide access to
Go documentation.  Simply give it a filename and offset within the file and
it will figure out what you're referring to and find the documentation
for it.

## Prerequisites

This tool relies on the `go/types` package, which **requires Go 1.6**.

If you attempt to install the tool with an earlier version of Go, you may see
the following error:

```
$ go get github.com/zmb3/gogetdoc
# github.com/zmb3/gogetdoc
gogetdoc\ident.go:17: impossible type assertion:
        *"golang.org/x/tools/go/types".PkgName does not implement "go/types".Object (wrong type for Parent method)
                have Parent() *"golang.org/x/tools/go/types".Scope
                want Parent() *"go/types".Scope
```

## Usage

Simply specify a filename and _byte_ offset with the `pos` flag:

```
$ gogetdoc -pos $GOROOT/src/fmt/format.go:#6274
func unicode/utf8.RuneCountInString(s string) (n int)

RuneCountInString is like RuneCount but its input is a string.

```

### Unsaved files

`gogetdoc` supports the same archive format as `guru` (formerly `oracle`).
Editors can supply `gogetdoc` with the contents of unsaved buffers by
using the `-modified` flag and writing an archive to stdin.  
Files in the archive will be preferred over those on disk.

Each archive entry consists of:
 - the file name, followed by a newline
 - the (decimal) file size, followed by a newline
 - the contents of the file

## Contributions

Are more than welcome!  For small changes feel free to open a pull request.
For larger changes or major features please open an issue to discuss.

## Credits

The following resources served as both inspiration for starting this tool
and help coming up with the implementation.

- Alan Donovan's GothamGo talk "Using `go/types` for Code Comprehension
  and Refactoring Tools" https://youtu.be/p_cz7AxVdfg
- Fatih Arslan's talk at dotGo 2015 "Tools for working with Go Code"
- The `go/types` example repository: https://github.com/golang/example/tree/master/gotypes

## License

3-Clause BSD license - see the LICENSE file for details.
