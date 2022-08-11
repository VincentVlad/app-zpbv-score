<template>
    <div class="post" v-for="team in localData" :key="team.id">
        <h4>{{team.name}}</h4>
        <input class="padding" placeholder="">
        <h3 class="padding">Очки {{team.point}}</h3>
        <h3 class="padding">Партия {{team.sets}}</h3>
        <div>
            <button v-on:click="increase(team.id), updatePoint(team.id)" class="btn"><h4>+1</h4></button>
            <button v-on:click="minusPoint(team.id)" class="btn"><h4>-1</h4></button>
        </div>
        <button disabled class="time-out">TimeOut (onwork)</button>
        </div>
</template>

<script>
import axios from "axios"
const API_URL = "http://192.168.0.33:3000/teams";

    export default {
        data() 
        {
            return {
            teams: [],
            localData: [
                {id: 1, name: "team1", point: 0, sets: 0,},
                {id: 2, name: "team2", point: 0, sets: 0,}
            ],
            }
        },
        mounted() {
            fetch(API_URL)
            .then(res => res.json())
            // .then(data => this.teams=data)
            .catch(err => consol.log(err.message))
        },
        
        methods: {
            increase(id) {
             this.localData = this.localData.map(team => {
                if (team.id === id) {
                team.point++;
            }
                return team
             })
                },


            async updatePoint(id) {
            try {
                let data = JSON.parse(JSON.stringify(this.localData))
                                
                await axios.patch(`${API_URL}/${id}`, {
                    id: data[id-1].id,
                    name: data[id-1].name,
                    point: data[id-1].point,
                    sets: data[id-1].sets,             
                 })

      } catch (e) {
        console.error(e);
      }
    }
        
        }
        }
</script>

<style>
body {
    background-color: rgb(6, 4, 42);
}

.post {
    background-color: rgb(33, 51, 77);
    display: block;
    border: 1px solid green;
    border-radius: 8px;
    margin: 20px;
    padding: 8px;
    box-shadow: 0px 0px 15px rgb(90, 255, 170);
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
    background-color: rgb(20, 16, 68);
    border:1px solid rgb(87, 220, 235);
    border-radius: 8px;
    margin-bottom: 20px;
    color: rgb(86, 152, 217);
    margin-right: 8px;
}

.time-out {
    width: 250px;
    height: 50px;
    align-content: center;
    margin-bottom: 20px;
    border-radius: 8px;
}

h1,h2,h3,h4,h5,p{
    color: white;
}


</style>
