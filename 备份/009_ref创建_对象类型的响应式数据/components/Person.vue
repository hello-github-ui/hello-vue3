<template>
    <div class="person">
        <h2>车辆信息：我有一个辆 {{ car.brand }} 车，价值 {{ car.price }} 万</h2>
        <button @click="changePrice">修改车辆的价格</button>

        <h2>游戏列表：</h2>
        <ul>
            <li v-for="game in games" :key="game.id">{{ game.name }}</li>
        </ul>
        <button @click="changeFirstGame">修改第一个游戏的名字</button>

    </div>
</template>

<script lang="ts" setup name="Person">
// reactive 是用来 将一个 对象 构造成  响应式对象的
// ref 是用来 将一个 基本的数据类型 构造成 响应式数据类型的

// TODO 其实上面两句话描述不太对，怎么样呢？
// TODO ref 可以用来 创建 基本类型、对象类型 的响应式数据
// TODO 而 reactive 只能用来 创建 对象类型的  响应式数据
// 怎们证明呢？，我们就把之前使用 reactive 包括起来的代码，使用 ref 来包括一下
import {reactive, ref} from 'vue'

// let car = reactive({
//     "brand": "奔驰",
//     "price": 100
// })

let car = ref({
    "brand": "奔驰",
    "price": 100
})

// 数组也是对象，
// let games = reactive([
//     {"id": "xxxx1", "name": "王者荣耀"},
//     {"id": "xxxx2", "name": "流星蝴蝶剑"},
//     {"id": "xxxx3", "name": "元神"},
// ])

let games = ref([
    {"id": "xxxx1", "name": "王者荣耀"},
    {"id": "xxxx2", "name": "流星蝴蝶剑"},
    {"id": "xxxx3", "name": "元神"},
])

// 那么这个 ref 和 reactive 在 都创建对象类型的响应式数据时， 有啥区别呢？
// 我们使用 reactive 创建一个 响应式对象，分别打印一下 这两种方式创建的 响应式对象，看看有啥发现
let ob = reactive({
    "id": 1
})

console.log("reactive创建的响应式对象:", ob)
console.log("ref创建的响应式对象:", car)
// 可以看到 使用 ref 创建 对象类型 的响应式对象时，底层其实还是使用的  reactive 的方式，观察其 _value 和 value 属性

// function changePrice() {
//     car.price += 10;
//     console.log(car.price)
// }
//
// function changeFirstGame() {
//     games[0].name = "英雄联盟"
//     // 此时打印出来的 games 就是一个 响应式对象（使用 Proxy 包起来的就是一个响应式代理对象）
//     console.log(games)
// }

// TODO 但是呢，如果使用 ref 后，我们之前讲过：如果想在 js 中修改 ref 包括起来的属性的值的话，需要使用 .value 的写法，因此我们来修改下
function changePrice() {
    /*
    注意：原本是下面的这样
    let car = ref({
    "brand": "奔驰",
    "price": 100

    你如果需要取到 ref() 括号里面的内容，你需要使用 .value 才能取到 该内容，
    即 car.value 取到的就是 car{} 这个对象
})
     */
    car.value.price += 10;
    console.log(car.value.price)
}

function changeFirstGame() {
    // 这里也是同理， games.value 取到的才是  games 本身的这个数组对象，千万不要写成这样：games[0].value
    games.value[0].name = "英雄联盟"
    // 此时打印出来的 games 就是一个 响应式对象（使用 Proxy 包起来的就是一个响应式代理对象）
    console.log(games)
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