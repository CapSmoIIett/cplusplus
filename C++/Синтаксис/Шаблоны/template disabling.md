#Syntax

Для этого шаблон надо переписать в следующем виде:
```c++
template<
	typename T, 
	typename S = std::enable_if_t<!std::is_integral<T>::value>>
	void Foo(T x);
```

Теперь для целочисленных аргументов этот шаблон нельзя конкретизировать и в соответствии с принципом [[SFINAE]] он будет исключен при разрешении перегрузки и, таким образом, будет выбрана нешаблонная функция и выполнены необходимые неявные преобразования аргументов.

- **`std::is_integral<T>::value`**: Это выражение проверяет, является ли тип `T` целочисленным. Если тип целочисленный, то `std::is_integral<T>::value` возвращает `true`.
- **`std::enable_if_t<...>`**: Если условие внутри `std::enable_if_t` истинно (т.е., тип не целочисленный), то `std::enable_if_t` предоставляет тип `void`. Если условие ложно (т.е., тип целочисленный), то `std::enable_if_t` не предоставляет никакого типа, что приводит к ошибке подстановки (SFINAE).


- Если тип `T` не является целочисленным (например, `float`, `double`, `std::string`), то функция `Foo(T x)` может быть вызвана без ошибок.
- Если тип `T` целочисленный (например, `int`, `unsigned int`), то попытка вызвать `Foo(T x)` приведет к ошибке компиляции из-за неудачной подстановки (SFINAE), поскольку `std::enable_if_t` не предоставит никакого типа.