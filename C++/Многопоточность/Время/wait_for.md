#Multithreading

Все функции ожидания возвращают код, показывающий, истек
ли таймаут или произошло ожидаемое событие

std::future_status::timeout - истек тайм аут
std::future_status::ready - выполненно успешно
std::future_status::deferred - задача отложенна 
