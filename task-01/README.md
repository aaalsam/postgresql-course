# PostgreSQL. Задание №1

---

## Цель задания:

1. Развернуть виртуальную машину (Linux) с PostgreSQL с помощью Docker.
2. Загрузить минимальный дамп базы данных «Тайские перевозки».
3. Посчитать количество поездок с помощью SQL-запроса:

```sql
select count(*) from book.tickets;
```

4. Остановить виртуальную машину после выполнения работы.

---

## Выполненные шаги:

### Шаг 1. Запуск PostgreSQL в Docker-контейнере:

Создан `docker-compose.yml`:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:17
    container_name: my-postgres
    environment:
      POSTGRES_DB: testdb
      POSTGRES_USER: testuser
      POSTGRES_PASSWORD: testpass
    ports:
      - "5432:5432"
    volumes:
      - postgres-data:/var/lib/postgresql/data

volumes:
  postgres-data:
```

Запуск контейнера:

```bash
docker-compose up -d
```

---

### Шаг 2. Загрузка базы данных "Тайские перевозки":

Скачивание и импорт дампа:

```bash
wget https://storage.googleapis.com/thaibus/thai_small.tar.gz
tar -xf thai_small.tar.gz
docker exec -it my-postgres createdb -U testuser thai
docker exec -i my-postgres psql -U testuser -d thai < thai.sql
```

---

### Шаг 3. Подсчёт количества поездок:

Подключение к базе и выполнение запроса:

```bash
docker exec -it my-postgres psql -U testuser -d thai
```

Выполнен SQL-запрос:

```sql
thai=# select count(*) from book.tickets;
  count  
---------
 5185505
(1 row)
```

---

### Шаг 4. Остановка контейнера (ВМ):

Остановка Docker-контейнера:

```bash
docker-compose stop
```

---