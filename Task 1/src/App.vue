<script setup>
import { nextTick, onMounted, onBeforeUnmount, ref } from 'vue';
const items = ref([
    'https://images.unsplash.com/photo-1472214103451-9374bd1c798e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80',
    'https://images.unsplash.com/photo-1426604966848-d7adac402bff?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80',
    'https://images.unsplash.com/photo-1475924156734-496f6cac6ec1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80',
    'https://plus.unsplash.com/premium_photo-1675368244123-082a84cf3072?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1850&q=80',
    'https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80'
]);
let carousel = null;
const newItem = ref('https://images.unsplash.com/photo-1465189684280-6a8fa9b19a7a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80')
function addNewItem() {
    items.value.push(newItem.value);
    carousel.destroy();
    nextTick(() => {
        carousel = new Flickity('#carousel',{
            freeScroll: true,
            wrapAround: true
        })
    })
}
onMounted(() => {
    carousel = new Flickity('#carousel',{
        freeScroll: true,
        wrapAround: true
    })
});
onBeforeUnmount(() => {
    if (carousel) {
        carousel.destroy();
    }
});
</script>
<template>
    <div class="main">
        <div class="container">
            <div class="row d-flex justify-content-center">
                <div class="col-md-6">
                    <h2 class="text-center mt-3">Carousel</h2>
                    <div id="carousel">
                        <div :style="`background-image:url(${item})`" class="item" v-for="item, index in items" :key="item"></div>
                    </div>
                    <div class="new-item-add mt-5">
                        <input type="text" class="form-control" v-model="newItem">
                        <button @click="addNewItem()" class="btn btn-primary btn-sm mt-2">Add Item</button>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
.items {
    width: 600px;
    height: 400px;
}
.item {
    width: 600px;
    height: 400px;
    background-color: #ccc;
    background-size: cover;
}
</style>