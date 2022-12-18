<script setup>
import axios from 'axios';
import { ref } from 'vue'
import Good from './Good.vue'

var good = ref({})
var resp = ref({})

function createGood() {
    axios.post('http://localhost:9090/api/goods/', JSON.stringify(good.value), {
        headers: {
            'Content-Type': 'application/json',
        }
    }).then(response => {
        resp.value = response
        console.log(response)
    }).catch((error) => {
        console.log(error)
    })
    console.log(resp.value)
}
</script>

<template>
    <div class="create-good-form">
        <label>Create Good</label>
        <input v-model="good.id" placeholder="Id" />
        <input v-model="good.title" placeholder="Title" />
        <input v-model="good.size" placeholder="Size" />
        <input v-model="good.amount" placeholder="Amount" />
        <input v-model="good.price" placeholder="Price" />
        <input v-model="good.idSupplyRequired" placeholder="Is supply required" />
        <input v-model="good.isDeleted" placeholder="Is deleted" />

        <button class="btn btn-outline-dark" @click="createGood">Create Good</button>
        <Good v-if="resp.status == 200" v-bind="resp.data"/>
    </div>
</template>

<style>
input,
label,
button {
    display: block;
}

input {
    margin-top: 2px;
}
</style>