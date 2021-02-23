<template>
    <div>
        <input type="text" v-model="inputValue" @keyup.enter="addItem(inputValue)">
        <table>
            <tr v-for="(item, index) in items" :key="index">
                <td>{{ index + 1 }}{{ item }}
                    <button type="button" @click="delItem(index)">x</button>
                </td>
            </tr>
            <tr v-show="items.length !== 0">
                <td>total: {{ items.length }}
                    <button type="button" @click="initItem">clean all!</button>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    name: "web-todo",
    data() {
        return {
            items: [],
            inputValue: '',
        }
    },
    methods: {
        initItem: function () {
            this.items = [];
        },
        addItem: function (value) {
            this.items.push(value);
            this.inputValue = '';
        },
        delItem: function (index) {
            this.items.splice(index, 1);
        }
    }
}
</script>

<style scoped>

</style>