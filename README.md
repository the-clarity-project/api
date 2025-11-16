# API для Clarity Project

**Clarity Project** — система аналітики відкритих даних, що поєднує інформацію з понад 120 відкритих державних реєстрів.

## Робота з API

Всі методи API викликаються за допомогою GET-запиту вигляду **https://clarity-project.info/api/api.method?key=xxx&param=value**, та повертають відповідь у форматі JSON.

Для роботи з API необхідно створити та використовувати ключ доступу, який передається у GET-параметрі **key**, наприклад: https://clarity-project.info/api/edr.info/14360570?key=f8028-7a2b9-50ab3-2505b

У випадку помилки, повертається об'єкт з ключом **error**, що містить опис помилки, наприклад: 
```json
{
  "error": {
    "code": 401,
    "text": "Invalid API key "
  },
  "stats": {
    "query_time": null
  }
}
```

У випадку успішного запиту у ключі **stats** повертається статистика запиту, а у ключі **quota** — ліміти запитів.
```json
{
  // ...
  "stats": {
    "query_time": 0.689716100692749
  },
  "quota": {
    "used": 173717,
    "max": -1,
    "key_used": 17615
  }
}
```

### Створення ключа доступу

Управляти ключами доступу можна на [сторінці налаштувань акаунту](https://clarity-project.info/me/api).

### Методи API:

#### Юридичні особи та ФОП
* **[edr.info/{edrpou}](edr.info.md#edrinfo)** - повертає інформацію по юридичній особі або ФОП за їх кодом ЄДРПОУ/РНОКПП;
* **[edr.search](edr.info.md#edrsearch)** - пошук юридичних осіб/ФОП;
* **[edr.changes](edr.info.md#edrchanges)** - повертає стрічку змін в інформації про юридичні особи;
* **[edrpou.history](edr.info.md#edrpouhistory)** - повертає історію змін з ЄДР для юридичної особи;
* **[edr.info/{edrpou}/licenses](edr.info.md#edrinfolicenses)** - повертає ліцензії обраної юо/фоп;
* **[edr.info/{edrpou}/persons](edr.info.md#edrinfopersons)** - повертає пов'язаних осіб;
* **[edr.info/{edrpou}/treasury](edr.info.md#edrinfotreasury)** - повертає інформацію по транзакціям Казначейства;
* **[edr.info/{edrpou}/vehicles](edr.info.md#edrinfovehicles)** - інформація про автотранспорт у користуванні;
* **[edr.finances/{edrpou}](edr.finances.md)** - фінансові звіти юридичних осіб;
* **[edr.history](edr.info.md#edrhistory)** - повертає історію змін;
* **[edr.relations](edr.info.md#)** - повертає зв'язки;

#### Власність
* **[vehicles.list/{code}](vehicles.list.md)** - повертає автотраспорт у власності 
  фізичної чи юридичної особи за її кодом РНОКПП чи ЄДРПОУ.
* **[realty.list](realty.list.md)** - повертає нерухомість у власності
  фізичної чи юридичної особи за її кодом РНОКПП, ПІБ чи ЄДРПОУ.

#### Податки
* **[tax.info/{edrpou}](tax.info.md)** - повертає інформацію про платника податків за кодом ЄДРПОУ/РНОКПП;

#### ФОП
* **[fop.byname](fop.info.md#fopbyname)** - повертає перелік ФОП за точним збігом по ПІБ;
* **[fop.bycode](fop.info.md#fopbycode)** - повертає інформацію по ФОП за його кодом РНОКПП;
* **[fop.info](fop.info.md#fopinfo)** - повертає інформацію по ФОП за його внутрішнім ідентифікатором;

#### Закупівлі
* **[tender.search](tender.search.md#tendersearch)** - пошук закупівель;
* **[tender.ids](tender.search.md#tenderids)** - пошук ідентифікаторів закупівель;

#### Фізичні особи
* **[persons.search](persons.search.md#personssearch)** - пошук за ПІБ;
* **[persons.info](persons.search.md#personsinfo)** - інформація за ПІБ;

#### Інше
* **[passport.check](passport.check.md)** - переварка номеру паспорта на (не-)дійсність;