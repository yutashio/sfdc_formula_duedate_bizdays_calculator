# 【数式】期日までの営業日ベースの残り日数計算  

## 概要
期日 (DueDate__c) に設定された日付までの残り営業日（土日を除く平日の日数）を計算する。  

## 数式
```
IF(
    DueDate__c < TODAY(),
    "期日超過",
    TEXT(
        DueDate__c - TODAY() - 
        FLOOR((DueDate__c - TODAY() + WEEKDAY(TODAY()) - 1) / 7) * 2 - 
        IF(MOD(WEEKDAY(TODAY()) + DueDate__c - TODAY() - 1, 7) = 6, 1, 0) - 
        IF(MOD(WEEKDAY(TODAY()) + DueDate__c - TODAY() - 1, 7) = 0, 1, 0)
    )
)
```