SQL Tips
======================

## Overview  
実際の開発で使ったＳＱＬを基に作ったＴｉｐｓ集です。  

## SampleDB
[environment]にあるSQLを使ってSampleDBを作ると、動作確認できます。

[environment]: https://github.com/suzuki-takashi/SQL_Tips/tree/master/environment

## Table of contents

#### [・LEFT JOINの使い方](#left-joinの使い方-1)
#### [・ランダムに行を取得する](#ランダムに行を取得する-1)

## Tips

#### LEFT JOINの使い方
    [良い例]
    SELECT A.NRJYUTYU,A.NRHINMOKU,B.TXHINBAN,B.TXHINMEI,A.QTJYUTYU
    FROM
      JTMS A
    LEFT JOIN HINMOKU B
      ON A.NRHINMOKU = B.NRHINMOKU
      AND 300 >= B.PRHANBAI --この条件は結合条件です
    
    [悪い例]
    SELECT A.NRJYUTYU,A.NRHINMOKU,B.TXHINBAN,B.TXHINMEI,A.QTJYUTYU
    FROM
      JTMS A
    LEFT JOIN HINMOKU B
      ON A.NRHINMOKU = B.NRHINMOKU
    WHERE
      300 >= B.PRHANBAI --結合条件を抽出条件に書いてはいけない

#### ランダムに行を取得する
    SELECT A.*
    FROM
      jtmd AS A
    INNER JOIN (
        SELECT  ROW_NUMBER() OVER (ORDER BY NRJYUTYU ) AS ROWNUM 
	           ,NRJYUTYU
        FROM
          jtmd
	    ) AS B
      ON A.NRJYUTYU = B.NRJYUTYU
      AND B.ROWNUM = (SELECT CEIL(RANDOM() * COUNT(NRJYUTYU)) FROM jtmd )



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
