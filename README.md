京东图书优惠券满减快速凑整

在JavaScript代码内修改促销的ID号后，在浏览器console内获取促销图书的价格列表。
#javascript代码

```javascript
promo = document.getElementById("product_promo_50008500387");
list = promo.getElementsByClassName("plus-switch");
var price = new Array(list.length);
for (var i = 0; i < list.length; i++) {
  price[i] = parseFloat(list[i].textContent.match(/\d+\.\d+/g));
}
console.log(price);
```

以下实际是S-lang语言的代码，类C。
最后如果凑整成功，会打印结果。
两个参数sum_expect是目标价格,tolerance是可以容忍的偏差。
以后会改成JavaScript版本，方便运行。


```c
define jd_book(sum_expect,tolerance)
{
        isSuccess = 1;
        n = 100000;

        stack_1=[207, 33.8, 115.2, 58.7, 36.5, 62.8, 87.5, 45.6, 159.6, 40.5, 53.1, 98.7, 834.7, 142.8, 232.8, 52.2, 64.6, 46.6, 50.2, 171, 27.4, 261.6];
        stack_2 = Double_Type [length(stack_1)];
        while (isSuccess && n)
        {
                n--;
                t = sum(stack_1);
                if (t > sum_expect+tolerance||t< sum_expect-tolerance)
                {
                        i = int((urand()*18));
                        temp1 = stack_1[i];
                        temp2 = stack_2[i];
                        stack_1[i] = temp2;
                        stack_2[i] = temp1;
                }
                else
                        isSuccess = 0;

        };

        stack_final=stack_1[where(stack_1!=0)];
        sum_final=sum(stack_final);
        if(n==0)
        {
                ()=printf("组合失败!\n");
        }
        else
        {
                ()=printf("总和:%.1f元。\n",sum_final);
                for(i=0; i<length(stack_final)-1; i++) ()=printf("%.1f元|",stack_final[i]);
                ()=printf("%.1f元\n",stack_final[-1]);
        }
}
```
