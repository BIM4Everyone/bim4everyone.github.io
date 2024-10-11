---
date: :git
draft: false

params:
  author: dosymep
  
title: PyCharm
linkTitle: PyCharm
description: |
  Руководство по установке и настройке PyCharm.

tags: [test, docs]
categories: [Examples, Placeholders]

weight: 30
---

[PyCharm](https://www.jetbrains.com/pycharm) - это IDE для разработки на Python
с поддерживаемой бесплатной версией (Community Edition).

## Установка

Перейдите по [ссылке](https://www.jetbrains.com/pycharm/download/?section=windows) на официальный сайт и скачайте установочный файл `PyCharm Community Edition`.

<img src="pycharm-setup-page-0.png" width="300"/>

 Запустите его и следуйте инструкциям по установке. Выберите следующие опции:

<img src="pycharm-setup-page-1.png" width="400"/>

После установки `перезапустите ПК`

## Настройка

### Добавление RevitAPIStubs

Скачайте архив с RevitAPIStubs по [ссылке](https://github.com/BIMOpenGroup/RevitAPIStubs/releases/latest). В этом архиве находится python код,
который помогает PyCharm делать подсказки по API Revit.

<img src="pycharm-settings-page-1.png" width="700"/>

Распакуйте содержимое архива. Папки `common` и `revit`:

<img src="pycharm-settings-page-2.png" width="450"/>

### Добавление интерпретаторов

Перед тем, как добавлять интерпретаторы, убедитесь, что на вашем ПК установлена сама платформа [Bim4Everyone](../../install/_index.md).

В главном окне при запуске PyCharm перейдите в раздел `Customize -> All settings`:

<img src="pycharm-settings-page-3.png" width="600"/>

Затем перейдите в раздел `Python Interpreter -> Show All`

<img src="pycharm-settings-page-4.png" width="600"/>

Нажмите `+` чтобы добавить интерпретатор:

<img src="pycharm-settings-page-5.png" width="600"/>

В открывшемся окне выберите раздел Virtual Environment. В качестве Base interpreter укажите путь к `python.exe`
(`python2.7` который вы устанавливали выше). Т.к. stub файлы различные для каждой версии Revit,
то под каждую версию Revit необходимо создавать свой интерпретатор.
Соответственно, надо создать папки для интерпретаторов под все версии Revit, которые установлены у вас.
При добавлении очередного интерпретатора указывайте соответствующую папку в `Location`.

<img src="pycharm-settings-page-6.png" width="600"/>

Затем необходимо настроить пути для каждого интерпретатора. Чтобы открыть окно настроек, нажмите ПКМ на интерпретатор и 
выберите `Show Interpreter Paths`:

<img src="pycharm-settings-page-7.png" width="600"/>

Для каждого добавленного интерпретатора необходимо `добавить 4 пути`:

- путь к соответствующим stubs файлам из архива, находящимся в revit/20xx (будет разный для каждого интерпретатора).
- путь к common файлам также из архива (будет одинаковый для всех интерпретаторов).
- путь к папке `%AppData%\pyRevit-Master\pyrevitlib` (будет одинаковый для всех интерпретаторов), 
    которая создается при установке pyRevit.
- путь к папке `%AppData%\pyRevit\Extensions\BIM4Everyone.lib` (будет одинаковый для всех интерпретаторов),
    которая создается при установке платформы Bim4Everyone.

<img src="pycharm-settings-page-8.png" width="450"/>

### PyCharm custom properties

Перейдите в раздел `Edit Custom Properties`:

<img src="pycharm-settings-page-9.png" width="600"/>

И замените весь существующий текст на следующий:

```
#---------------------------------------------------------------------
# Maximum file size (kilobytes) IDE should provide code assistance for.
# The larger file is the slower its editor works and higher overall system memory requirements are
# if code assistance is enabled. Remove this property or set to very large number if you need
# code assistance for any files available regardless their size.
#---------------------------------------------------------------------
idea.max.intellisense.filesize=40000

#---------------------------------------------------------------------
# Maximum file size (kilobytes) IDE is able to open.
#---------------------------------------------------------------------
idea.max.content.load.filesize=40000

```
