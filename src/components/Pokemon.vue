<template>
    <div id="pokemon">
          <div class="card">
        <div class="card-image">
            <a href=""><i class="fas fa-arrow-right"></i></a>
            <figure class="">
                <img :src="currentImg">
            </figure>
            <span class="icon">
    <i class="fas fa-arrow-right"></i>
  </span>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4">{{index}}. {{ name | toUpper }}</p>
                <p class="subtitle is-6">{{ pokeInfo.type }}</p>
            </div>
            </div>

            <div class="content">
                <button class="button is-medium is-fullwidth" @click="mudarSprite">Change Sprite</button>
            </div>
        </div>
        </div>
    </div>
  
</template>

<script>
import axios from 'axios';

export default {
    data(){
        return {
            isFront: true,
            currentImg: "",
            pokeInfo: {
                type: "",
                back: "",
                front: ""
            }
        }
    },
    created: function(){
        axios.get(this.url).then(response => {
            this.pokeInfo.type = response.data.types[0].type.name;
            this.pokeInfo.back = response.data.sprites.back_default;
            this.pokeInfo.front = response.data.sprites.front_default;
            this.currentImg = this.pokeInfo.front
            console.log(this.pokeInfo)
            
        })
    },
    props: {
        name: String,
        url: String,
        index: Number
    },
    filters: {
        toUpper: function(value) {
            let newName = value[0].toUpperCase() + value.slice(1)
            return newName 
        }
    },
    methods: {
        mudarSprite: function(){
            if(this.isFront == true){
                this.currentImg = this.pokeInfo.back
                this.isFront = false
            } else {
                this.currentImg = this.pokeInfo.front
                this.isFront = true
            }
        }
    },
}
</script>

<style>
#pokemon{
    margin-top: 2%;
}
</style>