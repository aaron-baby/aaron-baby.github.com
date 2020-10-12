>Reflection in computing is the ability of a program to examine its own structure, particularly through types; 
>it's a form of metaprogramming. It's also a great source of confusion.

反射
> 1. Reflection goes from interface value to reflection object.

the signature of `reflect.TypeOf` includes an empty interface:

    func TypeOf(i interface{}) Type


从 interface{} 变量可以反射出反射对象
> 2. Reflection goes from reflection object to interface value.
