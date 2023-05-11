# Торговый робот с использованием нейросетей
## Hackathon-Finam-NN-Trade-Robot
```shell
Сделан в рамках соревнования Хакатон «Финам Trade API» 
по созданию торговых систем на основе открытого торгового API «Финама»
```

#### Почему я выбрал использование нейросетей для торгового робота?
1. Тема использования искусственного интеллекта актуальна:
   - для прогнозирования поведения фондового рынка в целом, 
   - для осуществления предсказаний поведения цены отдельных акций и/или фьючерсов и других инструментов
   - для поиска определенных торговых формаций на графиках цен
    

2. Широкое применение искусственного интеллекта очень активно развивается на Западных рынках, на Российском всё только начинается.
   

3. В открытом доступе нет полноценных примеров по использованию нейросетей для прогнозирования цен акций/фьючерсов, а те которые есть
   - или не работают 
   - или чего-то для их работы постоянно не хватает.
     - По крайней мере лично мне ещё ни разу не встретились полноценно работающие примеры.


Поэтому и принял решение сделать торгового робота, который использует нейросети на основе компьютерного зрения для поиска определенных формаций 
на торговом графике акций и используя лучшую обученную модель осуществляет торговые операции.  

#### Какие есть скрытые цели? )))
Т.к. этот пример торгового робота с использованием нейросетей хорошо документирован и последовательно проходит через все этапы:
    
- получение исторических данных по акциям
- подготовка датасета с картинками формаций из графика акций по определенной логике
- обучение нейросети и выбор лучшей обученной модели по параметрам loss, accuracy, val_loss, val_accuracy 
- проверка предсказаний сделанных нейросетью
- проверка подключения к API Финама
- запуск live стратегии с использованием выбранной лучшей модели обученной нейросети
- записано обучающее видео как запускать и работать с этим кодом, выложенное [на YouTube](https://youtu.be/yrQFqvc4fk0 ) и [на RuTube](https://rutube.ru/video/private/1255dfe65f4db8736b894cae72b14c45/?p=oOFSDPr1El6lq586tIm2qg )

то, это позволит всем, кто только начинает свой путь по применению нейросетей для аналитики, использовать этот код, 
как стартовый шаблон с последующим его усовершенствованием и допиливанием)) 

- По крайней мере появился +1 рабочий пример использования нейросетей для аналитики цен графика акций.

Тем самым, станет больше роботов с использованием искусственного интеллекта,
```
- это повлечет большую волатильность нашего фондового рынка
- большую ликвидность за счет большего количества сделок
- и соответственно больший приток капитала в фондовый рынок
```

#### Зарабатывает ли сейчас этот робот?
Торговая стратегия заложенная в этом роботе не даст ему заработать, 
т.к. мы открываем позицию по подтвержденной нейросетью формации на графике 
(т.е. когда нейросеть предсказывает, что вероятно будет рост), 
но мы не ждем роста и закрываем позицию через +1 бар старшего таймфрейма.
*Как вариант, можно заходить в сделку 1 к 3 или 1 к 5 со стоп-лоссом. Т.е. ждать профита или стоп-лосса.))*

==========================================================================

## Установка
1) Самый простой способ:
```shell
git clone https://github.com/WISEPLAT/Hackathon-Finam-NN-Trade-Robot
```

2) Или через PyCharm:
- нажмите на кнопку **Get from VCS**:
![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/get_from_vcs.jpg )

Вот ссылка на этот проект:
```shell
https://github.com/WISEPLAT/Hackathon-Finam-NN-Trade-Robot
```

- вставьте эту ссылку в поле **URL** и нажмите на кнопку **Clone** 
![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/paste_url_push_clone.jpg)


- Теперь у нас появился проект торгового робота:
![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/hackathon_finam_nn_trade_robot.jpg )

### Установка дополнительных библиотек
Для работы торгового робота с использованием нейросетей, есть некоторые библиотеки, которые вам необходимо установить:
```shell
pip install aiohttp aiomoex pandas matplotlib tensorflow finam-trade-api
```

так же их можно установить такой командой
```shell
pip install -r requirements.txt
```

Обязательно! Выполните в корне вашего проекта через терминал эту команду:
```shell
git clone https://github.com/cia76/FinamPy
```
для клонирования библиотеки, которая позволяет работать с функционалом API брокера Финам.

