# mongoose

## 链接数据库

```js
const mongoose = require('mongoose');

const DB_URL = `mongodb://user:pass@ip:port/database`;

mongoose.connect(DB_URL, {
  poolSize: 20,
  useCreateIndex: true,
  useNewUrlParser: true
}, function (err) {
  if (err) {
    logger.error('connect to %s error: ', DB_URL, err.message);
    process.exit(1);
  } else {
    logger.success('connect to %s success: ', DB_URL);
  }
});
```

## Schema && Model

```js
const mongoose  = require('mongoose');

// 定义Schema
const schema = new mongoose.Schema({
  username: { // 用户名
    type: String,
    required: true
  },
  password: { // 密码
    type: String,
    required: true
  },
});

// 定义Model
const UserModel = mongoose.model('User', schema);

// 暴露接口
module.exports = UserModel;
```

```js
// import UserModel

// 使用
const userInfo = { username: 'xxx', password: '***' }
const userEntity = new UserModel(userInfo)

userEntity.save()

UserModel.create(userInfo)
UserModel.find({ username: 'xxx' })

Person
  .find({ occupation: /host/ })
  .where('name.last').equals('Ghost')
  .where('age').gt(17).lt(66)
  .where('likes').in(['vaporizing', 'talking'])
  .limit(10)
  .sort('-occupation')
  .select('name occupation')
  .exec(callback);
```

CRUD（增删改查）

## 文档新增

文档新增有三种方法

```js
save([options], [options.safe], [options.validateBeforeSave], [fn])
create(doc(s), [callback])
insertMany(doc(s), [options], [callback])
```

## 文档查询

文档查询有三种方法

```js
// 根据条件查询，返回的是数组
find(conditions, [projection], [options], [callback])
findById(id, [projection], [options], [callback])
// 根据条件查询，返回的是一条数据对象
findOne([conditions], [projection], [options], [callback])
```

文档查询中，常用的查询条件

```js
$or        或关系
$nor       或关系取反
$gt        大于
$gte       大于等于
$lt        小于
$lte       小于等于
$ne        不等于
$in        在多个值范围内
$nin       不在多个值范围内
$all       匹配数组中多个值
$regex     正则，用于模糊查询
$size      匹配数组大小
$maxDistance  范围查询，距离（基于LBS）
$mod        取模运算
$near       邻域查询，查询附近的位置（基于LBS）
$exists     字段是否存在
$elemMatch  匹配内数组内的元素
$within      范围查询（基于LBS）
$box         范围查询，矩形范围（基于LBS）
$center      范围醒询，圆形范围（基于LBS）
$centerSphere  范围查询，球形范围（基于LBS）
$slice        查询字段集合中的元素（比如从第几个之后，第N到第M个元素
```

## 文档更新

```js
update()
updateMany()
find() + save()
updateOne()
findOne() + save()
// 根据ID查找并更新
findByIdAndUpdate()
// 根据查询条件查找并更新
findOneAndUpdate()
```

## 文档删除

有三种方法用于文档删除

```js
remove(conditions, [callback])
findOneAndRemove(conditions, [options], [callback])
findByIdAndRemove(id, [options], [callback])
```

## 前后钩子

前后钩子即pre()和post()方法，又称为中间件，是在执行某些操作时可以执行的函数。中间件在schema上指定，类似于静态方法或实例方法等

可以在数据库执行下列操作时，设置前后钩子

```js
validate
save
remove
count
find
findOne
findOneAndRemove
findOneAndUpdate
insertMany
update
```

## 查询后处理

常用的查询后处理的方法如下所示

```js
sort     排序
skip     跳过
limit    限制
select   显示字段
exect    执行
count    计数
distinct 去重
```

## 文档验证

参考：

- https://mongoosejs.com/docs/
- https://segmentfault.com/a/1190000008366129
- https://segmentfault.com/a/1190000012095054
- https://i5ting.github.io/wechat-dev-with-nodejs/db/mongoose.html
- https://cnodejs.org/topic/504b4924e2b84515770103dd
