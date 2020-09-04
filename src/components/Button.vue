<template>
  <div>
    <button @click="handleClick">click</button>
    <p>count: {{count}}</p>
    <p>state.time: {{state.time}}</p>
    <p>abc.value: {{abc.value}}</p>
    <p>double: {{double}}</p>
    <p>copy.time:{{copy.time}}</p>
  </div>
</template>

<script>
import { ref, toRef,reactive, readonly,computed,watch, onMounted,watchEffect } from "vue";
export default {
  name: "Button",
  setup() {
    //  3种 创建响应式对象 方式
    // ref 一般值类型用ref string number
    const count = ref(0); // 将0创建成响应式对象
    // reactive，readonly(只读) {} [] 引用类型
    const state = reactive({ time: 0,age:0 });
    const statePlus = toRef(state,'time')
    // readonly 等同于 reactive ，但仅读，不可更改
    const abc = readonly({ key: 0 });
    console.log(count);
    console.log('state=>',state);
    console.log('statePlus=>',statePlus)
    console.log(abc);
    // 响应式系统 api
    // computed
    const double = computed(()=>{
      return count.value * 2;
    })

    const copy = readonly(state)
    const stop = watchEffect(()=>{
      console.log('watchEffect copy',copy.time)
    },
    {
      flush: 'pre',
    })
    watch(double,(n,o)=>{
      console.log("watch")
      console.log(n,o)
    })
    onMounted(()=>{
      console.log('mounted')
    })
    const handleClick = () => { 
      count.value++; // ref类型响应式对象 需要通过.value获取值 最新的eslint可以帮忙检测
      state.time++;
      if(state.time == 3) stop()
      // abc.value++;
      console.log('state=>',state);
      console.log('statePlus=>',statePlus)
    };
    return {
      count,
      handleClick,
      state,
      abc,
      double,
      copy
    };
  },
};
</script>

<style lang="scss" scoped>
</style>
