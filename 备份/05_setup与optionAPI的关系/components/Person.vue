<template>
    <div class="person">
        <h2>姓名: {{ name }}</h2>
        <h2>年龄: {{ age }}</h2>
        <button @click="changeName">修改名字</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="showTel">查看联系方式</button>
        <hr/>
        <h2>测试: {{c}}</h2>
    </div>
</template>

<script lang="ts">
export default {
    name: 'Person',
    beforeCreate() {
        console.log("生命周期函数: beforeCreate 被执行到...")
    },
    data() {
        return {
            // 在 data 中能不能直接访问 setup 中的数据呢？
            // data 和 methods 是能访问到 setup 中的数据和方法的，因为 setup 的生命周期比它们都要早
            // 但能访问到的前提是，必须要加 this
            c: this.tel + 'xxxxxx'
        }
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

        // 将数据、方法交出去，模板中才可以使用，此时 返回的是一个 对象，那是不是必须要返回一个对象呢？
        return {name, age, tel, changeName, changeAge, showTel}

        // 其实不是的，也可以直接返回一个渲染函数
        // return function (){
        //     return '哈哈哈' // 这时候，该 Person.vue 整个模板直接就返回了一个字符串 '哈哈哈'，与上面的 </template> 中定义的都没有关系了
        //     // 但是这种写法是不是有点麻烦了？因为这个匿名函数的作用是不是只要一个返回值，并没有涉及到 this 指向的问题？？？
        //     // 那么此时可以使用 箭头函数来改写？
        // }

        // return () => {
        //     return '哈哈哈' // 这种方式是不是还可以简写？因为当箭头函数的函数体中只有一行代码的话，可以简写成下面这个样子
        // }

        // return () => '哈哈哈'
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