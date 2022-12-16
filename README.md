# Лабораторная работа № 6 Интеграция рекламных сервисов в интерактивное приложение.
Отчет по лабораторной работе #6 выполнил(а):
- Данькин Сергей Викторович
- РИ-300016

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[Проект Dragon Picker](https://github.com/S1GARETA/Dragon_Picker)

[Шаблон на Яндекс Игры](https://yandex.ru/games/app/197772?draft=true&lang=ru)

## Цель работы

#### Создание интерактивного приложения с рейтинговой системой пользователя и интеграция игровых сервисов в готовое приложение.

## Задание 1

#### Используя видео-материалы практических работ 1-5 повторить реализацию приведенного ниже функционала:

1. Интеграция баннерной рекламы.
2. Интеграция видеорекламы.
3. Показ видеорекламы пользователю за вознаграждение.
4. Создание внутриигрового магазина.
5. Система антиблокировки рекламы.

## Ход работы

##### 1. Интеграция баннерной рекламы.

- Регистрируемся на Яндекс РСЯ.
- Создаём RTB-блок, для подключения рекламы.

![img](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.1.png)

- Копируем ID рекламного блока и всталяем в настройки билда.

![img](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.2.png)

- Собираем билд и проверяем в черновике.

![img](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.3.png)

##### 2. Интеграция видеорекламы.

- Добавляем строчку кода в скрипты [DragonPicker](https://github.com/S1GARETA/Dragon_Picker/blob/main/DragonPicker/Assets/_Scripts/DragonPicker.cs) и [CheckConnectYG](https://github.com/S1GARETA/Dragon_Picker/blob/main/DragonPicker/Assets/_Scripts/CheckConnectYG.cs), чтобы появлялась видео реклама.

```cs
YandexGame.RewVideoShow(0);
```

- Так же, включаем полную паузу при показе рекламы.

![img](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.4.png)

##### 3. Показ видеорекламы пользователю за вознаграждение.

- Создаем скрипт [ADRewerd](https://github.com/S1GARETA/Dragon_Picker/blob/main/DragonPicker/Assets/_Scripts/ADReward.cs) и подключаем его к объекту YandexManager.

```cs
using UnityEngine;
using YG;

public class ADReward : MonoBehaviour
{
    private void OnEnable() => YandexGame.CloseVideoEvent += Rewarded;
    private void OnDisable() => YandexGame.CloseVideoEvent -= Rewarded;
    void Rewarded(int id) 
    {
        if(id==1)
        {
            Debug.Log("Пользователь получил награду");
        }
        else
        {
            Debug.Log("Пользователь остался без награды");
        }
    }

    public void OpenAD()
    {
        YandexGame.RewVideoShow(Random.Range(0, 2));
    }

}
```

- Добавляем кнопку в главном меню, с помощью которой будет вызываться метод OpenAD

![gif](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.1.gif)

##### 4. Создание внутриигрового магазина.

- Создаем предмет покупки в Яндекс Консоль

![img](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.5.png)

- Перетаскиваем в главное меню префаб OnePurchase и передаем в него id предмета покупки

![gif](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.2.gif)

##### 5. Система антиблокировки рекламы.

- Включаем антиблокировку рекламы

![img](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.6.png)

## Задание 2

#### Добавить в приложение интерфейс для вывода статуса наличия игрока в сети (онлайн или офлайн).

### Ход работы:

- Добавить в главном меню текст, в котором будет выводится статус наличия игрока

![img](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.7.png)

- Дописать в скрипте [CheckConnectYG](https://github.com/S1GARETA/Dragon_Picker/blob/main/DragonPicker/Assets/_Scripts/CheckConnectYG.cs) в методе CheckSDK изменение текста.

```cs
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
            userStatus.text = "Online"; // Изменение текста статуса
            Debug.Log("User authorization ok");
        }
        else
        {
            Debug.Log("User not authorization");
            YandexGame.AuthDialog();
        }
    }
```

![gif](https://github.com/S1GARETA/UnityLab6/blob/main/Demo%20files/1.3.gif)

## Выводы

В ходе лаборатной работы были изучены разные способы интеграции рекламы. Также изучено создание внутриигрового магазина и, то как можно обходить антиблокировочные системы, чтобы пользователю всё же показывалась реклама.
