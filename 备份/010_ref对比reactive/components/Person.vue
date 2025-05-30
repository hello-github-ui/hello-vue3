<template>
    <div class="person">
        <h2>车辆信息：我有一个辆 {{ car.brand }} 车，价值 {{ car.price }} 万</h2>
        <button @click="changePrice">修改车辆的价格</button>

        <h2>总价是：{{ sum }}</h2>
        <button @click="changeSum">修改总价</button>
    </div>
</template>

<script lang="ts" setup name="Person">
// ref 可以用来 创建 基本类型、对象类型 的响应式数据
// reactive 只能用来 创建 对象类型的  响应式数据

/**
 * 使用原则：
 * 1.若需要一个基本类型的响应式数据，必须使用 ref
 * 2.若需要一个响应式对象，层级不深，ref，reactive都可以
 * 3.若需要一个响应式对象，且层级较深，推荐使用 reactive
 */

import {reactive, ref} from 'vue'


let car = reactive({
    "brand": "奔驰",
    "price": 100
})

let sum = ref(0)

function changePrice() {
    // car.price += 10;

    // 如果我现在想给 car 重新赋值一个 新对象呢？还能保留 之前的 响应式数据格式么
    // 直接这么写
    // car = {
    //     "brand": "奥托",
    //     price: 1
    // }
    // 直接上面这样写，是不行的，页面不更新

    // 如果模仿一开始 reactive 包括起来那样写呢？
    // car = reactive({
    //     "brand": "奥托",
    //     price: 1
    // })
    // 可以发现，上面这样写还是不行，页面不更新

    // 这时候，可以使用 Object.assign 这个内置的函数，来实现，这个写法 页面可以更新
    Object.assign(car, {"brand": "奥托", "price": 1})
}

function changeSum() {
    sum.value += 1;
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