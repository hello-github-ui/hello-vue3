<template>
    <div class="person">
        <h2>车辆信息：我有一个辆 {{ car.brand }} 车，价值 {{ car.price }} 万</h2>
        <button @click="changePrice">修改车辆的价格</button>

        <h2>游戏列表：</h2>
        <ul>
            <li v-for="game in games" :key="game.id">{{ game.name }}</li>
        </ul>
        <button @click="changeFirstGame">修改第一个游戏的名字</button>

        <hr>
        <h2>深度嵌套对象：{{ obj.a.b.c }}</h2>
        <button @click="changeObj">修改对象的值</button>
    </div>
</template>

<script lang="ts" setup name="Person">
// reactive 是用来 将一个 对象 构造成  响应式对象的
// ref 是用来 将一个 基本的数据类型 构造成 响应式数据类型的
import {reactive} from 'vue'

let car = reactive({
    "brand": "奔驰",
    "price": 100
})

// 数组也是对象，
let games = reactive([
    {"id": "xxxx1", "name": "王者荣耀"},
    {"id": "xxxx2", "name": "流星蝴蝶剑"},
    {"id": "xxxx3", "name": "元神"},
])

// reactive 还支持 深度嵌套对象
let obj = reactive({
    a: {
        b: {
            c: 666
        }
    }
})

function changePrice() {
    car.price += 10;
    console.log(car.price)
}

function changeFirstGame() {
    games[0].name = "英雄联盟"
    // 此时打印出来的 games 就是一个 响应式对象（使用 Proxy 包起来的就是一个响应式代理对象）
    console.log(games)
}

function changeObj() {
    obj.a.b.c = 999
}

</script>

<style scoped>
.person {
    background-color: skyblue;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}

li {
    font-size: 20px;
}

button {
    margin: 0 5px;
}
</style>