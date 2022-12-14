# Создание индивидуальной системы достижения пользователя и ее интеграция в пользовательский интерфейс
Отчет по лабораторной работе #5 выполнила:
- Россихина Ирина Александровна
- РИ-300002

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
  - Часть 1 - Интеграции авторизации с помощью Яндекс SDK.
  - Часть 2 - Сохранение данных пользователя на платформе Яндекс Игры.
  - Часть 3 - Сбор данных об игроке и вывод их в интерфейсе.
  - Часть 4 - Интеграция таблицы лидеров.
  - Часть 5 - Интеграция системы достижений в проект.
- Задание 2.
- Задание 3.
- Выводы.

## Цель работы
Cоздание интерактивного приложения с рейтинговой системой пользователя и интеграция игровых сервисов в готовое приложение.

## Задание 1
### Используя видео-материалы практических работ 1-5 повторить реализацию приведенного ниже функционала:
#### Часть 1 - Интеграции авторизации с помощью Яндекс SDK.
Ход работы:
1. Проверить, что на сцене _0Scene установлен объект YandexGame.
2. Создать скрипт CheckConnectYG, который проверяет наличие Яндекс SDK и авторизацию пользователя.

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using YG;

public class CheckConnectYG : MonoBehaviour
{
    private void OnEnable() => YandexGame.GetDataEvent += CheckSDK;
    private void OnDisable() => YandexGame.GetDataEvent -= CheckSDK;
    
    void Start()
    {
        if (YandexGame.SDKEnabled == true)
        {
            CheckSDK();
        }
    }

    public void CheckSDK()
    {
        if (YandexGame.auth == true)
        {
            Debug.Log("User authorization is successful");
        }
        else
        {
            Debug.Log("User authorization is failed");
            YandexGame.AuthDialog();
        }
    }
}
```
3. Создать пустой объект YandexManager, к которому будут прикреплены все скрипты, связанные с Яндекс SDK. Прикрепить к объекту скрипт CheckConnectYG.
4. Собрать проект. Проверить, что подключен плагин Яндекс SDK и Publishing Settings: Compression Format is Disabled.
5. Заархивировать проект в формате .zip и загрузить на Яндекс.Игры. Включить свойство "Игра поддерживает авторизацию или лидерборд".
6. F12 - проверить в консоли авторизацию.
7. Проверить два сценария: пользователь авторизован и пользователь не авторизован



#### Часть 2 - Сохранение данных пользователя на платформе Яндекс Игры.
Ход работы:
1. Модифицировать скрипт SavesYG, который лежит в Assets - YandexGame - WorkingData. После модификации выглядит так

```c#
namespace YG
{
    [System.Serializable]
    public class SavesYG
    {
        public bool isFirstSession = true;
        public string language = "ru";
        public int score;
    }
}
```

2. Зайти в папку Assets - YandexGame - Example - ExampleScripts и удалить файл SaverTest.
3. Модифицировать скрипт DragonPicker. Добавить библиотеку YG. Создать события

```c#
private void OnEnable() => YandexGame.GetDataEvent += GetLoadSave;
private void OnDisable() => YandexGame.GetDataEvent -= GetLoadSave;
```

Добавить метод GetLoadSave.

```c#
public void GetLoadSave()
{
    Debug.Log(YandexGame.savesData.score);
}
```

Добавить метод UserSave()

```c#
public void UserSave(int currentScore)
{
    YandexGame.savesData.score = currentScore;
}
```

Добавить код в метод Start

```c#
if (YandexGame.SDKEnabled == true)
{
    GetLoadSave();
}
```

Добавить вызов метода UserSave при количестве щитов, равном нулю.

4.

#### Часть 3 - Сбор данных об игроке и вывод их в интерфейсе.
Ход работы:



#### Часть 4 - Интеграция таблицы лидеров.
Ход работы:



#### Часть 5 - Интеграция системы достижений в проект.
Ход работы:


## Задание 2
### Описать не менее трех дополнительных функций Яндекс SDK, которые могут быть интегрированы в игру.
Ход работы:

## Задание 3
### Доработать стилистическое оформление списка лидеров и системы достижений, реализованных в задании 1.
Ход работы:


 
## Выводы
В ходе лабораторной работы была продолжена разработка игры Dragon Picker. Была создана стартовая сцена с главным меню. Также появилась возможность поставить игру на паузу и выйти из игры в главное меню. Добавлены фоновая музыка и звуковые эффекты, которые можно изменить в главном меню. В приложение был включён персонаж. Большинство этих модификаций было сделано для более объёмного восприятия игры.


## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
