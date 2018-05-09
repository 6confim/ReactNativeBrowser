
# 实现页面动态化思路

## 基础

1. react native 打包是把所有代码打包到一个文件中

2. 每个模块打包后引用的ID为自增的数字

3. 模块只能通过require 获得

4. 如果模块相同每次打包的moudleId一致

5. 每个模块执行的时候都能访问到（global, require, module, exports）

6. 可以调用___def()动态的定义模块

7. require方法仅仅是返回执行之后的module

## 实现

1. 把项目包拆分成，基础包、组件包、页面包

2. 把新增的动态页面（活动页、经常动态替换的页面）基于base包输出出来源文件
  如下：
  
```
  
__d(/* EventSubscriptionVendor */function(global, require, module, exports) {
'use strict';

var invariant = require(13                  ); // 13 = fbjs/lib/invariant

....


module.exports = EventSubscriptionVendor;
}, 61, null, "EventSubscriptionVendor");

````

3. 下载执行

  1. 使用native fetch 源代码 然后使用 bridge通过jscore调用该模块
  
  2. 使用js加载 调用并且使用eval、new Function('') 执行代码
  
  
4. 使用，显示组件

  1. 打开一个空页面，通过moduleId（服务端返回），拿到对应的组件 require(189)使用render方法 render 该模块
  
  2. 实现动态router，当组件执行完成后，动态添加到 router中，就可以像正常页面一样使用该页面了
 

  
  


