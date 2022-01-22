<template>
  <section>
    <p>{{ num }}</p>
    <p v-text="context.state"></p>
    <section>
      obj:
      <span>{{ obj.name}}</span>
      <span>{{ obj.age }}</span>
    </section>
    <section>
      obj1:
      <span>{{ obj1.name }}</span>
      <span>{{ obj1.age }}</span>
    </section>
    <section>
      obj2:
      <span>{{ obj1.name }}</span>
      <span>{{ obj1.age }}</span>
    </section>
    <section>
      var:
      {{ name }}/{{ age }}/{{ doubleAge }}
    </section>
  </section>
</template>

<script lang="ts">
import { defineComponent, ref, reactive, onMounted, watch, computed, toRaw, markRaw, toRefs, toRef } from 'vue';


export default defineComponent({
  name: 'Context',
  setup(props) {
    type IContext = {
      state: string
      formList: string[]
    }


    // 定义数据
    let num = ref(0); // Ref<number>
    let str = ref(''); // Ref<string>
    let context: IContext = reactive({
      state: 'common',
      formList: []
    })

    const obj = reactive({
      name: 'test',
      age: 33
    })


    // 响应式数据的解构
    let { name } = obj // 解构响应式对象获取的值为非响应式
    let { age } = toRefs(obj) // 使用toRefs解构


    // watch 和 computed
    watch(age, () => {
      console.log('age update')
    })
    let doubleAge = computed(() => age.value * 2)

    const obj1 = toRaw(obj)
    const obj2 = markRaw(obj)
    // setup中使用生命周期函数
    onMounted(() => {
      console.log(age.value)
      console.log(doubleAge.value)

      // setTimeout(() => {
      //   context.state = 'context-test';
      //   // num = 'num' // Type 'string' is not assignable to type 'Ref<number>'
      //   num.value = 10
      //   context.formList.push('formList first data')
      //   // context.formList.push(new Date()) // Argument of type 'Date' is not assignable to parameter of type 'string'
      //   // context.formList.push(1) // Argument of type 'number' is not assignable to parameter of type 'string'
      // }, 1000 * 3)
      // obj.age++
      setTimeout(() => {
        obj2.age++
        console.log(obj2.age)
        console.log(obj1.age)
        console.log(obj.age)
        console.log(age.value)
        name = 'jilon'
      }, 2000)

    })


    return {
      num,
      context,
      obj,
      obj1,
      obj2,
      name,
      age,
      doubleAge
    }
  }
})
</script>
