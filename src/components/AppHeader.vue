
<script>
export default {
    data() {
        return {
            links: [
                {
                    name: 'home',
                    title: 'Home'
                },
                {
                    name: 'about',
                    title: 'About Us'
                },
            ]
        }
    }
};
</script>

<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">
                <h2>BoolFolio</h2>
            </a>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item" v-for="link in links" :key="link.title">
                        <router-link :to="{ name: link.name }" class="nav-link">{{ link.title }}</router-link>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<style lang="scss" scoped></style>