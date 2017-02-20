# Просмотр экспериментов

При выполнении научных исследований необходимо сохранять данные проведенных вычислительных экспериментов. 
Наивный подход это сохранение всей информации в неструктурированный текстовый файл. У этого подхода есть множество недостатков:
- чтобы понять что содержится в файле его нужно явно прочитать
- не фиксированный формат файла увеличивает время обращения к информации
- данные находящиеся в файле требуют постобработки как для визуализации, так и для любых других целей

Чтобы решить названные проблемы был разработан специальный формат файла и механизм визуализации.

# Measurelook формат

Результаты эксперимента сохраняются в JSON файл в следующем формате (версия 0.1.0): 
- meta, объект - описание проводимого эксперимента в произвольном формате.
- constantParams, массив - массив неизменяемых параметров алгоритма
  - name, строка - название параметра
  - units, строка - единицы измерения параметра
  - value, число или строка - значение константы
- changedParams, массив - массив изменяемых параметров алгоритма
  - name, строка - название параметра
  - units, строка - единицы измерения параметра
- measuredParams, массив - массив измеряемых параметров алгоритма
  - name, строка - название параметра
  - units, строка - единицы измерения параметра
- measures, объект - данные по каждому измерению. Хранятся по measureKey (см. пример)
  - measureKey, строка - уникальный ключ каждого измерения. Рекомендуется собирать его как набор всех изменяемых параметров + номер прогона.
  - passId, число - номер прогона
  - changedParams.name, число - значения всех изменяемых параметров, зафиксиованных на время прогона
  - measuredParams.name, число - значения всех измеренных параметров, полученных во время прогона
  - raw, объект - произвольные данные о прогоне, которые вы хотите сохранить. Например чтобы в будущем перепроверить значения измеренных параметров
- version, строка - версия формата. В систему встроен мигратор, автоматически обновляющий файлы в старом формате до нового для обеспечения обратной совместимости.

TODO - Пример файла

# Measurelook просмотр

Для файлов указанного типа разработан просмотровщик в виде интерактивной веб-страницы.
Использование - откройте app.html в браузере.

В комплекте с визуализатором идёт база с результатами эксперимента, который иллюстрирует основные функции просмотра.

Для загрузки своих данных нажмите кнопку "Загрузить базу из файла" в правом верхнем углу программы.

При загрузке база будет обновлена с помощью мигратора до актуального формата, если в этом есть необходимость.
После мигратора база валидируется с помощью JSON schema. При обнаружении проблем будет выведено сообщение об ошибке.
Поскольку в базе ошибок может быть найдено очень много, все они выводятся в консоль браузера в текущей реализации.

# Примеры

Вы можете выполнить примеры вычислительных экспериментов, возращающих результат в Measurelook формате.
Использование - откройте example.html в браузере и следуйте инструкциям.

