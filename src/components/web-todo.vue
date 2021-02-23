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
        <button type="button" @click="getJoke">get joke</button>
        <p>{{jokeContent}}</p>
        <input type="text" @keyup.enter="searchWeather(city)" v-model="city">
        <button type="button" @click="searchWeather(city)">Search</button>
        <a href="#" v-for="(c, index) in defaultCitys" :key="index" @click="searchWeather(c)">{{c}}</a>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "web-todo",
    data() {
        return {
            items: [],
            inputValue: '',
            jokeContent: '',
            city: '',
            defaultCitys: ['北京', '上海', '深圳', '广州'],
        }
    },
    methods: {
        initItem: function () {
            this.items = [];
        },
        addItem: function (value) {
            if (value !== '') {
                this.items.push(value);
                this.inputValue = '';
            }
        },
        delItem: function (index) {
            this.items.splice(index, 1);
        },
        getJoke: function () {
            axios.get('https://autumnfish.cn/api/joke')
                .then((response) => {
                    this.jokeContent = response.data;
                }, (err) => {
                    console.log(err);
                });
        },
        searchWeather: function (c) {
            if (c === '') { return; }
            axios.get('http://wthrcdn.etouch.cn/weather_mini?city=' + c)
            .then((response) => {
                console.log(response.data);
                if (response.data.status === 1002) {
                    alert(response.data.desc)
                }
            }, (err) => {
                console.log(err);
            })
        }
    }
}
</script>

<style scoped>

</style>