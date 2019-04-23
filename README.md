京东图书优惠券满减快速凑整

在JavaScript代码内修改促销的ID号后，在浏览器console内获取促销图书的价格列表。已考虑缺货货品。

最后如果凑整成功，会打印结果。

用法: **jd_book(PromoName, ExpectedSum, Tolerance)** , 比如 jd_book("product_promo_50008500387",600,3);

三个参数，PromoName是促销的ID,可以从网页查到，ExpectedSum是目标价格，Tolerance是可以容忍的偏差。


#javascript代码

```javascript
function jd_book(PromoName, ExpectedSum, Tolerance) {
  promo = document.getElementById(PromoName);
  list = promo.getElementsByClassName("plus-switch");
  stock = promo.getElementsByClassName("ftx-03 ac");
  NoStock = 0;
  for (var i = 0; i < list.length; i++) {
    if (stock[i].textContent == "无货") {
      NoStock++;
      continue;
    }
    price[i - NoStock] = parseFloat(list[i].textContent.match(/\d+\.\d+/g));
  }
  price.splice(0, list.length - NoStock);
  //console.log(price);
  isSuccess = 1;
  n = 1000000;

  pool = price;
  backup = new Array(list.length);
  backup.fill(0);

  sum = (accumulator, currentValue) => accumulator + currentValue;
  price.reduce(sum);


  while (isSuccess && n) {
    n--;
    t = pool.reduce(sum);
    t = Math.round(t * 100) / 100.00;
    if (t > ExpectedSum + Tolerance || t < ExpectedSum - Tolerance) {
      i = Math.floor(Math.random() * 18);
      temp1 = pool[i];
      temp2 = backup[i];
      pool[i] = temp2;
      backup[i] = temp1;
    } else
      isSuccess = 0;

  };

  stack_final = pool.filter(function(element) {
    return element > 0;
  });
  if (n == 0) {
    console.log("组合失败!\n");
  } else {
    console.log("总共" + stack_final.length + "本书：" + t + "元。\n");

    var str = "";
    for (var i = 0; i < stack_final.length - 1; i++) {
      str += stack_final[i] + "元|";
    }
    str += stack_final[i] + "元\n";
  }
  console.log(str);
}
```