P.S. Библиотека finam-trade-api - тоже позволяет работать с API Финам, просто для тестов я использовал обе.))) А для live торговли FinamPy.

Теперь наш проект выглядит вот так:
![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/hackathon_finam_nn_trade_robot_add_lib.jpg )

### Начало работы

Вот перечень задач, которые нужно сделать для успешного запуска торгового робота использующего нейросети на основе компьютерного зрения для поиска формаций 
на торговом графике акций и осуществления им торговых операций:


1. Настроить конфигурационный файл my_config\trade_config.py

   - В нём можно указать по каким тикерам ищем формации и обучаем нейросеть (**training_NN**), и так же указать по каким тикерам торгуем (**portfolio**) используя обученную нейросеть. Остальные параметры можно оставить как есть.
   ![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/trade_config.png )
   

2. Нужно получить исторические данные по акциям, для обучения нейросети
   - Исторические данные для обучения нейросети мы получаем с MOEX. Т.к. получаем их бесплатно, то есть задержка в полученных данных на 15 минут.
   - Для этого используется файл **1_get_historical_data_for_strategy_from_moex.py**
   - Полученные исторические данные сохраняются в каталоге **csv** в CSV файлах.
   ![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/historical_data.png )
   

3. Когда есть исторические данные, теперь мы можем подготовить картинки для обучающего набора данных
   - подготовка датасета с картинками формаций из графика акций по определенной логике:
     - на картинке рисуется цена закрытия и две скользящие средние - картинки рисуются для младшего таймфрейма
     - если на старшем таймфрейме закрытие выше предыдущего закрытия, то такой картинке назначаем класс **1** иначе **0**
   - Для этого используется файл **2_prepare_dataset_images_from_historical_data.py**
   - Полученные картинки сохраняются в каталоге **NN\training_dataset_M1** в подкаталогах классификаций **0** и **1**.
   ![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/neural_network_training.png )


4. Наконец-то есть датасеты для обучения нейросети )) Теперь обучаем нейросеть 
   - Используем сверточную нейронную сеть (CNN)
   - Для этого используется файл **3_train_neural_network.py**
   - Лог обучения нейросети находится в файле **3_results_of_training_neural_network.txt**
   - Сходимость нейросети находится в файле **3_Training and Validation Accuracy and Loss.png**
   - При обучении нейросети файлы моделей сохраняются в каталог **NN\\_models** 
   ![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/training.png )


5. После успешного обучения нейросети нужно выбрать одну из обученных моделей для нашего торгового робота
   - Выбор лучшей обученной модели происходит по параметрам loss, accuracy, val_loss, val_accuracy
   - Выбранную модель нужно **вручную** сохранить в каталог **NN_winner** под именем **cnn_Open.hdf5**
   ![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/accuracy_loss.png )


6. Теперь нужно сделать проверку предсказаний сделанных нейросетью на части классифицированных картинках
   - Для этого используется файл **4_check_predictions_by_neural_network.py**
   - Как говорится просто проверить - что Ок
   ![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/classification.png )


