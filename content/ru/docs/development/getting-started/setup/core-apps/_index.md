---
date: :git
draft: false

params:
  author: dosymep
  
title: Необходимое ПО
linkTitle: Необходимое ПО
description: |
  Руководство по установке и настройке необходимого ПО

tags: [docs, setup, git, config, python, notepad]
categories: [docs, setup, environment]

weight: 10
---

## Git

[Git](https://git-scm.com/) - это распределенная система контроля версий файлов.

### Установка Git

Перейдите по [ссылке](https://git-scm.com/downloads/win) и скачайте установочный файл Git for Windows.
Запустите его и следуйте инструкциям по установке. Если вы незнакомы с [Git](https://git-scm.com/), выбирайте значения по умолчанию.
Если вы продвинутый пользователь, вы уже сами знаете, что вам нужно.

`Перезапустите ПК`.

### Настройка Git

Если у вас еще нет аккаунта на [GitHub](https://github.com/), то необходимо его создать.

В ```user.name``` напишите свой логин [GitHub](https://github.com/):

```
git config --global user.name "johndoe"
```

В ```user.email``` напишите свой публичный email, который привязан к [GitHub](https://github.com/):

```
git config --global user.email johndoe@example.com
```

## Python

[Python](https://www.python.org/) - это язык программирования, на котором можно легко и быстро писать простые плагины.

### Установка Python

Для разработки плагинов на python, необходимо установить последнюю версию `Python2.7` (не путать с [IronPython2.7](https://ironpython.net/)).
Для этого перейдите по [ссылке](https://www.python.org/downloads/release/python-2718/) и скачайте установочный файл:

<img src="python-setup-page-1.png" width="700"/>

Запустите его и следуйте инструкциям по установке. Выбирайте значения по умолчанию.

После установки `перезапустите ПК`

## Notepad++

[Notepad++](https://notepad-plus-plus.org/) - это очень удобный бесплатный текстовый редактор для любого формата файлов.

### Установка notepad++

Перейдите на [сайт](https://notepad-plus-plus.org/downloads/) и скачайте установочный файл. Запустите его и следуйте инструкциям.


