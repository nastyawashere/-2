# Отчёт по практической работе №4

## Цель работы
Разобрать работу Command&Control - фреймворков

## Ход работы

### 1. Развернуть на виртуальной машине Ubuntu Server фреймворк постэксплуатации
Для того чтобы приступить к выполнению практической работы, необходимо на виртуальной машине развернуть Ubuntu Server, а также, чтобы проверить 
работоспособность наших действий, необходимо на виртуальной машине развернуть Windows 10. В роли фреймворка постэксплуатации был выбран: 
Empire Framework - https://github.com/BC-SECURITY/Empire. Все действия выполненные в этом пункте будут представлены на скриншоте и дополнены текстом, если это 
будет необходимо.

Приступим к установке фремворка Empire Framework на Ubuntu Server

1. Сначала нужно установить зависимость ОС:
<img width="974" height="494" alt="image" src="https://github.com/user-attachments/assets/8d29b9c5-e0ff-44bf-87b7-6ddb9c1cbab3" />

**Рис. 1 - Выполнение команды "sudo apt update"**

<img width="992" height="229" alt="image" src="https://github.com/user-attachments/assets/9cdf9461-2eeb-40b5-8d49-98322d8b6fa9" />

**Рис. 2 - Выполнение команды "sudo apt install -y git python3 python3-pip"**

В моём случае видно, что python3 на моей ОС установлен, поэтому ничего нового не установилось.

### 2. Клонируем репозиторий с подмодулями:
<img width="1031" height="242" alt="image" src="https://github.com/user-attachments/assets/981b0936-6931-4ec6-a12e-56da1ee6c2ef" />

**Рис. 3 - Выполнение команды «git clone --recursive https://github.com/BC-SECURITY/Empire.git»**

<img width="974" height="58" alt="image" src="https://github.com/user-attachments/assets/fe2e2fad-9a98-498c-a354-67324908067a" />

**Рис. 4 - Выполнение команды "cd Empire/"**

### 3. Переключаемся на последний стабильный релиз:
Было создано задание "Тестовый проект" для проверки основных функций программы.

<img width="974" height="500" alt="image" src="https://github.com/user-attachments/assets/1b274cd9-d833-41cb-a9b3-2cc5656fdbb1" />

**Рис. 5 - Выполнение команды "./setup/checkout-latest-tag.sh"**

### 4. Установим Empire:

После выполнения команды, которая представлена в названии рисунка номер 6, должен появиться такой результат, который представлен на рисунке номер 6. Этот скрипт создаст виртуальное окружение, установит все Python-зависимости, соберёт необходимые бинарники.

<img width="828" height="145" alt="image" src="https://github.com/user-attachments/assets/61797b40-cc53-489d-8885-20fdfcd79fad" />

**Рис. 6 - Выполнение команды "./ps-empire install -y"**

### 5. Запускаем сервер:

<img width="974" height="453" alt="image" src="https://github.com/user-attachments/assets/29a6efb6-6807-481a-95c5-5f5fc4b64330" />

**Рис. 7 - Выполнение команды "./ps-empire server"**

Сервер запущен и работает, после этого можно выключить виртуальную машину, поменять настройки сети.

### 6. Подключаемся к серверу через браузер: на Windows машине открываем браузер, переходим по адресу http://192.168.100.10:1337

<img width="974" height="1039" alt="image" src="https://github.com/user-attachments/assets/5506a4d0-628d-44a8-bbb4-e6c25472ea19" />

**Рис. 8 - Успешный вход в веб-интерфейс Starkiller (Empire)**

### 7. Создание Listencer

<img width="902" height="675" alt="image" src="https://github.com/user-attachments/assets/7243a924-ea1a-40a5-8f14-ee0d4be2304a" />

**Рис. 9 - Рабочее окно Listencer**

### 8. Создание полезной нагрузки (Stager)

<img width="974" height="427" alt="image" src="https://github.com/user-attachments/assets/d74f33e1-bf65-410f-b29c-baced7694175" />

**Рис. 10 - Полезная нагрузка**

### 9. Просмотр появился ли агент

<img width="974" height="137" alt="image" src="https://github.com/user-attachments/assets/c4b360b4-188d-4b87-8896-58baf28fe837" />

**Рис. 11 - Список появившихся агентов**

Да, появился, но пока что, я только смог получить агента, выключив полностью антивирусник.

### 10. После подключения к системе и появление нового агента, мы имеем возможность узнавать различные данные о системе пользователя.

<img width="974" height="658" alt="image" src="https://github.com/user-attachments/assets/001eac00-b328-47fe-85e3-56f8b56561a0" />

**Рис. 12 - Результаты проделанной работы**

## Результаты
Успешно развёрнут сервер. Установлена программа Empire. Изучен теоретический материал, как работать с Empire, а также отточены навыки с равзорачивании сервера. Получен доступ к виртуальной машины другого пользователя.

## Вывод
Цель работы достигнута. Программа готова к использованию.
