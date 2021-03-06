# Приложение для создания и редактирования информации о встречах сотрудников

Написано для Node.js 8 и использует библиотеки:
* express
* sequelize
* graphql

## Задание
Код содержит ошибки разной степени критичности. Некоторых из них стилистические, а некоторые даже не позволят вам запустить приложение. Вам необходимо найти и исправить их.

Пункты для самопроверки:
1. Приложение должно успешно запускаться
2. Должно открываться GraphQL IDE - http://localhost:3000/graphql/
3. Все запросы на получение или изменения данных через graphql должны работать корректно. Все возможные запросы можно посмотреть в вкладке Docs в GraphQL IDE или в схеме (typeDefs.js)
4. Не должно быть лишнего кода
5. Все должно быть в едином codestyle

## Запуск
```
npm i
npm run dev
```

Для сброса данных в базе:
```
npm run reset-db
```


# Процесс работы

1. Изучаем проект: папки, файлы, package.json, краткие общие сведения о Express, Sequelize, Graphql.
2. npm i - успешно.
3. npm run dev -
  Error('Dialect needs to be explicitly supplied as of v4.0.0');
  ...
  Error: Dialect needs to be explicitly supplied as of v4.0.0
      at new Sequelize (E:\github\shri-2018-task-1\node_modules\sequelize\lib\sequelize.js:175:13)
      at Object.<anonymous> (E:\github\shri-2018-task-1\models\index.js:7:19)
<!-- > shri-2018@1.0.0 dev E:\github\shri-2018-task-1
> nodemon index.js

[nodemon] 1.12.5
[nodemon] to restart at any time, enter `rs`
[nodemon] watching: *.*
[nodemon] starting `node index.js`
E:\github\shri-2018-task-1\node_modules\sequelize\lib\sequelize.js:175
      throw new Error('Dialect needs to be explicitly supplied as of v4.0.0');
      ^

Error: Dialect needs to be explicitly supplied as of v4.0.0
    at new Sequelize (E:\github\shri-2018-task-1\node_modules\sequelize\lib\sequelize.js:175:13)
    at Object.<anonymous> (E:\github\shri-2018-task-1\models\index.js:7:19)
    at Module._compile (module.js:660:30)
    at Object.Module._extensions..js (module.js:671:10)
    at Module.load (module.js:573:32)
    at tryModuleLoad (module.js:513:12)
    at Function.Module._load (module.js:505:3)
    at Module.require (module.js:604:17)
    at require (internal/module.js:11:18)
    at Object.<anonymous> (E:\github\shri-2018-task-1\graphql\resolvers\query.js:1:82)
    at Module._compile (module.js:660:30)
    at Object.Module._extensions..js (module.js:671:10)
    at Module.load (module.js:573:32)
    at tryModuleLoad (module.js:513:12)
    at Function.Module._load (module.js:505:3)
    at Module.require (module.js:604:17)
    at require (internal/module.js:11:18)
    at Object.<anonymous> (E:\github\shri-2018-task-1\graphql\resolvers\index.js:3:15)
    at Module._compile (module.js:660:30)
    at Object.Module._extensions..js (module.js:671:10)
    at Module.load (module.js:573:32)
    at tryModuleLoad (module.js:513:12)
[nodemon] app crashed - waiting for file changes before starting... -->
4. Изучаем Sequelize, http://docs.sequelizejs.com/manual/installation/getting-started.html. Видим ошибку в задании параметров: null, null.
5. Вбиваем ошибку "Error: Dialect needs to be explicitly supplied as of v4.0.0" в поисковик. Убеждаемся в правильном ходе мыслей. Исправляем строку в models/index.js:
"const sequelize = new Sequelize(null, null, {...});"
на строку из документации:
"const sequelize = new Sequelize('database', 'username', 'password', {...});"
6. npm run dev - успешно.
7. Проверка http://localhost:3000/ - успешно.
8. Проверка http://localhost:3000/graphql/ - Cannot GET /graphql/
9. Изучаем npm graphql, express-graphql, graphql-tools, graphql-date (из package.json).
10. Переход к следующему этапу, так как пока знаний для последующей отладки не достаточно, а время, отведенное на выполнение, ограничено. Запланированно вернуться позже к предыдущему пункту.
11. npm run lint (из packaje.json) - найдены проблемные строки.
<!-- > shri-2018@1.0.0 lint E:\github\shri-2018-task-1
> semistandard

