# go1.18-generics

Useful resources 
1. https://go.dev/blog/go1.18beta1
1. https://tip.golang.org/doc/go1.18
1. https://go.dev/doc/tutorial/generics

### Prerequisites
An installation of Go 1.18 Beta 1 or later.

## generics syntax 

Syntax is pretty straightforward, add your generics definitions inside `[]` before function arguments.

```go
func DoSomething[MyGenericType any](myType MyGenericType) {
  log.Println(myType)
}
```

https://go.dev/play/p/GZxLfxLh5I5?v=gotip

## generics types 

You can use any golang type or even your own type.

```go
func DoSomething[MyGenericType string | int | MyType](myType MyGenericType) {
	log.Println(myType)
}
```

https://go.dev/play/p/Y7CJaVCXA_r?v=gotip

## derived types

Another nice thing is type approximation symbolized with `~`. It means that if `[MyGenericType ~int]` is defined it will match int and any other type
derived types of int like `type MySpecialInt int`.

```go
func DoSomething[MyGenericType ~int](input MyGenericType) {
	log.Println(input)
}
```

https://go.dev/play/p/IRpD0KIk7YO?v=gotip

## compareable 

One problem you can imagine is type comparison, for example that won't work. 
```go
func DoSomething[MyGenericType any](x, y MyGenericType) {
	log.Println(x == y)
}
```
`./prog.go:12:14: invalid operation: cannot compare x == y (operator == not defined on MyGenericType)`


Quick and easy way is use bulit in `comparable`.
```go
func DoSomething[MyGenericType comparable](x, y MyGenericType) {
	log.Println(x == y)
}
```

https://go.dev/play/p/McLvq6zy2f-?v=gotip

## generated code

Let's say we use `any` - does it mean that we gonna have performance impact ? not really. Complier will optimize the generated code like any other code, only used types will be generated. For example we asked for `any` but we have used that function only with strings, generated code will be `2eshape_string_0` only. 

![image](https://user-images.githubusercontent.com/4710984/147643964-511739e8-254e-4c63-a574-7a47d9fc26f9.png)

https://godbolt.org/z/q5MKhTKvs

![image](https://user-images.githubusercontent.com/4710984/147644148-465f6c62-2c67-4d45-9dcc-d307e1fa0c93.png)

https://godbolt.org/z/rbW9K4sjT


