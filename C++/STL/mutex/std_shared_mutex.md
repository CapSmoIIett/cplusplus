# std::shared_mutex

`std::shared_mutex` — это примитив синхронизации из C++17, который позволяет нескольким потокам одновременно получать доступ к ресурсу для чтения (shared lock), но только одному потоку — для записи (unique lock).

## Основные особенности
- **Shared lock (разделяемая блокировка):** Несколько потоков могут одновременно захватывать shared_mutex для чтения с помощью `lock_shared()` или `shared_lock`.
- **Unique lock (уникальная блокировка):** Только один поток может захватить shared_mutex для записи с помощью `lock()` или `unique_lock`. В это время другие потоки не могут получить ни shared, ни unique lock.
- **Использование:**
  - Для чтения: `std::shared_lock<std::shared_mutex> lock(mtx);`
  - Для записи: `std::unique_lock<std::shared_mutex> lock(mtx);`

## Пример использования
```cpp
#include <shared_mutex>
#include <thread>
#include <vector>

std::shared_mutex mtx;
int data = 0;

void reader() {
    std::shared_lock lock(mtx);
    // Чтение data
}

void writer() {
    std::unique_lock lock(mtx);
    // Изменение data
}
```

## Когда использовать
- Когда требуется частый параллельный доступ к ресурсу для чтения и редкий — для записи.
- Для реализации thread-safe кэшей, справочников, конфигураций и т.п.

## Отличие от std::mutex
- `std::mutex` допускает только эксклюзивную блокировку (только один поток — читатель или писатель).
- `std::shared_mutex` позволяет множественный доступ для чтения, что повышает производительность в сценариях с преобладанием чтения.