semistandard: Semicolons For All! (https://github.com/Flet/semistandard)
semistandard: Run `semistandard --fix` to automatically fix some problems.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:4:1: Expected indentation of 2 spaces but found 0.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:5:5: Expected indentation of 2 spaces but found 4.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:6:3: Expected indentation of 0 spaces but found 2.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:8:33: 'argumets' is not defined.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:10:1: Expected indentation of 2 spaces but found 0.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:11:5: Expected indentation of 2 spaces but found 4.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:12:3: Expected indentation of 0 spaces but found 2.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:16:1: Expected indentation of 2 spaces but found 0.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:17:5: Expected indentation of 2 spaces but found 4.
  E:\github\shri-2018-task-1\graphql\resolvers\query.js:18:3: Expected indentation of 0 spaces but found 2.
  E:\github\shri-2018-task-1\graphql\routes.js:18:17: Unexpected trailing comma.
  E:\github\shri-2018-task-1\index.js:13:26: Missing semicolon.
  E:\github\shri-2018-task-1\models\index.js:11:1: Expected indentation of 2 spaces but found 0.
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! shri-2018@1.0.0 lint: `semistandard`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the shri-2018@1.0.0 lint script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\Admin\AppData\Roaming\npm-cache\_logs\2018-01-02T15_17_14_363Z-debug.log -->
12. Исправляем форматирование кода в graphql\resolvers\query.js, а так же в events заменяем argumets на {} (по аналогии с users).
13. Исправляем форматирование кода в graphql\routes.js.
14. Исправляем форматирование кода в index.js.
15. Исправляем форматирование кода в models\index.js.
16. Возвращаемся к пункту 8 (http://localhost:3000/graphql/ - Cannot GET /graphql/). Ищем как вообще должен выглядеть GraphQL IDE. Из документации GraphQL для Express (http://graphql.org/graphql-js/running-an-express-graphql-server/) вставляем в index.js базовый пример кода (старый код закомментирован), проверям - GraphQL IDE открывается. Начинаем построчно возвращать структуру проекта, следя за работоспособностью. Переходя от файла index.js к graphql/routes.js и к graphql/resolvers/index.js, сверяемся с документацией к npm graphql-tools (https://www.npmjs.com/package/graphql-tools) - находим ошибку "resolvers: resolvers()" и "function resolvers ()". Исправляем.
17. Еще раз проходимся npm run lint.
18. Запросы  через graphql на первый взгляд работают корректно, но не хватает знаний для оценки. Планируем вернуться позже, если останется время. Переходим ко второй части тестового задания.
19. Когда второе задание завершено и разбирается третье, понимаем что нужны запросы и снова изучаем информацию о том какие бывают запросы и как они должны себя вести.
    * Проверяем query запросы.
    Находим ошибку в запросе event - вместо данных users и room возвращается null. Проверям graphql/resolvers, добавляем в index.js в users (event) и room (event) return.
    * Проверяем mutation запросы.
    Запрос на создание пользователя работает. Но при запросе данных по созданному пользователю, возвращается ошибка об отсутсвии авватарки. Проверяю typeDef.js. Я не уверена, что по заданию здесь можно исправлять данные, но не логично что у пользователя аватарка является обязательными данными, а домашний этаж нет, ведь он требуется для подбора рекомендованных переговорок. Изменяем в type User этаж на обязательный, а аватарку на необязательный пункт. Добавляем возможность указать аватарку в input UserInput, а также обязательным пуктом вставляем этаж пользователя.
    Запрос UpdateUser работает, но при так как у них с CreateUser одинаковое содержимое input, каждый раз нужно для обновления данных вводить в обязательном порядке login и homeFloor, хотя мы можем хотеть изменить только аватарку, поэтому создадим новый input UpdateInput, где есть эти два пункта и аватарка, но все пункты необязательные. То есть зная только id пользователя мы можем изменить любою другую информацию о нем.
    В запросе объекта Event комната (Room) является необязательными данными. Но не может же встреча проходить в "нигде". Делаем Room обязательной.
    По запросу addUserToEvent выдает null. Проверяем в typeDef.js описание addUserToEvent - оно есть и корректно. Проверяем mutation.js - addUserToEvent отсутствует. Добавляем его по аналогии с removeUserFromEvent.
    Проверяем запрос changeEventRoom. Он возвращает null. Проверяем mutation.js - changeEventRoom есть, но в нем отсутсвует return event - добавляем. Запрос возвращает event, но переговорка не изменилась. Изменяем в setRoom(Id) на setRoom(roomId). Запрос успешно изменяет переговорку.
20. Файл controllers.js в папке pages по сути просто содержит "заглушку" для главной страницы и нет причин хранить ее в отдельном файле. На месте заглушки потом появиться главная страница приложения. Объединяем файл controllers.js и routes.js. Проверяем - все работает.
21. В документации Express (генератор приложений) упоминается папка pages, но я уже знаю что у меня будет всего одна html-страница и мне достаточно одной строки в index.js:
```
app.use('/', express.static(path.join(__dirname, 'public')));
```
вместо всей папки pages. Для меня это спорный момент, но я решила все таки удалить папку и перенести заготовку index.html в папку public. В обычной ситуации я бы посоветовалась с кем-то более опытным.
22. В параметрах ответа на запрос в файле graphql/resolvers/query.js убираем "offset: 1", иначе при запросе теряем одну переговорку.
