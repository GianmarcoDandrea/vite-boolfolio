<script>
import axios from 'axios';
import ProjectCard from "./ProjectCard.vue";
export default {
    data() {
        return {
            projectsServerUrl: 'http://127.0.0.1:8000',
            projects: [],
        }
    },

    created() {
        axios.get(`${this.projectsServerUrl}/api/projects`)
            .then((resp) => {
                this.projects = resp.data.results.data
                console.log(resp.data.results.data);
            })
    },
    components: {
        ProjectCard
    }

}
</script>

<template>
    <div class="container py-4 text-center">

        <h1 class="mb-5">PROJECTS</h1>

        <div class="row row-cols-1 row-cols-md-3 row-cols-lg-4 g-3">
            <div v-for="project in projects" :key="project.id" class="col">
                <ProjectCard :project="project"/>
            </div>
        </div>

    </div>
</template>

<style lang="scss"></style>