# vue-matrix-raindrop
基于Vue的黑客帝国数字雨特效实现<br><br>
![img](https://github.com/houzisbw/vue-matrix-raindrop/blob/master/imgs/rain.gif)

# Installation
npm
```js
  npm install vue-matrix-digit-rain --save
```
yarn
```js
  yarn add vue-matrix-digit-rain
```
# Usage
In your .vue file:
```js
<template>
  <div id="app">
    <VueMatrixRaindrop></VueMatrixRaindrop>
  </div>
</template>

<script>
import VueMatrixRaindrop from 'vue-matrix-digit-rain'
export default {
  name: 'App',
  components:{
    VueMatrixRaindrop
  }
}
</script>
```
# Props
| Name | Type | Default | Description |
|------|------|---------|-------------|
| canvasWidth | number | 800 | The width of canvas |
| canvasHeight | number | 600 | The height of canvas |
| fontSize | number | 20 | The font-size of digit rain letter |
| fontFamily | string | 'arial' | The font-family of digit rain letter |
| textContent | string | 'abcdefghijklmnopqrstuvwxyz' | The text of rain letter,which will choose the  index of **textContent** randomly|
| textColor | string | '#0F0' | The format of color only supports '#' style, not rgb |
| backgroundColor | string | 'rgba(0,0,0,0.1)' | The background-color of canvas, please note the **0.1** in rgba, this value decides the tail length of rain drop, the bigger of the value, the shorter of the tail |
| speed | number(int) | 2 | The speed of rain drop down,the bigger of the value, the slower of the speed|

