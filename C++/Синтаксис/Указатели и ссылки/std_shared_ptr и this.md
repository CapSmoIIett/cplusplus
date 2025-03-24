
Создавть std::shared_ptr с помощью *this* - плохая идея.  

Но если нужно это сделать, используй std::еnаblе_shared_from_this.
std::еnаblе_shared_from_this - Это шаблон базового класса, который вы наследуете,
если хотите, чтобы класс, управляемый указателями std::shared_ptr, был способен
безопасно создавать std::shared_ptr из указателя this.

(std::enable_shared_from_this/<T/> - [[CRTP]])

Шаблое std::enable_shared_from_this - определяет функцию член, которая создает std::shared_ptr для this (shared_from_this).
При этом он не дублирует управляющие блоки.

```C++
class Widget : public std::enable_shared_from_this<Widget>
{
public:
    void process( )
    {
        array.emplace_back(shared_from_this());
    }
};
```

std::shared_from_this - внутри ищет управляющий блок объекта и создает  std::share_ptr, который использует этот же управляющий блок.
НО для этого управляющий блок должен быть создан.

Чтобы препятствовать вызову функции-члена, в которой используется shared_from_this, до того как на объект будет указывать указатель std::shared_ptr, классы, наследуемые от std::enable_shared_from_this, часто объявляют свои конструкторы как  private и заставляют клиентов создавать объекты путем вызова фабричных функций,  которые возвращают указатели std::shared_ptr.

```C++
class Widget : public std::enable_shared_from_this<Widget>
{
public:
    template<typename Ts>
    static std::shared_ptr<Widget> create(Ts&& ... params )  // Фабричная функция

private:
    // конструкторы

};
```
