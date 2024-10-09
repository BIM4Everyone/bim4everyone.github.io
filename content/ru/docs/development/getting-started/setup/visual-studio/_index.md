---
date: :git
draft: false

params:
  author: dosymep
  
title: Установка Visual Studio
linkTitle: Visual Studio
description: |
  Руководство по установке и настройке Visual Studio.

tags: [test, docs]
categories: [Examples, Placeholders]

weight: 20
---

# [Visual Studio](https://visualstudio.microsoft.com/)

IDE для разработки на C# с поддерживаемой бесплатной версией (Community Edition).

## Оглавление

1. [Установка](#установка)
2. [Настройка аккаунтов](#настройка-аккаунтов-в-visual-studio)
3. [Настройка текстового редактора](#настройка-текстового-редактора)
4. [Настройка автоформатирования при сохранении](#настройка-автоформатирования-при-сохранении)
5. [Установка плагинов для Visual Studio](#установка-плагинов-для-visual-studio)
   - [Установка Visual Studio Spell Checker](#установка-visual-studio-spell-checker)
   - [Установка Editor Guidelines](#установка-editor-guidelines)
   - [Установка VSColorOutput64](#установка-vscoloroutput64)
6. [Установка dotnet tools](#установка-dotnet-tools)
   - [Установка git tool](#установка-git-tool)
   - [Установка powershell tool](#установка-powershell-tool)
   - [Установка wix tool](#установка-wix-tool)
   - [Установка nuke tool](#установка-nuke-tool)

## Установка

Перейдите по [ссылке](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&channel=Release&version=VS2022&source=VSLandingPage&cid=2030&passive=false)
на официальный сайт и скачайте загрузочный файл программы установки.
Запустите его и следуйте инструкциям по установке Visual Studio Installer.
Когда появится окно для установки Visual Studio Community 2022 выберите следующие опции:

В Workloads выберите `.NET desktop development`:

![workloads.png](vs-setup-page-1.png)

В Language packs выберите `English`:

![language.png](vs-setup-page-2.png)

После завершения установки рекомендуется `перезапустить ПК`.

## Настройка аккаунтов в Visual Studio

При первом запуске справа снизу выберите `Continue without code`:

![img.png](vs-settings-page-1.png)

В правом верхнем углу нажмите `Sign in`:

![img.png](vs-settings-page-2.png)

В появившемся окне выберите свой аккаунт Microsoft и введите пароль.
Создайте аккаунт, если у вас еще нет аккаунта Microsoft. Далее добавьте аккаунт GitHub.
Если вы еще не зарегистрировались на GitHub, сделайте это:

![img.png](vs-settings-page-3.png)

## Настройка текстового редактора

Перейдите в Tools -> Options и задайте настройки, которые будут вам удобны.

![img.png](vs-settings-page-4.png)

![img.png](vs-settings-page-5.png)

## Настройка автоформатирования при сохранении

Чтобы код автоматически форматировался в соответствии с [.editorconfig](https://editorconfig.org/), необходимо включить флаг в настройках:

![img.png](vs-settings-page-6.png)

Нажав на `Configure Code Cleanup` можно задать дополнительные действия:

![img.png](vs-settings-page-7.png)

## Установка плагинов для Visual Studio

Перед установкой плагинов необходимо `закрыть Visual Studio`.

### Установка Visual Studio Spell Checker

Данный плагин делает проверку орфографии.

Перейдите на [страницу](https://marketplace.visualstudio.com/items?itemName=EWoodruff.VisualStudioSpellCheckerVS2022andLater)
плагина, в Marketplace и скачайте установочный файл.
Запустите его и следуйте инструкциям по установке.

Чтобы открыть настройки плагина, прейдите в `Tools -> Spell Checker -> Edit Global Configuration`:

![img.png](vs-settings-page-8.png)

Добавьте словари английского и русского языка:

![img.png](vs-settings-page-9.png)

Настройте опции проверки орфографии:

![img.png](vs-settings-page-10.png)

`Сохраните настройки`.

#### Добавление слов в словарь исключений

Чтобы добавить слово в словарь исключений необходимо нажать `Alt+Enter`:

![img.png](vs-settings-page-11.png)

На момент написания этой инструкции в плагине есть `особенность`: нельзя сразу добавить слово в словарь,
если это слово - название класса/пространства имен и прочее:

![img.png](vs-settings-page-12.png)

Обойти это можно, написав комментарий с этим словом, и добавив слово из комментария:

![img.png](vs-settings-page-13.png)

### Установка Editor Guidelines

Данный плагин отображает максимальную длину строки в виде вертикальной линии.

Перейдите на [страницу](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelinesPreview)
плагина, в Marketplace и скачайте установочный файл.
Запустите его и следуйте инструкциям по установке.

Чтобы настроить цвет линии, перейдите в `Tools -> Options -> Environment -> Fonts and Colors -> Guideline`:

![img.png](vs-settings-page-14.png)

### Установка VSColorOutput64

Данный плагин раскрашивает консольный вывод в цвета по типу сообщения вывода.

Перейдите на [страницу](https://marketplace.visualstudio.com/items?itemName=MikeWard-AnnArbor.VSColorOutput64)
плагина, в Marketplace и скачайте установочный файл.
Запустите его и следуйте инструкциям по установке.

Чтобы настроить плагин, перейдите в `Tools -> Options -> VSColorOutput64`:

![img.png](vs-settings-page-15.png)

## Установка [dotnet tools](https://learn.microsoft.com/en-us/dotnet/core/tools/global-tools)

Откройте [powershell](https://learn.microsoft.com/en-us/powershell/scripting/windows-powershell/starting-windows-powershell?view=powershell-7.4).
Это можно сделать сразу в Visual Studio. Для этого перейдите в `View -> Terminal`:

![img.png](dotnet-tools-setup-page-1.png)

### Установка git tool

```
dotnet tool install --global GitVersion.Tool
```

### Установка powershell tool

```
dotnet tool install --global PowerShell
```

### Установка [wix](https://wixtoolset.org/) tool

```
dotnet tool install --global wix --version 4.0.5
```
```
wix extension add -g WixToolset.UI.wixext/4.0.5
```
```
wix extension add -g WixToolset.Util.wixext/4.0.5
```

### Установка [nuke](https://nuke.build/) tool

```
dotnet tool install --global Nuke.GlobalTool
```
