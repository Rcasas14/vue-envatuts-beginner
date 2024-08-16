<template>
    <a class="nav-link opacity-75" 
    :class="activeClasses"
    aria-current="page" 
    :href="page.link.url" 
    :title="`This link is ${page.link.text}`">{{ page.link.text }}</a>
</template>

<script>
    export default {
        props: ['page', 'isActive'],
        computed: {
            activeClasses() {
                return {
                    active: this.isActive,
                    emphasize: this.isActive
                };
            }
        },
    }
</script>

<style scoped>
.emphasize {
    text-decoration: underline !important;
}
</style>