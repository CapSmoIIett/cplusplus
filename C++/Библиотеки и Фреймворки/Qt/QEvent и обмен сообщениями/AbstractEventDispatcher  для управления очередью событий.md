#Qt

`QAbstractEventDispatcher` — это базовый класс в Qt, который предоставляет интерфейс для управления очередью событий. Он играет ключевую роль в обработке событий, полученных из системы окна и других источников, и передаче их экземпляру `QCoreApplication` или `QApplication` для дальнейшей обработки и доставки.

Именно он взаимодействует с ивентами операционной системы и добавляет их в стэк.
#### Использование в потоках

У каждого потока может быть только один экземпляр `QAbstractEventDispatcher`, который устанавливается однажды. Это позволяет легко заменить диспетчер на более подходящий, если это необходимо, без изменения кода, использующего `QEventLoop`.

```c++
// Получение экземпляра диспетчера 
QAbstractEventDispatcher *dispatcher = QAbstractEventDispatcher::instance(); 

// Обработка событий 
dispatcher->processEvents(QEventLoop::AllEvents);
```