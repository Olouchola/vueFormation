<template>
    <div>
        <button class="bg-green-500 px-2 py-2 rounded text-white" @click="toggleProgress()">
            {{ this.iswatched ? 'Terminé' :'Terminé ?' }}
        </button>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    props:['episodeId','watchedEpisodes'],
    data() {
        return {
            watchedEp:this.watchedEpisodes,
            iswatched:null
        }
    },
    methods: {
        toggleProgress(){
           axios.post('/toggleProgress',{
               episodeId:this.episodeId, 
           })
           .then(response=>{
               if (response.status===200) {
                   this.iswatched=!this.iswatched;
                   //eventBus.$emit('toggleProgress', response.data);
               }
           })
           .catch(error=>console.log(error)); 
        },
        iswatchedEpisodes(){
            return this.watchedEp.find(episode=>episode.id===this.episodeId)? true:false;
        }
    },

    mounted() {
        this.iswatched=this.iswatchedEpisodes();
    },
}
</script>