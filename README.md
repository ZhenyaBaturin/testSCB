# app_test

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

Описание проекта
... Страница-Форма для получение паспортных данных. Страница сделана на фреймворке VUE JS. Состоит из 2-х компонетов:
1. StepThree, в котором находится сама форма, далее она рендерится на страницу.
2. Sugg, в которой реализован инпут с использование библиотеки vue-suggestions(dadata) позволяющая автоматически заполнять инпут. Такие импуты как Страна, Регион, Город, и Улица заполняются автоматически после выбора позиции из подсказок от dadata

Компановка элементов страницы была выполнена с использование технологии Flexbox. Сама страница динамична и реагирует на изменение окна. При величине экрана менее 763 px поля для ввода данных растягиваются по влей длине экрана.  



