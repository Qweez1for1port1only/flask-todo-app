# Практическая работа 2

Одноэтапная контейнеризация исходного Flask Todo на Python 3.9 slim.

## Запуск

```sh
git clone https://github.com/Qweez1for1port1only/flask-todo-app
cd flask-todo-app
docker build -t flask-todo-app:v1 .
docker images
docker run -d -p 7345:7345 --name my-todo-container flask-todo-app:v1
```

Открыть http://localhost:7345. Остановка: `docker stop my-todo-container`.
Повторный запуск существующего контейнера: `docker start my-todo-container`.

## Изменения

- Добавлены Dockerfile и .dockerignore.
- Импорты пакетов и print исправлены для Python 3.
- Импорт flask.ext.sqlalchemy заменён на flask_sqlalchemy.
- Зависимости закреплены в совместимых версиях для Flask-Script.
- Сортировка задач записана через Todo.id.desc().
- Отключён режим отладки; сервер слушает 0.0.0.0:7345.

Это учебная конфигурация с прежним Flask-Script и встроенным сервером Flask.
Файл todo.sqlite копируется из репозитория в /app и изменяется внутри контейнера.
Перезапуск контейнера сохраняет данные, удаление контейнера — нет.

## Проверка 10 ноября 2026

Сборка завершилась успешно. `pip check` не обнаружил конфликтов.
GET / возвращает HTTP 200. Добавление, редактирование, завершение,
возврат и удаление задач проверены через HTTP и SQLite.
Сохранение задачи после перезапуска контейнера проверено.
