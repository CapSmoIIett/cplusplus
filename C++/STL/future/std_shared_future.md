Устроен на подобии std::shared_ptr.

std::shared_future допускает копирование.

Функции-члены объекта std::shared_future не синхронизированы, поэтому во избежание гонки за данными при доступе к одному объекту из нескольких потоков вы сами должны обеспечить защиту. 
Желательно создание нескольких объектов.
Доступ к разделяемому асинхронному состоянию из нескольких потоков безопасен, если каждый поток обращается к этому состоянию через свой собственный объект std::shared_future.

![испольлзование нескольки объектов shared_future](images/shared_future.png)