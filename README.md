# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил:
- Поляков Александр Дмитриевич
- РИ-230913
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | ? |
| Задание 2 | * | ? |
| Задание 3 | * | ? |

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
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Научиться передавать в Unity данные из Google Sheets с помощью Python. Также научиться анализировать игровые переменные, описывать их изменение и поведение

## Задание 1
### Выберите одну из игровых переменных в игре СПАСТИ РТФ: Выживание (HP, SP, игровая валюта, здоровье и т.д.), опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.
Ход работы:
- Я выбрал переменную игровая валюта(R), ее роль в игре, закдючается в том, что за неё ты можешь улучшить своё оружие, для более простого прохождения.
  Изменение переменной:
  - если игрок убивает монстра, он получает игровую валюту.
  - если игрок покупает оружие в магазине, он её тратит.
  - если игрок во время прокачки выбрал соотвествующие навыки, то они восполняют здоровье.
  - если игрок выполняет одно из действий в игре, он получает дополнительные монеты(просмотр рекламы, оценка игры)
  Диапазон допустимых значений переменной прост, от 0 и до лимита, выстановленного разработчиками.
- Схема экономической модели ресурса:
![image](https://github.com/user-attachments/assets/770c3d8c-fb52-493e-bb86-51aba17c17b4)

## Задание 2
### ### С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в игре “СПАСТИ РТФ:Выживание”. Средствами google-sheets визуализируйте данные в google-таблице (постройте график / диаграмму и пр.) для наглядного представления выбранной игровой величины. Опишите характер изменения этой величины, опишите недостатки в реализации этой величины (например, в игре может произойти условие наступления эксплойта) и предложите до 3-х вариантов модификации условий работы с переменной, чтобы сделать игровой опыт лучше.
Ход работы:
- Для начала нужно определить как меняется выбранная мной игровая переменная:
Игровая валюта меняется в зависимсоти от убийств, это значит, что изменение этой переменной зависит от убийств монстров и его навыков. Я взял ситуцию, начальную, когда за каждое убйиство ты получаешь одну единицу игровой палюты.
-При помощи средств google-sheets я визуализировал данные в гугл таблице:
![image](https://github.com/user-attachments/assets/6e92845c-2422-4b9f-8dbf-6b24bfde1e8f)
Ссылка на таблицу: https://docs.google.com/spreadsheets/d/17c4pK7DmtMQ2w6cYD1antnonJNe-8mHy6X5Lq2FVcac/edit?gid=0#gid=0
```Python
import gspread
import numpy as np
gc = gspread.service_account(filename='unitydatascience-454511-04e86acaa808.json')
sh = gc.open('Lab2Unity')
coins = 0
i = 1
while i < 4:
    sh.sheet1.update_acell('A' + str(i), str(i))
    if i==1:
      coins+=6       
    else: coins += 1
    sh.sheet1.update_acell('B' + str(i), str(coins)) 
    i += 1
```
О проблемах связанных с начислением игровой валюты:
-Непонятно начисление после первого убийства, из 10 игры в первых 6 начислялось по 40 монет, в дальнейших по 6, то есть решением было бы, написанная легенда о правилах начисления монет.
-Также не сбалансированное начисление, за каждое убийство ты получаешь 1 монету, чтобы накопить на самое дешевое оружие в магазине надо сделать 600 убийств, что я считаю очень сложным к достижению, тут два варианта, либо изменение цен в магазине, либо увелечение начисление за каждое убийство, также как вариант можно рассмотреть получения моент за выполнение как либо достижений, то есть например: сделал 5 хедшотов подряд получил 50 монет.


## Задание 3
### Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.
Ход работы:
- Для реализации данного задания я выделил правильно по которым описывается динамика изменения здоровья:
    - Если игровой валюты хвататает на покупку, самого дорого оружия в магазине(coins = 10 000), то воспроизводится звук "хорошо"
    - Если игровой валюты хвататает на покупку, самого дешевого оружия в магазине(coins = 600), то воспроизводится звук "средне"
    - Если игровой валюты не хвататает на покупку, патронов в магазине (coins < 5), то воспроизводится звук "плохо"
- Для отображения этой динамики в Unity я создал компонент с таким скриптом (Это скрипт из методички, с небольшими изменениями):
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string,float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if (dataSet.Count == 0) return ;

        if (dataSet["Mon_" + i.ToString()] == 10000  & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] == 600 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] < 5 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1zveTVn6nZdWTtuBqLlO_PmKmV9gEts89cSWNd-XlWFY/values/Лист1?key=AIzaSyAY025NahCQGwDFeFa7uJYgIBuRut70nVs");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[2]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```
- Как видно на изображении ниже, скрипт работает без проблем
![image](https://github.com/user-attachments/assets/dac14018-e79c-4f2d-85db-deee40536259)

## Выводы

В ходе работы я научился ананлизировать ресурсы определенной игре, визуализировать изменения и поведения этого ресурса, с помощью соотвествующих схем и ПО

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
