<template>
    <div>
        <h1>示例页面333</h1>
        <button @click="toPage">跳转测试</button>
    </div>
</template>
<script>
    export default {
        data () {
            return {
            }
        },
        created(){
            // console.log("刷新了111");
        },
        methods:{
            toPage: function(){
                this.$router.push({
                    name:'page2',
                    params:{
                        id:11,
                        name:"路由参数",
                        refresh:true,   // 强制刷新 页面  
                    },
                });
            }
        }
    }
</script>

<style lang="scss">

</style>