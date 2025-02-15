# Тестовое задание для вакансии Senior Front

##  Что предстоит делать на работе

- Разработка фреймворка для сборки ERP приложений в команде с двумя middle специалистами.
- Создание комплексных компонентов с необходимым UX
- Сборка приложений на основе этих компонентов

## Необходимые знания и навыки

- OOP
- Методы разработки конфигурируемых интерфейсов

При проверке в первую очередь внимание будет уделяться архитектурному пониманию задания.


## Задание

Необходимо реализовать прототип фреймворка.

Два public git репозитория (сервис не важен, мы используем github):

1. npm пакет компонентов. С возможностью билда в Storybook
2. приложение, использующее npm пакет компонентов

Разместить Storybook и приложение на любом хостинге для просмотра финального результата.


### Первый репозиторий. npm пакет компонентов

Можно писать с нуля или брать за основу любой готовый UI-Kit (мы используем Ant Design).

Каждый компонент имеет конструктор из json конфигурации.
Storybook содержит три компонента

#### 1. Компонент Label

самый простой вариант вывода текста (без HTML)

Пример конфига:
```json

{
  "type": "Label",
  "data": "это текст метки"
}

```

#### 2. Компонент Input

самый простой текстовый инпут с плейсхолдером

Пример конфига:
```json

{
  "type": "Input",
  "settings": {
    "placeholder" : "текст плейсхолдера"
  },
  "data": "value заполняется этой строкой"
}

```

#### 3. Компонент Form

комплексный компонент, который может содержать в себе другие компоненты ( Label или Input )

имеет свойство unique-form-name

знает о своем REST API, этот API компонент использует для запроса собственного конфига

REST API:

```http request
GET {{BASE_URL}}/form/{{unique-form-name}}
```

Пример конфига:
```json 

{
  "type": "Form",
  
  "components": {
    "intro": {
      "type": "Label",
      "data": "Это пример метки на форме"
    },
    
    "fio" : {
      "type": "Input",
      "settings": {
        "placeholder" : "Фамилия Имя Отчество"
      },
      "data": ""
    }
  }
  
}

```


### Второй репозиторий. Приложение

React приложение. Использует npm пакет с компонентами.
Состоит из одной страницы.  На этой странице отображаются две формы.
Конфигурация каждой формы загружается через REST API.

#### Первая форма
```
unique-form-name = "first-form"

```
соответственно конфиг загружается компонентом формы по адресу

```
GET {BASE_URL}/form/first-form
```

RESPONSE для мока API:
```json

{
   "type": "Form",
    
    "components": {
        "intro": {
            "type": "Label",
            "data": "Это пример метки на форме"
        },
    
        "fio" : {
          "type": "Input",
          "settings": {
            "placeholder" : "Фамилия Имя Отчество"
          },
          "data": ""
        }
    }
}

```


#### Вторая форма
```
unique-form-name = "second-form"
```

соответственно конфиг загружается компонентом формы по адресу

```
GET {BASE_URL}/form/second-form
```

RESPONSE для мока API:
```json

{
   "type": "Form",
    
    "components": {
        "intro": {
            "type": "Label",
            "data": "Метка 1"
        },
    
        "fio" : {
            "type": "Input",
            "settings": {
              "placeholder" : "Фамилия Имя Отчество"
            },
            "data": "Иванов Иван"
        },
        
        "extra" : {
            "type": "Input",
            "settings": {
              "placeholder" : "Дополнительная информация"
            },
            "data": ""
        }
    }
}

```