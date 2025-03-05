# Лабораторная работа 4

## Документация по api

Работа с иногородними пациентами

#### Примечание:
* Так как все api работают с веб-интерфейсом, все ответы возвращают статус OK (200) для облегчения обработки ответов, внутри себя содержат DTO c со следующей структурой:

        {
            code: HttpStatusCode (int),
            message: string,
            success: bool
        }
    Все коды статусов ответов, описанных ниже будут взяты из DTO.

#### GET /api/Employee/Get

Описание: получить все работников скорых помощей

Заголовки:
* Authorization: Bearer

**Входные параметры:**
* Query Params согласно спецификации OData

Пример запроса:

URL:
`/api/Employee/Get`

Код статуса ответа:
* 200 OK - работники найдены
* 401 No authorizated - токен не прошел аутентификацию

Пример ответа: 

    [
        {
            "id": "66c9989edc88508d1eca3259",
            "snils": "***",
            "name": "Наталья",
            "gender": null,
            "surname": "***",
            "thirdname": "***",
            "birthday": "1980-12-19T03:00:00Z",
            "whenLoaded": "2024-08-26T05:45:13.121Z",
            "medOrgOid": "***"
        },
        ...
    ]

#### POST /api/Employee/Create

Описание: создание нового работника

Заголовки:
* Authorization: Bearer
* Content-Type: application/json

**Входные параметры:**

Body:
* id - идентификатор работника
* snils - Снилс
* name - Имя
* gender - пол
* surname - Фамилия
* thirdName - Отчество
* birthDay - Дата рождения
* whenLoaded -Дата создания записи
* medOrgOid - oid Подразделения

Пример запроса: 
Body:

    {
        "id": "string",
        "snils": "string",
        "name": "string",
        "gender": "string",
        "surname": "string",
        "thirdname": "string",
        "birthday": "2025-03-05T08:33:41.800Z",
        "whenLoaded": "2025-03-05T08:33:41.800Z",
        "medOrgOid": "string"
    }

Код статуса ответа:
* 201 Created - Пациент добавлен
* 409 Confict - Сотрудник с такими данными существует в БД
* 422 Unprocessable Entity - Сотрудник не прошел валидацию данных
* 401 No Authorized - Токен не прошел аутентификацию

Пример ответа:

    {
        "code": 201,
        "success": true,
        "message": "Пациент успешно добавлен"
    }

#### PATCH /api/Employee/Update

Описание: Отредактировать данные работника

Заголовки:
* Authorization: Bearer
* Content-Type: application/json

**Входные параметры:**

Query Params:
* id - идентификатор работника

Body: 
* id - идентификатор работника
* snils - Снилс
* name - Имя
* gender - пол
* surname - Фамилия
* thirdName - Отчество
* birthDay - Дата рождения
* whenLoaded -Дата создания записи
* medOrgOid - oid Подразделения

Пример запроса: 

URL: 
`/api/Employee/Update?id=452156215125125`

Body:

    {
        "gender": "Ж",
        "Name": "Кирилл"
    }

Код статуса ответа:
* 200 OK - работник обновлен
* 422 Unprocessable Entity - работник не прошел валидацию данных
* 401 No Authorized - Токен не прошел аутентификацию

Пример ответа: 

    {
        "code": 200,
        "success": true,
        "message": "работник обновлен!"
    }

#### DELETE /api/Employee/Delete

Описание: Удалить работника

Заголовки:
* Authorization: Bearer

**Входные параметры:**

Query Params:
* id - идентификатор работника

Пример запроса:

URL: 
`/api/Employee/Delete?id=qwgqwgqwgqwg`

Код статуса ответа:
* 200 OK - работник обновлен
* 404 Not Found - работник с переданным id не найден
* 401 No Authorized - Токен не прошел аутентификацию

Пример ответа:

    {
        "code": 200,
        "success": true,
        "message": "работник успешно удален"
    }


#### GET /api/Workplace/Get

