<script>
import axios from 'axios';

export default {
    data() {
        return {
            projectArray: [],
            imgPath: 'http://127.0.0.1:8000/storage'
        }
    },

    created() {
        axios.get('http://127.0.0.1:8000/api/projects').then((resp) => {
            console.log(resp.data.response);
            this.projectArray = resp.data.response;
        })
    }
}
</script>

<template>
    <div class="container mt-5">
        <div class="row">
            <div v-for="project in projectArray" class="col">
                <div class="card mb-3" style="width: 18rem;">
                    <img v-if="project.image_path !== null" :src="`${imgPath}/${project.image_path}`" class="card-img-top" alt="...">
                    <img v-else src="https://placehold.co/500x300?text=immagine+non+disponibile" alt="">

                    <div class="card-body">
                        <h5 class="card-title">{{ project.title }}</h5>
                        <p class="card-text">{{ project.description }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style></style>
