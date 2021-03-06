# Тестовое задание idaproject

[Описание тестового задания](https://idaproject.notion.site/Frontend-developer-test-9b834d020d8f406f851479791209beef)

[Макет в Figma](https://www.figma.com/file/kIuVw6nSk218pi9iE98iq5/Junior-frontend-developer-test?node-id=4%3A365)

Данное приложение - мой первый опыт работы с Vue и сборщиком Nuxt.js. Раньше работала только с ReactJS, Vue показался немного похожим и не очень сложным на таком уровне. 

В качестве CSS-препроцессора использовался SCSS.

Линтер - ESLint.

Выполнено - 3 уровня:

1 уровень: настроена сборка проекта, использовался фреймворк - Vue, CSS-препроцессор - SCSS, добавлена стилизация состояний и адаптивная версия под мобильные устройства.

2 уровень: добавлена валидация формы, реализовано поведение кнопки при пустой и не валидной форме, реализован функционал добавления товара на страницу, добавлен показ состояния при добавлении товара на страницу, анимация перехода состояний.

3 уровень: добавлен функционал удаления товара из списка, сохранение состояния при перезагрузке страницы (с помощью сохранения списка товаров в LocalStorage), разработан функционал сортировки по всем параметрам, добавлена анимация сортировки товара.

## Деплой
https://resilient-centaur-b4624b.netlify.app/

## Запуск сервера
```
npm i
npm run dev
```

## Запуск статической сборки
```
npm i
npm run generate
```
