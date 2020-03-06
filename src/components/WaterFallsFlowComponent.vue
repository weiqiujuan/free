<template>
    <WaterFallsFlow :load="load">
        <template slot-scope="{item}">
            <li
                    class="item-style"
                    :key="item.id"
            >
                {{item.text}}
            </li>
        </template>
    </WaterFallsFlow>
</template>

<script>
    import WaterFallsFlow from "./WaterFallsFlow";
    import _ from 'lodash'
    export default {
        name: "WaterFallsFlowComponent",
        components: {
            WaterFallsFlow
        },
        methods: {
            await: ms =>new Promise(resolve => setTimeout(resolve, ms)),
            load: (page => {
                return async function() {
                    await this.await(1000)
                    page.records = _.range((page.current-1)*page.size+1, (++page.current-1)* page.size+1)
                    .map(i=>({ id: i , text: `第 ${i} 行内容`}))
                    return page
                }
            })({
                current: 1,
                size: 10,
                pages: 100,
                total: this.current * this.pages,
                records: []
            })
        }
    }
</script>

<style>
    li {
        width: 500px;
        height: 100px;
        text-align: center;
        line-height: 100px;
        background-color: aqua;
        margin: 10px auto;
        list-style-type: none;
    }
</style>