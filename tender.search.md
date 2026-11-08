# API для Clarity Project

[Опис API](README.md)

### Інформація про закупівлі Prozorro

## tender.ids

Метод дозволяє перетворювати між собою `hash` та `UA-...` ідентифікатори закупівель.

##### Приклад запиту:
https://clarity-project.info/api/tender.ids?ids=UA-2018-07-23-000245-b,30552368575d47e689ed2cdcb1cedb8f&key=xxx

У параметрі ``ids`` передаються ідентифікатори (`UA-...` або hash) через кому, до 10 за один запит.

##### Приклад відповіді:
```json
{
  "list": [
    {
      "id": "bd97249f16d94bf6938a2fc6cb4a8ff7",
      "tender": "UA-2018-07-23-000245-b"
    },
    {
      "id": "30552368575d47e689ed2cdcb1cedb8f",
      "tender": "UA-2016-07-27-000340-b"
    },
    // ...
  ]
}
```

## tender.search

Метод дозволяю шукати закупівлі за обраними критеріями.

##### Приклад запиту:
https://clarity-project.info/api/tender.search?key=xxx

### Пошукові критерії

Пошукові критерії передаються як get-параметри запиту.
Зверніть увагу: зазви фільтрів **відрізняються** від пошуку [через веб-інтерфейс](https://clarity-project.info/tenders).  

* **offset** - використовується для пагінації, обирає, починаючи з якого результату повертати рядки. 
* **sort** - сортування результатів, завжди за спаданням, за замовчуванням **Modified**:
    * **Modified** - по даті оновлення;
    * **Created** - по даті створення;
    * **AwardDate** - по даті визначення переможця;
    * **Value** - по ціні;
    * **Economy** - по економії;
    * **Lots** - по кількості лотів;
    * **Bids** - по кількості пропозицій;
    * **Tenderers** - по кількості учасників;
    * **Disqualifications** - по кількості дискваліфікацій;
    * **Contracts** - по кількості договорів;
    * **ContractChanges** - по кількості додаткових угод;
* **tender_id** - ідентифікатори закупівель (до 10 за запит);
* **text** - повнотекстовий пошук за описом закупівлі;
* **status** - стан закупівлі: 
    * **active** - в процессі;
    * **complete** - успішні;
    * **cancelled** - відмінені;
    * **unsuccessful** - не відбулися;
* **entity** - ЄДРПОУ замовника;
* **entity_type** - тип замовника:
    * **defense** - Замовник, що здійснює закупівлі для потреб оборони,
    * **general** - Юридична особа, яка забезпечує потреби держави або територіальної громади,
    * **other** - Державне або комунальне підприємство, яке не належить до замовників,
    * **special** - Юридична особа, яка здійснює діяльність в одній або декількох окремих сферах господарювання,
    * **central** - Юридична особа, що здійснює закупівлі в інтересах замовників (ЦЗО),
    * **authority** - Орган державної влади, місцевого самоврядування або правоохоронний орган,
    * **social** - Орган соціального страхування.
* **tenderer** - ЄДРПОУ учасника закупівлі;
    * можна вказувати декілька кодів через `+` (закупівлі, де були ці учасники були разом) або `,` (закупівлі, де був
      хоча б один з учасників);
* **tenderer_status** - статус учасника:
    * **tenderer** - учасник;
    * **disqualified** - дискваліфікація;
    * **supplier** - переможець;
    * **contractor** - підписано договір;
    * *наприклад*, `tenderer=ххх&tenderer_status=contractor` обере лише закупівлі, де з цим 
    учасником було підписано контракт;
* **contract_status** - статус контракту, підписаного в результаті закупівлі:
    * **pending** - запропоновано;
    * **active** - підписано;
    * **cancelled** - скасовано;
    * **done** - завершено успішно;
    * **failed_no_paid** - розівано (з виплатами);
    * **failed_paid** - розівано (без виплат);
* **contract_term_reason** - причина розірвання договору;
* **disq_reason** - причина дискваліфікації учасника;
* **value_min**, **value_max** - очікувана вартість;
* **currency** - валюта;
* **nonprice** - наявність нецінових критеріїв:
    * **yes** - закупівлі з неціновими критеріями;
    * **no** - без нецінових критеріїв;
* **fin_source** - джерело фінансування:
    * **state** - Державний бюджет України;
    * **crimea** - Бюджет Автономної Республіки Крим;
    * **fund** - Бюджет цільових фондів;
    * **loan** - Кредити та позики міжнародних валютно-кредитних організацій;
    * **local** - Місцевий бюджет;
    * **own** - Власний бюджет (кошти від господарської діяльності підприємства);
    * **donor** - Кошти донора;
    * **other** - Інше;
* **modified_from**, **modified_to** - дата зміни інформації про закупівлю, у форматі `дд-мм-рррр`;
* **created_from**, **created_to** - дата створення закупівлі;
* **classification** - CPV-код предмету закупівлі;
* **cpv_class** - класифікація предмету закупівлі:
    * **works** - роботи;
    * **services** - рослуги;
    * **goods** - товари;
* **market_product** - ідентифікатор товару Prozorro Market;
* **market_profile** - ідентифікатор профілю Prozorro Market;
* **market_category** - ідентифікатор категорії Prozorro Market;
* **payment_type** - тип оплати:
    * **prepayment** - передоплата;
    * **postpayment** - післяплата;
* **payment_after** - оплата після:
    * **executionOfWorks** - виконання робіт;
    * **deliveryOfGoods** - поставки товару;
    * **submittingServices** - надання послуг;
    * **signingTheContract** - підписання договору;
    * **dateOfInvoicing** - дати виставлення рахунку;
    * **endDateOfTheReportingPeriod** - дати закінчення звітного періоду;
    * **anotherEvent** - іншої події;
* **region** - код регіону замовника;
* **method** - метод закупівлі: відкрита (**open**) або звітування (**limited**);
* **type** - процедура закупівлі:
    * **aboveThresholdUA** - Відкриті торги;
    * **aboveThresholdEU** - Відкриті торги (EU);
    * **belowThreshold** - Допорогова закупівля;
    * **negotiation** - Переговорна процедура;
    * **negotiation.quick** - Переговорна процедура (за нагальною потребою);
    * **reporting** - Звіт про договір;
    * **esco** - Закупівля енергосервісу;
    * **competitiveDialogue** - Конкурентний діалог;
    * **competitiveDialogueUA** - Конкурентний діалог (UA);
    * **competitiveDialogueEU** - Конкурентний діалог (EU);
    * **priceQuotation** - Запит ціни пропозицій;
    * **competitiveDialogue.stage2** - Конкурентний діалог, 2 етап;
    * **competitiveDialogueEU.stage2** - Конкурентний діалог (EU), 2 етап;
    * **competitiveDialogueUA.stage2** - Конкурентний діалог (UA), 2 етап;
    * **aboveThresholdUA.defense** - Закупівля для потреб оборони;
    * **closeFrameworkAgreementUA** - Укладання рамкової угоди';
    * **closeFrameworkAgreementSelectionUA** - Відбір для закупівлі за рамковою угодою';
* **method_rationale** - причина обрання процедури:
    * **COVID-19** - COVID-19;
    * **catalogue** - Е-каталог;
    * **negotiation.artContestIP** - Інтелектуальна власність;
    * **negotiation.noCompetition** - Відсутність конкуренції на ринку;
    * **negotiation.twiceUnsuccessful** - Двічі не відбулись торги;
    * **negotiation.additionalPurchase** - Додаткову закупівля в того самого постачальника;
    * **negotiation.additionalConstruction** - Нобхідність проведення додаткових будівельних робіт;
    * **negotiation.stateLegalServices** - Закупівля юридичних послуг;
    * **negotiation.quick** - Нагальна потреба;
* **complaints** - наявність скарг до закупівлі:
    * **yes** - зі скаргами;
    * **no** - без скарг;
* **complaint_from** - ЄДРПОУ скаржника;
* **monitorings** - наявність моніторингу:
    * **yes** - з моніторингом;
    * **no** - без моніторингу;
* **monitoring_reason** - причина моніторингу:
    * **indicator** - Індикатори ризиків;
    * **authorities** - Інформація, отримана від органів влади;
    * **media** - Повідомлення в ЗМІ;
    * **fiscal** - Виявлені органом державного фінансового контролю ознаки порушення;
    * **public** - Інформація від ГО;
* **monitoring_status** - статус моніторингу:
    * **declined** - Порушення не виявлені;
    * **active** - Здійснення моніторингу;
    * **addressed** - Виявлені порушення;
    * **closed** - Завершено;
* **contract_changes** - наявність додаткових угод:
    * **yes** - з додатковими угодами;
    * **no** - без додаткових угод;
* **tender_period_from** та **tender_period_to** - кінцева дата подання пропозицій;
* **award_date_from** та **award_date_to** - дата визначення переможця;
* **guarantee** - забезпечення пропозицій:
    * **yes** - з тендерним забезпеченням;
    * **no** - без тендерного забезпечення;
* **contract_security** - забезпечення виконання договору:
    * **yes** - із забезпеченням;
    * **no** - без забезпечення;
* **qualification_criteria** - кваліфікаційні критерії:
    * **CRITERION.SELECTION.TECHNICAL_PROFESSIONAL_ABILITY.TECHNICAL.EQUIPMENT** - Наявність обладнання, матеріально-технічної бази та технологій;
    * **CRITERION.SELECTION.TECHNICAL_PROFESSIONAL_ABILITY.TECHNICAL.STAFF_FOR_CARRYING_SCOPE** - Наявність працівників відповідної кваліфікації;
    * **CRITERION.SELECTION.TECHNICAL_PROFESSIONAL_ABILITY.REFERENCES.WORKS_PERFORMANCE** - Наявність досвіду виконання аналогічного договору;
    * **CRITERION.SELECTION.ECONOMIC_FINANCIAL_STANDING** - Наявність фінансової спроможності;
    * **CRITERION.SELECTION.TECHNICAL_PROFESSIONAL_ABILITY.MANAGEMENT.SUBCONTRACTING_PROPORTION** - Інформування про субпідрядників/співвиконавців;
    * **CRITERION.SELECTION.TECHNICAL_PROFESSIONAL_ABILITY.TECHNICAL.ENVIRONMENTAL_MANAGEMENT_MEASURES** - Відповідність екологічним нормам;
* **exclusion_grounds** - підстави для відмови в участі:
    * **CRITERION.EXCLUSION.CONFLICT_OF_INTEREST.MISINTERPRETATION** - Наявність впливу на прийняття рішення замовника;
    * **CRITERION.EXCLUSION.CONVICTIONS.CORRUPTION** - Вчинення корупційних правопорушень;
    * **CRITERION.EXCLUSION.CONVICTIONS.FRAUD** - Вчинення економічних правопорушень;
    * **CRITERION.EXCLUSION.CONVICTIONS.PARTICIPATION_IN_CRIMINAL_ORGANISATION** - Вчинення кримінальних правопорушень;
    * **CRITERION.EXCLUSION.MISCONDUCT.MARKET_DISTORTION** - Наявність зв'язку учасника з іншими учасниками процедури або замовником;
    * **CRITERION.EXCLUSION.BUSINESS.BANKRUPTCY** - Порушення справи про банкрутство;
    * **CRITERION.EXCLUSION.NATIONAL.ANTI-CORRUPTION** - Наявність антикорупційної програми;
    * **CRITERION.EXCLUSION.CONVICTIONS.TERRORIST_OFFENCES** - Вчинення правопорушень, пов'язаних із застосуванням санкцій;
    * **CRITERION.EXCLUSION.CONVICTIONS.CHILD_LABOUR-HUMAN_TRAFFICKING** - Вчинення правопорушень, пов'язаних з використанням дитячої праці чи будь-якими формами торгівлі людьми;
    * **CRITERION.EXCLUSION.CONTRIBUTIONS.PAYMENT_OF_TAXES** - Наявність заборгованості зі сплати податків і зборів;
    * **CRITERION.EXCLUSION.CONFLICT_OF_INTEREST.EARLY_TERMINATION** - Наявність не виконаних зобов'язань за раніше укладеним договором;
    * **CRITERION.EXCLUSION.NATIONAL.OTHER** - Наявність інших підстав для відмови в участі у процедурі закупівлі;
* **other_requirements** - інші вимоги:
    * **CRITERION.OTHER.SUBJECT_OF_PROCUREMENT.LOCAL_ORIGIN_LEVEL** - Створення передумов для сталого розвитку та модернізації вітчизняної промисловості;
    * **CRITERION.OTHER.SUBJECT_OF_PROCUREMENT.TECHNICAL_FEATURES** - Технічні, якісні та кількісні характеристики предмета закупівлі;
    * **CRITERION.OTHER.BID.VALIDITY_PERIOD** - Строк дії тендерної пропозиції;
    * **CRITERION.OTHER.BID.LANGUAGE** - Мова (мови) тендерної пропозиції;
    * **CRITERION.OTHER.UKRAINE_FACILITY** - Вимоги до товару та переможця закупівлі, що проводиться в рамках проєкту Ukraine Facility;
* **life_cycle_cost** - вартість життєвого циклу:
    * **CRITERION.OTHER.LIFE_CYCLE_COST.COST_OF_USE** - Витрати, пов'язані з користуванням, грн.;
    * **CRITERION.OTHER.LIFE_CYCLE_COST.MAINTENANCE_COST** - Витрати, пов'язані з обслуговуванням, грн.;
    * **CRITERION.OTHER.LIFE_CYCLE_COST.END_OF_LIFE_COST** - Витрати, пов'язані з завершенням користування, грн.;
    * **CRITERION.OTHER.LIFE_CYCLE_COST.ECOLOGICAL_COST** - Витрати, пов'язані з захистом навколишнього середовища, грн.;

Параметри `qualification_criteria`, `exclusion_grounds`, `other_requirements` та `life_cycle_cost` приймають одне значення 
або кілька у вигляді масиву, наприклад: `exclusion_grounds[]=CRITERION.EXCLUSION.BUSINESS.BANKRUPTCY&exclusion_grounds[]=CRITERION.EXCLUSION.CONVICTIONS.FRAUD`.

Якщо передано кілька критеріїв, у тому числі в різних параметрах, метод повертає лише закупівлі, в яких є всі вказані критерії.
Невідомі значення цих параметрів, зокрема кілька значень через кому, ігноруються.

### Додаткові поля

За замовчуванням метод повертає лише базову інформацію про закупівлі. 
Для отримання детальної інформації необхідно передати get-параметр `more_fields` з обраними розділами.

Станом на зараз, кількість додаткових розділів не обмежується.
*Можливо*, це зміниться в майбутньому. 

**Приклад запиту:**
https://clarity-project.info/api/tender.search?more_fields=edrs,contracts&key=xxx

**Опис можливих параметрів:**
* **edrs** - інформація про учасників і замовника;
* **lots** - інформація про лоти закупівлі;
* **items** - предмети закупівлі;
* **contracts** - договори;
* **docs** - документи закупівлі;
* **periods** - інформація про важливі дати;

**Приклад відповіді:**

[examples/tender.search.json](examples/tender.search.json)
