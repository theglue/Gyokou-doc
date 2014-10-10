API Reference.


* Core
  * `Gyokou.filter(statment)`
  * `Gyokou.order(orderBy)`
  * `Gyokou.fetch()`
  * `Gyokou.limit(num)`
  * `Gyokou.get(key)`
  * `Gyokou.len()`
  * `Gyokou.save(data)`
  * `Gyokou.update(data)`
  * `Gyokou.del(data)`
  * `Gyokou.extends(kls)`
  * `Gyokou.setGlobalConfig(config)`


##Core

`Gyokou.filter(statement)` -> `Gyokou`

指定された条件で検索をかけます。

```coffeescript
Gyokou
.filter 'size > 39'
.fetch()
```

-------

`Gyokou.order(orderBy)` -> 'Gyokou'

クエリの戻り値の並び順を指定します。

```coffeescript
Gyokou
.order('-id')
.fetch()
```

-------

`Gyokou.fetch()` -> 'Promise'

クエリから結果を取得します。

```coffeescript
Gyokou
.filter 'weight > 1400'
.fetch
.then (result) ->
  console.log result
  return
.faild (error) ->
  console.log error
  return
```

--------

`Gyokou.limit(num)` -> 'Promise'

クエリから指定した件数を取得します。

```coffeescript
Gyokou
.filter 'type == small_mouth'
.limit 5
.then (result) ->
  console.log result
  return
.faild (error) ->
  console.error 'ソイヤ'
  return
```

--------

`Gyokou.get(key)` -> `Gyokou(instance)`

指定したキーのインスタンスを取得します。

```coffeescript
Gyokou.get id=1
```

--------

`Gyokou.len()` -> `Promise`

指定したクエリの件数を取得します。

```coffeescript
Gyokou
.filter 'size > 40'
.len
.then (result) ->
  console.log result
  return
.faild (error) ->
  console.error 'ソイヤ'
  return
```

--------

`Gyokou.save(data)` -> `Promise`

指定したデータを作成します。

```coffeescript
data =
  size: 38
  weight: 900


Gyokou
.save data
.then (result) ->
  console.log 'success'
  return
.faild (error) ->
  console.error 'ソイヤ'
  return
```

--------

`Gyokou.update(data)` -> `Promise`

指定したデータを保存します。

```coffeescript
data = 
  id: 2
  size: 45
  weight: 1400

Gyokou
.update data
.then (result) ->
  console.log 'success'
  return
.faild (result) ->
  console.errro 'ソイヤ'
  return
```


--------

`Gyokou.del(key)` -> `Promise`

指定された条件のデータを削除します。

```coffeescript
Gyokou
.del id=1
then (result) ->
  console.log 'success'
  return
.faild (result) ->
  console.error 'ソイヤ'
  return
```


--------

`Gyokou.extends(kls)`

指定されたクラスに Gyokou が保持しているクラスメソッドを継承します。

```coffeescript
class BassModel
  @TABLE_NAME: 'BassModel'
  @url: '/bass'
  @ddl:
    id:
      type: 'int'
      key: true
    size:
      type: 'number'
    weight:
      type: 'number'

Gyokou.extends BassModel
```

--------

`Gyokou.setGlobalConfig(config)`

全体に関する設定を実行します。
Gyokou を継承している全てのモデルに影響を及ぼします。

```coffeescript
Gyokou.setGlobalConfig
  api_host: 'www.example.com'
  api_port: '3000'
  api_prefix: '/api'
```


