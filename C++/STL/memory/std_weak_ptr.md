
Проблема неизвестного указателя - ситуация когда умный указатель указывает на освобожденную память.

std::weak_ptr - неявляется автономным интелектуальным указателем, это дополнение к std::shared_ptr. 
В нем нет операций разыменования.

std::weak_ptr создается из указателей std::shared_ptr, но не влияют на счетчики ссылок (У них есть свой - weak счетчик), на который указывают.

```c++
auto spw = std::make_shared<Widget>();

std::weak_ptr<Widget> wpw (spw) ;

spw = nullptr;
// после этого объект Widget уничтожается а wpw становиться висячим (просроченым - expired)

if (wpw.expired())  // проверка на то, просрочен ли указатель
```

чтобы из std::weak_ptr получить даные из него нужно сделать std::shared_ptr
Есть два пособа это сделать:

1. std::weak_ptr::lock() - возвращает shared_ptr (нулевой если std::weak_ptr - expired)

```C++
std::shared_ptr<Widget> spw1 = wpw.lock();
auto spw2 = wpw.lock();
```

2.  конcтруктор std::shared_ptr

```c++
std::shared_ptr<Widget> spw(wpw);   // Если wpw просрочен генерирует std::bad_weak_ptr
```

**Для чего нужен std::weak_ptr?**

Пример: есть фабричный метод возвращающий умные указатели. 
Допустим этот метод очень нагружает систему.

Логично использование кэширования для улучшения производительности.
Но большое количество копий объекта очень засорит память.
Тогда кэшировать стоит, когда эти объекты больше нигде в программе не используются.
Тогда данный метод будет возвращать std::shared_ptr, а кэшировать std::weak_ptr.  
Грубая (очень грубая) реализация:

```c++
std::shared_ptr<const Widget> fastLoadWidget (Widget ID id)
{
    static std::unordered_map<WidgetID,
        std::weakytr<const Widget>> cache;
    
    auto obj_ptr = cache[id].lock(); 
    // obj Ptr является std::shared_pt для кешированного объекта и
    // нулевым указателем для объекта, отсутствующего в кеше

    if (!obj_ptr) 
    {
        obj_ptr = loadWidget (id);
        cache[id] = obj_ptr;
        //При отсутствии в кеше объект загружается и кешируется
    }

    return obj Ptr;
}
```

**Второй пример применения:**

Шаблон проектирования [[Observer]]. 
В большинстве реализаций объект за которым наблюдают (субъект) имеет указатели на его наблюдателей.
Каждый субъект хранит контейнер std::weak_ptr на его наблюдателей.

**Еще пример:**

Есть структуры A, B,C. 
A и C имеют указатели на B.
![Пример weak_ptr](images/weak_ptr_1.png)
Нам нужен указатель из B на A, как это лучше делать?  
Варианты:
- **Обычный указатель**. 
В таком случае если A уничтожить, то B сохранит висячий указатель на него.
- **std::shared_ptr**.
Если A и B имеют std::shared_ptr друг на друга то их уничтожение - большая проблема.
- **std::weak_ptr**. 
Этот вариант лишен выше указаных проблем.

std::weak_ptr - соразмерен std::shared_ptr (используют теже управляющие блоки).  
А создание, уничтожение, присваивание - атомарные операции взаимодействующие со счтечиком ссылок(они работают со своим счетчиком ссылок).

- Используйте std::weak_ptr как std::shared_ptr - oбpaзныe указатели, которые могут быть висячими.
- Потенциальные применения std::weak_ptr включают хеширование, списки наблюдателей и предупреждение циклов указателей std::shared_ptr. 