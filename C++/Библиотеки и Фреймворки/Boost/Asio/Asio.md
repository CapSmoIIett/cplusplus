# Boost.Asio

**Boost.Asio** — это кроссплатформенная библиотека для организации ввода-вывода (I/O) в C++: сетевого, файлового, таймеров и др. Поддерживает как синхронный, так и асинхронный режимы работы.

---

## Основные возможности
- Асинхронная и синхронная работа с TCP, UDP, UNIX-сокетами, сериал-портами, таймерами и др.
- Поддержка event loop (io_context).
- Высокая производительность и масштабируемость.
- Совместимость с стандартом C++11 и выше.
- Поддержка coroutines (C++20) и future/promise.
- Используется как часть Boost, а также как отдельная библиотека (standalone Asio).

## Архитектура
- **io_context** — основной объект для управления событиями и асинхронными операциями (event loop).
- **socket** — абстракция для работы с сетевыми соединениями (tcp::socket, udp::socket и др.).
- **resolver** — DNS-резолвер для преобразования имён в адреса.
- **timer** — таймеры для асинхронных задержек (steady_timer, deadline_timer).
- **strand** — механизм для сериализации вызовов обработчиков (thread safety).

## Пример: асинхронный TCP-клиент
```cpp
#include <boost/asio.hpp>
#include <iostream>

using boost::asio::ip::tcp;

int main() {
    boost::asio::io_context io;
    tcp::resolver resolver(io);
    auto endpoints = resolver.resolve("example.com", "80");
    tcp::socket socket(io);
    boost::asio::async_connect(socket, endpoints,
        [&](const boost::system::error_code& ec, const tcp::endpoint&) {
            if (!ec) {
                std::cout << "Connected!" << std::endl;
            }
        });
    io.run();
}
```

## Асинхронные операции
- Все асинхронные методы принимают callback (completion handler), который вызывается по завершении операции.
- Для интеграции с coroutines (C++20) используются co_await и awaitable.

## Пример: асинхронный таймер с coroutines
```cpp
#include <boost/asio.hpp>
#include <iostream>

boost::asio::awaitable<void> timer_example() {
    boost::asio::steady_timer timer(co_await boost::asio::this_coro::executor);
    timer.expires_after(std::chrono::seconds(1));
    co_await timer.async_wait(boost::asio::use_awaitable);
    std::cout << "Timer fired!" << std::endl;
}

int main() {
    boost::asio::io_context io;
    boost::asio::co_spawn(io, timer_example(), boost::asio::detached);
    io.run();
}
```

## Особенности
- Для масштабируемости можно запускать несколько потоков с одним io_context.
- Поддерживает интеграцию с std::future, std::thread, coroutines.
- Позволяет реализовывать высоконагруженные серверы, клиенты, прокси, таймеры и др.

## Важно
- Boost.Asio — де-факто стандарт для асинхронного I/O в C++.
- Требует внимательного проектирования логики обработки событий и ошибок.
- Для production-кода рекомендуется использовать обработку ошибок через boost::system::error_code.
