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
- централизованно редактировать параметры для всех плагинов в случае их изменения;
- выявлять проблемы при работе с параметрами (например, при несовпадении StorageType или при отсутствии параметров в проекте)
- предоставлять базовый функционал по работе с параметрами разработчикам плагинов с уже встроенными проверками.

Данный подход базируется на:
- ряде классов платформы, через которые производится копирование, настройка, хранение параметров в коде и т.п.
- файле Revit, который используется как шаблон-хранилище, из которого производится копирование параметров 
в целевые проекты для последующего использования плагинами.


## Структура классов платформы
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
Содержит ряд виртуальных свойств и методов, которые переопределяются в следующих классах-наследниках:
  - ProjectParam - класс параметра проекта Revit;
  - SystemParam - класс системного параметра Revit;
  - SharedParam - класс общего параметра Revit.

#### Методы и свойства RevitParam и классов-наследников
<table>
    <tr>
        <td>Свойства</td>
        <td>Методы</td>
    </tr><tr>
        <td colspan="2" width="600">class <b>RevitParam</b></td>
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
        <td colspan="2">class <b>ProjectParam</b> : RevitParam</td>
    </tr>
    <tr>
        <td>
        </td>
        <td>
            <a href="#getunittype">GetUnitType</a>
        </td>
    </tr>
    <tr>
        <td colspan="2">class <b>SystemParam</b> : RevitParam</td>
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
        <td colspan="2">class <b>SharedParam</b> : RevitParam</td>
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


>Revit поддерживает как встроенные, так и определяемые пользователем параметры. 
>Встроенные параметры поставляются с приложением и не хранятся в документах Revit. 
>Определяемые пользователем параметры создаются динамически и хранятся в документах, которые их используют, 
>упакованные в объекты ParameterElement. Различные подклассы ParameterElement представляют различные виды 
>определяемых пользователем параметров.


### RevitParamsConfig
RevitParamConfig - абстрактный класс по работе с конфигурациями параметров платформы. Через него реализуется:
1. ведения реестра параметров платформы конфигурации по умолчанию
2. использование параметров нестандартной конфигурации после ее загрузки из файла
3. добавление/изменение/копирование параметров в рамках одной конфигурации

>Конфигурация - набор параметров одного типа (проекта/общий/системный) для использования в плагинах платформы.

RevitParamConfig содержит ряд виртуальных свойств и методов, которые переопределяются в следующих классах-наследниках:
  - ProjectParamConfig - класс конфигурации параметров проекта Revit;
  - SystemParamConfig - класс конфигурации системных параметров Revit;
  - SharedParamConfig - класс конфигурации общих параметров Revit.

>В классах-наследниках RevitParamConfig прописаны параметры конфигурации по умолчанию, которые используются 
> в плагинах платформы, например:  
> 
>*public SharedParam **AlbumBlueprints** <span id="albumblueprints">AlbumBlueprints</span> =>  
>&nbsp;&nbsp;&nbsp;&nbsp;new **SharedParam**(nameof(AlbumBlueprints), new Guid("e1b06433-f527-403c-8986-af9a01e6be7f"))  
> &nbsp;&nbsp;&nbsp;&nbsp;{  
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Name = "ADSK_Комплект чертежей",  
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UnitType = SharedParam.GetUnitType(nameof(AlbumBlueprints)),  
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;StorageType = StorageType.String  
&nbsp;&nbsp;&nbsp;&nbsp;};*

#### Методы и свойства RevitParamsConfig и классов-наследников
<table>
    <tr>
        <td>Свойства</td>
        <td>Методы</td>
    </tr><tr>
        <td colspan="2" width="600">class <b>RevitParamsConfig</b></td>
    </tr>
    <tr>
        <td>
            <a href="#thisid">this[id]</a><br>
        </td>
        <td>
            <a href="#save">Save</a><br>
            <a href="#getrevitparams">GetRevitParams</a><br>
        </td>
    </tr>
    <tr>
        <td colspan="2">class <b>ProjectParamConfig/SystemParamConfig/SharedParamConfig</b> : RevitParamConfig</td>
    </tr>
    <tr>
        <td>
            <a href="#instance">Instance</a>
        </td>
        <td>
            <a href="#createrevitparam">CreateRevitParam</a><br>
            <a href="#loadinstance">LoadInstance</a><br>
            <a href="#getdefaultconfig">GetDefaultConfig</a>
        </td>
    </tr>
</table>


##### Свойства классов
Ниже представлены свойства, которые можно встретить в классе RevitParamConfig и в классах-наследниках:

1. <span id="thisid">this[id]</span> - возвращает параметр Revit по его имени (или идентификатору).
2. <span id="instance">Instance</span> - текущее состояние конфигурации, у которой можно запросить параметр

##### Методы классов
Ниже представлены методы, которые можно встретить в классе RevitParamConfig и в классах-наследниках:
1. <span id="save">Save</span> - сохраняет конфигурацию по заданному пути.
2. <span id="getrevitparams">GetRevitParams</span> - возвращает весь список настроек параметров.
3. <span id="createrevitparam">CreateRevitParam</span> - создает параметр проекта
4. <span id="loadinstance">LoadInstance</span> - загрузка конфигурации по указанному пути, либо если она не найдена, 
то загрузка конфигурации по умолчанию
5. <span id="getdefaultconfig">GetDefaultConfig</span> - возвращает конфигурацию по умолчанию


