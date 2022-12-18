<script setup>
defineProps({
    "id": Number,
    "title": String,
    "size": String,
    "amount": Number,
    "price": Number,
    "supplyRequired": Boolean
})
</script>

<template>
    <div class="good-block">
        <div>Id: {{ id }}</div>
        <div>Title: {{ title }}</div>
        <div>Size: {{ size }}</div>
        <div>Amount: {{ amount }}</div>
        <div>Price: {{ price }}</div>
        <div>Supply required: {{ supplyRequired }}</div>
    </div>
</template>

<style scoped>
.good-block {
    display: flex;
    flex-direction: column;
    margin-top: 10px;
    margin-bottom: 10px;
    max-width: 30%;
}

div {
    border: 1px solid black;
}
</style>