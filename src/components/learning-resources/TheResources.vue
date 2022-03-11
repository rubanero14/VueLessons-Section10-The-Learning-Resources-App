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
            isDeleted: false,
            results: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'Official Vue JS documentation.',
                    link: 'https://vuejs.org',
                    icon: 'https://w7.pngwing.com/pngs/595/279/png-transparent-vue-js-javascript-library-angularjs-react-vue-js-template-angle-text-thumbnail.png',
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to Google..',
                    link: 'https://google.com',
                    icon: 'https://google.com/favicon.ico',
                },
            ],
        };
    },
    provide() {
        return {
            resources: this.results,
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
        },
    },
    mounted(){
        this.storedResources();
    },
    methods: {
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        
        storedResources(){
            if(this.isDeleted === true){
                fetch('https://vue-http-demo-e06ca-default-rtdb.firebaseio.com/resource-link.json').then((response) => {
                 if(response.ok) {
                    return response.json();
                }
             }).then((data) => {
                 console.log(data);  
                const results = [];
                for (const id in data) {
                    results.push({
                        id: id,
                        title: data[id].title,
                        description: data[id].description,
                        link: data[id].link,
                        icon: data[id].icon,
                    });
                }
                this.results.push(...results);
                console.log(this.results);  
            })} else {
                fetch('https://vue-http-demo-e06ca-default-rtdb.firebaseio.com/resource-link.json').then((response) => {
                 if(response.ok) {
                    return response.json();
                }
             }).then((data) => {
                 console.log(data);  
                const results = [];
                for (const id in data) {
                    results.push({
                        id: id,
                        title: data[id].title,
                        description: data[id].description,
                        link: data[id].link,
                        icon: data[id].icon,
                    });
                }
                this.results.push(...results);
                console.log(this.results);  
            });
            }
        },
        addResource(title, description, link, icon){
            fetch('https://vue-http-demo-e06ca-default-rtdb.firebaseio.com/resource-link.json', {
                method: 'POST',
                header: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify({
                    title: title,
                    description: description,
                    link: link,
                    icon: icon,
                }),
            });
            this.selectedTab = 'stored-resources';
            window.location.reload();
        },
        deleteResource(resId){
            if(resId === 'official-guide' || resId === 'google'){
                const resIndex = this.results.findIndex(resource => resource.id === resId);
                this.results.splice(resIndex, 1);
            } else {
                this.isDeleted = true;
                console.log(this.isDeleted);
                fetch(`https://vue-http-demo-e06ca-default-rtdb.firebaseio.com/resource-link/${resId}.json`, {
                    method: 'DELETE',
                });
                 setTimeout(function(){ location.reload(); }, 1000);
            }
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
