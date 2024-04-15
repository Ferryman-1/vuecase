# vuecase
## 输入学生成绩案例业务技术点总结：
### 1. 渲染功能（不及格高亮）
v-if v-else v-for v-bind:class
`:class="{red: item.score < 60}"`
### 2. 删除功能
点击传参 filter过滤覆盖原数组
```javascript
//传过来的id和当前item.id不相等，就保留下来；相等就移除掉
this.list = this.list.filter((item) => item.id !== id)
```
.prevent 阻止默认行为
### 3. 添加功能
v-model v-model修饰符(.trim .number)
push 修改数组更新视图
```javascript
add(){
 // !this.subject取反是判断输入是否为空
if(this.subject.trim() === ''){
alert('请输入科目')
 return
}else if(typeof this.score !== 'number'){
alert('请输入正确的分数')
return
}
this.list.push({
id: +new Date(),
subject: this.subject,
score: this.score
})
this.subject = ''
this.score = ''
}
```
### 4. 统计总分，求平均分
计算属性 reduce求和和求平均分
```javascript
computed: {
totalScore(){
return this.list.reduce((sum, item) => sum + item.score, 0)
},
averageScore(){
if (this.list.length === 0) {
return 0
}
//number数字保留两位小数 4舍5入
return (this.totalScore / this.list.length).toFixed(2)
}
}
```

## 翻译器技术总结：
watch语法实时的监控到当前数据的一个变化，一旦监视到数据的值，拿到变化后的值，我们可以基于它来发送请求获得对应的结果，最后到页面当中做一个渲染
## 业务：
输内容立刻翻译结果，渲染到页面
## 问题：
每输入一个字母，都发出请求，翻译一次，性能不高，对服务器的压力很大
## 解决1：
防抖优化（又称为：延迟执行 → 干啥事先等一等，延迟一会，一段时间内没有再次触发，才执行）
## 解决2：
如果一段时间内触发了，需要将原来开的延时器清除掉，clearTimeout（延时器id）
延时器id在setTimeOut（）里边就有了。
- 步骤：在第一次开延时器的时候存一存，等下一次过来的时候清除一下。
`this.timeId`

## 注：
(setTimeout 返回一个非负整数，这个标识符可以传递给 clearTimeout 函数，用于取消尚未执行的定时器。达到防抖效果。)
### 原理：
这里做的这个防抖其实就是，在我们的设定单位时间内，输入框一直有值输入。那么我就一直清除定时器。直到在这个时间内没有值。我们在会进入到延时函数里面进行发送请求数据。
