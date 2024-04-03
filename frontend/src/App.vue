<template>
    <div>
        <div class = "app-loader" v-show = 'loader'>
            <Loader />
        </div>
        <div class = 'sidebar-container' v-if = "controllerStore.is_admin">
            <Sidebar />
        </div>
        <div class="menu-container" v-if = "controllerStore.is_admin">
            <Menu />
        </div>
        <div class = 'page-container' :class = "controllerStore.is_admin == false ? 'full-screen' : controllerStore.sidebar_open == true ? 'page-active' : '' " >
            <div class="page-loader" v-show = "controllerStore.page_loader">
                <Loader />
            </div>
            <RouterView />
        </div>
    </div>
</template>


<script setup>
    import { RouterLink, RouterView } from 'vue-router'
    import AdminPage from './views/admin/adminPage.vue'
    import Sidebar from './components/sidebar.vue'
    import Menu from './components/menu.vue'

    import Loader from './components/loader.vue'
    import { useRouter } from 'vue-router';
    import { onMounted, ref } from 'vue';
    import {useControllerStore} from './stores/controller'
import axios from 'axios'
import { useUserStore } from './stores/users'

    const router = useRouter()
    const controllerStore = useControllerStore()
    const userStore = useUserStore()
    const loader = ref(true)

    onMounted(()=>{


        axios.get('login/', {
            headers : {
                'Authorization' : `token ${localStorage.getItem('access_token')}`
            }
        })
            .then((data)=>{
                if(data.status == 200){
                    console.log(data.data)
                    controllerStore.is_admin = true
                    userStore.admin = data.data.role
                    console.log(data.data.role)

                }             
                else{
                }

            })
            .catch((error)=>{
                router.push('login')

            })
        
        loader.value = false


    })


</script>



<style scoped>

/* nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
} */

</style>
