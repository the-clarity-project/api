# API для Clarity Project

[Опис API](README.md)

### Інформація про фізичних осіб

## persons.search
Метод повертає результати пошуку фізичних осіб за запитом, який передається у параметрі `q`.

##### Параметри:
* **q** - пошуковий запит;

##### Приклад запиту:
[https://clarity-project.info/api/edr.search/?q=шевченко&key=xxx]()

##### Приклад відповіді:
```json
{
  "list": [
    {
      "source": "asvp",
      "name": "ШЕВЧЕНКО НІНА ІВАНІВНА",
      "hash": "cb96b7a8518d2400e290682d0ec601f1"
    },
    {
      "source": "asvp",
      "name": "ШЕВЧЕНКО ЄВГЕНІЙ ВАЛЕНТИНОВИЧ",
      "hash": "cb9724bdd5992bdd74dfc15e0a6db25b"
    },
    {
      "source": "asvp",
      "name": "ШЕВЧЕНКО ВІРА ВАЛЕНТИНІВНА",
      "hash": "caee0d9e3c6f7eb151af4228809ae070"
    }
  ]
}
```
##### Опис полів:
* `source` - джерело запису;
* `name` - знайдений ПІБ;
* `hash` - ідентифікатор;

## persons.info
Метод повертає результати інформацію про фізичну особу за її ідентифікатором (`hash`).

##### Приклад запиту:
[https://clarity-project.info/api/edr.search/?q=шевченко&key=xxx]()

##### Приклад відповіді:
[[1](examples/persons.info/cc0e4e062a2139ac749698097e285d81.json)]
[[2](examples/persons.info/98e3856b5a0a13c64343b30c74810932.json)]
