#UnrealEngine

- Базовый класс для Actor, ActorComponent и еще 4284 объектов (не считая того, что придумаете Вы)
- В том числе базовый для классов рефлексии UСlass, UProperty и т.д
- Автоматическая инициализация свойств (через FObjectInitializer)
- Runtime type information и приведение типов (Cast) (стандартный dynamic-cast не работает, т.к. не работает на ps4)
- Сетевая репликация
- Поддерживает подсчет ссылок и сборку мусора (garbage collection)