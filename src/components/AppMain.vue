<script>
import axios from "axios";
import { RouterLink } from "vue-router";

export default {
  data() {
    return {
      projectArray: [],
      imgPath: "http://127.0.0.1:8000/storage",
      lastPage: 0,
      curPage: 0,
    };
  },

  created() {
    this.getPost();
  },

  methods: {
    getPost() {
      axios
        .get("http://127.0.0.1:8000/api/projects", {
          params: {
            page: this.curPage,
          },
        })
        .then((resp) => {
          console.log(resp.data.results.data);
          this.projectArray = resp.data.results.data;
          this.lastPage = resp.data.results.last_page;
        });
    },
    changePage(newPage) {
      // console.log(newPage);
      this.curPage = newPage;
      console.log(this.curPage);
      this.getPost();
    },
    showNext() {
      console.log("next ", this.curPage);
      if (this.curPage <= this.lastPage) {
        this.getPost();
      } else {
        this.curPage = 4;
      }
    },

    showPrev() {
      console.log("previous ", this.curPage);
      if (this.curPage >= 1) {
        this.getPost();
      } else {
        this.curPage = 1;
      }
    },
  },
};
</script>

<template>
  <div class="container mt-5">
    <h1>Progetti</h1>
    <div class="row">

      <div v-for="project in projectArray" class="col">
        <RouterLink :to="{ name: 'single-project', params: { 'slug': project.slug } }">
          <div class="card mb-3" style="width: 18rem">
            <img v-if="project.image_path !== null" :src="`${imgPath}/${project.image_path}`" class="card-img-top"
              alt="..." />
            <img v-else src="https://placehold.co/500x300?text=immagine+non+disponibile" alt="" />

            <div class="card-body">
              <h5 class="card-title">{{ project.title }}</h5>
              <p class="card-text">{{ project.description }}</p>
            </div>
          </div>
        </RouterLink>
      </div>
    </div>
    <div class="mt-5 d-flex justify-content-center">
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li @click.prevent="showPrev(--curPage)" :disabled="curPage === 1" class="page-item">
            <a class="page-link" href="#">Previous</a>
          </li>

          <li v-for="page in lastPage" @click.prevent="changePage(page)" class="page-item"
            :class="curPage === page ? 'active' : ''">
            <a class="page-link" href="#">{{ page }}</a>
          </li>

          <li @click.prevent="showNext(++curPage)" :disabled="curPage === lastPage" class="page-item">
            <a class="page-link" href="#">Next</a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<style></style>
