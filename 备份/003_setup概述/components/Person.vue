<template>
    <div class="person">
        <h2>姓名: {{ name }}</h2>
        <h2>年龄: {{ age }}</h2>
        <button @click="changeName">修改名字</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="showTel">查看联系方式</button>
    </div>
</template>

<script lang="ts">
export default {
    name: 'Person',
    beforeCreate() {
        console.log("生命周期函数: beforeCreate 被执行到...")
    },
    setup() { // vue3 中的 setup 其实也是 vue2 中的一个 选项，因此类似 data，methods的写法
        console.log("生命周期函数: setup 被执行到") // vue3 中的 setup 函数生命周期要比 vue2 中的 beforeCreate() 函数还要早，早于 vue2 中的 data(), methods(), watch() 等
        // 数据
        let name = '张三' // 直接这样写数据的话，不是响应式的，即不是双向绑定的
        let age = 18 // 直接这样写数据的话，不是响应式的，即不是双向绑定的
        let tel = '12345678' // 直接这样写数据的话，不是响应式的，即不是双向绑定的

        console.log("vue3中的this指向: ", this) // vue3中的this指向:  undefined
        // setup 函数中的 this 是 undefined，vue3 正在弱化 this

        // 方法
        function changeName() {
            name = 'zhang-san'
            console.log("点击了 changeName(): ", name)
            // 页面上点击 修改名字 后确实能够响应到这里，但是页面上的名字是不会有变化的？why？就是因为此时的 name 不是响应式的数据
        }
        function changeAge() {
            age += 1
            console.log("点击了 changeAge(): ", age)
        }
        function showTel() {
            alert(tel)
            console.log("点击了 showTel(): ", tel)
        }

        // 将数据、方法交出去，模板中才可以使用
        return {name, age, tel, changeName, changeAge, showTel}
    }
}
</script>

<style scoped>
.person {
    background-color: skyblue;
    box-shadow: 0 0 10px;
    border-radius: 10px;
    padding: 20px;
}

button{
    margin: 0 5px;
}
</style>