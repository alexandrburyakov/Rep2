# 1.1. Введение в DevOps

### Задание №1 - Подготовка рабочей среды.
1. [jsonnet](https://a.radikal.ru/a12/2110/af/3e4c6fe040c2.png)
2. [md](http://d.radikal.ru/d33/2110/2c/c52fe609c8de.png)
3. [sh](https://d.radikal.ru/d01/2110/00/ebfb6bff13a9.png)
4. [tr](https://c.radikal.ru/c07/2110/7a/fdbbca7f68f6.png)
5. [yaml](https://d.radikal.ru/d00/2110/26/28ddb9db7cf2.png)

### Задание №2 - Описание жизненного цикла задачи (разработки нового функционала).
1. Менеджер ставит перед разработчиками задачу на разработку нового функционала, перед тестировщикам - задачу на написание дополнительных тест-кейсов для тестирования данного функционала (напр. в Jira).
2. Разаработчики дополняют функционал, обновляя файлы проекта в репозитории (напр. ветка develop). Тестировщики, в свою очередь, дописывают новые тест-кейсы в соответствии с новой (дополненной) функциональной спецификацией.
3. DevOps инженер дорабатывает пайплайн (напр. в Jenkins) по автоматическому развертыванию и запуску проекта на тестовом стенде из ветки develop репозитория, обновляя процесс автотестирования с учетом новых тест-кейсов. Кроме того, в случае необходимости, DevOps инженер обновляет необходимые докер-образы (при использовании докера) на тестовом контуре. В идеале, данный процесс так же должен быть автоматизирован (в рамках пайплайна). Дополнительно, DevOps инженер добавляет в пайплайн возможность отката новой версии проекта и запуска предыдущей версии в случае возникновения ошибок при развертывании и запуске проекта, а так же при непрохождении автотестов. 
4. При возникновении ошибок на каком-либо из этапов при запуске пайплайна на тестовом контуре (а так же при непрохождении тест-кейсов) происходит откат на предыдущую версию сервиса. При необходимости, разработчики дорабатывают (исправляют) новый функционал, тестировщики дорабатывают тест-кейсы.    
5. При нормальном прохождении пайплайна (с прохождением всех тест-кейсов) менеджер проекта презентует новый функционал заказчику.
6. При одобрении нового функционала заказчиком, ветка develop в репозитории проекта сливается с веткой master.
7. DevOps инженер обновляет пайплайн по автоматическому развертыванию и запуску проекта на продуктовом хосте из ветки master репозитория.
8. При нормальном срабатывании пайплайна на продуктовом хосте - устанавливается и запускается новая версия проекта.
9. При возникновении ошибок на каком-либо из этапов при запуске пайплайна происходит откат новой версии и запуск предыдущей версии проекта. Возобновляется процесс доработки сервиса.      

# 2.4. Инструменты Git

### 1. aefead2207ef7e2aa5dc81a34aedf0cad4c32545 Update CHANGELOG.md
Результат выполнения команды: git log -1 --pretty=oneline aefea
### 2. v0.12.23
Результат выполнения команды: git tag --points-at 85024d3
### 3. 2 родителя с хешами: 56cd7859e05c36c06b56d013b55a252d0bb7e158 9ea88f22fc6269854151c571162c5bcf958bee2b
Результат выполнения команды: git log -1 --pretty=%P b8d720
### 4. Хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24
b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links

3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md

6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable

5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location

06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md

d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows

4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md

dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md

225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release

#### Команда для получения списка: git log v0.12.23..$(git log --pretty=%P -1 v0.12.24) --pretty=oneline

### 5. 8c928e83589d90a031f811fae52a81be7153e82f
Результат выполнения команды: git log -S 'func providerSource(' --pretty=%H

### 6. Список коммитов, в которых была изменена функция globalPluginDirs
78b122055

52dbf9483 

41ab0aef7

66ebff90c

8364383c3

1. Находим короткий хеш коммита создания функции командой: git log -S 'func globalPluginDirs(' --pretty=%h
2. С помощью найденного короткого хеша (8364383c3) просматриваем коммит: git show 8364383c3
3. Находим файл в котором была создана функция (plugins.go)
4. Запускаем команду: git log -L :globalPluginDirs:plugins.go --pretty=%h

### 7. Martin Atkins
1.Выполняем команду: git log -S "func synchronizedWriters(" --pretty="%an, %aD"

2.Выбираем автора самого раннего коммита.

# 3.1. Работа в терминале, лекция 1 <a name="3"></a>

### 1. Cредство виртуализации Oracle VirtualBox установлено.
### 2. Средство автоматизации Hashicorp Vagrant установлено.
### 3. Терминал в основном окружении подготовлен.
### 4. Запущен Ubuntu 20.04 в VirtualBox посредством Vagrant.
### 5. Выделенные ресурсы:
1. Оперативная память: 1024 Мб
2. Процессоры: 2
3. HDD: 64 Гб
4. Видеопамять: 4 Гб
### 6. Добавить оперативной памяти или ресурсов процессора ВМ можно добавлением в Vagrantfile следующего:
```bash
config.vm.provider "virtualbox" do |v|
  v.memory = 1024
  v.cpus = 2
end
```
### 7. Выполнено.
### 8. Ознакомиться с разделами man bash, почитать о настройках самого bash:
1. Длину журнала `history` можно задать переменной `HISTSIZE` (количество сохраняемых в истории команд, строка 637), 
а так же переменной `HISTFILESIZE` (максимальное количество строк, содерждащихся в файле истории, строка 627).
2. Директива `ignoreboth` объединяет 2 директивы: `ignorespace`(не включать в историю команды начинающиеся с пробела) и
`ignoredups` (не включать команды, которые уже включены в историю).
### 9. В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
В командах используются при механизме раскрытия скобок, позволяя создать различные строки. Например, команда `touch f{1..10}` создаст набор фалов 
f1, f2  и т.д. до f10. Строка 806 man bash.

Используются для ограничения тела функции. Строка 311.

Используются для ограничения списка команд, которые выполняются в текущем окружении. Строка 206.
### 10. Как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000?
1. 100000 файлов можно создать, например, командой `touch f{1..100000}`.
2. 300000 таким же образом создать не получается из-за слишком большого количества аргументов для `touch`.
### 11. Что делает конструкция `[[ -d /tmp ]]`?
Данная конструкция возвращает статус 1 или 0 в зависимости от оценки, содержащегося в двойных квадратных скобках условного выражения. 
В нашем случае: 1 - если папка /tmp существует, иначе - 0.
### 12. Добиться в выводе `type -a bash` в виртуальной машине наличия первым пунктом в списке `bash is /tmp/new_path_directory/bash` можно след. командами:
```bash
mkdir /tmp/new_path_directory/
cp /bin/bash /tmp/new_path_directory/
PATH=/tmp/new_path_directory/:$PATH
```
### 13. Чем отличается планирование команд с помощью batch и at?
1. batch используется для запуска команд, когда загрузка системы становится меньше 1.5
2. at используется для запуска команд в заданное время
### 14. Выполнено

# 3.2. Работа в терминале, лекция 2
### 1. Какого типа команда cd? Попробуйте объяснить, почему она именно такого типа; опишите ход своих мыслей, если считаете что она могла бы быть другого типа.
`cd` является встроенной командой оболочки.
```bash
vagrant@vagrant:~$ type cd
cd is a shell builtin
```
Если бы она была отдельной программой, то она меняла бы рабочий каталог только в своем окружениии, и это не влияло бы на другие программы, запущенные от этого же родительского процесса.
### 2. Какая альтернатива без pipe команде grep <some_string> <some_file> | wc -l? man grep поможет в ответе на этот вопрос. Ознакомьтесь с документом о других подобных некорректных вариантах использования pipe.
`grep <some_string> <some_file> -c`
### 3. Какой процесс с PID 1 является родителем для всех процессов в вашей виртуальной машине Ubuntu 20.04?
Процесс `systemd`.
```bash
vagrant@vagrant:~$ pstree -p
systemd(1)─┬─VBoxService(769)─┬─{VBoxService}(771)
           │                  ├─{VBoxService}(772)
           │                  ├─{VBoxService}(773)
```

### 4. Как будет выглядеть команда, которая перенаправит вывод stderr ls на другую сессию терминала?
Вызов в pts/0
```bash
vagrant@vagrant:~$ tty
/dev/pts/0
vagrant@vagrant:~$ ls /rrr 2>/dev/pts/1
```
вывод в pts/1
```bash
vagrant@vagrant:~$ tty
/dev/pts/1
vagrant@vagrant:~$ ls: cannot access '/rrr': No such file or directory
```
### 5. Получится ли одновременно передать команде файл на stdin и вывести ее stdout в другой файл? Приведите работающий пример.
```bash
vagrant@vagrant:~$ cat file1
3
4
2
1
vagrant@vagrant:~$ sort < file1 > file1_sorted
vagrant@vagrant:~$ cat file1_sorted
1
2
3
4
```
### 6. Получится ли находясь в графическом режиме, вывести данные из PTY в какой-либо из эмуляторов TTY? Сможете ли вы наблюдать выводимые данные?
Вывести получится с помощью перенаправления вывода.
```bash
user@user-Aspire-F5-573G:~$ echo hello to tty2 > /dev/tty2
```
Данные можно посмотреть перейдя, в данном случае, в терминал tty2 (Ctrl-Alt-F2).
### 7. Выполните команду bash 5>&1. К чему она приведет? Что будет, если вы выполните echo netology > /proc/$$/fd/5? Почему так происходит?
```bash
vagrant@vagrant:~$ bash 5>&1
vagrant@vagrant:~$ echo netology > /proc/$$/fd/5
netology
```
Первая команда создаст новый дескриптор "5" для данной сессии и перенаправит его в `stdout`.
Вторая команда запишет строку `netology` в этот дескриптор, который перенаправит её на `stdout`.
### 8. Получится ли в качестве входного потока для pipe использовать только stderr команды, не потеряв при этом отображение stdout на pty? Напоминаем: по умолчанию через pipe передается только stdout команды слева от | на stdin команды справа. Это можно сделать, поменяв стандартные потоки местами через промежуточный новый дескриптор, который вы научились создавать в предыдущем вопросе.
Получается с такой командой: `ls <some folder> 5>&1 1>&2 2>&5| grep <some string>`.
```bash
root@user-Aspire-F5-573G:/home/user/test_folder# ls
file1  file2  file3  file4  file5
root@user-Aspire-F5-573G:/home/user/test_folder# ls 5>&1 1>&2 2>&5| grep "Нет такого"
file1  file2  file3  file4  file5
root@user-Aspire-F5-573G:/home/user/test_folder# ls \ddd 5>&1 1>&2 2>&5| grep "Нет такого"
ls: невозможно получить доступ к 'ddd': Нет такого файла или каталога
root@user-Aspire-F5-573G:/home/user/test_folder# ls \ddd 5>&1 1>&2 2>&5| grep "Нет такого" -c
1
```
### 9. Что выведет команда cat /proc/$$/environ? Как еще можно получить аналогичный по содержанию вывод?
Команда `cat /proc/$$/environ` выводит переменные окружения. Аналогичный по содержанию вывод можно так же получить командой `env`.

### 10. Используя man, опишите что доступно по адресам /proc/<PID>/cmdline, /proc/<PID>/exe.
`/proc/[pid]/cmdline` - файл только для чтения, содержащий полную строку команды для процесса.
`/proc/[pid]/exe` - данный файл является символической ссылкой, содержащей актуальный путь исполняемой команды.

### 11. Узнайте, какую наиболее старшую версию набора инструкций SSE поддерживает ваш процессор с помощью /proc/cpuinfo.
`sse4_2` Помогла следующая команда: `cat /proc/cpuinfo | grep sse`.
### 12. При открытии нового окна терминала и vagrant ssh создается новая сессия и выделяется pty. Это можно подтвердить командой tty, которая упоминалась в лекции 3.2. Однако:
```sh
vagrant@netology1:~$ ssh localhost 'tty'
not a tty
```
###    Почитайте, почему так происходит, и как изменить поведение.
Это происходит из-за того что при попытке выполнить команду `tty` удаленно через `SSH`, например `ssh localhost 'tty'`, 
`tty` не выделяется. Для принудительного выделения `tty` необходимо использовать ключ `-t`. В таком случае псевдотерминал 
выделится принудительно, даже если у текущего `SSH` его нет.

### 13. Бывает, что есть необходимость переместить запущенный процесс из одной сессии в другую. Попробуйте сделать это, воспользовавшись reptyr. Например, так можно перенести в screen процесс, который вы запустили по ошибке в обычной SSH-сессии.
Выполнено.
### 14. sudo echo string > /root/new_file не даст выполнить перенаправление под обычным пользователем, так как перенаправлением занимается процесс shell'а, который запущен без sudo под вашим пользователем. Для решения данной проблемы можно использовать конструкцию echo string | sudo tee /root/new_file. Узнайте что делает команда tee и почему в отличие от sudo echo команда с sudo tee будет работать.
Команда `tee` вычитывает из `STDIN` и записывает в `STDOUT` или в файл. В данном случае команда получает вывод из `STDIN`, 
перенаправленный через pipe от `STDOUT` команды echo, а далее команде `tee` мы, в свою очередь, уже от root говорим писать в файл /root/new_file. 

# 3.3. Операционные системы, лекция 1
### 1. Какой системный вызов делает команда cd? В прошлом ДЗ мы выяснили, что cd не является самостоятельной программой, это shell builtin, поэтому запустить strace непосредственно на cd не получится. Тем не менее, вы можете запустить strace на /bin/bash -c 'cd /tmp'. В этом случае вы увидите полный список системных вызовов, которые делает сам bash при старте. Вам нужно найти тот единственный, который относится именно к cd. Обратите внимание, что strace выдаёт результат своей работы в поток stderr, а не в stdout.
Системный вызов, относящийся к `CD` - `chdir("/tmp")`.
### 2. Попробуйте использовать команду file на объекты разных типов на файловой системе. Например... Используя strace выясните, где находится база данных file на основании которой она делает свои догадки.
База данных `file` - `/usr/share/misc/magic.mgc`. Так же ищет в: `~/.magic.mgc`, `~/.magic`, `/etc/magic.mgc`, `/etc/magic`. 
### 3. Предположим, приложение пишет лог в текстовый файл. Этот файл оказался удален (deleted в lsof), однако возможности сигналом сказать приложению переоткрыть файлы или просто перезапустить приложение – нет. Так как приложение продолжает писать в удаленный файл, место на диске постепенно заканчивается. Основываясь на знаниях о перенаправлении потоков предложите способ обнуления открытого удаленного файла (чтобы освободить место на файловой системе).
1. По `pid` процесса находим дескриптор файла `<desc>`.
2. С использованием команды `echo` записываем в файл пустое значение, удаляя его содержимое: `echo '' > /proc/<pid>/fd/<desc>`.
### 4. Занимают ли зомби-процессы какие-то ресурсы в ОС (CPU, RAM, IO)?
Зомби-процессы освобождают ресурсы, но оставляют запись в таблице процессов.
### 5. В iovisor BCC есть утилита opensnoop: ... На какие файлы вы увидели вызовы группы open за первую секунду работы утилиты? Воспользуйтесь пакетом bpfcc-tools для Ubuntu 20.04.
``` bash
root@vagrant:~# dpkg -L bpfcc-tools | grep sbin/opensnoop
/usr/sbin/opensnoop-bpfcc
root@vagrant:~# /usr/sbin/opensnoop-bpfcc
PID    COMM               FD ERR PATH
783    vminfo              4   0 /var/run/utmp
578    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
578    dbus-daemon        18   0 /usr/share/dbus-1/system-services
578    dbus-daemon        -1   2 /lib/dbus-1/system-services
578    dbus-daemon        18   0 /var/lib/snapd/dbus-1/system-services/
```
### 6. Какой системный вызов использует uname -a? Приведите цитату из man по этому системному вызову, где описывается альтернативное местоположение в /proc, где можно узнать версию ядра и релиз ОС.
Использует системный вызов - `uname()`. Цитата в `man`:
```TEXT
Part of the utsname information is also accessible  via  /proc/sys/ker‐
nel/{ostype, hostname, osrelease, version, domainname}.
```
### 7. Чем отличается последовательность команд через ; и через && в bash? Например:... Есть ли смысл использовать в bash &&, если применить set -e?
`;` - просто разделитель команд. Вторая команда отработает при любом статусе завершения первой. В случае с `&&` - вторая команда не будет отработана, если первая завершится с ошибкой.
С `set -e` произойдет выход из шелла при ненулевом коде возврата команды, однако если ошибочно завершится одна из команд, разделённых &&, то выхода из шелла не произойдёт. 
### 8. Из каких опций состоит режим bash set -euxo pipefail и почему его хорошо было бы использовать в сценариях?
```TEXT
  -e - сценарий завершится если команда завершится с ненулевым статусом
  -u - сценарий завершится, при попытке использовать незаданную переменную
  -x - выведет команды и их аргументы по мере выполнения
  -o pipefail - вернет статус последней команды с ошибкой в пайплайне
```
Это хорошо использовать в сценариях т.к.: `-x` подробно покажет работу сценария, `-u` обнаружит, что какая-то переменная не задана, а `-e` вместе с `pipefail` покажут на какой команде произошла ошибка сценария.

### 9. Используя -o stat для ps, определите, какой наиболее часто встречающийся статус у процессов в системе. В man ps ознакомьтесь (/PROCESS STATE CODES) что значат дополнительные к основной заглавной буквы статуса процессов. Его можно не учитывать при расчете (считать S, Ss или Ssl равнозначными).
Наиболее часто встречающийся статус - `S`: прерываемый сон (ожидает события для завершени), а так же - `I`: неактивный процесс ядра. Дополнительные (к основной) буквы статуса процесса: < - процесс с высоким приоритетом, N - процесс с низким приоритетом, s - процесс инициировавший сессию. 

# 3.4. Операционные системы, лекция 2
### 1. На лекции мы познакомились с node_exporter. В демонстрации его исполняемый файл запускался в background. Этого достаточно для демо, но не для настоящей production-системы, где процессы должны находиться под внешним управлением. Используя знания из лекции по systemd, создайте самостоятельно простой unit-файл для node_exporter.
Команды установки:
```bash
cd /opt
sudo wget https://github.com/prometheus/node_exporter/releases/download/v1.3.0/node_exporter-1.3.0.linux-amd64.tar.gz
sudo tar xzf node_exporter-1.3.0.linux-amd64.tar.gz
sudo touch node_exporter-1.3.0.linux-amd64/nodex_env
sudo touch /etc/systemd/system/nodex.service
```
Содержимое unit-файла (/etc/systemd/system/nodex.service):
```TEXT
[Unit]
Description=node_exporter

[Service]
EnvironmentFile=/opt/node_exporter-1.3.0.linux-amd64/nodex_env
ExecStart=/opt/node_exporter-1.3.0.linux-amd64/node_exporter $EXTRA_OPTS

[Install]
WantedBy=multi-user.target
```
Содержимое файла для добавления опций (/opt/node_exporter-1.3.0.linux-amd64/nodex_env):
```TEXT
EXTRA_OPTS="--log.level=info"
```
Запущенные команды:
```TEXT
systemctl daemon-reload - для применения настроек
systemctl enable nodex - для добавления в автозагрузку
systemctl start nodex - для запуска
systemctl status nodex - для просмотра статуса
systemctl stop nodex - для остановки.
```
Процесс корректно стартует, завершается, а после перезагрузки автоматически поднимается.

### 2. Ознакомьтесь с опциями node_exporter и выводом /metrics по-умолчанию. Приведите несколько опций, которые вы бы выбрали для базового мониторинга хоста по CPU, памяти, диску и сети.
CPU:
```TEXT
node_cpu_seconds_total{cpu="0",mode="iowait"} 34.59
node_cpu_seconds_total{cpu="0",mode="system"} 15.86
node_cpu_seconds_total{cpu="0",mode="user"} 12.34
node_cpu_seconds_total{cpu="1",mode="iowait"} 27.35
node_cpu_seconds_total{cpu="1",mode="system"} 15.33
node_cpu_seconds_total{cpu="1",mode="user"} 10.92
```
Memory:
```TEXT
node_memory_MemAvailable_bytes 7.2894464e+08
node_memory_MemFree_bytes 3.42368256e+08
node_memory_MemTotal_bytes 1.028694016e+09
node_memory_SwapFree_bytes 1.027600384e+09
node_memory_SwapTotal_bytes 1.027600384e+09
```
Disk:
```TEXT
node_disk_io_now{device="sda"} 0
node_disk_read_bytes_total{device="sda"} 5.14757632e+08
node_disk_read_time_seconds_total{device="sda"} 158.163
node_disk_write_time_seconds_total{device="sda"} 4.869
```
Net:
```TEXT
node_network_receive_bytes_total{device="eth0"} 76393
node_network_receive_errs_total{device="eth0"} 0
node_network_transmit_bytes_total{device="eth0"} 94528
node_network_transmit_errs_total{device="eth0"} 0
```
### 3. Установите в свою виртуальную машину Netdata. Воспользуйтесь готовыми пакетами для установки (sudo apt install -y netdata). 
Netdata установлена. Необходимые файлы отредактированы. Порты проброшены.
[Image](https://c.radikal.ru/c15/2111/dc/ec80dc508ef6.png)

### 4. Можно ли по выводу dmesg понять, осознает ли ОС, что загружена не на настоящем оборудовании, а на системе виртуализации?
Можно. Часть вывода `dmesg`:
```bash
[    0.000000] DMI: innotek GmbH VirtualBox/VirtualBox, BIOS VirtualBox 12/01/2006
[    0.000000] Hypervisor detected: KVM
```
### 5. Как настроен sysctl fs.nr_open на системе по-умолчанию? Узнайте, что означает этот параметр. Какой другой существующий лимит не позволит достичь такого числа (ulimit --help)?
Значение `fs.nr_open` можно получить выполнив команду: `sysctl -n fs.nr_open`. Данное значение указывает на максимальное количество открытых файлов на процесс.
Значение по умолчанию - 1048576. Это значение не позволит достичь другое ограничение: `open files` из вывода команды: `ulimit -a`, дефолтное значение у
которого - 1024.

### 6. Запустите любой долгоживущий процесс (не ls, который отработает мгновенно, а, например, sleep 1h) в отдельном неймспейсе процессов; покажите, что ваш процесс работает под PID 1 через nsenter.
```bash
root@vagrant:~# ps -e | grep sleep
   1748 pts/0    00:00:00 sleep
root@vagrant:~# nsenter --target 1748 --pid --mount
root@vagrant:/# ps
    PID TTY          TIME CMD
      1 pts/0    00:00:00 sleep
      2 pts/0    00:00:00 bash
     11 pts/0    00:00:00 ps
```
### 7. Найдите информацию о том, что такое :(){ :|:& };:. Запустите эту команду в своей виртуальной машине Vagrant с Ubuntu 20.04 (это важно, поведение в других ОС не проверялось). Некоторое время все будет "плохо", после чего (минуты) – ОС должна стабилизироваться. Вызов dmesg расскажет, какой механизм помог автоматической стабилизации. Как настроен этот механизм по-умолчанию, и как изменить число процессов, которое можно создать в сессии?
:(){ :|:& };: - fork-бомба. Данную запись можно представить более наглядно:
```bash
func() {
  func | func &
};
func
```
При запуске такой функции, она начнет порождать процессы до тех пор, пока не достигнет ограничения `ulimit -u` (кол-во процессов на пользователя).
Сообщение об этом в `dmesg`:
```bash
[   88.898126] cgroup: fork rejected by pids controller in /user.slice/user-1000.slice/session-4.scope
```
Данную величину (количество процессов на пользователя) можно поменять командой  `ulimit -u N`, где `N`  - новое значение.

# 3.5. Файловые системы
### 1. Узнайте о sparse (разряженных) файлах.
Выполнено (изучено).
### 2. Могут ли файлы, являющиеся жесткой ссылкой на один объект, иметь разные права доступа и владельца? Почему?
Не могут, т.к. ссылаются на один inode, который содержит информацию о правах доступа и владельце.
### 3. Сделайте vagrant destroy на имеющийся инстанс Ubuntu. Замените содержимое Vagrantfile следующим:... Данная конфигурация создаст новую виртуальную машину с двумя дополнительными неразмеченными дисками по 2.5 Гб.
Добавились `sdb`, `sdc` диски.
```bash
vagrant@vagrant:~$ lsblk
NAME                 MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                    8:0    0   64G  0 disk 
├─sda1                 8:1    0  512M  0 part /boot/efi
├─sda2                 8:2    0    1K  0 part 
└─sda5                 8:5    0 63.5G  0 part 
  ├─vgvagrant-root   253:0    0 62.6G  0 lvm  /
  └─vgvagrant-swap_1 253:1    0  980M  0 lvm  [SWAP]
sdb                    8:16   0  2.5G  0 disk 
sdc                    8:32   0  2.5G  0 disk 
```
### 4. Используя fdisk, разбейте первый диск на 2 раздела: 2 Гб, оставшееся пространство.
```bash
root@vagrant:~# fdisk -l /dev/sdb
Disk /dev/sdb: 2.51 GiB, 2684354560 bytes, 5242880 sectors
Disk model: VBOX HARDDISK   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x80e456f9

Device     Boot   Start     End Sectors  Size Id Type
/dev/sdb1          2048 4196351 4194304    2G 83 Linux
/dev/sdb2       4196352 5242879 1046528  511M 83 Linux
```
### 5. Используя sfdisk, перенесите данную таблицу разделов на второй диск.
```bash
root@vagrant:~# sfdisk -d /dev/sdb > partitions-sdb
root@vagrant:~# sfdisk /dev/sdc < partitions-sdb
Checking that no-one is using this disk right now ... OK
...
Device     Boot   Start     End Sectors  Size Id Type
/dev/sdc1          2048 4196351 4194304    2G 83 Linux
/dev/sdc2       4196352 5242879 1046528  511M 83 Linux

The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```
### 6. Соберите mdadm RAID1 на паре разделов 2 Гб.
```bash
root@vagrant:~# mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
```
### 7. Соберите mdadm RAID0 на второй паре маленьких разделов.
```bash
root@vagrant:~# mdadm --create /dev/md1 --level=0 --raid-devices=2 /dev/sdb2 /dev/sdc2
```
### 8. Создайте 2 независимых PV на получившихся md-устройствах.
```bash
root@vagrant:~# pvcreate /dev/md1 /dev/md0
  Physical volume "/dev/md1" successfully created.
  Physical volume "/dev/md0" successfully created.
```
### 9. Создайте общую volume-group на этих двух PV
```bash
root@vagrant:~# vgcreate vol_grp1 /dev/md1 /dev/md0
  Volume group "vol_grp1" successfully created
root@vagrant:~# vgs
  VG        #PV #LV #SN Attr   VSize   VFree 
  vgvagrant   1   2   0 wz--n- <63.50g     0 
  vol_grp1    2   0   0 wz--n-  <2.99g <2.99g
root@vagrant:~# vgdisplay
...   
  --- Volume group ---
  VG Name               vol_grp1
  System ID             
  Format                lvm2
  Metadata Areas        2
  Metadata Sequence No  1
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                0
  Open LV               0
  Max PV                0
  Cur PV                2
  Act PV                2
  VG Size               <2.99 GiB
  PE Size               4.00 MiB
  Total PE              765
  Alloc PE / Size       0 / 0   
  Free  PE / Size       765 / <2.99 GiB
  VG UUID               mafQt8-W6Ob-Iv2K-vyds-5VJF-YeEA-mbXZnq
```
### 10. Создайте LV размером 100 Мб, указав его расположение на PV с RAID0.
```bash
root@vagrant:~# lvcreate -L 100M -n log_vol0 vol_grp1 /dev/md1
  Logical volume "log_vol0" created.
root@vagrant:~# lvs
  LV       VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root     vgvagrant -wi-ao---- <62.54g                                                    
  swap_1   vgvagrant -wi-ao---- 980.00m                                                    
  log_vol0 vol_grp1  -wi-a----- 100.00m 
root@vagrant:~# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda                       8:0    0   64G  0 disk  
├─sda1                    8:1    0  512M  0 part  /boot/efi
├─sda2                    8:2    0    1K  0 part  
└─sda5                    8:5    0 63.5G  0 part  
  ├─vgvagrant-root      253:0    0 62.6G  0 lvm   /
  └─vgvagrant-swap_1    253:1    0  980M  0 lvm   [SWAP]
sdb                       8:16   0  2.5G  0 disk  
├─sdb1                    8:17   0    2G  0 part  
│ └─md0                   9:0    0    2G  0 raid1 
└─sdb2                    8:18   0  511M  0 part  
  └─md1                   9:1    0 1018M  0 raid0 
    └─vol_grp1-log_vol0 253:2    0  100M  0 lvm   
sdc                       8:32   0  2.5G  0 disk  
├─sdc1                    8:33   0    2G  0 part  
│ └─md0                   9:0    0    2G  0 raid1 
└─sdc2                    8:34   0  511M  0 part  
  └─md1                   9:1    0 1018M  0 raid0 
    └─vol_grp1-log_vol0 253:2    0  100M  0 lvm  
```
### 11. Создайте mkfs.ext4 ФС на получившемся LV.
```bash
root@vagrant:~# mkfs.ext4 /dev/vol_grp1/log_vol0
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done
```
### 12. Смонтируйте этот раздел в любую директорию, например, /tmp/new.
```bash
root@vagrant:~# mkdir /tmp/new
root@vagrant:~# mount /dev/vol_grp1/log_vol0 /tmp/new
```
### 13. Поместите туда тестовый файл, например wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz
```bash
root@vagrant:~# wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz
root@vagrant:~# ll /tmp/new
total 22076
drwxr-xr-x  3 root root     4096 Nov 25 19:15 ./
drwxrwxrwt 10 root root     4096 Nov 25 19:10 ../
drwx------  2 root root    16384 Nov 25 19:06 lost+found/
-rw-r--r--  1 root root 22581153 Nov 25 17:27 test.gz
```
### 14. Прикрепите вывод lsblk.
```bash
root@vagrant:~# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda                       8:0    0   64G  0 disk  
├─sda1                    8:1    0  512M  0 part  /boot/efi
├─sda2                    8:2    0    1K  0 part  
└─sda5                    8:5    0 63.5G  0 part  
  ├─vgvagrant-root      253:0    0 62.6G  0 lvm   /
  └─vgvagrant-swap_1    253:1    0  980M  0 lvm   [SWAP]
sdb                       8:16   0  2.5G  0 disk  
├─sdb1                    8:17   0    2G  0 part  
│ └─md0                   9:0    0    2G  0 raid1 
└─sdb2                    8:18   0  511M  0 part  
  └─md1                   9:1    0 1018M  0 raid0 
    └─vol_grp1-log_vol0 253:2    0  100M  0 lvm   /tmp/new
sdc                       8:32   0  2.5G  0 disk  
├─sdc1                    8:33   0    2G  0 part  
│ └─md0                   9:0    0    2G  0 raid1 
└─sdc2                    8:34   0  511M  0 part  
  └─md1                   9:1    0 1018M  0 raid0 
    └─vol_grp1-log_vol0 253:2    0  100M  0 lvm   /tmp/new
```
### 15. Протестируйте целостность файла:
```bash
root@vagrant:~# gzip -t /tmp/new/test.gz
root@vagrant:~# echo $?
0
```
### 16. Используя pvmove, переместите содержимое PV с RAID0 на RAID1.
```bash
root@vagrant:~# pvmove /dev/md1 /dev/md0
  /dev/md1: Moved: 20.00%
  /dev/md1: Moved: 100.00%
root@vagrant:~# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda                       8:0    0   64G  0 disk  
├─sda1                    8:1    0  512M  0 part  /boot/efi
├─sda2                    8:2    0    1K  0 part  
└─sda5                    8:5    0 63.5G  0 part  
  ├─vgvagrant-root      253:0    0 62.6G  0 lvm   /
  └─vgvagrant-swap_1    253:1    0  980M  0 lvm   [SWAP]
sdb                       8:16   0  2.5G  0 disk  
├─sdb1                    8:17   0    2G  0 part  
│ └─md0                   9:0    0    2G  0 raid1 
│   └─vol_grp1-log_vol0 253:2    0  100M  0 lvm   /tmp/new
└─sdb2                    8:18   0  511M  0 part  
  └─md1                   9:1    0 1018M  0 raid0 
sdc                       8:32   0  2.5G  0 disk  
├─sdc1                    8:33   0    2G  0 part  
│ └─md0                   9:0    0    2G  0 raid1 
│   └─vol_grp1-log_vol0 253:2    0  100M  0 lvm   /tmp/new
└─sdc2                    8:34   0  511M  0 part  
  └─md1                   9:1    0 1018M  0 raid0 
```
### 17. Сделайте --fail на устройство в вашем RAID1 md.
```bash
root@vagrant:~# mdadm /dev/md0 --fail /dev/sdc1
mdadm: set /dev/sdc1 faulty in /dev/md0
```
### 18. Подтвердите выводом dmesg, что RAID1 работает в деградированном состоянии.
```bash
root@vagrant:~# dmesg | grep md0 
...
[15593.116340] md/raid1:md0: Disk failure on sdc1, disabling device.
               md/raid1:md0: Operation continuing on 1 devices.
```
### 19. Протестируйте целостность файла, несмотря на "сбойный" диск он должен продолжать быть доступен:
```bash
root@vagrant:~# gzip -t /tmp/new/test.gz
root@vagrant:~# echo $?
0
```
### 20. Погасите тестовый хост, vagrant destroy.
Выполнено

# 3.6. Компьютерные сети, лекция 1
### 1. Работа c HTTP через телнет.
```bash
$ telnet stackoverflow.com 80
Trying 151.101.65.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: b001454a-9d59-4de4-ab7a-b3b7076f9168
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Sun, 28 Nov 2021 18:21:26 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-fra19133-FRA
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1638123687.902163,VS0,VE92
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=e95a13dd-43f1-a2d5-bc2c-9a54ada54daa; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```
Код ответа - `301`, что означает редирект на другой адрес (location: https://stackoverflow.com/questions).
### 2. Повторите задание 1 в браузере, используя консоль разработчика F12
[image1](https://d.radikal.ru/d06/2111/b9/9e537bcef892.png)
[image2](https://b.radikal.ru/b18/2111/da/cc060a1afef0.png)
Код ответа первого HTTP запроса - 200. Время загрузки - 1.01 с. Дольше всего обрабатывался этот же запрос - 135 мс. 
### 3. Какой IP адрес у вас в интернете?
Мой IP: 109.252.xx.xx Результат запроса в браузере: https://whoer.net/.
### 4. Какому провайдеру принадлежит ваш IP адрес? Какой автономной системе AS? Воспользуйтесь утилитой whois
```bash
$ whois 109.252.xx.xx | grep descr
descr:          Moscow Local Telephone Network (OAO MGTS)
...
$ whois 109.252.xx.xx | grep origin
origin:         AS25513
```
Провайдер - Moscow Local Telephone Network (OAO MGTS). Автономная система - AS25513 
### 5. Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой traceroute
```bash
$ traceroute -An 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  10.0.2.2 [*]  0.581 ms  0.418 ms  0.319 ms
 2  192.168.1.1 [*]  6.292 ms  6.102 ms  5.924 ms
 3  100.68.0.1 [*]  6.951 ms  6.784 ms  6.681 ms
 4  212.188.1.106 [AS8359]  8.376 ms  8.239 ms  8.344 ms
 5  212.188.1.105 [AS8359]  8.469 ms  8.080 ms  8.043 ms
 6  212.188.56.13 [AS8359]  9.921 ms  7.953 ms  7.822 ms
 7  195.34.50.74 [AS8359]  7.716 ms  7.866 ms  7.720 ms
 8  212.188.29.82 [AS8359]  7.397 ms  7.263 ms  7.140 ms
 9  108.170.250.34 [AS15169]  7.895 ms  7.700 ms 108.170.250.99 [AS15169]  7.524 ms
10  209.85.249.158 [AS15169]  22.871 ms 209.85.255.136 [AS15169]  26.212 ms  26.408 ms
11  209.85.254.20 [AS15169]  26.245 ms 216.239.57.222 [AS15169]  22.243 ms 108.170.235.64 [AS15169]  27.519 ms
12  172.253.51.237 [AS15169]  27.383 ms 74.125.253.147 [AS15169]  35.288 ms 216.239.47.165 [AS15169]  73.430 ms
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * 8.8.8.8 [AS15169]  25.404 ms  25.145 ms
```
```bash
$ whois AS8359 | grep as-name
as-name:        MTS
$ whois AS15169 | grep OrgName
OrgName:        Google LLC
```
Пакет проходит через следующие AS: AS8359, AS15169. Они принадлежат МТС и Google.
### 6. Повторите задание 5 в утилите mtr. На каком участке наибольшая задержка - delay?
```bash
$ mtr 8.8.8.8 -znrc 1
Start: 2021-11-28T20:09:55+0000
HOST: vagrant                     Loss%   Snt   Last   Avg  Best  Wrst StDev
  1. AS???    10.0.2.2             0.0%     1    0.7   0.7   0.7   0.7   0.0
  2. AS???    192.168.1.1          0.0%     1    5.1   5.1   5.1   5.1   0.0
  3. AS???    100.68.0.1           0.0%     1    5.8   5.8   5.8   5.8   0.0
  4. AS8359   212.188.1.106        0.0%     1    6.0   6.0   6.0   6.0   0.0
  5. AS8359   212.188.1.105        0.0%     1    6.0   6.0   6.0   6.0   0.0
  6. AS8359   212.188.56.13        0.0%     1   28.1  28.1  28.1  28.1   0.0
  7. AS8359   195.34.50.74         0.0%     1    7.9   7.9   7.9   7.9   0.0
  8. AS8359   212.188.29.82        0.0%     1    8.2   8.2   8.2   8.2   0.0
  9. AS15169  108.170.250.34       0.0%     1    7.7   7.7   7.7   7.7   0.0
 10. AS15169  172.253.66.116       0.0%     1   23.7  23.7  23.7  23.7   0.0
 11. AS15169  72.14.235.69         0.0%     1   23.6  23.6  23.6  23.6   0.0
 12. AS15169  172.253.79.169       0.0%     1   21.9  21.9  21.9  21.9   0.0
 13. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 14. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 15. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 16. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 17. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 18. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 19. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 20. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 21. AS???    ???                 100.0     1    0.0   0.0   0.0   0.0   0.0
 22. AS15169  8.8.8.8              0.0%     1   24.9  24.9  24.9  24.9   0.0
```
Максимальная задержка на 6 пункте (хопе). 
### 7. Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой dig
```bash
vagrant@vagrant:~$ dig NS dns.google +short
ns3.zdns.google.
ns1.zdns.google.
ns2.zdns.google.
ns4.zdns.google.
vagrant@vagrant:~$ dig A dns.google +short 
8.8.8.8
8.8.4.4
```
### 8. Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой dig
```bash
vagrant@vagrant:~$ dig -x 8.8.8.8 +short
dns.google.
vagrant@vagrant:~$ dig -x 8.8.4.4 +short
dns.google.
```
# 3.7. Компьютерные сети, лекция 2
### 1. Проверьте список доступных сетевых интерфейсов на вашем компьютере. Какие команды есть для этого в Linux и в Windows?
Linux: `ifconfig -a`, `ip l`
### 2. Какой протокол используется для распознавания соседа по сетевому интерфейсу? Какой пакет и команды есть в Linux для этого?
Используется протокол `LLDP`. Пакет `lldpd`.
Команды:
```bash
lldpcli show neighbors - для вывода соседей
lldpcli show interfaces - для вывода информации о всех локальных интерфейсах
lldpcli show statistics - для вывода статистики: кол-во переданных, полученных, отклоненных кадров. 
```
### 3. Какая технология используется для разделения L2 коммутатора на несколько виртуальных сетей? Какой пакет и команды есть в Linux для этого? Приведите пример конфига.
Технология - VLAN, пакет в Linux Ubuntu - `vlan`. Пример конфига (/etc/network/interfaces):
```bash
#vlan id-100
auto wlp3s0.100
iface wlp3s0.100 inet static
        address 192.168.1.1
        netmask 255.255.255.0
        vlan-raw-device wlp3s0
```
### 4. Какие типы агрегации интерфейсов есть в Linux? Какие опции есть для балансировки нагрузки? Приведите пример конфига.
Типы агрегации интерфейсов в Linux:
```bash
$ modinfo bonding | grep mode
... 0 for balance-rr, 1 for active-backup, 2 for balance-xor, 3 for broadcast, 4 for 802.3ad, 5 for balance-tlb, 6 for balance-alb
```
```Text
active-backup и broadcast обеспечивают только отказоустойчивость
balance-tlb, balance-alb, balance-rr, balance-xor и 802.3ad обеспечат отказоустойчивость и балансировку
```
Пример конфига:
```yaml
    bonds: 
      bond0:
        dhcp4: no
        interfaces: [wlp3s0, enp4s0f1]
        parameters:
          mode: 802.3ad
          mii-monitor-interval: 1
```
### 5. Сколько IP адресов в сети с маской /29 ? Сколько /29 подсетей можно получить из сети с маской /24. Приведите несколько примеров /29 подсетей внутри сети 10.10.10.0/24.
В сети с маской /29 - 8 адресов. Для хостов можно использовать 6 (за исключением широковещательного адреса и адреса сети).

Сеть с маской /24 разбивается на 32 подсети с маской /29. Примеры:
```bash
Network			- 10.10.10.0      - 10.10.10.7
Network			- 10.10.10.8      - 10.10.10.15
Network			- 10.10.10.16     - 10.10.10.23
Network			- 10.10.10.24     - 10.10.10.31
Network			- 10.10.10.32     - 10.10.10.39
```
### 6. Задача: вас попросили организовать стык между 2-мя организациями. Диапазоны 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 уже заняты. Из какой подсети допустимо взять частные IP адреса? Маску выберите из расчета максимум 40-50 хостов внутри подсети.
Адреса можно взять из сети Carrier-Grade NAT: `100.64.0.0/10`. Маску можно взять `/26`. Подсеть с такой маской расчитана на 62 хоста.  
### 7. Как проверить ARP таблицу в Linux, Windows? Как очистить ARP кеш полностью? Как из ARP таблицы удалить только один нужный IP?
Проверка ARP таблицы в Linux: `ip neigh show`, `ip n`.

Очистить ARP кеш полностью в Linux: `ip neigh flush`.

Удалить из ARP таблицы только один нужный IP: `ip neigh del dev <INTERFACE> <IP>`.

# 3.8. Компьютерные сети, лекция 3
### 1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP: ...
```bash
route-views>show ip route 109.252.xx.xx 
Routing entry for 109.252.0.0/16
  Known via "bgp 6447", distance 20, metric 0
  Tag 8283, type external
  Last update from 94.142.247.3 3d12h ago
  Routing Descriptor Blocks:
  * 94.142.247.3, from 94.142.247.3, 3d12h ago
      Route metric is 0, traffic share count is 1
      AS Hops 3
      Route tag 8283
      MPLS label: none
route-views>show bgp 109.252.xx.xx 
BGP routing table entry for 109.252.0.0/16, version 1391417923
Paths: (24 available, best #13, table default)
  Not advertised to any peer
  Refresh Epoch 1
  6939 8359 25513
    64.71.137.241 from 64.71.137.241 (216.218.252.164)
      Origin IGP, localpref 100, valid, external
      path 7FE15B593A70 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 3
  3303 8359 25513
    217.192.89.50 from 217.192.89.50 (138.187.128.158)
      Origin IGP, localpref 100, valid, external
      Community: 0:151 3303:1004 3303:1006 3303:1030 3303:3054 8359:100 8359:5500 8359:55277
      path 7FE114A17770 RPKI State not found
      rx pathid: 0, tx pathid: 0
...
```
### 2. Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.
Создание dummy0 интерфейса:
```bash
$ sudo ip link add dummy0 type dummy
$ ip -br l
lo               UNKNOWN        00:00:00:00:00:00 <LOOPBACK,UP,LOWER_UP> 
eth0             UP             08:00:27:73:60:cf <BROADCAST,MULTICAST,UP,LOWER_UP> 
dummy0           DOWN           f6:2f:e9:3c:30:39 <BROADCAST,NOARP> 
```
Добавление статических маршрутов:
```bash
# Добавление маршрута через шлюз: 
$ sudo ip route add 192.168.5.0/24 via 10.0.2.15
# Добавление маршрута через интерфейс: 
$ sudo ip route add 192.168.6.0/24 dev eth0
# Добавление маршрута через интерфейс с метрикой:
$ sudo ip route add 192.168.7.0/24 dev eth0 metric 100
```
Проверка таблицы маршрутизации:
```bash
$ ip r
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100 
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15 
10.0.2.2 dev eth0 proto dhcp scope link src 10.0.2.15 metric 100 
192.168.5.0/24 via 10.0.2.15 dev eth0 
192.168.6.0/24 dev eth0 scope link 
192.168.7.0/24 dev eth0 scope link metric 100 
```
### 3. Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров.
```bash
$ sudo ss -tnlp
State          Recv-Q         Send-Q                 Local Address:Port                 Peer Address:Port        Process                                                          
LISTEN         0              4096                   127.0.0.53%lo:53                        0.0.0.0:*            users:(("systemd-resolve",pid=608,fd=13))                       
LISTEN         0              128                          0.0.0.0:22                        0.0.0.0:*            users:(("sshd",pid=958,fd=3))                                   
LISTEN         0              4096                         0.0.0.0:111                       0.0.0.0:*            users:(("rpcbind",pid=607,fd=4),("systemd",pid=1,fd=35))        
LISTEN         0              128                             [::]:22                           [::]:*            users:(("sshd",pid=958,fd=4))                                   
LISTEN         0              4096                            [::]:111                          [::]:*            users:(("rpcbind",pid=607,fd=6),("systemd",pid=1,fd=37))
```
Порт 53 - DNS

Порт 22 - SSH
### 4. Проверьте используемые UDP сокеты в Ubuntu, какие протоколы и приложения используют эти порты?
```bash
$ sudo ss -unap
State         Recv-Q         Send-Q                  Local Address:Port                 Peer Address:Port        Process                                                          
UNCONN        0              0                       127.0.0.53%lo:53                        0.0.0.0:*            users:(("systemd-resolve",pid=608,fd=12))                       
UNCONN        0              0                      10.0.2.15%eth0:68                        0.0.0.0:*            users:(("systemd-network",pid=419,fd=15))                       
UNCONN        0              0                             0.0.0.0:111                       0.0.0.0:*            users:(("rpcbind",pid=607,fd=5),("systemd",pid=1,fd=36))        
UNCONN        0              0                                [::]:111                          [::]:*            users:(("rpcbind",pid=607,fd=7),("systemd",pid=1,fd=38)) 
```
Порт 53 - DNS

Порт 68 - DHCP
### 5. Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали.
[image1](https://a.radikal.ru/a21/2112/90/63ea3c798627.png)

# 3.9. Элементы безопасности информационных систем.
### 1. Установите Bitwarden плагин для браузера. Зарегестрируйтесь и сохраните несколько паролей.
![](https://raw.githubusercontent.com/alexandrburyakov/Rep2/master/images/bitwarden.png)
### 2. Установите Google authenticator на мобильный телефон. Настройте вход в Bitwarden акаунт через Google authenticator OTP.
![](/home/user/PycharmProjects/Rep2/images/twostepauth.png)
### 3. Установите apache2, сгенерируйте самоподписанный сертификат, настройте тестовый сайт для работы по HTTPS.
Все сделано в соответствии с изложенным в презентации:
```shell
$ sudo nano /etc/apache2/sites-enabled/homework.conf
VirtualHost *:443>
  ServerName 127.0.0.1
  DocumentRoot /var/www/homework.com
  SSLEngine on
  SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
  SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
</VirtualHost>

$ openssl x509 -text -noout -in  /etc/ssl/certs/apache-selfsigned.crt | grep Subject
Subject: C = RU, ST = Moscow, L = Moscow, O = Company Name, OU = Org, CN = www.example.com
...

$ cat /var/www/homework.com/index.html
<h1>Homework for netology</h1>
```
![](/home/user/PycharmProjects/Rep2/images/localhost2.png)
![](/home/user/PycharmProjects/Rep2/images/cert.png)
### 4. Проверьте на TLS уязвимости произвольный сайт в интернете.
Проверка https://mail.ru/
```shell
$ ./testssl.sh -U --sneaky https://mail.ru/
 Testing vulnerabilities 

 Heartbleed (CVE-2014-0160)                not vulnerable (OK), timed out
 CCS (CVE-2014-0224)                       not vulnerable (OK)
 Ticketbleed (CVE-2016-9244), experiment.  not vulnerable (OK)
 ROBOT                                     not vulnerable (OK)
 Secure Renegotiation (RFC 5746)           supported (OK)
 Secure Client-Initiated Renegotiation     not vulnerable (OK)
 CRIME, TLS (CVE-2012-4929)                not vulnerable (OK)
 BREACH (CVE-2013-3587)                    potentially NOT ok, "gzip" HTTP compression detected. - only supplied "/" tested
                                           Can be ignored for static pages or if no secrets in the page
 POODLE, SSL (CVE-2014-3566)               not vulnerable (OK)
 TLS_FALLBACK_SCSV (RFC 7507)              Downgrade attack prevention supported (OK)
 SWEET32 (CVE-2016-2183, CVE-2016-6329)    VULNERABLE, uses 64 bit block ciphers
 FREAK (CVE-2015-0204)                     not vulnerable (OK)
 DROWN (CVE-2016-0800, CVE-2016-0703)      not vulnerable on this host and port (OK)
                                           make sure you don't use this certificate elsewhere with SSLv2 enabled services
                                           https://censys.io/ipv4?q=73CE7337E1FE4D5E6CBAB304B5E401B21C006CCEC612092AD83209BBABEED18B could help you to find out
 LOGJAM (CVE-2015-4000), experimental      not vulnerable (OK): no DH EXPORT ciphers, no common prime detected
 BEAST (CVE-2011-3389)                     TLS1: ECDHE-RSA-AES256-SHA ECDHE-RSA-AES128-SHA ECDHE-RSA-DES-CBC3-SHA DHE-RSA-AES256-SHA DHE-RSA-AES128-SHA EDH-RSA-DES-CBC3-SHA AES256-SHA AES128-SHA
                                                 DES-CBC3-SHA 
                                           VULNERABLE -- but also supports higher protocols  TLSv1.1 TLSv1.2 (likely mitigated)
 LUCKY13 (CVE-2013-0169), experimental     potentially VULNERABLE, uses cipher block chaining (CBC) ciphers with TLS. Check patches
 Winshock (CVE-2014-6321), experimental    not vulnerable (OK) - CAMELLIA or ECDHE_RSA GCM ciphers found
 RC4 (CVE-2013-2566, CVE-2015-2808)        no RC4 ciphers detected (OK)


 Done 2021-12-07 20:38:46 [  46s] -->> 217.69.139.202:443 (mail.ru) <<--
```
### 5. Установите на Ubuntu ssh сервер, сгенерируйте новый приватный ключ. Скопируйте свой публичный ключ на другой сервер. Подключитесь к серверу по SSH-ключу.
Установка ssh-сервера, генерация ключей:
```bash
~# apt install openssh-server
~# systemctl start sshd.service
~# ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): /root/.ssh/homework_rsa      
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/homework_rsa.
Your public key has been saved in /root/.ssh/homework_rsa.pub.
The key fingerprint is:
SHA256:XqqSZlKO4JWxS0qIf0+nrN5ORMlrTkMwpgEXMcb8lgU root@user-Aspire-F5-573G
The key's randomart image is:
+---[RSA 2048]----+
|.+BoE.           |
| oo= +..         |
|  .. o=          |
|   .+o .         |
|o  .+ * S .      |
|+. =.= o o       |
|oo++..+ +        |
| o+.B= +         |
|   *o=B          |
+----[SHA256]-----+
```
Копирование ключа на другой сервер. Подключение к серверу по SSH-ключу:
```bash
~# ssh-copy-id -i .ssh/homework_rsa.pub root@192.168.0.2
~# ssh -i .ssh/homework_rsa root@192.168.0.2
```
### 6. Переименуйте файлы ключей из задания 5. Настройте файл конфигурации SSH клиента, так чтобы вход на удаленный сервер осуществлялся по имени сервера.
Переименование файлов ключей:
```bash
~# mv .ssh/homework_rsa .ssh/new_homework_rsa
~# mv .ssh/homework_rsa.pub .ssh/new_homework_rsa.pub
```
Настройка файла конфигурации:
```bash
~# cat .ssh/config
Host nas01
     HostName 192.168.0.2
     User root
     IdentityFile /root/.ssh/new_homework_rsa
```
Подключение:
```bash
~# ssh nas01
```
### 7. Соберите дамп трафика утилитой tcpdump в формате pcap, 100 пакетов. Откройте файл pcap в Wireshark.
```bash
~# tcpdump -c 100 -w dump_file.pcap
tcpdump: listening on wlp3s0, link-type EN10MB (Ethernet), capture size 262144 bytes
100 packets captured
118 packets received by filter
0 packets dropped by kernel
```
![](/home/user/PycharmProjects/Rep2/images/wireshark.png)
