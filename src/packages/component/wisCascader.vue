<template>
    <Cascader 
        v-model="value"
        :data="data" 
        trigger="hover"
        filterable
        :disabled="disabled"
        @on-change="changeHandle"
    ></Cascader>
</template>
<script>
    export default {
		model: {
			prop: 'value',
			event: 'cv'
		},        
        data () {
            return {
                loading:false,

                // table 数据
                data:[]
            }
        },
        created(){
            this.initHandle();
        },
        methods:{
            /**
             * 初始化
             */
            initHandle: function(){


                // 模拟请求
                setTimeout(()=>{
                    this.data=[{
                        value: 'beijing',
                        label: '北京',
                        children: [
                            {
                                value: 'gugong',
                                label: '故宫'
                            },
                            {
                                value: 'tiantan',
                                label: '天坛'
                            },
                            {
                                value: 'wangfujing',
                                label: '王府井'
                            }
                        ]
                    }, 
                    {
                        value: 'jiangsu',
                        label: '江苏',
                        children: [
                            {
                                value: 'nanjing',
                                label: '南京',
                                children: [
                                    {
                                        value: 'fuzimiao',
                                        label: '夫子庙',
                                    }
                                ]
                            },
                            {
                                value: 'suzhou',
                                label: '苏州',
                                children: [
                                    {
                                        value: 'zhuozhengyuan',
                                        label: '拙政园',
                                    },
                                    {
                                        value: 'shizilin',
                                        label: '狮子林',
                                    }
                                ]
                            }
                        ],
                    }
                    ]

 

                },2000);
            },
            /**
             * change
             */
            changeHandle: function(id){
                this.$emit("cv",id);
            }
        },
        props:{
			value: {
				type: [String,Array,Number,Object]
			}, 
            disabled:{
				type: Boolean,
				default: false
            },
        }
    }
</script>
<style lang="scss">

</style>
