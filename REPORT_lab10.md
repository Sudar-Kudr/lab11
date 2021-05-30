## Laboratory work XI

Данная лабораторная работа посвещена изучению процесса создания сеансов совместной разработки с использованием инструмента **ngrok**

```sh
$ open https://ngrok.com/
```

## Tasks

- [ok] 1. Ознакомиться со ссылками учебного материала
- [ok] 2. Выполнить инструкцию учебного материала
- [ok] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ cd ~                           #спускаемся в корневую директорию
$ mkdir install                   #создаем директорию install 
$ mkdir tmp                        #создаем директорию tmp
$ export HOME_PREFIX=`pwd`/install  #присваиваем текущий каталог вместе с install в переменную HOME_PREFIX
$ echo $HOME_PREFIX                #запускаем HOME_PREFIX
$ export USERNAME=`whoami`        #присваиваем whoami в переменную USERNAME
```

```sh
$ cd tmp               #спускаемся в tmp
```

```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz  #скачиваем архив libevent
--2021-05-30 13:24:56--  https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz
....................................................................
$ tar -xvzf libevent-2.1.8-stable.tar.gz    #извлекаем файл из архива
x libevent-2.1.8-stable/
x libevent-2.1.8-stable/util-internal.h
x libevent-2.1.8-stable/evmap.c
....................................................................
$ cd libevent-2.1.8-stable                #спускаемся в директорию libevent-2.1.8-stable
$ ./configure --prefix=${HOME_PREFIX}    #указываем директорию, в которую будет производится установка
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
....................................................................
$ make && make install                 #устанавливаем
GEN      test/rpcgen-attempted
  GEN      include/event2/event-config.h
/Applications/Xcode.app/Contents/Developer/usr/bin/make  all-am
  CC       buffer.lo
....................................................................
$ cd ..                      #поднимаемся наверх
```

```sh
$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz  #скачиваем архив ncurses
--2021-05-30 13:35:39--  http://invisible-island.net/datafiles/release/ncurses.tar.gz
Распознаётся invisible-island.net (invisible-island.net)… 192.124.249.12
....................................................................
$ tar -xvzf ncurses.tar.gz    #извлекаем файл из архива
x ncurses-6.2/
x ncurses-6.2/aclocal.m4
x ncurses-6.2/Ada95/
x ncurses-6.2/ANNOUNCE
....................................................................
$ cd ncurses-6.2                #спускаемся в директорию
$ ./configure --prefix=${HOME_PREFIX}    #указываем директорию, в которую будет производится установка
checking for egrep... grep -E
Configuring NCURSES 6.2 ABI 6 (Sun May 30 13:38:14 MSK 2021)
checking for package version... 6.2
....................................................................
$ make && make install                 #устанавливаем
cd man && /Applications/Xcode.app/Contents/Developer/usr/bin/make DESTDIR="" RPATH_LIST="/Users/user/install/lib" all
....................................................................
$ cd ..                      #поднимаемся наверх
```


```sh
$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz  #скачиваем архив tmux
--2021-05-30 13:41:28--  https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz
Распознаётся github.com (github.com)… 140.82.121.3
....................................................................
$ tar -xvzf tmux-2.5.tar.gz    #извлекаем файл из архива
x tmux-2.5/
x tmux-2.5/compat/
x tmux-2.5/compat/asprintf.c
....................................................................
$ cd tmux-2.5                #спускаемся в директорию
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib"    #указываем директорию, в которую будет производится установка
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
....................................................................
$ make && make install                 #устанавливаем
depbase=`echo alerts.o | sed 's|[^/]*$|.deps/&|;s|\.o$||'`;\
gcc -DPACKAGE_NAME=\"tmux\" -DPACKAGE_TARNAME=\"tmux\" -DPACKAGE_VERSION
....................................................................
$ cd ..                     #поднимаемся наверх
```

```sh
$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip  #скачиваем архив equinox
e-linux-amd64.zip
--2021-05-30 13:45:13--  https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
....................................................................
$ unizp ngrok-stable-linux-amd64.zip    #распакуем
Archive:  ngrok-stable-linux-amd64.zip
inflating: ngrok
....................................................................
$ mv ngrok ${HOME_PREFIX}/bin    #перемещаем папку ngrok в папку /Users/user/install/bin
```

```sh
$ export LD_LIBRARY_PATH=${HOME_PREFIX}/lib     #присваиваем HOME_PREFIX/lib в переменную LD_LIBRARY_PATH
$ export PATH="${HOME_PREFIX}/bin:${PATH}"    #присваиваем HOME_PREFIX/bin в переменную PATH
$ tmux                                       #запускаем
```

```sh
$ cd ~                            #спускаемся в корневую директорию
$ rm -rf tmp install             #удаляем директории tmp и install
```

```sh
#cкачиваем tmux и ngrok
$ brew install tmux ngrok # or use linuxbrew 🎉
Downloading https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-darwin-amd64.z
....................................................................
```

```sh
$ tmux new -s session_with_group            #создаем новую сессию
```

```sh
# Alisa:
$ open https://ngrok.com/signup     #открываем сайт по ссылке
$ export NGROK_TOKEN=<токен>       #присваиваем <токен> в переменную NGROK_TOKEN
$ ngrok authtoken ${NGROK_TOKEN}  #указываем этот токен в качестве аутентификационного токена
Authtoken saved to configuration file: /Users/user/.ngrok2/ngrok.yml
$ ngrok tcp 22                   #указываем порт, чтобы получить доступ по SSH
<порт_ngrok_сервера>
```

```sh
# Bob:
$ ssh ${USERNAME}@0.tcp.ngrok.io -p<порт_ngrok_сервера>  #подключаем виртуальную машину
<пароль_от_учетной_записи> 
$ tmux a -t session_with_group                          #подключемся к групповой сессии
$ <C-B>"                                               #вертикальное разделение окна
```

## Report

```sh
$ cd ~/workspace/                                                                    #спускаемся в директорию workspace
$ export LAB_NUMBER=11                                                              #присваиваем 11 в переменную LAB_NUMBER
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER} #клонируем из ссылки в директорию (в нашем случае-tasks/lab11)
$ mkdir reports/lab${LAB_NUMBER}                                                  #создаем директорию (в нашем случае- lab11)
cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md           #копируем из одной директории в другую
cd reports/lab${LAB_NUMBER}                                                     #спускаемся в директорию (в нашем случае- lab11)
edit REPORT.md                                                                 #редактируем REPORT.md
gist REPORT.md                                                                #сохраняем REPORT.md

```

## Links

- [Tmux](https://raw.githubusercontent.com/tmux/tmux/master/README)
- [Libevent](http://libevent.org)
- [Ncurses](http://invisible-island.net/ncurses/)

```
Copyright (c) 2015-2021 The ISC Authors
```
