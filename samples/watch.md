# watch

---

## watch object/array

watch 無法監視整個物件或陣列的內容變化，且宣告時只能是 var.field.field... 的方式宣告，
若要監視一個物件/陣列中的任何內容有變化，必須透過宣告可執行函數來達成。

watch 可接受下面的宣告：

```js
data: {
  field: 'field',
  obj: {
    field1: 'obj.field1',
    field2: 'obj.field2',
    obj: {
      field1: 'obj.obj.field1',
      field2: 'obj.obj.field2',
    }
  },
  arr: [1, 2, 3]
},
computed: {
  computedForWatch() {
    return this.arr[0];
    // 監視 this.obj 的內容是否有任何的變動
    // return JSON.stringify(this.obj);
  }
},
watch: {
  field: function() {}, // 監視 field 值是否變動
  obj() {}, // 只能監視 obj 是否有重新指派
  arr() {}, // 只能監視 arr 是否有重新指派
  this.obj.field1() {}, // 同 field 只監視 obj.field1 值是否變動
  // arr[0]() {}, // 錯誤！watch 只接受 var.field.field...
  // 必須透過 computed
  computedForWatch: function(newValue, oldValue) {
    console.log('watch', 'computedForWatch', newValue, oldValue);
  }

  // 監視 vue-router 路徑的變動
  $route: function(route) { /* ... */ },
}
```

References:

- [vue-$watch的使用](https://my.oschina.net/zhangdq/blog/1610647)
- [How to watch only one object in an array?](https://stackoverflow.com/questions/43750569/how-to-watch-only-one-object-in-an-array)
