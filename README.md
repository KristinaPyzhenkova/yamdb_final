# YAMDB_FINAL
![workflow](https://github.com/KristinaPyzhenkova/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

Проект развернут по адресу: http://84.201.142.84/redoc/

## Описание проекта.
Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха.
Произведению может быть присвоен жанр (Genre) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.

Данный проект был выполнен в команде (3 ученика Яндекс.Практикум). В команде мне досталась роль разработчика, реализующего модели, представления и эндпойнты для них в следующих разделах:
- категории (Categories);
- жанры (Genres);
- произведения (Titles).

Данный проект реализован на библиотеке djangorestframework.

## Как запустить проект:
Проект развёрнут и запущен на Яндекс Облаке
Для обновления данных
```
git push  в ветку master
```

Проект доступен по адресу:
```
http://localhost/
```

### Примеры обращений к API:

#### Самостоятельно зарегистрироваться и получить код подтвердения для получения токена:

Обратиться по методу Post на - ``` http://{url}/api/v1/auth/signup/ ```
В теле запроса передать параметры username и email и их значения. После этого, если пользователь новыйй произойдет его регистрация, если пользователь уже существует, то регистрация не произойдет, на указанную почту будет выслан код подтверждения:
Пример тела запроса:
```
{
    "username": "test1",
    "email": "test12@yamdb.ru"
}
```
#### Получить токен для авторизации пользователя:

Обратиться по методу Post на - ``` http://{url}/api/v1/auth/token/ ```
В теле запроса передать параметры username и confirmation_code и их значения.
Полученный токен использовать для авторизации в сервисе api по методу bearer.
Пример тела запроса:
```
{
    "username": "test1",
    "confirmation_code": "123456"
}
```
Пример ответа:
```
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjUzOTI3ODgxL"
}
```
#### Получить список произведений:

Метод Get - ``` http://{url}/api/v1/titles/ ```

Ответ
```
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "name": "string",
        "year": 0,
        "rating": 0,
        "description": "string",
        "genre": [
          {
            "name": "string",
            "slug": "string"
          }
        ],
        "category": {
          "name": "string",
          "slug": "string"
        }
      }
    ]
  }
]

```
#### Добавить произведение (доступно только администратору):

Обратиться по методу Post на эндпойнт - ``` http://{url}/api/v1/titles/ ```
В теле запроса передать название произведения, год создания, описание, список жанров, категорию
Тело запроса:
```
{
  "name": "string",
  "year": 0,
  "description": "string",
  "genre": ["string",],
  "category": "string"
}
```
Ответ:
```
{
  "id": 0,
  "name": "string",
  "year": 0,
  "rating": 0,
  "description": "string",
  "genre": [
    {
      "name": "string",
      "slug": "string"
    }
  ],
  "category": {
    "name": "string",
    "slug": "string"
  }
}

```
#### Просмотреть детали по произведению:

Обратиться по методу Get на эндпойнт - ``` http://{url}/api/v1/titles/{titles_id}/ ```
Ответ:
```
{
  "id": 0,
  "name": "string",
  "year": 0,
  "rating": 0,
  "description": "string",
  "genre": [
    {
      "name": "string",
      "slug": "string"
    }
  ],
  "category": {
    "name": "string",
    "slug": "string"
  }
}

```
Администратору на эндпойнте ``` http://{url}/api/v1/titles/{titles_id}/ ``` также доступны методы Patch и Delete

#### Получить список отзывов:

Метод Get - ``` http://{url}/api/v1/titles/{title_id}/reviews/ ```

Ответ:
```
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "text": "string",
        "author": "string",
        "score": 1,
        "pub_date": "2019-08-24T14:15:22Z"
      }
    ]
  }
]

```
#### Получить отзыв по id:

Метод Get - ``` http://{url}/api/v1/titles/{title_id}/reviews/{review_id}/ ```

Ответ:
```
{
  "id": 0,
  "text": "string",
  "author": "string",
  "score": 1,
  "pub_date": "2019-08-24T14:15:22Z"
}

```
#### Добавить отзыв:

Отправить запрос по методу Post - ``` http://{url}/api/v1/titles/{title_id}/reviews/ ```

Тело запроса:
```
{
  "text": "string",
  "score": 1
}
Ответ:
{
  "id": 0,
  "text": "string",
  "author": "string",
  "score": 1,
  "pub_date": "2019-08-24T14:15:22Z"
}
```
Администратору, модератору и автору на эндпойнте ``` http://{url}/api/v1/titles/{title_id}/reviews/{review_id}/ ``` также доступны методы Patch и Delete

