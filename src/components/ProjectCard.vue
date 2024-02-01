<script>
export default {
    data() {
        return {
            projectsServerUrl: 'http://127.0.0.1:8000',
        }
    },
    props: {
        project: Object,
    },
    computed: {
        truncateText() {
            if (this.project.description && this.project.description.length > 100) {
                return this.project.description.substring(0, 100) + '...';
            }
            return this.project.description
        },
    },
    methods: {
        getNoImg() {
            return new URL(`../assets/img/image_not_available.jpg`, import.meta.url).href;
        }
    }
}
</script>

<template>
    <div class="card" style="width: 18rem;">
        <img :src="project.cover_image ? `${projectsServerUrl}/storage/${project.cover_image}` : getNoImg()"
            class="card-img-top" :alt="project.cover_image ? `Poster of ${project.title} project` : 'Image not avaiable'">

        <div class="card-body">
            <h5 class="card-title">{{ project.title }}</h5>
            <p class="card-text">{{ truncateText }}</p>
        </div>

        <ul class="list-group list-group-flush">
            <li class="list-group-item">
                <span class="fw-bold ">
                    Type:
                </span>
                {{ project.type ? project.type.name : 'No type for this project' }}

            </li>
            <li class="list-group-item">
                <span class="fw-bold ">
                    Technologies:
                </span>

                <span v-if="project.technologies > 0">
                    <span v-for="technology in technologies" class="badge bg-light text-dark fs-5" :key="technology.id">
                        {{ count(project.technology) > 0 ? project.technology.name : 'No technologies for this project' }}
                    </span>
                </span>

                <span v-else>
                    No technologies for this project
                </span>

            </li>
        </ul>
    </div>
</template>

<style lang="scss" scoped></style>