### Использование параметра платформы
Если параметр имеется в конфигурации по умолчанию (прописан в ProjectParamConfig, SystemParamConfig или SharedParamConfig), 
то его можно использовать при разработке плагина путем вызова свойства Instance. 
Например:

SharedParamsConfig.Instance.AlbumBlueprints - используем конфигурацию для общих параметров (SharedParamsConfig), 
поэтому запрос вернет экземпляр класса SharedParam, описывающий общий Revit-параметр, 
под названием "ADSK_Комплект чертежей" (<a href="#albumblueprints">см. выше</a>). 

В случае, если работа ведется не с конфигурацией по умолчанию, то получить параметр можно обратившись к экземпляру 
конфигурации и указав в квадратных скобках имя параметра (или идентификатор, в зависимости от типа параметра)
Например:
SharedParamsConfig["ADSK_Комплект чертежей"]


### Загрузка параметров в проект Revit
Для использования параметра плагином может потребоваться сначала загрузить параметр в проект. 
Этот процесс реализуется благодаря файлу Revit, используемому как шаблон, в котором хранятся параметры платформы.
Для копирования и настройки параметров в проекте Revit предназначен класс ProjectParameters.  
Методика копирования параметров в нужный проект:
1. На классе ProjectParameters вызвать метод Create и получить ProjectParameters приложения;
2. Вызвать на нем метод SetupRevitParam, чтобы скопировать один параметр в нужный проект;
3. Или вызвать SetupRevitParams, чтобы скопировать несколько параметров в нужный проект;
4. После этого платформа найдет указанный параметр в Revit-шаблоне, и произведет копирование в нужный Revit проект.

При этом механизм получения параметров работает следующим образом:
1. сначала производится синхронизация параметров, т.е. в случае если в целевом проекте указанный для добавления 
параметр уже присутствует, но в нем изменился список категорий, то нужные категории будут добавлены (сниматься галочки 
категорий, не будут);
2. далее если параметр не был найден в целевом проекте, то производится копирование нужного параметра.






## Файл-шаблон Revit
Файл-шаблон Revit используется платформой для хранения параметров, которые в дальнейшем через методы платформы 
можно скопировать в целевой проект, где будет запускаться плагин.

Файл располагается по пути:
%appdata%\pyRevit\Extensions\BIM4Everyone.lib\dosymep_libs\libs\<Revit version>\templates\project_parameters.rvt

Также файл-шаблон можно открыть при помощи кнопки "Открыть шаблон параметров" на вкладке Admin.
Через кнопку Параметры проекта на вкладке Управление можно увидеть перечень всех параметров, которые добавлены 
в платформу.



## Работа с параметрами
В платформе присутствует классы DocumentExtensions, ElementExtensions и т.п. благодаря которым есть возможность 
выполнять операции с параметрами у соответствующих типов.

### Получение значения параметра
**GetParamValue** - метод, который возвращает значение параметра элемента.
При использовании в формате:
- GetParamValue() вернет объект класса object (рекомендуется для использования при написании кода на Python);
- GetParamValue<string>() вернет объект класса string (или любой другой, какой будет указан; удобнее, когда известно 
какой тип содержится в параметре).
Пример:
string levelValue = element.GetParamValue<string>(SharedParamsConfig.Instance.Level)

При этом механика работы следующая:
1. Метод пытается получить значение параметра у элемента
2. Если параметра нет, или значение параметра null или пустая строка, то он выбрасывает исключение

**GetParamValueOrDefault** - метод, который возвращает значение параметра элемента, либо значение по умолчанию.
При использовании в формате:
- GetParamValueOrDefault() вернет объект класса object (рекомендуется для использования при написании кода на Python);
- GetParamValueOrDefault<string>() вернет объект класса string (или любой другой, какой будет указан; удобнее, 
когда известно какой тип содержится в параметре).
Пример:
string levelValue = element.GetParamValueOrDefault<string>(SharedParamsConfig.Instance.Level)

При этом механика работы следующая:
1. Метод пытается получить значение параметра у элемента
2. Если параметра нет, или значение параметра null или пустая строка, то он возвращает значение по умолчанию (с учетом 
типа, если он был передан).

При этом если в аргументах метода указано значение по умолчанию, то в случае возникновения проблем будет возвращено 
не стандартное значение по умолчанию, а то, которое было указано.
Пример:
string levelValue = element.GetParamValueOrDefault<string>(SharedParamsConfig.Instance.Level, "Произошла ошибка!")

Также в платформе присутствуют методы для работы со значениями параметров, в случае, когда параметры не принадлежат 
платформе - GetSharedParamValue (и аналоги) и GetProjectParamValue (и аналоги).

### Проверка наличия параметра
**IsExistsParam** - метод, который проверяет есть ли параметр у элемента. Возвращает true, если есть. При этом проверка
производится через ParameterBindings документа. 

Пример:
element.IsExistsParam(SharedParamsConfig.Instance.Level)

### Проверка наличия значения параметра
**IsExistsParamValue** - метод, который проверяет, содержит ли параметр элемента значение. Возвращает true, если содержит.
При этом проверка имеют следующую механику:
1. Проверяется, что у элемента есть параметр;
2. Проверяется, что HasValue параметра true;
3. Проверяется, что в значение параметра не равно null или пустой строке.

Пример:
element.IsExistsParamValue(SharedParamsConfig.Instance.Level)










