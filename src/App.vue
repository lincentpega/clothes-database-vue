<script setup>
import { ref, watchEffect } from 'vue'
import axios from 'axios';

import Good from './components/Good.vue'
import CreateGood from './components/CreateGood.vue';

const good_arr = ref([]);
const id = ref();

const size = ref('')
const id_to_delete = ref()

watchEffect(() => {
  if (id.value) {
    axios
      .get(`http://localhost:9090/api/goods/${id.value}`)
      .then((r) => {
        good_arr.value = [r.data];
      })
  }
})

watchEffect(() => {
  if (size.value) {
    axios
      .get(`http://localhost:9090/api/goods/?size=${size.value}`)
      .then((r) => {
        good_arr.value = r.data
      })
  }
})

function del() {
  axios
    .delete(`http://localhost:9090/api/goods/${id_to_delete.value}`)
}
</script>

<template>
  <div class="main-flex">
    <div class="all-inp">
      <div class="inp-unit">
        <label>Find by id</label>
        <input class="inp-field" v-model="id" placeholder="Enter good id" />
      </div>
      <div class="inp-unit">
        <label>Find by size </label>
        <input class="inp-field" v-model="size" placeholder="Enter good size" />
      </div>
      <div class="inp-unit">
        <label>Delete by id</label>
        <input class="inp-field" @keyup.enter="del" v-model="id_to_delete" placeholder="Enter id to delete" />
        <button class="btn btn-outline-dark" @click="del">Delete item</button>
      </div>
    </div>
    <Good class="good-item" v-for="good in good_arr" v-bind="good" />
    <CreateGood class="create-good-form" />
  </div>
</template>

<style>
.main-flex {
  display: flex;
  flex-direction: column;
  margin-left: 20px;
}

input,
label {
  display: block;
}

.inp-unit {
  margin: 10px 0px;
}

.all-inp {
  float: left;
  margin-right: 10px;
}


label {
  color: darkgoldenrod;
  font-weight: bold;
}

input[type="text"] {
  border: 1px solid #cccccc;
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  -khtml-border-radius: 3px;
  background: #ffffff !important;
  outline: none;
  height: 24px;
  width: 120px;
  color: #cccccc;
  font-size: 11px;
  font-family: Tahoma;
}
</style>