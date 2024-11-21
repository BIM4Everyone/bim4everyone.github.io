---
date: :git
draft: false

params:
  author: dosymep
  
title: FAQ
linkTitle: FAQ
description: |
  Часто задаваемые вопросы.

tags: [faq]
categories: [faq]

weight: 70
---


## Что такое пайревит?

[pyRevit](https://pyrevitlabs.notion.site/) - это среда для быстрой разработки под Autodesk Revit.
Благодаря pyRevit, можно создавать плагины на python и C#, не отвлекаясь на инфраструктуру.
Также имеются широкие возможности для логирования и телеметрии.

## Как установить пайревит?

[Здесь](./getting-started/install/_index.md) вы найдете инструкцию по установке pyRevit.

## Где скачать платформу?

[Скачать](https://github.com/Bim4Everyone/Bim4EveryoneSetup/releases/latest) последнюю версию установщика платформы можно с github. 

## Как установить платформу?

[Здесь](./getting-started/install/_index.md/) вы найдете инструкцию по установке платформы Bim4Everyone.

## Как посмотреть изменения платформы?

Обновления в платформе пишутся в [CHANGELOG](https://github.com/Bim4Everyone/Bim4EveryoneSetup/blob/master/CHANGELOG.md) в репозиторий [Bim4EveryoneSetup](https://github.com/Bim4Everyone/Bim4EveryoneSetup).

## Как настроить логи платформы?

[Здесь](https://pyrevitlabs.notion.site/Collecting-Debug-Log-61941fa7782844e98e416e66ac39e4cf) вы найдете инструкцию по настройке логирования pyRevit.
Логи платформы по умолчанию пишутся в [журнал Revit](https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/Location-of-journal-files.html).
Если у вас запущен [сервис телеметрии](https://github.com/Bim4Everyone/Bim4EveryoneTelemetry), то можно также [настроить](https://github.com/Bim4Everyone/Bim4EveryoneSetup?tab=readme-ov-file#c%D0%B2%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%B0-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BA-%D1%82%D0%B5%D0%BB%D0%B5%D0%BC%D0%B5%D1%82%D1%80%D0%B8%D0%B8) запись логов в него.

## Как добавить телеметрию в платформу?

[Здесь](https://pyrevitlabs.notion.site/Telemetry-System-992d72659457447f86b79cf1c9034541) вы найдёте подробную инструкцию по настройке телеметрии в pyRevit.
Вы можете развернуть свой сервис телеметрии, используя репозиторий [Bim4EveryoneTelemetry](https://github.com/Bim4Everyone/Bim4EveryoneTelemetry).
Настройки телеметрии можно задать прямо в [установщике платформы](https://github.com/Bim4Everyone/Bim4EveryoneSetup?tab=readme-ov-file#c%D0%B2%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%B0-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BA-%D1%82%D0%B5%D0%BB%D0%B5%D0%BC%D0%B5%D1%82%D1%80%D0%B8%D0%B8) при его сборке, или указать через [pyRevit CLI](https://pyrevitlabs.notion.site/Configure-pyRevit-07446b4e07b7429091c89f472ef39136).


## Как зарепортить баг в платформе?

Если у вас возникла ошибка в pyRevit, то создайте issue в репозитории [pyRevit](https://github.com/pyrevitlabs/pyRevit/issues/new/choose).
Если у вас возникла ошибка при установке платформы, то вы также можете создать issue в репозитории [Bim4EveryoneSetup](https://github.com/Bim4Everyone/Bim4EveryoneSetup/issues/new), или можете написать в нашу [группу](https://t.me/bim4everyone_group) в telegram.
Если у вас возникла ошибка при использовании какого-то определенного плагина, то аналогично вы можете написать в ту же группу в telegram или создать issue в репозитории соответствующей вкладки:
  - [2D](https://github.com/Bim4Everyone/2DExtensions/issues/new)
  - [BIM](https://github.com/Bim4Everyone/BIMExtensions/issues/new)
  - [АР](https://github.com/Bim4Everyone/ARExtensions/issues/new)
  - [КР](https://github.com/Bim4Everyone/KRExtensions/issues/new)
  - [ОВиВК](https://github.com/Bim4Everyone/HVACExtension/issues/new)

## Можно ли запустить платформу на старых версиях Revit?

На данный момент платформа поддерживается для 2022, 2023, 2024 версий Revit.
Поддержка более старых версий не осуществляется.
Если необходимо, можно при помощи [pyRevit CLI](https://pyrevitlabs.notion.site/Attach-pyRevit-to-Installed-Revits-abf190044ffc4ac29671152ec9b91335) включить pyRevit на других версиях Revit, но стабильная работа платформы на них не гарантируется.
