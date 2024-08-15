<template>
    <nav 
                class="navbar navbar-expand-lg"
                :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
            >
                <dev class="container-fluid">
                    <a href="#" class="navbar-brand">My Vue</a>
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <navbar-link
                            v-for="(page,index) in publishedPages" class="nav-item" :key="index"
                            :page = "page"
                            :index="index"
                            @actived = "$emit('actived')"
                        ></navbar-link>
                    </ul>
                    <form class="d-flex">
                        <button 
                            class="btn btn-primary"
                            @click.prevent="ChangeTheme()"
                        >Toggle Navbar</button>
                    </form>
                </dev>
            </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';
export default {
  components: { NavbarLink },
    data(){
        return{
            theme:'dark',
            pages:[]
        };
    },
    inject:['$pages','$bus'],
    created() {
        this.GetThemeSetting();

        this.pages = this.$pages.getAllPages();

        this.$bus.$on('page-updated',()=>{
            this.pages = [...this.$pages.getAllPages()];
        })
    },
    computed:{
        publishedPages(){
            return this.pages.filter(p=>p.published)
        }
    },
    methods: {
        ChangeTheme(){
            let theme = 'light';

            if(this.theme == 'light'){
                theme='dark';
            }

            this.theme = theme;
            this.StoreThemeSetting();
        },
        StoreThemeSetting(){
            localStorage.setItem('theme',this.theme);
        },
        GetThemeSetting(){
            let theme = localStorage.getItem('theme');

            if(theme){
                this.theme = theme;
            }
        }
    },
}
</script>
