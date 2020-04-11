<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <HelloWorld msg="Welcome to Your Vue.js App"/>
    </div>
</template>

<script>
    import HelloWorld from './components/HelloWorld.vue'

    export default {
        name: 'App',
        components: {
            HelloWorld
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>

<template>
    <div>
        <ul :key="user.id" v-for="user in users">
            <li>
                <span>{{user.name}}</span> &#160;
            </li>
            <li>
                <span>{{user.name}}</span> &#160;
                <button @click="edit(user)">Edit</button>
                ||
                <button @click="del(user)">Delete</button>
            </li>
        </ul>
    </div>
</template>

<form @submit.prevent="add">
    <input type="hidden" v-model="form.id">
    <input type="text" v-model="form.name">
    <button type="submit" v-show="!updateSubmit">add</button> <!-- jika tidak update maka tombol update tidak muncul -->
    <button @click="update(form)" type="button" v-show="updateSubmit">Update</button>
    <!-- jika tombol edit di klik maka tombol add akan berubah menjadi update -->
</form>

<script>
    /* eslint-disable */
    import axios from 'axios'

    export default {
        data() {
            return {
                users: []
            }
        },
        mounted() {
            this.load()
        },
        methods: {
            load() {
                axios.get('http://localhost:3000/users').then(res => {
                    this.users = res.data //respon dari rest api dimasukan ke users
                }).catch((err) => {
                    console.log(err);
                })
            },
            add() {
                axios.post('http://localhost:3000/users/', this.form).then(res => {
                    this.load()
                    this.form.name = ''
                })
            },
        }
    }
</script>