7. Наконец-то делаем проверку подключения к API Финама, чтобы мы смогли торговать
   - Для этого используется файл **5_test_api_finam_v1.py** - используем [FinamPy](https://github.com/cia76/FinamPy ) для тестов
   - и файл **6_test_api_finam_v2.py** - используем [FinamTradeApiPy](https://github.com/DBoyara/FinamTradeApiPy ) для тестов

      ####  Как получить токен API Финам:
      - Открыть счет в "Финаме" https://open.finam.ru/registration
      - Зарегистрироваться в сервисе Comon https://www.comon.ru/
      - В личном кабинете Comon получить токен https://www.comon.ru/my/trade-api/tokens для выбранного торгового счета
      - Скопируйте и вставьте в файл **my_config\Config.py** полученный **Ключ API** и **номер торгового счета** (пример конфиг файла здесь: **my_config\Config_example.py**)
      
      ```python
      # content of my_config\Config.py 
      class Config:
          ClientIds = ('<Торговый счет>',)  # Торговые счёта
          AccessToken = '<Токен>'  # Торговый токен доступа
      ```


8. Теперь мы готовы запустить торгового робота в live режиме
      - Не забываем про **Ключ API** и **номер торгового счета**, уже должны быть прописаны в файле **my_config\Config.py**
      - запуск live стратегии осуществляется с помощью файла **7_live_strategy.py**
      - в строке 266 этот параметр **days_back** отвечает за сколько дней назад взять данные, если запускаете скрипт в понедельник или после выходного/праздничного дня, то увеличьте это значение
   
          ```days_back = 1  # на сколько дней назад берем данные```

      - строку 206 можно раскомментировать, чтобы скрипт например не запускался, если рынок не открыт (выходные и праздники не учитывает)
   
          ```await self.ensure_market_open()  # проверяем, что рынок открыт```

      - конфигурация торгового робота находится в файле **my_config\trade_config.py** 
   хотелось бы указать, что т.к. мы берем исторические данные из MOEX, а не по API Финам (т.к. такой функционал будет реализован позже), то доступные тикеры для аналитики и скачивания данных необходимо подбирать вручную.
          ```
            training_NN = {"SBER", "VTBR"}  # тикеры по которым обучаем нейросеть
            portfolio = {"SBER", "VTBR"}  # тикеры по которым торгуем и скачиваем исторические данные
           ```
      - лог запуска торгового робота в live режиме торгов находится в файле **7_live_trading_log.txt** 
      
      запущенный в live режиме торговый робот и торговый терминал:
      ![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/live_orders_2_r.jpg )
      
      ордера выставленные торговым роботом:
      ![alt text](https://raw.githubusercontent.com/WISEPLAT/imgs_for_repos/master/live_orders_r.jpg )


Теперь можно запускать и смотреть, а предварительно лучше посмотреть видео по работе с этим кодом
, выложенное [на YouTube](https://youtu.be/yrQFqvc4fk0 ) и [на RuTube](https://rutube.ru/video/private/1255dfe65f4db8736b894cae72b14c45/?p=oOFSDPr1El6lq586tIm2qg )

### Внимание
Некоторые файлы содержат строку:
```exit(777)  # для запрета запуска кода, иначе перепишет результаты```
это сделано специально, чтобы случайно не перезаписать данные, её можно закомментировать, когда будете тестировать свои модели и свои настройки.


P.S. В коде стратегии не реализована проверка на доступность денежных средств на счете для входа в сделку.

Код тестировался на ```M1=>M10``` и ```M10=>H1```, для других таймфреймов необходимо создавать большее число обучающих выборок.

Работоспособность проверялась на ```Python 3.10+``` и ```Python 3.11+``` с последними версиями библиотек.


==========================================================================

## Спасибо
- [FinamPy](https://github.com/cia76/FinamPy ): Игорю за библиотеку, которая позволяет работать с функционалом API брокера Финам.
- [FinamTradeApiPy](https://github.com/DBoyara/FinamTradeApiPy ): DBoyara за библиотеку, асинхронного REST-клиента для API Finam.
- tensorflow: За простую и классную библиотеку для работы с нейросетями.
- aiomoex: За хорошую реализацию получения данных с moex.

## Важно
Исправление ошибок, доработка и развитие кода осуществляется автором и сообществом!

**Пушьте ваши коммиты!** 

# Условия использования
Программный код выложенный по адресу https://github.com/WISEPLAT/Hackathon-Finam-NN-Trade-Robot в сети интернет, позволяющий совершать торговые операции на фондовом рынке с использованием нейросетей - это **Программа** созданная исключительно для удобства работы и изучения применений нейросетей/искусственного интеллекта.
При использовании **Программы** Пользователь обязан соблюдать положения действующего законодательства Российской Федерации или своей страны.
Использование **Программы** предлагается по принципу «Как есть» («AS IS»). Никаких гарантий, как устных, так и письменных не прилагается и не предусматривается.
Автор и сообщество не дает гарантии, что все ошибки **Программы** были устранены, соответственно автор и сообщество не несет никакой ответственности за
последствия использования **Программы**, включая, но, не ограничиваясь любым ущербом оборудованию, компьютерам, мобильным устройствам, 
программному обеспечению Пользователя вызванным или связанным с использованием **Программы**, а также за любые финансовые потери,
понесенные Пользователем в результате использования **Программы**.
Никто не ответственен за потерю данных, убытки, ущерб, включаю случайный или косвенный, упущенную выгоду, потерю доходов или любые другие потери,
связанные с использованием **Программы**.

**Программа** распространяется на условиях лицензии [MIT](https://choosealicense.com/licenses/mit).
