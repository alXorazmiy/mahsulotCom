<template>
    <div class="menu">
       
            <select v-model = "$i18n.locale" @change="change_language($i18n.locale)">
                <option value="UZ">UZ</option>
                <option value="RU">RU</option>
                <option value="EN">EN</option>
            </select>
            <select v-model = "theme" @change="change_theme">
                <option value="light">{{ $t('light_mode') }}</option>
                <option value="dark">{{ $t('dark_mode') }}</option>
            </select>
            
        
    </div>
</template>

<script setup>
    import { onMounted, ref } from "vue";


    const theme = ref()

    function change_language(lang){
        console.log(lang)
        localStorage.setItem('language', lang)
    }

    function change_theme(){
        if (theme.value == 'light'){
            document.body.classList.remove("dark-mode-variables")
            localStorage.setItem("themeMode", 'light')

        }else{
            document.body.classList.add("dark-mode-variables")
            localStorage.setItem("themeMode", 'dark')
        }   
    }
    onMounted(()=>{
        if(localStorage.getItem("themeMode") == 'light'){
            theme.value = 'light'
            document.body.classList.remove("dark-mode-variables")
        }
        else if (localStorage.getItem("themeMode") == 'dark') {
            console.log('dark')
            theme.value = 'dark'
            document.body.classList.add("dark-mode-variables")
        }
    })

</script>

<style>

</style>