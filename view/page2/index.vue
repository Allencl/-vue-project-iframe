<template>
    <div>
        <h1>示例页面222</h1>
    </div>
</template>
<script>
    export default {
        data () {
            return {
            }
        },
        created(){
            // 路由取值
            console.log( this.$route.params );

                this.$Notice.open({
                    title: '路由参数',
                    desc: JSON.stringify(this.$route.params)
                });
            // console.log("刷新了222");
        }        
    }
</script>

<style lang="scss">

</style>