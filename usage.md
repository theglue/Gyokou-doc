usage
-------

## 1. Model 定義

```coffeescript
Model = require 'Gyokou.Model'
class ExampleModel extends Model
  @TABLE_NAME: 'ExampleModel'
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
.filter 'size > 40'
.limit 3
.then (result) ->
  #引数にコレクション
  console.log result
  return
.faild (error) ->
  console.log error
  return 
```
