В C++ классы могут быть сделаны _non-copyable_ (некопируемыми) и/или _non-movable_ (неперемещаемыми) с помощью удаления соответствующих конструкторов и операторов. Это полезно для управления ресурсами.

[[Конструкторы]]
### **Non-copyable**

Класс считается _non-copyable_, если его конструктор копирования и оператор присваивания копированием явно удалены. Это предотвращает создание копий объекта, что важно для классов, управляющих уникальными ресурсами, например `std::unique_ptr`.

```c++
class NonCopyable
{
  public: 
    NonCopyable (const NonCopyable &) = delete;
    NonCopyable & operator = (const NonCopyable &) = delete;

  protected:
    NonCopyable () = default;
    ~NonCopyable () = default; /// Protected non-virtual destructor
};
class CantCopy : private NonCopyable
{};
```

Класс, наследующийся от `NonCopyable`, не сможет быть скопирован.
Попытка копирования приведет к ошибке компиляции.

[Источник](https://en.wikibooks.org/wiki/More_C%2B%2B_Idioms/Non-copyable_Mixin)

### **Non-Moveable**

Класс становится _non-movable_, если его конструктор перемещения и оператор присваивания перемещением удалены. Это полезно для объектов, которые не должны менять свое местоположение в памяти (например, `std::mutex`).

```c++
class NonMovable {
protected:
    NonMovable() = default;
    ~NonMovable() = default;

    NonMovable(NonMovable&&) = delete;
    NonMovable& operator=(NonMovable&&) = delete;
};
```

Класс, наследующийся от `NonMovable`, не сможет быть перемещен.
Попытка перемещения также приведет к ошибке компиляции.