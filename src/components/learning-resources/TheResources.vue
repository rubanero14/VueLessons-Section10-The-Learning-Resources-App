<template>
    <span>
        <base-card>
            <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
            <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
        </base-card>
        <keep-alive>
            <component :is="selectedTab"></component>
        </keep-alive>
    </span>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
    components: {
        StoredResources,
        AddResource,
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: 
            [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'Official Vue JS documentation.',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to Google..',
                    link: 'https://google.com'
                },
            ],
        };
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.deleteResource,
        };
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'stored-resources'? 'btn-purple p-2' : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resource'? 'btn-purple p-2' : 'flat';
        }
    },
    methods: {
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        addResource(title, description, link){
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: link,
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        deleteResource(resId){
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        },
    },
}
</script>

<style scoped>
div {
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>
