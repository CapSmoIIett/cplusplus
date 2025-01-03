

Альтернативные имена стандартных атомарных типов и соответствующие им специализации std::atomic:

| Атомарный тип   | Соответствующая специализация atomic_bool std::atomic |
| --------------- | ----------------------------------------------------- |
| atomic_bool<br> | std::atomic bool                                      |
| atomic_char     | std::atomic cahr                                      |
| atomic_schar    | std::atomic signed char                               |
| atomic_uhar     | std::atomic unsigned char                             |
| atomic_int      | std::atomic int                                       |
| atomic_uint     | std::atomic unsigned                                  |
| atomic_short    | std::atomic short                                     |
| atomic_ushort   | std::atomic unsigned short                            |
| atomic_long     | std::atomic long                                      |
| atomic_ulong    | std::atomic unsigned long                             |
| atomic_llong    | std::atomic long long                                 |
| atomic_ullong   | std::atomic unsigned long long                        |
| atomic_char16_t | std::atomic char16_t                                  |
| atomic_char32_t | std::atomic char32_t                                  |
| atomic_wchar_t  | std::atomic wchar_t                                   |
Помимо основных атомарных типов, в стандартной библиотеке C++ определены также псевдонимы typedef для атомарных типов, соответствующих различным неатомарным библиотечным typedef, например std::size_t. 
Атомарный тип, соответствующий стандартному typedef T, имеет такое же имя с префиксом atomic_: atomic_T

Стандартные атомарные типы не допускают копирования и присваивания в обычном смысле, то есть не имеют копирующих конструкторов и операторов присваивания

операции разбиты на три категории . 
- Операции сохранения , для которых можно задавать упорядочение 
	- memory_order_relaxed, 
	- memory_order_release,
	- memory_order_seq_cst. 
- Операции загрузки , для которых можно задавать упорядочение 
	- memory_order_relaxed, 
	- memory_order_consume, 
	- memory_ order_acquire,
	- memory_order_seq_cst 
- Операции чтения-модификации-записи, для которых можно задавать упорядочение 
	- memory_order_relaxed, 
	- memory_ order_consume, 
	- memory_order_acquire, 
	- memory_order_ release, 
	- memory_order_acq_rel,
	- memory_order_seq_cst. 
По умолчанию для всех операций подразумевается упорядочение memory_order_seq_cst.