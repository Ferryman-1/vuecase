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
