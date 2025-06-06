
**Curiously Recurring Template Pattern (CRTP)** идиома языка C++, название которой можно примерно перевести как Странно рекурсивный шаблон или Странно повторяющийся шаблон, часто просто Рекурсивный Шаблон, состоящая в том, что некоторый класс X наследуется от шаблона класса, использующего X как шаблонный параметр.

```c++
template <typename Derived>
class Base {
public:
    void interface() {
        // Вызов метода производного класса через static_cast
        static_cast<Derived*>(this)->implementation();
    }
};

class Derived : public Base<Derived> {
public:
    void implementation() {
        std::cout << "Derived implementation\n";
    }
};

int main() {
    Derived obj;
    obj.interface(); // Вывод: "Derived implementation"
    return 0;
}

```
#### Как это работает
1. **Шаблонный базовый класс**:
    - Базовый класс (`Base`) принимает тип производного класса (`Derived`) в качестве аргумента шаблона.
    - Это позволяет базовому классу вызывать методы производного класса через приведение `static_cast`.
2. **Наследование**:
    - Производный класс наследуется от базового класса, передавая свой собственный тип (`Derived`) в шаблон.
3. **Статический полиморфизм**:
    - Вызов методов производного класса происходит во время компиляции, что исключает накладные расходы на динамический полиморфизм (таблицы виртуальных функций).
#### Преимущества CRTP
- **Статический [[Полиморфизм]]**:  
    Позволяет эмулировать поведение виртуальных функций без затрат на динамическое определение типа.
- **Оптимизация производительности**:  
    Уменьшение накладных расходов, связанных с динамическим полиморфизмом.
- **Гибкость**:  
    Базовый класс может предоставлять общий интерфейс или добавлять функциональность производному классу.
	
[Классно работает с паттерном мост](https://habr.com/ru/articles/543098/)
[[мост]]