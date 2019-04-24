京东图书优惠券满减快速凑整。比如我的优惠券买600块钱的书最划算，但是购物车里有好多书不知道那些组合最接近600。

在浏览器console内获取促销图书的价格列表。已考虑缺货货品。

最后如果凑整成功，会输出结果。

用法: 浏览器控制台内输入**jd_book(PromoName, ExpectedSum, Tolerance)**

比如 jd_book("product_promo_50008500387",600,3)；

三个参数，PromoName是促销的ID,可以从网页代码查到，ExpectedSum是目标价格，Tolerance是可以容忍的偏差价格。

下载地址[Greasyfork](https://greasyfork.org/scripts/382167)
