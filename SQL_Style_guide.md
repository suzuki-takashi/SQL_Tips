ＳＱＬスタイルガイド
======================

## Overview  
本スタイルガイドはＳＱＬ開発者向けのスタイルガイドです。


## Table of contents
#### [・命名規約](#命名規約-1)
#### [・フォーマット規約](#フォーマット規約-1)  
#### [　　ＳＥＬＥＣＴ](#ＳＥＬＥＣＴ-1)  
#### [　　ＩＮＳＥＲＴ](#ＩＮＳＥＲＴ-1)  
#### [　　ＵＰＤＡＴＥ](#ＵＰＤＡＴＥ-1)  
#### [　　ＤＥＬＥＴＥ](#ＤＥＬＥＴＥ-1)  
#### [　　ＣＲＥＡＴＥ](#ＣＲＥＡＴＥ-1)  

## 命名規約
・名前には英字、数字、アンダースコアのみを使用する。  
・名前はアンダースコアでは終わらない。  
　　理由：見づらいため。  
　　　例：COLUMN1_　　←←←アンダースコア付けています。  
・複数の連続したアンダースコアの使用を避ける。読取るのが難しくなるため。  
　　理由：見づらいため。  
　　　例：COLUMN__01　←←←アンダースコア２つ付けています。   
・名前にスペースを含めるのが自然な場合は、アンダースコアを使用する。  
　　　例：first nameはfirst_name  



## フォーマット規約
・タブを使わず、スペースを使う。  
・インデントは2スペース（4スペースでも良い）  
・予約語も含めて原則小文字で書く。  
　　理由：大文字か小文字かで迷ったりレビューで指摘するのがムダに思えるためです。  
・項目名を並べるときは、カンマを先頭にする。  
　　理由：カンマを項目の後にすると、仮に項目を１行追加するとき、１行変更して１行追加となってしまうため。  
・文末のセミコロンは改行して書く。  
　　理由：カンマと同じ理由。  
・コメントは--（ハイフンハイフン）で書く。/* （スラッシュアスタリスク）は使わない。  
　　理由：grep検索したときにコメント行かどうかがすぐわかるため。  

#### ＳＥＬＥＣＴ
・SELECTは全体がごく短い場合は１行で書いても良い。  
　　　例：select A from B where A='1'  
・全列ワイルドカード * （アスタリスク）の使用はせず、カラム名を明記する。  
・別名を定義するときはASをつける。  
　　　例：COLUMN1 AS 列名  
・FROMには複数のテーブル名を並べない。JOINを使う。  
　　悪い例：from TABLE01,TABLE02  
　　良い例：from TABLE01  
　　　　　　inner join TABLE02  
・INNER JOINを先に記述し、その後にLEFT JOINを記述する。RIGHT JOINは使わない。  
　　理由：機能的な意味は無く、制限が強いものから順番に書いた方がわかり易いと思うため。  
・EXISTS句は１を使う。  
　　　例：exists (select 1 from TABLE04 ・・・  
・ORDER BY句、GROUP BY句は数字ではなくカラム名を使う  
　　悪い例：order by 1 , 2  
　　良い例：order by COLUMN1,COLUMN2  


    select
       COLUMN1
      ,COLUMN2
      ,COLUMN3
      ,sum(COLUMN4) as SUM_D
    from
      TABLE01 as TB1
      inner join TABLE02 as TB2
        on  TB1.COLUMN1 = TB2.COLUMN1
        and TB1.COLUMN2 = TB2.COLUMN2
        and '1'         = TB2.COLUMN3
      left join TABLE03 as TB3
        on  TB1.COLUMN1 = TB3.COLUMN1
        and TB1.COLUMN2 = TB3.COLUMN2
    where
          TB1.COLUMN4 = 'A'
      and TB1.COLUMN5 = 'B'
      and exists (select 1
                  from 
                    TABLE04 as TB4
                  where
                        TB1.COLUMN1 = TB4.COLUMN1
                    and '1'         = TB4.COLUMN2)
    group by
       COLUMN1
      ,COLUMN2 
      ,COLUMN3
    order by
       COLUMN1
      ,COLUMN2
      ,COLUMN3
    ;


#### ＩＮＳＥＲＴ
    insert into
      TABLE01
    (
     COLUMN1
    ,COLUMN2
    ,COLUMN3
    )
    values
    (
     VALUE1
    ,VALUE2
    ,VALUE3
    )
    ;


#### ＵＰＤＡＴＥ 
    UPDATE
      TABLE01 AS TB1
    SET
       TB1.COLUMN3 = 100
      ,TB1.COLUMN4 = 100
    WHERE
          TB1.COLUMN1 = 10
      and TB1.COLUMN2 = 20
    ;


#### ＤＥＬＥＴＥ
    DELETE
    FROM
      TABLE01 AS TB1
    WHERE
          TB1.COLUMN1 = 1
      and TB1.COLUMN2 = 2
    ;


#### ＣＲＥＡＴＥ
・できるだけベンダー固有のデータ型は使用しないようにする。  
　　理由：これからシステムの保守をする人が、必ずしもそのＤＢに詳しいとは限らないため。    
・数値型はNUMERICとDECIMAL型が望ましい。  
　　理由：浮動小数点は誤差に気をつける必要があるため。  


Note
-------

References
-------


Contributing
-------
Pull requests are welcome!!  
Or If you find issues, please send it!!

Authors
----------
Copyright &copy; [IT & Strategy](http://suzukitakashi.net/)  
  
License
----------
Distributed under the [MIT License][mit].
 
[MIT]: http://www.opensource.org/licenses/mit-license.php


