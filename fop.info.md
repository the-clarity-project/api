# API для Clarity Project

[Опис API](README.md)

### Інформація про ФОП

## edr.search
Метод повертає результати пошуку ю/о та ФОП за запитом, який передається у параметрі `q`.

[Документація](edr.info.md#edrsearch)

## fop.bycode

Метод повертає актуальну інформацію про ФОП за його РНОКПП.

##### Приклад запиту:
[https://clarity-project.info/api/fop.bycode/1234567890?key=xxx]()

## fop.byname

Метод повертає перелік ФОП за **точним співпадінням** по ПІБ.

##### Приклад запиту:
[https://clarity-project.info/api/fop.byname?name=ГОНЧАРУК ОЛЕКСІЙ ВАЛЕРІЙОВИЧ&key=xxx]()

##### Приклад відповіді:
```json
{
  "list": [
    {
      "FopID": "e3e107a9628762a1aa6c349c5d6c8eec",
      "Name": "ГОНЧАРУК ОЛЕКСІЙ ВАЛЕРІЙОВИЧ",
      "Status": "terminated",
      "Address": "ЧЕРНІГІВСЬКА ОБЛ., М. ЧЕРНІГІВ, ВУЛ. БЄЛОВА, БУД. 21, КОРП. 3, КВ. 49",
      "RegDate": "1265148000",
      "Locality": "ЧЕРНІГІВ",
      "LocalityType": "місто",
      "Region": "ЧЕРНІГІВСЬКА область",
      "StatusName": "Припинено"
    },
    {
      "FopID": "083f18e0b84c7f21cd5c572f9ecdd4dc",
      "Name": "ГОНЧАРУК ОЛЕКСІЙ ВАЛЕРІЙОВИЧ",
      "Status": "terminated",
      "Address": "ЧЕРНІГІВСЬКА ОБЛ., М. ЧЕРНІГІВ, ВУЛ. БЄЛОВА, БУД. 21, КОРП. 3, КВ. 49",
      "RegDate": "1441918800",
      "Locality": "ЧЕРНІГІВ",
      "LocalityType": "місто",
      "Region": "ЧЕРНІГІВСЬКА область",
      "StatusName": "Припинено"
    },
    // ...
  ]
}
```

##### Опис полів:
* **FopID** - [ідентифікатор ФОП](fop.info.md#fopinfo);
* **Name** - ПІБ;
* **Status, StatusName** - стан ФОП;
* **Address**, **Locality, Region** - адреса, населений пункт та регіон реєстрації ФОП;
* **RegDate** - дата реєстрації (UNIX-timestamp);

## fop.info

Повертає актуальну інформацію про ФОП за його внутрішнім ідентифікатором.

##### Приклад запиту:
https://clarity-project.info/api/fop.info/c0a7d2d26cfc02758f1492aab0fca287?key=xxx

##### Приклад відповіді:
[examples/fop.info.json](examples/fop.info.json)