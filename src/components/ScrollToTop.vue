<template>
    <div :style="scrollToTopStyle"
         v-show="isShowToTop"
         @click="scrollToTop"
    >
        <slot></slot>
    </div>
</template>

<script>
    export default {
        name: "ScrollToTop",
        data(){
            return{
                isShowToTop: false,
                scrollToTopStyle:{
                    position:'fixed',
                    top:'',
                    bottom:'10px',
                    left: '',
                    right: '10px'
                },
                timer: null,
            }
        },
        methods:{
            initBindScroll(){
              document.onscroll=((oldHeight)=>{
                  const clientHeight= document.documentElement.clientHeight;
                  return ()=>{
                      const scrollTop =  document.documentElement.scrollTop || document.body.scrollTop
                      if(!this.timer){
                          this.isShowToTop = scrollTop > clientHeight;
                      }
                      if(scrollTop > oldHeight && this.timer){
                          this.timer =  clearInterval(this.timer)
                      }
                      oldHeight = scrollTop;
                  }
              })(0)
            },
            scrollToTop(){
                this.timer = setInterval(()=>{
                    const scrollTop =  document.documentElement.scrollTop || document.body.scrollTop;
                    if (scrollTop<= 0) {
                        this.timer = clearInterval(this.timer)
                        this.isShowToTop = false
                    }
                    const speed = scrollTop/5
                    document.documentElement.scrollTop = document.body.scrollTop = scrollTop - speed
                }, 30)
            }
        },
        mounted(){
            this.initBindScroll()
        }
    }
</script>

<style scoped>

</style>