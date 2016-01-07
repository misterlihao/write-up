###問題
題目就是一個zip檔案，解開來會發現很多.py、還有一個.pyc

###解題過程
打開.py看一看覺得很冗長，於是就先對pyc做了[decompile](https://github.com/wibiti/uncompyle2)
沒想到吐出一個神奇的[Url](http://kchung.co/lol.py)
，連上去就可以看到flag隱藏在註解裡面了
