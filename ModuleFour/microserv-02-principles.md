# Домашнее задание к занятию «Микросервисы: принципы»

### Задача 1: API Gateway
Предложите решение для обеспечения реализации API Gateway. Составьте сравнительную таблицу возможностей различных программных решений. На основе таблицы сделайте выбор решения.

__Решение должно соответствовать следующим требованиям:__

1. маршрутизация запросов к нужному сервису на основе конфигурации,
2. Возможность проверки аутентификационной информации в запросах,
3. Обеспечение терминации HTTPS.

<table>
    <tr>
        <th>Решение</th>
        <th>Маршрутизация</th>
        <th>Аутентификация</th>
        <th>HTTPS терминация</th>
        <th>Легкость настройки</th>
        <th>Поддержка Docker</th>
        <th>Примечания</th>
    </tr>
    <tr>
        <td><b>NGINX</b></td>
        <td>Да</td>
        <td>Частично (через LUA/OpenResty или внешний сервис)</td>
        <td>Да</td>
        <td>Средняя</td>
        <td>Да</td>
        <td>Очень популярный, но требует ручной настройки логики</td>
    </tr>
    <tr>
        <td><b>Traefik</b></td>
        <td>Да</td>
        <td>Да (JWT, OIDC, OAuth2)</td>
        <td>Да</td>
        <td>Простая</td>
        <td>Да</td>
        <td>Расширяем через плагины, есть UI и база данных</td>
    </tr>
    <tr>
        <td><b>Envoy</b></td>
        <td>Да</td>
        <td>Да (через фильтры)</td>
        <td>Да</td>
        <td>Сложная</td>
        <td>Да</td>
        <td>Мощный, и требует сложной конфигурации</td>
    </tr>  
    <tr>
        <td><b>HAProxy</b></td>
        <td>Да</td>
        <td>Частично  (через ACL и LUA)</td>
        <td>Да</td>
        <td>Средняя</td>
        <td>Да</td>
        <td>Производительный, но менее удобный для микросервисов</td>
    </tr> 
  </table>

__Выбор:__ Traefik

__Обоснование:__ Traefik идеально подходит для микросервисной архитектуры:
Простая интеграция с Docker Compose и Kubernetes,
Встроенная поддержка HTTPS через Let's Encrypt,
Удобная маршрутизация и возможность настройки проверки JWT токенов через middleware,
Минимальные усилия для запуска в dev-среде.

### Задача 2: Брокер сообщений
Составьте таблицу возможностей различных брокеров сообщений. На основе таблицы сделайте обоснованный выбор решения.

__Решение должно соответствовать следующим требованиям:__

1. Поддержка кластеризации для обеспечения надёжности
2. Хранение сообщений на диске в процессе доставки
3. Высокая скорость работы
4. Поддержка различных форматов сообщений
5. Разделение прав доступа к различным потокам сообщений,
простота эксплуатации.

Обоснуйте свой выбор.

<table>
    <tr>
        <th>Брокер</th>
        <th>Кластеризация</th>
        <th>Хранение на диске</th>
        <th>Скорость</th>
        <th>Поддержка форматов</th>
        <th>Разделение прав</th>
        <th>Простота эксплуатации</th>
    </tr>
    <tr>
        <td><b>RabbitMQ</b></td>
        <td>Да</td>
        <td>Да</td>
        <td>Средняя</td>
        <td>JSON, XML, бинарные</td>
        <td>Да</td>
        <td>Простая</td>
    </tr>
    <tr>
        <td><b>Apache Kafka</b></td>
        <td>Да</td>
        <td>Да</td>
        <td>Очень высокая</td>
        <td>JSON, Avro, Protobuf </td>
        <td>Да</td>
        <td>Сложнее</td>
    </tr>
    <tr>
        <td><b>NATS</b></td>
        <td>Да (JetStream)</td>
        <td>Да</td>
        <td>Очень высокая</td>
        <td>JSON, Protobuf, бинарные</td>
        <td>Да</td>
        <td>Простая</td>
    </tr>  
    <tr>
        <td><b>Redis Streams</b></td>
        <td>Частично</td>
        <td>Да</td>
        <td>Высокая</td>
        <td>JSON, бинарные</td>
        <td>Да</td>
        <td>Простая, но ограничена</td>
    </tr> 
    <tr>
        <td><b>ActiveMQ</b></td>
        <td>Да</td>
        <td>Да</td>
        <td>Средняя</td>
        <td>XML, JSON, бинарные</td>
        <td>Да</td>
        <td>Средняя</td>
    </tr> 
  </table>


__Выбор:__ RabbitMQ

__Обоснование:__

Прост в установке и эксплуатации (есть UI, легко деплоится в Docker)
Поддерживает все требуемые фичи: кластеризацию, хранение сообщений, безопасность
Не требует сложной настройки, как Kafka, и подходит для большинства микросервисных задач
Поддерживает разные форматы сообщений.
