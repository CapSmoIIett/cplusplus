похож на std::unique_ptr

std::future get() срабатывает единоразово. Повторные вызовы тригерят 
```bash
terminate called after throwing an instance of 'std::future_error'
  what():  std::future_error: No associated state
```

Создавая std::future, вы даете обещание предоставить значение или исключение, а, уничтожая объект (std::packaged_task или std::promise), не задав ни того, ни другого, вы это обещание нарушаете. Если бы компилятор в этом случае не сохранил ничего в будущем результате, то ожидающие потоки могли бы никогда не выйти из состояния ожидания.

не копируемый, перемещаемый
[[Семантика перемещения]]

В std::future есть метод share возвращающий std::shared_future
[[std_shared_future]]