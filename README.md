[![license](https://img.shields.io/github/license/karashinasou/json-formatter.svg?style=flat-square)](https://github.com/karashinasou/json-formatter/blob/master/LICENSE)
[![release](https://img.shields.io/github/release/karashinasou/json-formatter.svg?style=flat-square)](https://github.com/karashinasou/json-formatter/releases)
[![GitHub](https://img.shields.io/github/followers/karashinasou.svg?label=@karashinasou&style=social)](https://github.com/karashinasou)

# json-formatter

## Description

json-formatterはJSONのフォーマットクラスです

## Install

[releases](https://github.com/tomoriaki/json-formatter/releases)からjson-formatter.unitypackageをダウンロードしてプロジェクトにインポートしてください

## Example

```csharp
using UnityEngine;
using System;
using System.IO;
using HC.Common;


public class Example : MonoBehaviour
{
    #region イベントメソッド

    private void Start()
    {
        string json = ReadText("JsonFormatter/Demo/example.json");

        json = JsonFormatter.ToMinifyPrint(json);
        Debug.Log("MinifyPrint: " + Environment.NewLine + json);

        json = JsonFormatter.ToPrettyPrint(json, JsonFormatter.IndentType.Space);
        Debug.Log("PrettyPrint: " + Environment.NewLine + json);
    }

    #endregion


    #region メソッド

    /// <summary>
    /// テキストをファイルから読み込む
    /// </summary>
    /// <param name="path">Application.dataPath以降のファイルパス</param>
    /// <returns>読み込んだテキスト</returns>
    public static string ReadText(string path)
    {
        string text = string.Empty;

        try
        {
            using (var streamReader = new StreamReader(Path.Combine(Application.dataPath, path)))
            {
                text = streamReader.ReadToEnd();
                streamReader.Close();
            }
        }
        catch (Exception e)
        {
            Debug.LogAssertion(e.Message);
        }

        return text;
    }

    #endregion
}
```

```json
MinifyPrint: 
{"characters":[{"id":1,"name":"武闘家","EquipWeaponTypes":["片手剣","両手剣","槍","斧"],"hp":140,"mp":40,"power":80,"intelligence":20,"agility":14.0},{"id":2,"name":"遊び人","EquipWeaponTypes":[],"hp":60,"mp":0,"power":20,"intelligence":80,"agility":8.0}]}
```

```json
PrettyPrint: 
{
    "characters": [
        {
            "id": 1,
            "name": "武闘家",
            "EquipWeaponTypes": [
                "片手剣",
                "両手剣",
                "槍",
                "斧"
            ],
            "hp": 140,
            "mp": 40,
            "power": 80,
            "intelligence": 20,
            "agility": 14.0
        },
        {
            "id": 2,
            "name": "遊び人",
            "EquipWeaponTypes": [],
            "hp": 60,
            "mp": 0,
            "power": 20,
            "intelligence": 80,
            "agility": 8.0
        }
    ]
}
```
