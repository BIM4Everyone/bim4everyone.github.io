---
date: :git
draft: false

params:
  author: dosymep
  
title: Visual Studio
linkTitle: Visual Studio
description: |
  Руководство по установке и настройке Visual Studio.

tags: [docs, setup, visual studio, VS 2022, plugins, options, settings, code cleanup, autoformat, reformat, actions on save, Visual Studio Spell Checker, spell check, spelling, Editor Guidelines, line max length, VSColorOutput64, color output, dotnet tools, powershell, nuke]
categories: [docs, setup, visual studio]

weight: 20
---

[Visual Studio](https://visualstudio.microsoft.com/) - это IDE для разработки на C#
с поддерживаемой бесплатной версией (Community Edition).

## Установка

Перейдите по [ссылке](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&channel=Release&version=VS2022&source=VSLandingPage&cid=2030&passive=false)
на официальный сайт и скачайте загрузочный файл программы установки.
Запустите его и следуйте инструкциям по установке Visual Studio Installer.
Когда появится окно для установки Visual Studio Community 2022 выберите следующие опции:

В Workloads выберите `.NET desktop development`:

<img src="vs-setup-page-1.png" width="900"/>

В Language packs выберите `English`:

<img src="vs-setup-page-2.png" width="900"/>

После завершения установки рекомендуется `перезапустить ПК`.

## Настройка аккаунтов в Visual Studio

При первом запуске справа снизу выберите `Continue without code`:

<img src="vs-settings-page-1.png" width="600"/>

В правом верхнем углу нажмите `Sign in`:

<img src="vs-settings-page-2.png" width="300"/>

В появившемся окне выберите свой аккаунт Microsoft и введите пароль.
Создайте аккаунт, если у вас еще нет аккаунта Microsoft. Далее добавьте аккаунт GitHub.
Если вы еще не зарегистрировались на GitHub, сделайте это:

<img src="vs-settings-page-3.png" width="300"/>

## Настройка текстового редактора

Перейдите в `Tools -> Options` и задайте настройки, которые будут вам удобны.

<img src="vs-settings-page-4.png" width="500"/>

Пример настроек текстового редактора (`Text Editor`):

<img src="vs-settings-page-5.png" width="500"/>

## Настройка автоформатирования при сохранении

Чтобы код автоматически форматировался в соответствии с [.editorconfig](https://editorconfig.org/), необходимо включить флаг в настройках:

<img src="vs-settings-page-6.png" width="500"/>

Нажав на `Configure Code Cleanup` можно задать дополнительные действия:

<img src="vs-settings-page-7.png" width="500"/>

## Установка плагинов для Visual Studio

Перед установкой плагинов необходимо `закрыть Visual Studio`.

### Установка Visual Studio Spell Checker

Данный плагин делает проверку орфографии.

Перейдите на [страницу](https://marketplace.visualstudio.com/items?itemName=EWoodruff.VisualStudioSpellCheckerVS2022andLater)
плагина, в Marketplace и скачайте установочный файл.
Запустите его и следуйте инструкциям по установке.

Чтобы открыть настройки плагина, прейдите в `Tools -> Spell Checker -> Edit Global Configuration`:

<img src="vs-settings-page-8.png" width="500"/>

Добавьте словари английского и русского языка:

<img src="vs-settings-page-9.png" width="900"/>

Настройте опции проверки орфографии:

<img src="vs-settings-page-10.png" width="900"/>

`Сохраните настройки`.

#### Добавление слов в словарь исключений

Чтобы добавить слово в словарь исключений необходимо нажать `Alt+Enter`:

<img src="vs-settings-page-11.png" width="300"/>

На момент написания этой инструкции в плагине есть `особенность`: нельзя сразу добавить слово в словарь,
если это слово - название класса/пространства имен и прочее:

<img src="vs-settings-page-12.png" width="300"/>

Обойти это можно, написав комментарий с этим словом, и добавив слово из комментария:

<img src="vs-settings-page-13.png" width="300"/>

### Установка Editor Guidelines

Данный плагин отображает максимальную длину строки в виде вертикальной линии.

Перейдите на [страницу](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelinesPreview)
плагина, в Marketplace и скачайте установочный файл.
Запустите его и следуйте инструкциям по установке.

Чтобы настроить цвет линии, перейдите в `Tools -> Options -> Environment -> Fonts and Colors -> Guideline`:

<img src="vs-settings-page-14.png" width="500"/>

### Установка VSColorOutput64

Данный плагин раскрашивает консольный вывод в цвета по типу сообщения вывода.

Перейдите на [страницу](https://marketplace.visualstudio.com/items?itemName=MikeWard-AnnArbor.VSColorOutput64)
плагина, в Marketplace и скачайте установочный файл.
Запустите его и следуйте инструкциям по установке.

Чтобы настроить плагин, перейдите в `Tools -> Options -> VSColorOutput64`:

<img src="vs-settings-page-15.png" width="500"/>

## Установка dotnet tools

Чтобы установить [dotnet tools](https://learn.microsoft.com/en-us/dotnet/core/tools/global-tools), 
откройте [powershell](https://learn.microsoft.com/en-us/powershell/scripting/windows-powershell/starting-windows-powershell?view=powershell-7.4).
Это можно сделать сразу в Visual Studio. Для этого перейдите в `View -> Terminal`:

<img src="dotnet-tools-setup-page-1.png" width="400"/>

### Установка powershell tool

```
dotnet tool install --global PowerShell
```

### Установка nuke tool

[Nuke](https://nuke.build/) - это утилита для автоматизации сборки и публикации проектов.

```
dotnet tool install --global Nuke.GlobalTool
```
