# go1.18-generics

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
