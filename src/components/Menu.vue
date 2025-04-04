<template>
<div class="row align-items-center">
    <div class="col">
        <h2 class="mb-0">Academic performance</h2>
    </div>
</div>    

<br>
  <div class="card-body bg-info bg-opacity-10 p-3">
    <li class="list-group-item" v-for="(sub,id) in data_sub" :key="id">
        <h4>{{ sub.name }}</h4>
        <h5>ID of subject : {{ sub.id }}</h5>
        <h5>GRADE : {{ sub.grade }}</h5>
        <h5>CREDIT : {{ sub.credit }}</h5>
        <br>
    </li>
  </div>
</template>

<script>

export default {
    name: "Menu",
    data(){
        return{
            data_sub: [],
            addSelect: false
        }
    },
    mounted() {
        this.fetchData();
    },
    methods: {
        fetchData() {
            fetch(`http://localhost:3000/subject/`)
                .then(res => res.json())
                .then(data=>this.data_sub=data)
                .catch(err => console.error("Fetch error:", err));
        },
    },
}
</script>
<style>
</style>