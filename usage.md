usage
-------

## 1. Model 定義

```coffeescript
Model = require 'Gyokou.Model'
class ExampleModel extends Model
  
  @ddl: 
    id: 
      key: true
      type: 'int'

    weight:
      type: 'int'

    size:
      type: 'int'

  constructor: ->
    super()


module.exports = ExampleModel
```

## 2.クエリ

```coffeescript
ExampleModel
.where 'size > 40'
.limit 3
.success (result) ->
  #引数にコレクション
  console.log result
  return
.faild (error) ->
  console.log error
  return 
```

## 3.インスタンス

```coffeescript
#save data
model = new ExampleModel data
model
.save #send by POST method.
.success (event) ->
  #保存に成功した
  console.log event
.faild (error) ->
  console.log error
  return

model.weight = 1400
model
.update #send by PUT method.
.success (result) ->
  console.log result
  return
.faild (error) ->
  console.log error
  return

model
.del #send by DELETE method
.success (result) ->
  console.log result
  return
 .faild (error) ->
   console.log error
   return
```