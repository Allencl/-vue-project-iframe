<template>
    <Select 
        v-model="value"
        placeholder="请选择"
        :multiple="multiple"
        :disabled="disabled"
        @on-change="changeHandle"
        :loading="loading"
    >
        <Option 
            v-for="(o,index) in data" 
            :value="o['id']"
            :key="index"
        >{{o["label"]}}</Option>
    </Select>    
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
                this.loading=true;

                // 模拟请求
                setTimeout(()=>{
                    this.data=[
                        {
                            id: 1,
                            label: '北京',
                        },
                        {
                            id: 2,
                            label: '厦门',
                        },
                        {
                            id: 3,
                            label: '南京',
                        },                        
                    ];

                    this.loading=false;

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
            // 多选
            multiple:{
				type: Boolean,
				default: false
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
