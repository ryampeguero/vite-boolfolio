<script>
import AppHeader from "./partials/AppHeader.vue";
export default {
    components: {
        AppHeader
    }
}
</script>

<template>
    <AppHeader/>
    <router-view></router-view>
</template>