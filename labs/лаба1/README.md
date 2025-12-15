Абросимова Анастасия, группа 22-К-АС1
# Лабораторная работа №1: Применение дизассемблеров

## Цель работы
Ознакомление с дизассемблерами на примере IDA Pro, анализ вредоносного программного обеспечения (ВПО) и определение его характеристик.

##  Используемые инструменты
- Виртуальная машина: Windows 10
- Дизассемблер: IDA Pro
- Дополнительное ПО:
  - Кейген для лицензии IDA Pro
  - Компилятор Python (для кейгена)
  - Распаковщик архивов 7z
- **Источник ВПО**: [vx-underground.org](https://vx-underground.org/) (раздел Samples)

##  Ход работы

### 1. Подготовка среды
- Установлен образ Windows 10 на виртуальную машину
- Установлены необходимые приложения:
  - IDA Pro
  - Кейген для лицензии (находится в одной папке с IDA Pro)
  - Компилятор Python
  - Распаковщик архивов 7z
<img width="974" height="530" alt="image" src="https://github.com/user-attachments/assets/5a17ffeb-1545-49cb-b643-6bcb7a2308d9" />

### 2. Загрузка и подготовка образца ВПО
- Скачан образец вредоносного ПО с сайта vx-underground.org
- Образец распакован для возможности чтения IDA Pro (в противном случае программа читает файл как бинарный)
<img width="974" height="711" alt="image" src="https://github.com/user-attachments/assets/7cfff38e-32c9-425a-8648-ddabf0942cf0" />
<img width="974" height="767" alt="image" src="https://github.com/user-attachments/assets/a834c671-599f-4bd2-a76c-5d49f931af70" />
<img width="916" height="708" alt="image" src="https://github.com/user-attachments/assets/c8954dea-7001-4933-b0a2-350188fe20fa" />
<img width="514" height="670" alt="image" src="https://github.com/user-attachments/assets/f90686c7-1f38-4b53-8575-2c6b5145c8d0" />

### 3. Анализ первого образца ВПО

**Характеристики:**
- **Язык программирования**: C/C++
- **Точка входа**: `WinMain(x,x,x,x)` - первая функция, выполняемая после загрузки программы
- **Тип ВПО**: Троян/руткит, маскирующийся под драйвер Realtek
- **Особенности**:
  - Функция `sub_401030` работает с дескрипторами безопасности Windows: `InitializeSecurityDescriptor(pSecurityDescriptor, dwRevision)`
  - Работает как драйвер/системный компонент

### 4. Анализ второго образца ВПО
<img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/095a83c5-5a10-43d1-8317-862dce837692" />
<img width="974" height="549" alt="image" src="https://github.com/user-attachments/assets/48c6c477-1910-411c-bf2e-a2275475266b" />
<img width="845" height="747" alt="image" src="https://github.com/user-attachments/assets/557a9b85-eb8b-416b-b087-56a8c5580957" />

**Характеристики:**
- **Язык программирования**: Java (с элементами JNI)
- **Платформа**: Android
- **Название**: `"com.alala.core.A"` - имя пакета Android-приложения
- **Тип приложения**: Android бот (ботнет-клиент или мессенджер-бот)
- **Особенности**:
  - Сетевые возможности (TCP-клиент)
  - Используется нативная компиляция (присутствуют низкоуровневые типы данных like `__int8`)
  - Основная Activity: `MainActivity_onCreate@Vl` содержит метод `onCreate` - стандартная точка входа Android приложений

##  Результаты анализа
1. **Первый образец** - троян/руткит, маскирующийся под драйвер Realtek, написанный на C/C++ с функциональностью работы с дескрипторами безопасности Windows.
2. **Второй образец** - Android-бот на Java с нативными компонентами, обладающий сетевыми возможностями и функционирующий как TCP-клиент.

