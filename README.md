# 🐚 Bash Utilities Collection

Набор полезных bash-скриптов для повседневных задач в терминале.  
Идеально подходит для обучения, автоматизации и быстрого прототипирования!

---

## 📋 Список скриптов

| Скрипт | Описание |
|-------|--------|
| greeting.sh | Запрашивает имя и выводит приветствие |
| sum_calculator.sh | Складывает два числа (поддержка дробей через bc) |
| even_odd.sh | Проверяет, чётное ли число |
| create_project.sh | Создаёт структуру веб-проекта: HTML, CSS, JS |
| line_counter.sh | Считает количество строк в указанном файле |
| password_generator.sh | Генерирует случайный 8-символьный пароль |
| find_files.sh | Ищет файлы по расширению в текущей папке |

---



 #!/bin/bash
# Приветствие пользователя

read -p "Как вас зовут? " name
echo "Привет, $name!"



#!/bin/bash
# Сложение двух чисел

read -p "Введите первое число: " num1
read -p "Введите второе число: " num2

if [[ "$num1" =~ ^-?[0-9]+([.][0-9]+)?$ ]] && [[ "$num2" =~ ^-?[0-9]+([.][0-9]+)?$ ]]; then
    sum=$(echo "$num1 + $num2" | bc)
    echo "Сумма: $sum"
else
    echo "Ошибка: введите корректные числа."
fi



#!/bin/bash
# Проверка, чётное ли число

read -p "Введите целое число: " num

if [[ "$num" =~ ^-?[0-9]+$ ]]; then
    if [ $((num % 2)) -eq 0 ]; then
        echo "$num — чётное число."
    else
        echo "$num — нечётное число."
    fi
else
    echo "Ошибка: введите целое число."
fi



#!/bin/bash
# Генератор структуры веб-проекта

read -p "Введите имя проекта (по умолчанию 'my-project'): " project_name
project_name=${project_name:-my-project}

mkdir -p "$project_name"/{css,js}

cat > "$project_name/index.html" <<EOF
<!DOCTYPE html>
<html>
<head>
    <title>My Project</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <h1>Hello World!</h1>
    <script src="js/script.js"></script>
</body>
</html>
EOF

cat > "$project_name/css/style.css" <<EOF
/* Стили */
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
}
EOF

cat > "$project_name/js/script.js" <<EOF
// JavaScript
console.log('Project loaded!');
EOF

echo "✅ Структура проекта '$project_name' успешно создана!"



#!/bin/bash
# Подсчёт строк в файле

read -p "Введите имя файла: " filename

if [ -f "$filename" ]; then
    lines=$(wc -l < "$filename")
    echo "📄 Количество строк в '$filename': $lines"
else
    echo "❌ Файл '$filename' не найден."
fi




#!/bin/bash
# Генерация случайного пароля (8 символов)

password=$(tr -dc 'A-Za-z0-9!@#$%^&*()' < /dev/urandom | head -c 8)
echo "🔑 Сгенерированный пароль: $password"



#!/bin/bash
# Поиск файлов по расширению в текущей директории

read -p "Введите расширение (например, txt): " ext
[[ "$ext" != .* ]] && ext=".$ext"

shopt -s nullglob
files=(*"$ext")

if [ ${#files[@]} -gt 0 ]; then
    echo "📂 Найдено ${#files[@]} файл(ов) с расширением '$ext':"
    for f in "${files[@]}"; do
        echo " - $f"
    done
else
    echo "🔍 Файлы с расширением '$ext' не найдены."
fi

