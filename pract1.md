# Практическое занятие №1. Введение, основы работы в командной строке

П.Н. Советов, РТУ МИРЭА

Научиться выполнять простые действия с файлами и каталогами в Linux из командной строки. Сравнить работу в командной строке Windows и Linux.

## Задача 1

```
grep '.*' /etc/passwd | cut -d: -f1 | sort
```
![image](https://github.com/user-attachments/assets/5933ccb3-76fd-4f50-ad7b-4107d26a1c1b)


## Задача 2

```
cat /etc/protocols|sort -k 2,2nr|head -n 5|awk '{print $2, $1}'
```
![изображение](https://github.com/user-attachments/assets/b125f881-a005-44ae-85fa-ebab6b7bb3db)


## Задача 3

```
text="Hello from RTU MIREA!"; text_length=${#text}; line=$(printf "%${text_length}s" | tr ' ' '-'); echo "+${line}+"; echo "| ${text} |"; echo "+${line}+"
```
![изображение](https://github.com/user-attachments/assets/e295298e-1679-4db1-9cb8-636ee6a70992)

## Задача 4

```
#!/bin/bash

file="$1"

identifiers=$(grep -o -E '\b[a-zA-Z]*\b' "$file" | sort -u)

echo "Идентификаторы:"
echo "$identifiers"
```
![изображение](https://github.com/user-attachments/assets/4b315a68-f1a6-463b-9235-2523fc01634e)


## Задача 5

```
#!/bin/bash

file=$1

# 755 - Чтение, запись, исполнение - Владалец | Чтение, исполнение - Другие пользователи
chmod 755 "./$file"

# Копируем команду в /usr/local/bin
sudo cp "$file" /usr/local/bin/

echo "Файл '$file' скопирован в usr/local/bin/, права были выданы"
```
![изображение](https://github.com/user-attachments/assets/6b1594d0-53b6-4d85-9184-ee09689f0c06)


## Задача 6

```
#!/bin/bash

for file in *.c *.js *.py; do
    # Чтение первой строки с начала
    line=$(head -n 1 "$file")
    if [[ $line == "#"* || $line == "//"* || $line == "/*"* ]]; then
        echo "Файл $file начинается с комментария"
    else
        echo "Файл $file не начинается с комментария"
    fi
done
```
![изображение](https://github.com/user-attachments/assets/87ec0b91-07ac-4f67-8fba-ca1497b5ccae)

## Задача 7

```

```

## Задача 8

```
#!/bin/bash

# Ищем все файлы с заданным расширением в текущем каталоге и сохраняем их в массиве
files=( $(find . -type f -name "*.$1") )

# Создаем архив файлов без повторений
tar -cvf "archive.tar" "${files[@]}"

echo "Архив создан"
```
![изображение](https://github.com/user-attachments/assets/32761009-9eb5-473a-b7cb-cebada43f883)


## Задача 9

```
#!/bin/bash

# sed s/что_заменять/на_что_заменять/опции
# g - Замените все вхождения строки в файле
# > - передача вывода второму аргументу
sed 's/    /\t/g' "$1" > "$2"

# Выводим сообщение об успешном завершении скрипта
echo "Файл исправлен"

```
![изображение](https://github.com/user-attachments/assets/d469729c-73be-4c2b-bdec-2673a58020e0)


## Задача 10

```
#!/bin/bash

# Итерируемся по всем файлам в директории, проверяем, что это текстовый файл и он пустой
for file in "$1"/*; do
    # Если найден файл и данный файл имеет размер 0 (т.е -s - true, если размер файла больше 0), 
    if [[ -f "$file" && ! -s "$file" ]]; then
        echo "Пустой файл: $file"
    fi
done
```
![изображение](https://github.com/user-attachments/assets/5273247a-c773-478c-87c9-e9187bd553a9)


## Полезные ссылки

Линукс в браузере: https://bellard.org/jslinux/

ShellCheck: https://www.shellcheck.net/

Разработка CLI-приложений

Общие сведения

https://ru.wikipedia.org/wiki/Интерфейс_командной_строки
https://nullprogram.com/blog/2020/08/01/
https://habr.com/ru/post/150950/

Стандарты

https://www.gnu.org/prep/standards/standards.html#Command_002dLine-Interfaces
https://www.gnu.org/software/libc/manual/html_node/Argument-Syntax.html
https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html

Реализация разбора опций

Питон

https://docs.python.org/3/library/argparse.html#module-argparse
https://click.palletsprojects.com/en/7.x/
