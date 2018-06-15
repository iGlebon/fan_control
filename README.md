# Автоматическое управление вентиляторами видеокарт Nvidia для linux в том числе HiveOS
## Функционал контроля температуры:
- Задается коридор температур (по умолчанию 58-60) в котором скрипт будет пытаться держать карты.
- При снижении температуры ниже нижнего порога - происходит плавное снижение оборотов кулера.
- При достижении верхнего порога - плавное увеличение оборотов.
- При достижении второго порога (по умолчанию 65)- сразу включается турборежим кулера (по умолчанию 70), и после этого плавное увеличение вплоть до максимальных оборотов, пока температура не снизится.
- При снижении оборотов ниже минимальных (по умолчанию 35) - происходит переключение на автоматическое управление кулерами. Полезно при зимнем балконном майнинге, чтобы не крутить вентиля, когда картам и так холодно. (на многих картах вентиля просто отключаются ниже определенной температуры)

## Функционал WatchDog (можно отключить):
- Считываются значения загрузки карт.
- В случае ошибки получения данных (отвал карты). Или в случае снижения загрузки карты ниже установленного порога (не работает майнер), начинается обратный отсчет. Если по прошествии заданного количества циклов - загрузка карт не восстанавливается - происходит перезагрузка с одновременной записью даты ребута и его причины в ~/watchdog.log

Входные переменные для настройки вынесены в отдельный файл fan.conf. Этот файл должен находиться в одной директории со скриптом. В файле есть описание переменных.

Переменные можно изменять на лету без перезапуска скрипта. Скрипт считывает переменные из конфигурационного файла на каждом цикле.

Запускать желательно в отдельном окне терминала или в screen

## Использование в HiveOS
- скачать архив в домашнюю директорию /home/user

> cd /home/user

> wget https://github.com/lexandr0s/fan_control/archive/v2.2.tar.gz

- распаковать архив

> tar -xvf v2.2.tar.gz

- присвоить скриптам права на исполнение

> chmod +x fan_control-2.2/*

- скопировать файлы в домашнюю директорию

> cp fan_control-2.2/* /home/user

- при неообходимости отредактировать файл конфигурации fan.conf
- перезагрузить риг или запустить скрипт без перезагрузки выполнив команду:

> screen -dmS fan /home/user/fan.sh


После этого скрипт будет запускаться при старте рига в фоновом режиме в screen.

Восстановить окно скрипта и понаблюдать за его работой можно с помощью команды

> screen -r fan

Отключиться от окна скрипта:

> Ctrl+A

> D


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
## Change Log:
## v2.1
Мелкий фикс

## v2.1
Изменение оборотов кулеров теперь производится одной командой один раз за цикл. В связи с этим скрипт отрабатывает очень быстро, независимо от количества карт в риге.

Настройки вынесены во внешний файл конфигурации. Их можно менять на лету, не перезапуская скрипт.

## v.2.0
Скрипт кардинально переработан. 
Получение данных с карт теперь происходит одним запросом на все карты.
Добавлен блок предотвращения возможных конфликтов при сборе данных с карт со стороны HiveOS.
Достигнуто значительное увеличение скорости работы и стабильности.

### *For donate*

*LTC:* LaeSwaV5mnXJb6DgccCdHiZNKUCvbfDMFT

*ETH:* 0x4e2cE16142600DE62E41b107BA06701c80C82fc4

