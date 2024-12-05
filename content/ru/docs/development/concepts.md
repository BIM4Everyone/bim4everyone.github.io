---
date: :git
draft: false

params:
  author: dosymep
  
title: Концепт
linkTitle: Концепт
description: |
  Обзор ключевых идей и архитектуры платформы для эффективного создания и интеграции приложений.

tags: [test, docs]
categories: [Examples, Placeholders]

weight: 20
---

## Введение
В платформе реализован подход с хранением параметров, которые используются в плагинах постоянно.
Это позволяет:
- быстро копировать параметры в проект при запуске скриптов;
- централизованно редактировать наименование параметров;
- выявлять проблемы при работе с параметрами (например, при несовпадении StorageType или при отсутствии параметров в проекте)
- предоставлять базовый функционал по работе с параметрами разработчикам плагинов с уже встроенными проверками.


## Структура классов:
Классы, отвечающие за работу с параметрами платформы имеют следующую структуру наследования:
- RevitParam:
  - ProjectParam
  - SystemParam
  - SharedParam
- RevitParamConfig:
  - ProjectParamConfig
  - SystemParamConfig
  - SharedParamConfig

### RevitParam
RevitParam - абстрактный класс обладающий базовым функционалом по работе с параметрами Revit.
Содержит ряд виртуальных свойств и методов, которые переопределяются в классах-наследниках:
  - ProjectParam - класс параметров проекта Revit
  - SystemParam - класс системного параметра
  - SharedParam - класс общего параметра 

Класс RevitParam имеет следующие публичные методы, которые переопределяются в дальнейшем в классах-наследниках:
1. IsExistsParam - проверяет наличие параметра в проекте или на элементе;
2. GetParamBinding - возвращает настройки привязки параметра
3. GetRevitParamElement - возвращает элемент, хранящий определенный пользователем параметр.
4. GetParam - возвращает параметр элемента (Autodesk.Revit.DB.Parameter)
5. IsRevitParam - проверяет является ли определение параметра параметром проекта.

А также свойства:
1. Id - идентификатор параметра.
2. Name - наименование параметра.
3. Description - описание параметра.
4. StorageType - тип хранения параметра
5. UnitType - тип измерения параметра.
6. UnitTypeName - наименование свойства типа измерения параметра.


>Revit поддерживает как встроенные, так и определяемые пользователем параметры. 
>Встроенные параметры поставляются с приложением и не хранятся в документах Revit. 
>Определяемые пользователем параметры создаются динамически и хранятся в документах, которые их используют, 
>упакованные в объекты ParameterElement. Различные подклассы ParameterElement представляют различные виды 
>определяемых пользователем параметров.


#### ProjectParam
Класс переопределяет виртуальные методы RevitParam и добавляет методы:
1. GetUnitType - Возвращает единицу измерения параметра по его идентификатору.

#### SystemParam
Класс переопределяет виртуальные методы RevitParam и добавляет методы:
1. GetSystemParamId - возвращает идентификатор встроенного параметра (BuiltInParameter)

И свойства:
1. SystemParamId - Системное наименование параметра.
2. LanguageType - Язык системного параметра

#### SharedParam
Класс переопределяет виртуальные методы RevitParam и добавляет методы:
1. GetExternalDefinition - Возвращает описание общего параметра из ФОП.
2. GetUnitType - Возвращает единицу измерения параметра по его идентификатору.

И свойства:
1. Guid - Guid общего параметра.



<table>
    <tr>
        <td>Свойства</td>
        <td>Методы</td>
    </tr><tr>
        <td colspan="2" width="500">class RevitParam</td>
    </tr>
    <tr>
        <td>
            <a href="#id">Id</a><br>
            <a href="#name">Name</a><br>
            <a href="#description">Description</a><br>
            <a href="#storagetype">StorageType</a><br>
            <a href="#unittype">UnitType</a><br>
            <a href="#unittypename">UnitTypeName</a>
        </td>
        <td>
            <a href="#isexistsparam">IsExistsParam</a><br>
            <a href="#getparambinding">GetParamBinding</a><br>
            <a href="#getrevitparamelement">GetRevitParamElement</a><br>
            <a href="#getparam">GetParam</a><br>
            <a href="#isrevitparam">IsRevitParam</a>
        </td>
    </tr>
    <tr>
        <td colspan="2">class ProjectParam : RevitParam</td>
    </tr>
    <tr>
        <td>
        </td>
        <td>
            <a href="#getunittype">GetUnitType</a>
        </td>
    </tr>
    <tr>
        <td colspan="2">class SystemParam : RevitParam</td>
    </tr>
    <tr>
        <td>
            <a href="#systemparamid">SystemParamId</a><br>
            <a href="#languagetype">LanguageType</a>
        </td>
        <td>
            <a href="#getsystemparamid">GetSystemParamId</a>
        </td>
    </tr>
    <tr>
        <td colspan="2">class SharedParam : RevitParam</td>
    </tr>
    <tr>
        <td>
            <a href="#guid">Guid</a>
        </td>
        <td>
            <a href="#getexternaldefinition">GetExternalDefinition</a><br>
            <a href="#getunittype">GetUnitType</a>
        </td>
    </tr>
</table>


#### Получение 
Если в скрипте платформы используется общий параметр или параметр проекта, то его надо вызывать через поле 
класса SharedParamsConfig.Instance или ProjectParamsConfig.Instance платформы. Правило используется для утвержденной технологии.




##### Свойства классов
Ниже представлены свойства, которые можно встретить в классе RevitParam и в классах-наследниках:
1. <span id="id">Id</span> - идентификатор параметра.
2. <span id="name">Name</span> - наименование параметра.
3. <span id="вescription">Description</span> - описание параметра.
4. <span id="storagetype">StorageType</span> - тип хранения параметра.
5. <span id="unittype">UnitType</span> - тип измерения параметра.
6. <span id="unittypename">UnitTypeName</span> - наименование свойства типа измерения параметра.
7. <span id="systemparamid">SystemParamId</span> - Системное наименование параметра. 
8. <span id="languagetype">LanguageType</span> - Язык системного параметра
9. <span id="guid">Guid</span> - Guid общего параметра.

##### Методы классов
Ниже представлены методы, которые можно встретить в классе RevitParam и в классах-наследниках:
1. <span id="isexistsparam">IsExistsParam</span> - проверяет наличие параметра в проекте или на элементе;
2. <span id="getparambinding">GetParamBinding</span> - возвращает настройки привязки параметра
3. <span id="getrevitparamelement">GetRevitParamElement</span> - возвращает элемент, хранящий определенный пользователем параметр.
4. <span id="getparam">GetParam</span> - возвращает параметр элемента (Autodesk.Revit.DB.Parameter)
5. <span id="isrevitparam">IsRevitParam</span> - проверяет является ли определение параметра параметром проекта.
6. <span id="getunittype">GetUnitType</span> - Возвращает единицу измерения параметра по его идентификатору.
7. <span id="getsystemparamid">GetSystemParamId</span> - возвращает идентификатор встроенного параметра (BuiltInParameter)
8. <span id="getexternaldefinition">GetExternalDefinition</span> - Возвращает описание общего параметра из ФОП.
9. <span id="getunittype">GetUnitType</span> - Возвращает единицу измерения параметра по его идентификатору.