Описание: получить все рабочие места

Заголовки:
* Authorization: Bearer

**Входные параметры:**
* Query Params согласно спецификации OData

Пример запроса:

URL:
`/api/Workplace/Get/`

Код статуса ответа:
* 200 OK - рабочие места найдены
* 401 No authorizated - токен не прошел аутентификацию

Пример ответа: 
    
    [
        {
        "id": "string",
        "employeeId": "string",
        "cardId": "string",
        "structGroupOID": "string",
        "medOrgOID": "string",
        "employmentType": "string",
        "specializationId": 0,
        "whenLoaded": "2025-03-05T09:13:48.281Z"
        }
    ]

#### GET /api/Workplace/Get/{id}

Описание: получить все рабочее место по id

Заголовки:
* Authorization: Bearer

**Входные параметры:**
* Query Params согласно спецификации OData

Пример запроса:

URL:
`/api/Workplace/Get/196`

Код статуса ответа:
* 200 OK - работники найдены
* 401 No authorizated - токен не прошел аутентификацию

Пример ответа: 
    
    [
        {
        "id": "string",
        "employeeId": "string",
        "cardId": "string",
        "structGroupOID": "string",
        "medOrgOID": "string",
        "employmentType": "string",
        "specializationId": 0,
        "whenLoaded": "2025-03-05T09:33:10.056Z"
        }
    ]


#### POST /api/Workplace/Create

Описание: создание нового рабочего места для работника

Заголовки:
* Authorization: Bearer
* Content-Type: application/json

**Входные параметры:**

Body:
* id - идентификатор рабочего места
* employeeId - Снилс
* cardId - табельный номер
* structGroupOID - oid структурного подразделения
* medOrgOID - oid мед организации
* employmentType - тип должности
* specializationId - id должности
* whenLoaded -Дата создания записи

Пример запроса: 
Body:

    {
        "id": "string",
        "employeeId": "string",
        "cardId": "string",
        "structGroupOID": "string",
        "medOrgOID": "string",
        "employmentType": "string",
        "specializationId": 0,
        "whenLoaded": "2025-03-05T09:36:20.307Z"
    }

Код статуса ответа:
* 201 Created - Рабочее место добавлено
* 409 Confict - Рабочее место с такими данными существует в БД
* 422 Unprocessable Entity - Рабочее место не прошел валидацию данных
* 401 No Authorized - Токен не прошел аутентификацию

Пример ответа:

    {
        "code": 201,
        "success": true,
        "message": "Пациент успешно добавлен"
    }

#### GET /api/Employee/GetEmployeesBySnilsOrCardId

Описание: получить все работника скорой помощи по снилсу или мед оргонизации

Заголовки:
* Authorization: Bearer

**Входные параметры:**
* Query Params согласно спецификации OData

Пример запроса:

URL:
`/api/Employee/GetEmployeesBySnilsOrCardId?identifiers=string&systemOid=1`

Код статуса ответа:
* 200 OK - работники найдены
* 401 No authorizated - токен не прошел аутентификацию

Пример ответа: 
    
    [
      {
        "employee": {
          "id": "string",
          "snils": "string",
          "name": "string",
          "gender": "string",
          "surname": "string",
          "thirdname": "string",
          "birthday": "2025-03-05T09:07:51.458Z",
          "whenLoaded": "2025-03-05T09:07:51.458Z",
          "medOrgOid": "string"
        },
        "contacts": [
          {
            "id": "string",
            "employeeId": "string",
            "contactString": "string",
            "type": "string",
            "whenLoaded": "2025-03-05T09:07:51.458Z"
          }
        ],
        "workplaces": [
          {
            "id": "string",
            "employeeId": "string",
            "cardId": "string",
            "structGroupOID": "string",
            "medOrgOID": "string",
            "employmentType": "string",
            "specializationId": 0,
            "whenLoaded": "2025-03-05T09:07:51.458Z"
          }
        ]
      }
    ]
