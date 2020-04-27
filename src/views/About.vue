<template>
  <div class="test">
    <h1>test count: {{ count }}</h1>
    <div>count * 2 = {{ doubleCount }}</div>
    <button @click="add">add</button>
  </div>
</template>

<script>
import { ref, computed, watch, reactive, watchEffect, onMounted } from "vue";

export default {
  setup() {
    const count = ref(0); // 和 reactive类似  取值count.value
    const add = () => {
      count.value++;
    };

    watch(
      () => count.value,
      val => {
        console.log(`count is ${val}`);
      }
    );
    const doubleCount = computed(() => count.value * 2);

    const state = reactive({
      // Vue.observable() 等效 类似主动加上get和set方法 当然 proxy不需要
      count: 0
    });

    watchEffect(
      () => {
        // 类似watch  当state.count发生变化  他会自动更新  在这处理html
        document.body.innerHTML = `count is ${state.count}`;
      },
      {
        // 组件更新前
      }
    );

    onMounted(() => {
      // 挂载后的钩子
      console.log("onMounted");
    });

    // ref   count.value  （非对象的简单值） //  reactive  不用.value (对象)

    return {
      count,
      doubleCount,
      add
    };
  }
};
</script>
