SQL Tips
======================

## Overview  
実際の開発で使ったＳＱＬを基に作ったＴｉｐｓ集です。  

## Table of contents

#### [・LEFT JOINの使い方](#LEFTJOINの使い方)

## Tips

#### LEFTJOINの使い方
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


 
Note
-------


Authors
----------
Copyright &copy; [IT & Strategy](http://suzukitakashi.net/)  
  
License
----------
Distributed under the [MIT License][mit].
 
[MIT]: http://www.opensource.org/licenses/mit-license.php
