<template>
    <div>
        <p v-for=" i in 50" :key="i">我是第 {{i}} 行</p>
        <ScrollToTop>
            <button>返回顶部</button>
        </ScrollToTop>
    </div>
</template>

<script>
    import ScrollToTop from './ScrollToTop'
    export default {
        name: "ScrollTopComponent",
        components:{
            ScrollToTop,
        }
    }
</script>

<style scoped>

</style>