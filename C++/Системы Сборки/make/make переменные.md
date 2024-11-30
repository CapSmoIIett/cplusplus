Переменные в make представляют собой именованные строки и определяются очень просто:

```make
<VAR_NAME> = <value string>

SRC = main.c hello.c

gcc -o hello $(SRC)
```