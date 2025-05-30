<template>
    <div class="person">
        <h2>姓名: {{ name }}</h2>
        <h2>年龄: {{ age }}</h2>
        <button @click="changeName">修改名字</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="showTel">查看联系方式</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import {ref} from 'vue'

// 数据
let name = ref('张三') // 直接这样写数据的话，不是响应式的，即不是双向绑定的，当用 ref 包起来的话，此时就是响应式的了
let age = ref(18) // 直接这样写数据的话，不是响应式的，即不是双向绑定的
let tel = '12345678' // 直接这样写数据的话，不是响应式的，即不是双向绑定的

// setup 函数中的 this 是 undefined，vue3 正在弱化 this

// 方法
function changeName() {
    // 使用 Ref 包含的 属性，要想修改其属性值， data 部分不用.value，但是 在 js 中必须使用 .value
    // name = 'zhang-san'
    // console.log("点击了 changeName(): ", name)
    // // 页面上点击 修改名字 后确实能够响应到这里，但是页面上的名字是不会有变化的？why？就是因为此时的 name 不是响应式的数据

    // 如上这样写后，页面中点击 修改名字，还是不会有响应式变化，需要如下写法才行
    name.value = 'zhang-san'
    console.log("name: ", name.value)
}

function changeAge() {
    // age += 1
    // console.log("点击了 changeAge(): ", age)

    age.value += 1
    console.log("age: ", age.value)
}

function showTel() {
    alert(tel)
    console.log("点击了 showTel(): ", tel)
}

</script>

<style scoped>
.person {
    background-color: skyblue;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}

button {
    margin: 0 5px;
}
</style>