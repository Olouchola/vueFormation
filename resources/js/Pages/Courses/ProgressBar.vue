<template>
    <div>
        <div class="bg-gray-200 w-full rounded">
            <div class="bg-green-500 text-white rounded-l text-center transition-width duration-500" :style="'width:'+percentage+'%'">
              {{percentage}}% 
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props:['watchedEpisodes','episodes'],
    data() {
        return {
           watchedEpisodesData:this.watchedEpisodes, 
        }
    },
    computed: {

        percentage(){
          let filterEp= this.episodes.filter(courseEp=>{
             return this.watchedEpisodesData.find(watchedEP=>{
                return watchedEP.id==courseEp.id;
              });
          });
          return Math.ceil(filterEp.length/this.episodes.length*100);
        }

    },
    mounted() {
        console.log(this.watchedEpisodes,this.episodes );
        //eventBus.$on('toggleProgress',data=>this.watchedEpisodesData=data);
    },
}
</script>