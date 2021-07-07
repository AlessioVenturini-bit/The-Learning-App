<template>
<base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resources')" :mode="addResButtonMode">Add Resources</base-button>
</base-card>
<component :is="selectedTab"></component>
</template>

<script>
import AddResources from './AddResources.vue'
import StoredResources from './StoredResources.vue'
export default {
    components: {
        AddResources,
        StoredResources
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [{
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue js Documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn how to use Google',
                    link: 'https://google.com'
                },

            ]
        }
    },
    provide() {
        return {
            resources: this.storedResources,
            addResourceData: this.addResourceData,
            removeResourceData: this.removeResourceData
        }
    },
    computed:{
        storedResButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat'
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resources' ? null : 'flat'
        },

    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab
        },
        addResourceData(title,description,link){
            const newResource = 
            {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: link
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources'
        },
        removeResourceData(resId){
            console.log(resId)
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            console.log(resIndex)
            this.storedResources.splice(resIndex, 1)
        }
    },

}
</script>

<style lang="">
    
</style>
