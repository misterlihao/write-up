####題目內容
一個購物系統，功能有add delete checkout cart

####資料結構
```
item {
  price, name, next, prev
}
```
.bss有一個item，作為購物車mycart(double linked list)，mycart.next指向購買的第一個物品。

####漏洞
在金額7174的時候呼叫checkout，會新增一個物件(iphone8)到購物車尾端。
此物件並非使用malloc得來的空間，而是直接使用區域變數，
所以原本最後一個物件的next會指向stack上。
這就導致我們可以用delete修改stack內容。

####解法
delete會對next prev指向的位置做寫入(heap unlink弱點)。
```
item->next->prev = item->prev;
item->prev->next = item->next;
```
因為delete的輸入buffer有覆蓋到iphone8的next&prev，
我們可以直接調用delete(iphone8)來完成隨機寫入。

因為unlink的特性，若想直接把system@libc寫到ret address，system@lib附近的code也會被寫到，
所以只能修改

####心得
