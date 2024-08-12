<template>
    <navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index)=>{activePage=index}"></navbar>

    <router-view>
        
    </router-view>
    <!--<page-viewer
    v-if="pages.length >0"
        :page="pages[activePage]"
    ></page-viewer> 
    <create-page
    @page-created ="pageCreated"
    ></create-page>-->
</template>

<script>
import CreatePage from './components/CreatePage.vue';
import Navbar from './components/Navbar.vue';
import PageViewer from "./components/PageViewer.vue"

export default {
    components:{
        PageViewer,
        CreatePage,
        Navbar,
    },
    created() {
        this.getPages();

        this.$bus.$on('navbarLinkActived',(index)=>{this.activePage=index})
    },
    data(){
        return{
            activePage: 0,
            pages: []  
                    
        };
    },
    methods: {
        async getPages(){
            let res = await fetch('page.json');
            let data = await res.json();

            this.pages = data;
        },
        pageCreated(pageObj){
            this.pages.push(pageObj);
        }
    },
}

</script>
