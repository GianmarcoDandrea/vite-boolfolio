<script>
import axios from 'axios';
import ProjectCard from "../components/ProjectCard.vue";
import { store } from "../store";
export default {
    data() {
        return {
            store,
            projects: [],
            curPage: 1,
            lastPage: 1,
            total: 0, 
            page_count : 2,
        }
    },

    created() {
        this.getProjects(1);
    },
    components: {
        ProjectCard
    },

    mounted() {
        const container = document.querySelector('.container');
        if (container.length && (Math.ceil(window.scrollTop()) + 1) >= Math.ceil(document.height() - window.height()) && scroll == false) {
            console.log('ciao');
            // getNextBatch(page_count)
        }
    },

    methods: {
        getProjects(pageNum) {

            this.curPage = pageNum;


            axios.get(`${this.store.projectsServerUrl}/api/projects`, {
                params: {
                    page: pageNum,
                },
            })
                .then((resp) => {
                    this.projects = resp.data.results.data;
                    this.lastPage = resp.data.results.last_page;
                });

            window.scrollTo(0, 0);
        },

        getNextBatch(page_count) {
            this.loading = true;
            axios.get(`${this.store.projectsServerUrl}/api/projects`, {
                params: {
                    page: page_count,
                },
            })
                .then((resp) => {
                    this.projects = resp.data.results.data;
                    this.lastPage = resp.data.results.last_page;
                });

            this.projects.push(project)

            this.loading = false;
        },
    }
}
</script>

<template>
    <div class="container py-4 text-center">

        <h1 class="mb-5">PROJECTS</h1>

        <div class="row row-cols-1 row-cols-md-3 row-cols-lg-4 g-3">
            <div v-for="project in projects" :key="project.id" class="col">
                <ProjectCard :project="project" />
            </div>
        </div>

        <div class="my-4 ">
            <button class="btn btn-dark me-3" :disabled="curPage === 1" href="" @click="getProjects(curPage - 1)">
                Prev
            </button>

            <button class="btn btn-dark mx-1" :class="{ 'disabled': num === curPage }" v-for="num in lastPage"
                @click="getProjects(num)">
                {{ num }}
            </button>

            <button class="btn btn-dark ms-3" href="" :disabled="curPage === lastPage" @click="getProjects(curPage + 1)">
                Next
            </button>
        </div>
    </div>
</template>

<style lang="scss"></style>