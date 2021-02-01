学习笔记
## String
- ASCII
- Unicode
- UCS
- GB
  GB2312
  GBK(GB13000)
  GB18030
- ISO-8859
- BIG5

## Null 和 undefined
- null 表示有值，但是值为空，是关键字
- undefined 没有设置过这个值，没有定义，不是关键字
 null == undefined -> true

## Javascript 类型
- String （ASCII，Unicode，UTF编码方式）
- Number (float表示方法：符号位（1），指数位（11），有效数字位（52）)
- Boolean
- Null
- Undefined
- Object
- Symbol

## 对象的基础知识
1. 核心要素：
   - 唯一性标识
   - 状态
   - 行为
2. 狗咬人练习
```
	class Human {
		hurt(damage){

		}
	}
```

## js对象
1. 原型 prototype
  - 如果自身不包含这个属性，就去原型上找，如果原型的原型是不为空，还会继续到原型的原型上找，一直找到null

2. 属性(键值对)
  - key: String 或 Symbol
  - value: 数据属性 或 访问器属性

3. 语法和api
 - {}.[] Object.defineProperty (创建对象，访问属性，定义新的属性以及改变属性的特征值)
 - Object.create / Object.setPrototypeOf / Object.getPrototypeOf（基于原型的描述方法）
 - new / class / extends （基于分类的方法描述对象）
 - new / function / prototype（建议别用）

4. Host Object 
 - 浏览器访问到window 和setTimeout和js原生对象无关
 












