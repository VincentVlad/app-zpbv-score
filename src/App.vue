<template>
    <div class="post" v-for="team in teams" :key="team.id">
        <h4>{{team.name}}</h4>
        <input class="padding" placeholder="">
        <h3 class="padding">Очки {{team.point}}</h3>
        <h3 class="padding">Партия {{team.sets}}</h3>
        <div>
            <button v-on:click="addPoint" class="btn"><h4>+1</h4></button>
            <button class="btn"><h4>-1</h4></button>
        </div>
        <button disabled class="time-out">TimeOut (onwork)</button>
        </div>
</template>

<script>
    export default {
        data() 
        {
            return {
            teams: [],
            }
        },
        mounted() {
            fetch('http://localhost:3000/teams')
            .then(res => res.json())
            .then(data => this.teams=data)
            .catch(err => consol.log(err.message))
        },
        methods: {

        }
        
    }
</script>

<style>
body {
    background-color: rgb(6, 4, 42);
}

.post {
    background-color: rgba(169, 169, 169, 0.44);
    display: block;
    border: 1px solid green;
    border-radius: 8px;
    margin: 20px;
    padding: 8px;
}

.post input {
    width: 100px;
    height: 30px;
}

.padding {
margin-right: 8px;
}

.btn {
    width: 50px;
    border-radius: 8px;
    margin-bottom: 20px;
}

.time-out {
    width: 250px;
    height: 50px;
    align-content: center;
    margin-bottom: 20px;
    border-radius: 8px;
}



</style>
