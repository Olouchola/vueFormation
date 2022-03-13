<template>
    <app-layout>
        <template #header>
            Lises des formations
        </template>
        <section class="py-6">
        <div class="mx-6 rounded p-2 mt-4">
            <div class="bg-green-200 text-green-500 p-3 py-3" v-if="$page.props.flash.success"> 
                {{$page.props.flash.success}}
            </div>
        </div>
        <div class="py-3" v-for="course in courseList" v-bind:key="course.id">
             <div class="mx-8 bg-white rounded shadow p-4" >
                <div class="text-sm text-gray-500">Mise en ligne par  {{course.user.name}} - <span class="text-gray-500 text-sm">{{course.participants}} participant <span v-if="parseInt(course.participants)>1">s</span></span> </div>
                <div class="flex justify-between items-center">
                    <div class="text-2xl">{{course.title}}</div>  
                    <div class="text-sm text-gray-400">{{course.episodes_count}} épisodes </div>
                </div>
                <div class="text-sm text-gray-500">{{course.description}}</div>
                <div class="flex items-center justify-between">
                    <a :href="'course/'+ course.id" class="bg-indigo-500 text-white px-2 py1 text-sm mt-3 rounded hover:bg-indigo-700 inline-block">Voir la formation</a>
                    <a :href="'courses/edit/'+ course.id"  class="bg-gray-500 text-white px-2 py1 text-sm mt-3 rounded hover:bg-gray-500 inline-block">Editer</a>
                </div>
            </div>  
        </div>
        </section>
    </app-layout>
</template>

<script>

import AppLayout from './../../Layouts/AppLayout';
export default {

    components:{
        AppLayout
    },

    props:['courses'],
    data() {
        return {
            courseList:this.courses
        }
    },
     
    mounted() {
        console.log(this.courseList);
    },

    methods: {
      
    },
}
</script>