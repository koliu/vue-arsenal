# loader

## [Sample 1](https://jsfiddle.net/9jse9zrn/1/)

> Base on [Emit event and component’s parent update](https://forum.vuejs.org/t/emit-event-and-components-parent-update/23975)

```html
<div id="vue">
  <div v-if="loading">
    Loading
  </div>
  <loader @start="loading = true" @finish="loading = false"/>
</div>

<script>
Vue.component('loader',{
	template:`<button @click="load">Load</button>`,
  methods:{
  	load(){
    	this.$emit('start')
      this.$nextTick(()=>{
        requestAnimationFrame(()=>{
          //requestAnimationFrame(()=>{
            const time = Date.now()
            for(let i = 0; i < 10 ** 9; i++){
              //do slow stuff
            }
            console.log(Date.now() - time)
            this.$emit('finish')
          //})
        })
      })
    }
  }
})

new Vue({
	el:'#vue',
  data(){
  	return {
    	loading:false
    }
  }
})
</script>
```
