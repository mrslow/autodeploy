# Введение


## Поряд работы с библиотекой:
1. Установить плагин.
2. Создать файл fabfile.py
3. Установить библиотеку [fabric](http://www.fabfile.org/installing.html). 
4. В модуле fabfile сделать импорт из модуля fablib следующих функций:
    1. init - функция для инициализации проекта на сервере. 
    2. deploy - функция обновления проекта на сервере.
    3. rollback - функция для отката приложения на определенную версию.
5. Запустить функцию из консоли командой `fab init:some.yaml`, где
    1. fab - ключевое слово для библиотеки fabric
    2. init - одна из функций модуля fablib. Может быть заменена на 
    deploy или rollback.
    3. some.yaml - yaml файл с конфигурацией проекта на сервере.


## Содержание файла с конфигурациями

### Параметры конфигурации:
#### Необязательные параметры(их можно не указывать):
1. `branch` - ветка с проектом. По умолчанию `master`.
2. `venv_requirements` - имя файла с указанием всех библиотек и их версий.
По умолчанию `requirements.txt`.
3. `python` - путь python-интерпретатора. По умолчанию `venv/bin/python`.
4. `pip` - пусть до pip. По умолчанию `venv/bin/pip`.

#### Обязательные параметры(без них работать не будет):
1. `hosts` - список хостов. Указывается в таком формате: `user@host:port`.
2. `work_service` - сервис, который взаимодействует с сервиром. 
Он будет запущен при инициализации и перезагружен при обновлении или откате.
Если сервер не использует какой-либо сервис то, в качестве параметра следует указать `None`.
3. `path` - путь к каталогу с проектом.
4. `repository` - путь к репозиторию с проектом.
5. `path_key` - путь по которому можно найти публичный ключ для входа на сервер.
6. `migrate_command` - команда для миграции базы данных.

[Пример файла с конфигурациями.](../myservers.yaml)


## Параметры запуска функций
### `init` и `deploy`
Для удобства можно воспользоваться возможностью указать сервис в настройках запуска, например:
 `fab init:some.yaml,service=nginx`
 `fab deploy:some.yaml,service=nginx`
### `rollback`
По умолчанию при запуске отката типа `fab rollback:some.yaml` произойдет откат на один коммит назад.
Для отката к определенному коммиту следует воспользоваться параметром `commit_hash`:
`fab rollback:some.yaml,commit_hash=92s29f7`



**[Обратно к README](../README.md)**