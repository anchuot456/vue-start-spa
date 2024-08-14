<template>
    <li>
        <router-link 
            :to="`/${index}`"
            :title="`This link lead to ${page.link.text} page`"
            class="nav-link" 
            active-class="active"
            aria-current="page"
        >{{page.link.text}}</router-link>
    </li>
    
</template>

<script>
export default{
    props:['page','index'],
    
}
</script>
