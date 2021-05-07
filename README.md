# mobile-keyboard-vue3

> 适用于 Vue3.x 版本的自定义移动端键盘输入，支持输入整数、浮点数、手机号、身份证号四种模式

### 示例

```vue

<template>
  <p @click="show = !show">{{ inputValue }}</p>
  <keyboard v-model="inputValue" type="decimal" v-model:show="show"></keyboard>
</template>
<script setup>
import keyboard from './components/keyboard.vue'
import {ref} from "vue"

const inputValue = ref('123')
const show = ref(false)
</script>
<style>
html, body {
  margin: 0;
  padding: 0;
}
</style>

```

### 属性

| Property      | Type     | Default | Description                              |
| :------------ | :------- | :------ | :--------------------------------------- |
| type          | String   | decimal | 键盘类型：decimal 小数，integer 整数，phone 手机号，card 身份证 |
| value/v-model      | String   | chinese | 默认输入字符串                         |

### 预览图


![小数](https://cdn.jsdelivr.net/gh/lzq920/picx-image-host@master/20210506/10.0.0.23_3000_(iPhone 6_7_8).5ugx3q5jqaw0.png)

![整数](https://cdn.jsdelivr.net/gh/lzq920/picx-image-host@master/20210506/10.0.0.23_3000_(iPhone 6_7_8) (1).3bsjiypuo1m0.png)

![手机号](https://cdn.jsdelivr.net/gh/lzq920/picx-image-host@master/20210506/10.0.0.23_3000_(iPhone 6_7_8) (2).30irsu2lc4s0.png)

![身份证号](https://cdn.jsdelivr.net/gh/lzq920/picx-image-host@master/20210506/10.0.0.23_3000_(iPhone 6_7_8) (3).aac7fv5qf4o.png)


