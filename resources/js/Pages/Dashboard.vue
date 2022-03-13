 <template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Dashboard
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
            <div class="w-full ">
            <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="submit">
                <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="title">
                    Titre de la formation
                </label>
                <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="title" type="text" placeholder="Titre de la formation" v-model="form.title">
                <div class="bg-red-200 text-red-800 p-4 my-2"  v-if="errors.title">{{ errors.title }}</div>
                </div>

                <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="title">
                    Description de la formation
                </label>
                <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="description" type="text" placeholder="Description" v-model="form.description"></textarea>
                <div class="bg-red-200 text-red-800 p-4 my-2"  v-if="errors.description">{{ errors.description }}</div>
                </div>
                <div class="mb-4">
                    <h2 class="text-2xl">Episodes de la formation</h2>
                    <div v-for="(episode, index) in form.episodes" v-bind:key="index">
                        <label class="block text-gray-700 text-sm font-bold mb-2" :for="'title-'+index">
                            Titre de l'épisode n° {{index+1}}
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" :id="'title-'+index" type="text" placeholder="Titre de l'episode" v-model="form.episodes[index].title">
                        <div class="bg-red-200 text-red-800 p-4"  v-if="errors['episodes.'+index+'.title']">{{ errors['episodes.'+index+'.title'] }}</div>
                         
                        <label class="block text-gray-700 text-sm font-bold mb-2" :for="'description-'+index">
                            Description de l'épisode n° {{index+1}}
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" :id="'description-'+index" type="text" placeholder="Description de l'episode" v-model="form.episodes[index].description">
                        <div class="bg-red-200 text-red-800 p-4"  v-if="errors['episodes.'+index+'.description']">{{ errors['episodes.'+index+'.description'] }}</div>

                        <label class="block text-gray-700 text-sm font-bold mb-2" :for="'video_url-'+index">
                           Url de la video de l'épisode n° {{index+1}}
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mb-5" :id="'video_url-'+index" type="text" placeholder="Url de la video de l'episode" v-model="form.episodes[index].video_url">
                        <div class="bg-red-200 text-red-800 p-4"  v-if="errors['episodes.'+index+'.video_url']">{{ errors['episodes.'+index+'.video_url'] }}</div>

                          
                    </div>
                </div>

                <div class="flex justify-between items-center">
                    <button class="bg-green-500 rounded py-2 px-4 my-2 text-white " v-if="this.form.episodes.length<15" @click.prevent="add">+</button>
                    <button class="bg-red-500 rounded py-2 px-4 my-2 text-white " v-if="this.form.episodes.length>1" @click.prevent="remove">🗑️</button>
                </div>

                <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                    Créer ma formation
                </button>
            </form>
            </div>     
            </div>
        </div>
    </app-layout>
</template>

<script>
    import { defineComponent } from 'vue'
    import AppLayout from '@/Layouts/AppLayout.vue'

    export default defineComponent({
        props: {
            errors: Object,
        },
        components: {
            AppLayout,
        },
        data() {
            return {
                form:{
                    title:null,
                    description:null,
                    episodes:[
                        {
                            title:null,
                            description:null,
                            video_url:null
                        }
                    ] 
                }
            }
        },
        methods: {
            submit() {
            this.$inertia.post('/courses', this.form)
            },
            add(){
                this.form.episodes.push(
                    {
                            title:null,
                            description:null,
                            video_url:null
                    }
                );

            },
            remove(){
            this.form.episodes.pop();
            }
        },
    })
</script>
