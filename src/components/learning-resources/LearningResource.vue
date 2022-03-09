<template>
    <li>
        <base-card>
            <header>
                <h3>{{ title }}</h3>
                <base-button class="btn btn-purple" @click="deleteResource">Delete</base-button>
            </header>
            <p>{{ description }}</p>
            <nav class="d-flex justify-content-between">
                <a class="btn link" :href="link">Read More..</a>
                <img :src="icon" :alt="title+' logo'">
            </nav>
        </base-card>
    </li>    
</template>

<script>
export default {
    inject: ['deleteResource'],
  components: ['base-card'],
    props: [
        'title',
        'description',
        'link',
        'icon',
    ],
}
</script>

<style scoped>
li {
    margin: auto;
    max-width: 40rem;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

a.link {
    text-decoration: none;
    background-color: #D2AC47;
    color: #fff;
    box-shadow: none;
}

a.link:hover, a.link:active {
    background-color: #AE8625;
    color: #fff;
}

p {
    margin: 0.5rem 0;
}

h3 {
    font-size: 1.25rem;
    margin: 0.5rem 0;
}

img {
    width: 50px;
    height: auto;
    position: absolute;
    right: 1rem;
    bottom: 1rem;
}
</style>