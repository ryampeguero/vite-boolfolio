<script>
import axios from 'axios';

export default {
    data() {
        return {
            project: null,
            slug: this.$route.params.slug
        }
    },
    created() {
        console.log(this.slug);
        axios.get(`http://127.0.0.1:8000/api/projects/${this.slug}`).then((resp)=>{
            console.log(resp.data.results);
            this.project = resp.data.results;
        }).catch((error)=>{
            console.log(error.response);
        });
    }
}
</script>

<template>
    <div class="container">
        <h1>Progetto singolo</h1>
        <div class="row">
            <div class="col">
                <h2>{{ project.title }}</h2>
                <p>{{ project.description }}</p>
                <h4>Tecnologie:</h4> 
                <div class="d-flex gap-3">
                    <span v-for="technology in project.technologies" class="badge text-bg-secondary">{{ technology.name }}</span>
                </div>
                    
            </div>
        </div>
    </div>
</template>