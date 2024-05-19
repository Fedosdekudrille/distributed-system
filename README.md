*Этот проект я посвящаю Александру Гемзе*
# Распределённая клиент-серверная система
### Основной функционал и задачи: 
- Синхронизация времени
- Генерация данных на локальных серверах 
- Обработка ошибок
- Ожидание серверов, в случае если они лежат 
- Асинхронный опрос центральным сервером 
- Протоколирование работы сервисов
- Получение данных о состоянии сервисов 
- Репликация данных между локальными и центральным серверами

Общая схема взаимодействия выглядит примерно следующим образом:
![lab4_6main_scheme](https://github.com/mirmicuper/RIS_6sem/blob/main/FilesForMD/lab4_6main_scheme.png)
### Репликация данных между локальными и центральным серверами
Итак, самое важное что есть в этой лабе, это репликация 2 видов. 
Рассмотрим их на простой схеме с центральным и 1 локальным веб-сервисом:
![lab4_6replication_shemes](https://github.com/mirmicuper/RIS_6sem/blob/main/FilesForMD/lab4_6replication_schemes.png)
Обе репликации так или иначе инициируются центральный веб-сервисом. 
### Вытягивающая репликация. 
Вытягивающая она, потому что она ~~как бы~~ вытягивает данные из наших локальных веб-сервисов. 
Т.Е. центральный веб-сервис отправляет get-запрос нашему локальному веб-сервису, по типу "А дайка мне данные, которые у тебя есть"
И в ответе наш локальный веб-сервис отправляет все данные которые есть в его локальной БД.
Далее уже на центральном веб-сервисе происходит обработка этих данных. В случае если их нет в центральной БД, тогда они туда вставляются.
### Выталкивающая репликация. 
Выталкивающая она, потому что она ~~как бы~~ выталкивает данные из своей БД в локальные веб-сервисы, НО выталкивает она не все данные, а только те, которые принадлежат данному локальному сервису. 
Происходит это следующим образом: 
На нашем центральном веб-сервисе мы запрашиваем из центральной БД все данные которые принадлежат определенному локальному веб-сервису. Далее мы через post-запрос отправляем эти данные определенному веб-сервису. На локальном веб-сервисе происходит проверка данные, есть ли они в локальной БД этого локального веб-сервиса, и в случае если какие-то их них отсутствуют, происходит их вставка в БД. 
