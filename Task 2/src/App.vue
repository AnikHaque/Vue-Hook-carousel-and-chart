<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
let chart = null;
const dataset = [300, 50, 100];
const newItem = ref(16);
const data = {
    labels: [
        'Red',
        'Blue',
        'Yellow'
    ],
    datasets: [{
        label: 'My First Dataset',
        data: dataset,
        backgroundColor: [
            'rgb(255, 99, 132)',
            'rgb(54, 162, 235)',
            'rgb(255, 205, 86)',
            'rgb(43, 105, 86)',
            'rgb(21, 21, 186)',
        ],
        hoverOffset: 4
    }]
};
const config = {
    type: 'pie',
    data: data,
};
onMounted(() => {
    const ctx = document.getElementById('chart');
    chart = new Chart(ctx, config);

});
function updateChart() {
    dataset.push(newItem.value);
    chart.data.datasets[0].data = dataset;
    chart.update();
}
onBeforeUnmount(() => {
    chart.destroy();
});
</script>
<template>
    <div class="container">
        <div class="row d-flex justify-content-center">
            <div class="col-md-4">
                
                <canvas id="chart" width="400" height="400"></canvas>

                <div class="mt-5">
                    <input type="text" class="form-control" v-model="newItem">
                    <button @click="updateChart()" class="btn btn-primary btn-sm mt-2">Add Item</button>
                </div>

            </div>
        </div>
    </div>
</template>