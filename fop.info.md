# API для Clarity Project

[Опис API](README.md)

### Інформація про ФОП

## edr.search
Метод повертає результати пошуку ю/о та ФОП за запитом, який передається у параметрі `q`.

[Документація](edr.info.md#edrsearch)

## fop.byname

Метод повертає перелік ФОП за **точним співпадінням** по ПІБ.

##### Приклад запиту:
[https://com.clarityapp.pro/api/fop.byname/ГОНЧАРУК ОЛЕКСІЙ ВАЛЕРІЙОВИЧ?key=xxx]()

##### Приклад відповіді:
```json
{
  "list": [
    {
      "FopID": "083f18e0b84c7f21cd5c572f9ecdd4dc",
      "Name": "ГОНЧАРУК ОЛЕКСІЙ ВАЛЕРІЙОВИЧ",
      "Status": "terminated",
      "Locality": "ЧЕРНІГІВ",
      "Region": "ЧЕРНІГІВСЬКА область",
      "StatusName": "Припинено"
    },
    {
      "FopID": "e21c185c72bcf52b6df98abe3480bac1",
      "Name": "ГОНЧАРУК ОЛЕКСІЙ ВАЛЕРІЙОВИЧ",
      "Status": "registered",
      "Locality": "ГОРОДИЩЕ-ПУСТОВАРІВСЬКЕ",
      "Region": "КИЇВСЬКА область",
      "StatusName": "Зареєстровано"
    },
    // ...
  ]
}
```

##### Опис полів:
* **FopID** - [ідентифікатор ФОП](fop.info.md#fopinfo);
* **Name** - ПІБ;
* **Status, StatusName** - стан ФОП;
* **Locality, Region** - населений пункт та регіон реєстрації ФОП;

## fop.info

Повертає інформацію про ФОП за його ідентифікатором.

##### Приклад запиту:
https://com.clarityapp.pro/api/fop.info/c0a7d2d26cfc02758f1492aab0fca287?key=xxx

##### Приклад відповіді:
[examples/fop.info.json]()