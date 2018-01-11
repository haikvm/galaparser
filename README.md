## Полное обновление базы товаров
[POST] https://galamart.ru/importer/post/v1/catalog

### Переменные в запросе:
- **debug**: *1 или 0 (При 1 в ответе будет расширенный лог о работе парсера),*
- **file**: *ZIP-архив с JSON-файлом внутри*

### Формат JSON-массива:
```
{
  "date": "2018-01-11T13:31:38", // Дата формирования файла
  "sections": [ // Разделы
    {
      "id": "4S7MRAD", // ID раздела
      "name": "Посуда и кухонные принадлежности", // Название раздела
      "parent": "L" // ID родительского раздела
    },
    ...
  ],
  "categories": [ // Категории номенклатуры
    {
      "id": "d08483d1-2e3b-11e2-820e-78e3b5191410", // ID категории
      "title": "Цена управляющего" // Наименование
    },
    ...
  ],
  "items": [ // Товары
    {
      "id": "5N0GRAD", // ID товара
      "s_id": "4YS5RAD", // ID раздела
      "name": "SILAPRO Сноутьюб d100см,камера ПВХ, 3 дизайна", // Название товара
      "new": 0/1, // Новинка 
      "show": 0/1, // Показывать на сайте
      "code": "112-034", // Артикул
      "barcode": "4680259407179", // Штрихкод
      "dsc": "Сноутюб - санки, представляющие собой колесную камеру в специальном чехле." // Описание товара
      "props": [ // Массив свойств товара в формате НазваниеСвойства=ЗначениеСвойства
        "Размер=100 см",
        "Тип товара=сноутьюб",
        "Материал=ПВХ",
        "Бренд=SILAPRO",
        "Коллекция=сноутьюб",
        ...
      ],
      "shops": [ // Массив параметров магазинов
        "6f9a046a-bb62-11e5-95c0-00155d0b1018": { // ID магазина в качестве ключа
          "price": 1250, // Цена
          "old": 1313, // Старая цена
          "cat": "d08483d1-2e3b-11e2-820e-78e3b5191410", // Категория номенклатуры
          "q": 1 // Количество в магазине
        },
        ...
      ]
    },
    ...
  ]
}
```



## Обновление остатков и цен
[POST] https://galamart.ru/importer/post/v1/remains

### Переменные в запросе:
- **shop_id**: *'03fb1206-aaf8-11e6-86a8-d850e63b78b6' - ID магазина*
- **debug**: *1 или 0 (При 1 в ответе будет расширенный лог о работе парсера),*
- **file**: *ZIP-архив с JSON-файлом внутри*


### Формат JSON-файла с остатками и ценами:
```
{
  "date": "2018-01-11T13:31:38", // Дата формирования файла
  "shop_id": "03fb1206-aaf8-11e6-86a8-d850e63b78b6", // ID магазина
  "items": [ // Массив товаров
    {
      "id": "3GUSRAD", // ID товара
      "cat": "00000000-0000-0000-0000-000000000000", // /Категория номенклатуры
      "price": 360, // Новая цена
      "old": 514, // Старая цена
      "q": 1 // Количество
    },
    ...
  ]
}
```

### Формат JSON-файла только с остатками:
```
{
  "date": "2018-01-11T13:31:38", // Дата формирования файла
  "shop_id": "03fb1206-aaf8-11e6-86a8-d850e63b78b6", // ID магазина
  "items": [ // Массив товаров
    {
      "id": "3GUSRAD", // ID товара
      "q": 1 // Количество
    },
    ...
  ]
}
```



## Обновление/добавление магазинов
[POST] https://galamart.ru/importer/post/v1/shops

### Переменные в запросе:
- **debug**: *1 или 0 (При 1 в ответе будет расширенный лог о работе парсера),*
- **file**: *ZIP-архив с JSON-файлом внутри*
### Формат JSON-файла:
```
{
  "date": "2018-01-11T13:31:38", // Дата формирования файла
  "shops": [ // Массив магазинов
    {
      "id": "03fb1206-aaf8-11e6-86a8-d850e63b78b6", // ID магазина
      "fr": 1/0, //Франшизный магазин или нет.
      "title": "ЕКБ 40 лет Октября", // Краткое наименование
      "city": "Екатеринбург", // Город
      "adress": "ул. 40 лет Октября, 75", // Адрес
      "dsc": "ТЦ Калинка", // Комментарий
      "phones": [ // Массив телефонов
        "+7 (343) 378-40-03 (доб. 4085)",
        "+7 (343) 378-40-03 (доб. 4085)",
      ],
      "hrs": "Пн-Вс (09.00-21.00)" // Часы работы
    },
    ...
  ]
}
```

## Текущий статус работы парсера
[GET] https://galamart.ru/importer/post/v1/status
