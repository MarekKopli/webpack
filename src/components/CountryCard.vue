<template>
    <chart :labels="labels" :data="confirmed"></chart>
</template>

<script>
import axios from 'axios';
import Chart from '../components/Chart.vue';

export default {
  components: { Chart },
    created(){
        axios.get('https://api.covid19api.com/dayone/country/' + this.$route.params.country).then(response => {
            console.log(response.data);
            this.dataset = response.data;
        });
    },
    data(){
        return {
            dataset: []
        }
    },
    computed: {
        labels(){
            let nth = Math.floor(this.dataset.length/50);
            return this.dataset.map(data => data.Date).filter((data, key) => key%nth === 0);
        },
        confirmed(){
            let nth = Math.floor(this.dataset.length/50);
            return this.dataset.map(data => data.Confirmed).filter((data, key) => key%nth === 0);
        }
    }
}
</script>

<style>



</style>