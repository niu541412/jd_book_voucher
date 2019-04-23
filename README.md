京东图书优惠券满减快速凑整

在JavaScript代码内修改促销的ID号后，在浏览器console内获取促销图书的价格列表。已考虑缺货货品。

最后如果凑整成功，会打印结果。

用法: **jd_book(PromoName, ExpectedSum, Tolerance)** , 比如 jd_book("product_promo_50008500387",600,3);

三个参数，PromoName是促销的ID,可以从网页查到，ExpectedSum是目标价格，Tolerance是可以容忍的偏差。


#javascript代码

```javascript
function jd_book(PromoName, ExpectedSum, Tolerance) {
  var promo = document.getElementById(PromoName);
  var list = promo.getElementsByClassName("plus-switch");
  var stock = promo.getElementsByClassName("ftx-03 ac");
  var NoStock = 0;
  var price = new Array(list.length);
  var book = new Array(list.length);
  for (var i = 0; i < list.length; i++) {
    if (stock[i].textContent == "无货") {
      NoStock++;
      continue;
    }
    price[i - NoStock] = parseFloat(list[i].textContent.match(/\d+\.\d+/g));
    book[i - NoStock] = promo.getElementsByClassName("p-name")[i].innerText;
  }
  price = price.splice(0, list.length - NoStock);
  book = book.splice(0, list.length - NoStock);
  var NotEND = 1;
  var n = 10*2**price.length;

  var pool = price;
  var backup = new Array(list.length);
  backup.fill(0);

  var sum = (accumulator, currentValue) => accumulator + currentValue; //数组求和
  price.reduce(sum);

  while (NotEND && n) {
    n--;
    var t = pool.reduce(sum);
    t = Math.round(t * 100) / 100.00;
    if (t > ExpectedSum + Tolerance || t < ExpectedSum - Tolerance) {
      i = Math.floor(Math.random() * price.length);
      var temp1 = pool[i];
      var temp2 = backup[i];
      pool[i] = temp2;
      backup[i] = temp1;
    } else{
      NotEND = 0;
    }
  };

  if (n == 0) {
    console.log("组合失败!\n");
  } else {
    var j=0;
    for (i = 0; i < pool.length; i++) {
      if (pool[i]>0){
        console.log(pool[i]+"元:"+book[i]);
        j++;
      }
    }
    console.log("总共" + j + "本书：" + t + "元。\n");
  }
}
```
