## ssh настроить чтобы не выкидывало по таймауту

При работе с ssh есть одна проблема — когда на минуту другую отвлекся от терминала — соединение разрывается. Решается просто:

    $ touch ~/.ssh/config

добавляем в этот файл строку:

```
ServerAliveInterval 5
```



## как в Linux узнать размер директорий первого уровня

Можно так:

    $ find . -maxdepth 1 -type d -exec du -hs {} \;

а можно так:

    # du -h --max-depth=1 .


## Выставить 777 на папки и подпапки в текущей директории

    $ chmod -R 777 $(find . -type d)


## Старый добрый ламповый терминал

Добро тут: https://github.com/Swordifish90/cool-old-term

Любители электронных ламп и катодных мониторов, ловите сие программерское произвидение искусства cool-old-term! Собрать достаточно просто — ставим зависимости (на гитхабе всё расписано, под какой дистрибутив что ставить), клонируем реп из Github к себе на машину, собираем и запускаем! Куча настроек, думаю каждый сделает родною консоль немного приятней


## Как узнать какому пакету может принадлежать файл

    $ sudo apt-get install apt-file
    $ apt-file update
    $ apt-file search Xlib.h


## пара полезных вещей с ffmpeg

Допустим у нас есть avi-файл, и мы хотим выбрать оттуда звуковую дорожку. Живой пример — мне понравился фильм и я хочу вытащить дорожку на англ языке, чтобы слушая на досуге, улучшать свой английский. В этом нам поможет пакет ffmpeg.

    $ ffmpeg -i film.avi -map 0:2 -vn -ar 44100 -ac 2 -ab 192 -f mp3 english.mp3

параметр map 0:2 говорит нам что мы извлекаем дорожку 2 (допустим первая — у нас на русском языке, и даром не сдалась)
Если у вас Ubuntu и нет этого пакета в репах, поставить можно следующим образом: 

    $ sudo add-apt-repository ppa:mc3man/trusty-media
    $ sudo apt-get update
    $ sudo apt-get install ffmpeg

Может быть также полезен рецепт:

    $ ffmpeg -i input_file.wav -vn -ar 44100 -ac 2 -ab 192 -f mp3 output_file.mp3


## Сконвертировать CR2 в jpeg или png

    $ sudo apt-get install ufraw ufraw-batch
    $ ufraw-batch --out-type jpeg *.CR2
    $ ufraw-batch --out-type png *.CR2
    $ sudo apt-get install gimp-ufraw


## ZXTune123 слушаем тёплые восьмибитные треки

    $ zxtune123 --alsa = filename.ext
    $ zxtune123 --mp3 filename='filename' track.ext
    $ zxtune123 --loop --alsa device=hw:0,mixer=PCM filename.ext

## linux конвертировать WAV в MP3 и обратно

    $ sudo apt-get install lame

Чтобы сконвертировать один wav-файл с битрейтом 128, пишем:

    $ lame file.wav

с битрейтом 320:

    $ lame -b 320 -q 0 file.wav

Чтобы декодировать файл из mp3 в wav:

    $ lame --decode file.mp3

Можно автоматизировать процесс — например, если вам надо сжать сразу несколько файлов в директории:

    $ find . -iname "*.wav" -exec lame '{}' ';'

Если вдруг выскочила ошибка **Unsupported data format: 0×0055** поможет этот ключ:

    $ lame --mp3input file.wav

Ошибка связана с некорректностью заголовка в файле wav


## Linux Включить проверку орфографии в LibreOffice

    $ sudo apt-get install libreoffice-l10n-ru aspell aspell-en dictionaries-common hunspell myspell-ru myspell-uk mozilla-libreoffice language-support-writing-ru


## Linux Конвертировать mp4 в mp3

Сначала установим необходимые пакеты:

    $ sudo apt-get install ffmpeg libavcodec-unstripped-52

И произведем, собственно, конвертацию:

    $ ffmpeg -i видеофайл.mp4 -f mp3 -ab 192000 -vn звуковаядорожка.mp3

Если нет необходимого кодека, его можно поискать командой:

    $ aptitude search имя_кодека


## linux ограничение ширины канала для конкретной программы

Часто нужна задача ограничения скорости закачки или скорости скачки какого-либо файла, торрента, дистрибутива.

Linux-way путь как всегда прекрасен и лаконичен. Нам поможет программа **trickle**

Установим программу (для Debian-based)

    $ sudo apt-get install trickle

Для Gentoo:

    $ sudo eix-sync
    $ sudo emerge trickle

Для RadHat Linux, Fedora Core, CentOS:

    $ sudo yum install trickle

Использование программы:

Органичим скорость скачки для программы ftp в 100 Кбит/сек:

    $ trickle -d 100 ftp

И скорость закачки:

    $ trickle -u 100 ftp

Или одной операцией:

    $ trickle -u 100 -d 100 ftp

В общем случае, синтаксис выглядит так:

    $ trickle -d download-bandwidth -u upload-bandwidth command

Полезная опция:

    $ trickle -s -d download-bandwidth -u upload-bandwidth command

запустить программу отдельно от демона **trickled**

Полная справка по программе:

    $ man trickle


## ssh настроить чтобы не выкидывало по таймауту

При работе с ssh есть одна проблема — когда на минуту другую отвлекся от терминала — соединение разрывается. Решается просто:

    $ vi ~/.ssh/config

добавляем в этот файл строку:

    ServerAliveInterval 5


## Создать кнопку терминала с правами ROOT

Добавляете как и обычную кнопку запуска приложения но в строке команда указывате:

    $ gksu xfce4-terminal
