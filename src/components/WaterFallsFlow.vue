<template>
    <div class="waterfallsFlow_container">
        <slot v-for="item in items" :item="item"></slot>
    </div>
</template>

<script>
    export default {
        props: {
            load: {
                type: Function,
                default: function () {
                    throw new Error('你需要为组件定义分页加载的参数')
                }
            }
        },
        name: "WaterFallsFlow",
        data(){
            return {
                items:[],
                page:{
                    total: 0,
                    size: 10,
                    pages: 10,
                    current: 1,
                    records: []
                }
            }
        },
        methods:{
            async loadPage (current, size) {
                this.page = await this.load(current, size)
                this.items.push(...this.page.records)
                this.page.records = []
            },
            async init(){
                this.loadPage();
                //定义窗口滚动事件，计算加载的高度，判断是否到底，到底加载下一页数据。
                const scrollFn = document.onscroll ? document.onscroll : function () {}
                document.onscroll = () => {
                    scrollFn()
                    const scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
                    const clientHeight = document.documentElement.clientHeight;
                    const scrollHeight = document.documentElement.scrollHeight;
                    if(scrollHeight-scrollTop-clientHeight<=0 && this.page.current <this.page.pages){
                        this.loadPage(this.page.current+1, this.page.size)
                    }
                }
            }
        },
        mounted() {
            this.init();
        }
    }
</script>

<style scoped>
    .waterfallsFlow_container{
        width: 100%;
    }
</style>