# GoRazor

GoRazor is the Go port of the razor template engine originated from [asp.net world](http://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx).

This port is essentially a re-port from razor's port in javascript: [vash](https://github.com/kirbysayshi/vash).

It modifies on vast's generation function to emit go code instead of javascript code.

In summay, GoRazor is:

* Consice syntax
* Able to mix go code in template
  * import is supported
  * Call arbitrary functions
* Take code generation approach, i.e. no reflection overhead
* Strong type template model
* Utils class

# Rules

## Naming

* Template *folder name* will be used as *package name* in generated code
* Template file name must has the extension name `.gohtml`
* Template strip of `.gohtml` extension name will be used as the *function name* in generated code, with *fisrt letter Capitalized*.
  * So that the function will be accessible to other modules. (I hate GO about this.)
* Helper templates *must* has the package name *helper*

## Decleration

The *first code block* in template is strictly for decleration:

* imports
* model type
* layout

like:

```
@{
	import  (
		"kp/models"
	)
	var totalMessage int
	var u *kpm.User
}
....
```

*first code block* must be at the begining of the template, i.e. before any html.

Any other codes inside the first code block will *be ignored*.

Must wrapped import in `()`, `import "packagename"` is not yet supported.

# FAQ

TBA

# Todo

* Refactor all the quick & dirty code
* Test suite
* Add tools, like monitor template changes and auto re-generate
* Performance benchmark
* Generate more function overloads, like accept additional buffer parameter for write
* Support direct usage of int/date variables in tempate?
  * i.e. use @user.Level directly, instead of @gorazor.Itoa(user.Level)
