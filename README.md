
# Лабораторная работа №3: Средства обфускации

## Цель_работы
Изучение методов обфускации исходного кода на примере обфускатора `obfus.h` для языка C/C++, анализ изменений в дизассемблированном коде до и после применения обфускации с помощью IDA Pro.
### Инструменты:
- **Язык программирования**: C++
- **Обфускатор**: [obfus.h](https://github.com/DosX-dev/obfus.h)
- **Компилятор**: Tiny C Compiler (TCC)
- **Дизассемблер**: IDA Pro
- **Операционная система**: Windows 11
### 1. Написание исходной программы
Был создан файл `lab3_clean.c` со следующим кодом:

```c
#include <windows.h>
#include <stdio.h>

int main() {
    char path[MAX_PATH];

    // Вывод списка студентов
    printf("Students: Kondratova, Abrosimova, Dulcev, Piguchin\n");

    // Получение текущей директории
    GetCurrentDirectoryA(MAX_PATH, path);
    printf("Current directory: %s\n", path);

    // Вывод содержимого папки Documents
    system("dir %USERPROFILE%\\Documents");

  return 0;
}
```

### 2. Компиляция чистого файла
Выполнена компиляция с помощью Tiny C Compiler:
``` tcc lab3_clean.c -o lab3_clean.exe ```

### 3. Обфускация кода
```
#define OBFUSCATE_STRINGS
#include "obfus.h"

#include <windows.h>
#include <stdio.h>

int main() {
    char path[MAX_PATH];

    printf(OBF("Students: Kondratova, Abrosimova, Dulcev, Piguchin\n"));

    GetCurrentDirectoryA(MAX_PATH, path);
    printf(OBF("Current directory: %s\n"), path);

    system(OBF("dir %USERPROFILE%\\Documents"));

    return 0;
}
```
### 4. Компиляция обфусцированного файла
``` tcc lab3_obf.c -o lab3_obf.exe```
### 5. С применением IDA Pro  дизассемблировать полученный exe .
<img width="974" height="697" alt="image" src="https://github.com/user-attachments/assets/40646563-630d-44b7-9e9a-6112113eec4e" />
Открываю чистый исполняемый файл lab3_clean.exe в программе IDA Pro. Загружаю файл как Portable executable for AMD64 (PE). После завершения автоматического анализа нажимаю Shift+F12, чтобы открыть окно со строками. В списке вижу все строки моей программы в открытом виде: "Students: Kondratova, Abrosimova, Dulcev, Piguchin"
<img width="666" height="781" alt="image" src="https://github.com/user-attachments/assets/f27b5c72-3915-4257-b5f3-d7807846fe16" />
<img width="889" height="601" alt="image" src="https://github.com/user-attachments/assets/2cb43cd6-f0fa-477d-907a-2843732072de" />

### 6. Аналогично дизассемблировать полученный exe
Вместо понятной, читаемой структуры с явными вызовами функций и открытыми строковыми константами, анализатор сталкивается с искусственно усложнённым и запутанным кодом.
Первое, что бросается в глаза при открытии строкового окна (Shift+F12) — это полное отсутствие читаемых строк из исходной программы. Нет ни списка студентов, ни форматированных сообщений для вывода в консоль.
<img width="622" height="1045" alt="image" src="https://github.com/user-attachments/assets/a8faee27-fddd-4040-ac9b-572907a12e9c" />
<img width="856" height="1036" alt="image" src="https://github.com/user-attachments/assets/20222afc-3bec-4203-b15e-5e02abe40060" />
### Вывод по exe без обфускации:
Вижу понятную структуру функций, главную функцию main с прямыми вызовами printf, GetCurrentDirectoryA и system. Код читаемый и легко анализируется.
### Вывод по exe с обфускацией:
В окне строк не нахожу ни одной строки из моей программы. Видны только названия системных библиотек и функций, таких как msvcrt.dll, printf, system. Список функций программы увеличился в несколько раз — вместо 10 функций вижу более 50, большинство из которых имеют имена вида sub_401033 и являются "мусорным" кодом, добавленным обфускатором. Граф вызовов стал чрезвычайно запутанным, появились обёртки для простых API-вызовов и добавлены функции, связанные с антиотладкой, например SuspendThread и GetThreadContext, которые затрудняют динамический анализ.
По итогам анализа делаю вывод, что обфускатор obfus.h успешно выполнил свою задачу: он скрыл все строковые константы, значительно усложнил структуру программы, добавил мусорный код и механизмы против отладки, что в совокупности серьёзно затрудняет реверс-инжиниринг программы, увеличивая время и усилия, необходимые для её анализа.
