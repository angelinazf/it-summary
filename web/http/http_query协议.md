### 例子1
* yaml协议表述

```yaml
type: InSimpleConditionalExpress
value:
  field: id
  value: [1,3,5,6]
```
* json协议表述

```json
{
  "type":"InSimpleConditionalExpress",
  "value":{
    "field":"id",
    "value":[1,3,5,6]
  }
}
```

* http_query协议表述
(去掉换行,并且进行url的encode)

```
type=InSimpleConditionalExpress&
value[field]=id&
value[value][]=1&
value[value][]=3&
value[value][]=5&
value[value][]=6
```
