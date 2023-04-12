<h2> Базовые возможности mongodb </h2>
<h3> Развертывание ВМ </h3>
Развернул тестовую виртуалку на Ubuntu 20.2 в облаке Яндекс, настроил авторизацию по ssh-ключу пары, сгенеренной в MobaXterm:

<img width="511" alt="Убунта" src="https://user-images.githubusercontent.com/130138730/231439912-384369e5-3275-4177-924e-b7650a063072.png">

<h3> Установка mongdb 6 </h3>
Добавил репозитории, установил и запустил БД

<img width="775" alt="image" src="https://user-images.githubusercontent.com/130138730/231440465-8f2aea20-d59f-43a9-bfc9-348e42a394a9.png">

Манипуляции с БД и данными:
Создал БД, коллекцию, импортировал тестовые данные на 10000 документов (нашел в интернетах) через mongoimport:

<img width="829" alt="image" src="https://user-images.githubusercontent.com/130138730/231447176-258b4709-3959-415c-8adc-b7e3cfb953fc.png">

```
test> use meteo
switched to db meteo
meteo> show collections
show collections

meteo> show collections
weather
meteo> db.weather.countDocuments()
10000
meteo> db.weather.find().limit(2)
[
  {
    _id: ObjectId("5553a998e4b02cf7151190b8"),
    st: 'x+47600-047900',
    ts: ISODate("1984-03-05T13:00:00.000Z"),
    position: { type: 'Point', coordinates: [ -47.9, 47.6 ] },
    elevation: 9999,
    callLetters: 'VCSZ',
    qualityControlProcess: 'V020',
    dataSource: '4',
    type: 'FM-13',
    airTemperature: { value: -3.1, quality: '1' },
    dewPoint: { value: 999.9, quality: '9' },
    pressure: { value: 1015.3, quality: '1' },
    wind: {
      direction: { angle: 999, quality: '9' },
      type: '9',
      speed: { rate: 999.9, quality: '9' }
    },
    visibility: {
      distance: { value: 999999, quality: '9' },
      variability: { value: 'N', quality: '9' }
    },
    skyCondition: {
      ceilingHeight: { value: 99999, quality: '9', determination: '9' },
      cavok: 'N'
    },
    sections: [ 'AG1' ],
    precipitationEstimatedObservation: { discrepancy: '2', estimatedWaterDepth: 999 }
  },
  {
    _id: ObjectId("5553a998e4b02cf7151190b9"),
    st: 'x+45200-066500',
    ts: ISODate("1984-03-05T14:00:00.000Z"),
    position: { type: 'Point', coordinates: [ -66.5, 45.2 ] },
    elevation: 9999,
    callLetters: 'VC81',
    qualityControlProcess: 'V020',
    dataSource: '4',
    type: 'FM-13',
    airTemperature: { value: -4.7, quality: '1' },
    dewPoint: { value: 999.9, quality: '9' },
    pressure: { value: 1025.9, quality: '1' },
    wind: {
      direction: { angle: 999, quality: '9' },
      type: '9',
      speed: { rate: 999.9, quality: '9' }
    },
    visibility: {
      distance: { value: 999999, quality: '9' },
      variability: { value: 'N', quality: '9' }
    },
    skyCondition: {
      ceilingHeight: { value: 99999, quality: '9', determination: '9' },
      cavok: 'N'
    },
    sections: [ 'AG1' ],
    precipitationEstimatedObservation: { discrepancy: '2', estimatedWaterDepth: 999 }
  }
]
meteo>
```
Выбрал 2 записи, где температура была выше -1 градуса:
```
meteo> db.weather.find( { "airTemperature.value": { $gt: -1 } } ).limit(2)
[
  {
    _id: ObjectId("5553a998e4b02cf7151190ba"),
    st: 'x+51900+003600',
    ts: ISODate("1984-03-05T14:00:00.000Z"),
    position: { type: 'Point', coordinates: [ 3.6, 51.9 ] },
    elevation: 9999,
    callLetters: 'PLAT',
    qualityControlProcess: 'V020',
    dataSource: '4',
    type: 'FM-13',
    airTemperature: { value: 4.4, quality: '1' },
    dewPoint: { value: 3.5, quality: '1' },
    pressure: { value: 1030.8, quality: '1' },
    wind: {
      direction: { angle: 200, quality: '1' },
      type: 'N',
      speed: { rate: 1, quality: '1' }
    },
    visibility: {
      distance: { value: 999999, quality: '9' },
      variability: { value: 'N', quality: '9' }
    },
    skyCondition: {
      ceilingHeight: { value: 99999, quality: '9', determination: '9' },
      cavok: 'N'
    },
    sections: [ 'AG1', 'MD1', 'OA1', 'SA1', 'UA1' ],
    precipitationEstimatedObservation: { discrepancy: '2', estimatedWaterDepth: 999 },
    atmosphericPressureChange: {
      tendency: { code: '2', quality: '1' },
      quantity3Hours: { value: 0.9, quality: '1' },
      quantity24Hours: { value: 99.9, quality: '9' }
    },
    seaSurfaceTemperature: { value: 4.5, quality: '9' },
    waveMeasurement: {
      method: 'I',
      waves: { period: 4, height: 0.5, quality: '9' },
      seaState: { code: '99', quality: '9' }
    }
  },
  {
    _id: ObjectId("5553a998e4b02cf7151190bb"),
    st: 'x+60900-005300',
    ts: ISODate("1984-03-05T15:00:00.000Z"),
    position: { type: 'Point', coordinates: [ -5.3, 60.9 ] },
    elevation: 9999,
    callLetters: 'TFRB',
    qualityControlProcess: 'V020',
    dataSource: '4',
    type: 'FM-13',
    airTemperature: { value: 7.5, quality: '1' },
    dewPoint: { value: 999.9, quality: '9' },
    pressure: { value: 1018.5, quality: '1' },
    wind: {
      direction: { angle: 220, quality: '1' },
      type: 'N',
      speed: { rate: 12.3, quality: '1' }
    },
    visibility: {
      distance: { value: 4000, quality: '1' },
      variability: { value: 'N', quality: '9' }
    },
    skyCondition: {
      ceilingHeight: { value: 99999, quality: '9', determination: '9' },
      cavok: 'N'
    },
    sections: [ 'AG1', 'AY1', 'GF1', 'MW1' ],
    precipitationEstimatedObservation: { discrepancy: '2', estimatedWaterDepth: 0 },
    pastWeatherObservationManual: [
      {
        atmosphericCondition: { value: '0', quality: '1' },
        period: { value: 3, quality: '1' }
      }
    ],
    skyConditionObservation: {
      totalCoverage: { value: '08', opaque: '99', quality: '1' },
      lowestCloudCoverage: { value: '99', quality: '9' },
      lowCloudGenus: { value: '99', quality: '9' },
      lowestCloudBaseHeight: { value: 99999, quality: '9' },
      midCloudGenus: { value: '99', quality: '9' },
      highCloudGenus: { value: '99', quality: '9' }
    },
    presentWeatherObservationManual: [ { condition: '02', quality: '1' } ]
  }
]
meteo>
```
Для разнообразия профилировал запрос в Компасе:
<img width="746" alt="image" src="https://user-images.githubusercontent.com/130138730/231453272-6d03842d-12bc-461b-b1bf-c927ba9ca54b.png">

Создал индекс по значению температуры воздуха и повторил запрос. Стало медленнее.

<img width="749" alt="image" src="https://user-images.githubusercontent.com/130138730/231454117-3cc8fd16-c8f2-4af0-bba2-7414acf8cea3.png">

Причина - низкая селективность запроса. Зададим условие равенства, чтобы повысить селективность.
С индексом:

<img width="749" alt="image" src="https://user-images.githubusercontent.com/130138730/231454725-7949828d-b20a-4ca4-9297-08bfe334eda5.png">
Без индекса те же 9 миллисекунд:

<img width="743" alt="image" src="https://user-images.githubusercontent.com/130138730/231455001-d8393f3b-ff0a-475b-a436-d6f7ab7d4a0d.png">

С индексом работает быстро, ура!
