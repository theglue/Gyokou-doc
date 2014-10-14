API Reference.
------------


* Core
  - [`Gyokou.filter(statment)`](#gyokoufilterstatement---gyokou)
  - [`Gyokou.order(orderBy)`](#gyokouorderorderby---gyokou)
  - [`Gyokou.fetch()`](#gyokoufetch---promise)
  - [`Gyokou.limit(num)`](#gyokoulimitnum---promise)
  - [`Gyokou.get(key)`](#gyokougetkey---gyokouinstance)
  - [`Gyokou.len()`](#gyokoulen---promise)
  - [`Gyokou.save(data)`](#gyokousavedata---promise)
  - [`Gyokou.update(data)`](#gyokouupdatedata---promise)
  - [`Gyokou.del(data)`](#gyokoudelkey---promise)
  - [`Gyokou.extends(kls)`](#gyokouextendskls)
  - [`Gyokou.setGlobalConfig(config)`](#gyokousetglobalconfigconfig)
  - [`options`](#options)
* Options
  - [`Gyokou.ddl`]()
  - [`Gyokou.TABLE_NAME`]()
  - [`Gyokou.xhrConfig`]()


##Core

##### `Gyokou.filter(statement)` -> `Gyokou`

指定された条件で検索をかけます。

```coffeescript
Gyokou
.filter 'size > 39'
.fetch()
```

-------

##### `Gyokou.order(orderBy)` -> `Gyokou`

クエリの戻り値の並び順を指定します。

```coffeescript
Gyokou
.order('-id')
.fetch()
```

-------

##### `Gyokou.fetch()` -> `Promise`

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

##### `Gyokou.limit(num)` -> `Promise`

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

##### `Gyokou.get(key)` -> `Gyokou(instance)`

指定したキーのインスタンスを取得します。

```coffeescript
Gyokou.get 1
```

--------

##### `Gyokou.len()` -> `Promise`

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

##### `Gyokou.save(data)` -> `Promise`

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

##### `Gyokou.update(data)` -> `Promise`

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

##### `Gyokou.del(key)` -> `Promise`

指定された条件のデータを削除します。

```coffeescript
Gyokou
.del 1
then (result) ->
  console.log 'success'
  return
.faild (result) ->
  console.error 'ソイヤ'
  return
```


--------

##### `Gyokou.extends(kls)`

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

**memo:** 中に仕舞いこみたい

--------

##### `Gyokou.setGlobalConfig(config)`

全体に関する設定を実行します。
Gyokou を継承している全てのモデルに影響を及ぼします。

```coffeescript
Gyokou.setGlobalConfig
  api:
    host: 'www.example.com'
    port: '3000'
    prefix: '/api'
    beforeRequest: (ctx) ->
      #do something.
      return
    afterRequest: (ctx) ->
      #do something.
      return
  local:
    store: LSStore
    prefix: 'example-prefix'
    lazyQuery: false
```

**memo:** Configクラス作る?

----------

##### `Gyokou.getGlobalConfig()` -> `Object`

現在の全体設定を返します。

----------

##### options

各クラスの設定

[Options]() の項目を参照。

-------


##Options

Gyokou を継承してモデルを定義するときに指定するオプション。

##### `Gyokou.TABLE_NAME` 

ローカルデータストアに蓄積するときのテーブル名

```coffeescript
class ExampleModel
  @TABLE_NAME: 'ExampleModel'
```

-----------

##### `Gyokou.ddl`

モデルのデータ構造を定義します。

```coffeescript
class ExampleModel
  @ddl:
    id: 
      type: 'int'
      key: true
    size:
      type: 'number'
    weight:
      type: 'number'
```

##### `Gyokou.xhrConfig`

モデルが通信する API との通信に関する設定を行います。

```coffeescript
class ExampleModel
  @xhrConfig:
    prefix: 'example'
    actions:
      get: 
        method: 'GET'
      post: 
        method: 'POST'
      put:
        method: 'POST'
        url: 'example/update'
      delete:
        method: 'DELETE'
    beforeRequest: (ctx) ->
      #do something.
      return
    afterRequest: (ctx) ->
      #do something
      return
```

**memo:** XHRConfig クラスとか作ってそいつを投げるようにしたほうがすっきりはするかもしれない(ネスト深くなるし。)




