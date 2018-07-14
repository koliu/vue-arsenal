# $emit

---

## $emit on \<router-view>

- [trying to update parent from child emit in vue 2](https://stackoverflow.com/questions/47025903/trying-to-update-parent-from-child-emit-in-vue-2)

```pug
<!-- parent -->
router-view(@test-emit="testEmit")

script
  methods: {
    testEmit(callerPath) {}
  }

<!-- child -->
.submit(@click="callParent")

script
  methods: {
    callParent() {
      this.$emit('test-emit', ...);
    }
  }
```
