<script>
import axios from 'axios';
import { store } from '../store';
import { DateTime } from 'luxon';


export default {
    data() {
        return {
            store,
            project: null,
            loading: true
        }
    },
    created() {
        axios.get(`${store.projectsServerUrl}/api/projects/${this.$route.params.slug}`)
            .then((resp) => {
                this.project = resp.data.results;
            })
            .finally(() => {
                this.loading = false
            })
    },

    methods: {
        getNoImg() {
            return new URL(`../assets/img/image_not_available.jpg`, import.meta.url).href;
        }
    },

    computed: {
        addedDate() {
            if (this.project)
                return DateTime.fromISO(this.project.created_at).toFormat('dd LLLL yyyy');
        },
        updatedDate() {
            if (this.project)
                return DateTime.fromISO(this.project.updated_at).toFormat('dd LLLL yyyy');
        }

    }
}
</script>

<template>
    <div class="container py-5">

        <h1 class="text-center" v-if="loading">Loading...</h1>

        <div v-else>
            <!-- Go Back button -->
            <div class="d-flex justify-content-end mb-3">
                <router-link class="btn btn-dark fs-5" :to="{ name: 'home' }">Go Back</router-link>
            </div>

            <!-- Project details -->
            <div class="d-flex flex-column justify-content-between align-items-start w-75 mx-auto">
                <div>
                    <h2 class="fs-2 mb-5 text-center">{{ project.title }}</h2>
                </div>

                <div class="mx-auto w-50 d-flex justify-content-center mb-4">
                    <img :src="project.cover_image ? `${store.projectsServerUrl}/storage/${project.cover_image}` : getNoImg()"
                        class="align-self-center"
                        :alt="project.cover_image ? `Poster of ${project.title} project` : 'Image not avaiable'">
                </div>


                <div class="mb-3">
                    <span class="fw-bold fs-5">Type: </span>

                    <span class="fs-5">
                        {{ project.type ? project.type.name : 'No type for this project' }}
                    </span>
                </div>

                <div class="mb-3">
                    <span class="fw-bold fs-5">Technologies: </span>

                    <span v-if="project.technologies.length > 0">
                        <span v-for="technology in project.technologies" class="badge bg-light text-dark fs-5"
                            :key="technology.id">
                            {{ technology.name }}
                        </span>
                    </span>

                    <span v-else class="fs-5">
                        No technologies for this project
                    </span>

                </div>

                <div class="mb-3">
                    <span class="fw-bold fs-5">Description: </span>

                    <span class="fs-5">
                        {{ project.description }}
                    </span>
                </div>

                <div class="mb-3">
                    <span class="fw-bold fs-5">Added On: </span>

                    <span class="fs-5">
                        {{ addedDate }}
                    </span>
                </div>

                <div class="mb-3" v-if="project.updated_at != project.created_at">
                    <span class="fw-bold fs-5">Updated On: </span>

                    <span class="fs-5">
                        {{ updatedDate }}
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss"></style>