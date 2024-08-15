<template>
    <div>
        <h4>Edit {{ page.pageTitle }} </h4>
        <div class="container mb-3">
            <form action="">
                <div class="mb-3">
                    <label for="" class="form-label">
                        Page Title
                    </label>
                    <input 
                    type="text" 
                    class="form-control"
                    v-model="page.pageTitle"/>
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">
                        Content
                    </label>
                    <textarea 
                    type="text" 
                    rows="5" 
                    class="form-control"
                    v-model="page.content">
                    
                    </textarea>

                </div>
                <div class="mb-3">
                    <label for="" class="form-label">
                        Link Text
                    </label>
                    <input 
                    type="text" 
                    class="form-control"
                    v-model="page.link.text"/>
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">
                        Link Url
                    </label>
                    <input 
                    type="text" 
                    class="form-control"
                    v-model="page.link.url"/>
                </div>
                <div class="mb-3">
                    <div class="form-check">
                        <input 
                        type="checkbox" 
                        class="form-check-input"
                        v-model="page.published"/>
                        <label for="gridCheck1" class="form-label">
                            Published
                        </label>
                    </div>
                </div>
                <div class="mb-3">
                    <button 
                    class="btn btn-primary me-2"
                    @click.prevent="submit">
                        Edit
                    </button>
                    <button 
                    class="btn btn-secondary"
                    @click.prevent="goToPagesList">
                        Cancel
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>

<script setup>
import { useRouter } from 'vue-router';
import { useRoute } from 'vue-router';
import { inject } from 'vue';

const router = useRouter();
const route = useRoute();
const pages = inject('$pages');
const bus = inject('$bus');

const {index} = defineProps(['index']);

const page = pages.getSinglePage(index);
console.log(page);

function submit(){
    pages.editPage(index,page);

    bus.$emit('page-updated',{
        index,
        page
    })
}

function goToPagesList(){
    router.push({path:"/pages"});
}
</script>
