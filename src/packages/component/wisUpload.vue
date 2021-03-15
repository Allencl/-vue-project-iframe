<template>
    <div>
        <Upload
            :max-size="5"
            :before-upload="handleUpload"
        >
            <Button icon="ios-cloud-upload-outline">
                <span>选择文件</span>
            </Button>
            <Tag v-if="files['length']" color="success" style="margin-left: 12px;">已选 {{files["length"]}}</Tag>
        </Upload>
        <div v-if="files['length']">
            <ul class="wis-upload-container">
                <li v-for="(file,index) in files" :key="index">
                    <span :title="file.name">{{file.name}}</span>
                    <Icon type="md-close-circle" title="删除" @click="deleteHandle(index)" />
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
    export default {
		model: {
			prop: 'value',
			event: 'cv'
		},        
        data () {
            return {
                files: [],  // 文件
                loadingStatus: false
            }
        },
        created(){

        },
        methods:{
            /**
             * 上传
             */
            handleUpload: function(file){

                // 限制 类型
                if( this.accept["length"] && !this.accept.filter(o=>o.toLowerCase()==(file["name"].split(".")[1].toLowerCase()) )['length'] ){
                    this.$Message.info(`不支持文件类型 ${file["name"].split(".")[1]}`);
                    return false;  
                }

                // 限制大小
                if( parseInt(file["size"]/1024) > this.maxSizeKB ) {
                    this.$Message.info(`文件不能大于 ${this.maxSizeKB}kb`);
                    return false;                    
                }

                // 限制数量
                if(this.maximum && this.files["length"]>=this.maximum){
                    this.$Message.info(`文件数量不能超过 ${this.maximum}`);
                    return false;
                }

                this.files=this.files.concat([file]);
                return false;
            },
            /**
             * 删除
             */
            deleteHandle: function(index){
                this.files=this.files.filter((o,i)=>i!=index);
            }
        },
        props:{
			value: {
				type: [String,Array,Number,Object]
			}, 
            // 限制 数量
            maximum:{
				type: Number,
				default: ()=> 0
            },
            // 限制 大小  KB
            maxSizeKB:{
				type: Number,
				default: ()=> 0                
            },
            // 限制 类型
            accept:{
				type: Array,
				default: ()=> []  
            },
            disabled:{
				type: Boolean,
				default: false
            },
        }
    }
</script>
<style lang="scss">
    .wis-upload-container{
        li{
            list-style: none;
            position: relative;
            padding-right: 36px;
            height: 32px;
            line-height: 32px;

            span{
                width: 100%;
                display: inline-block;
                overflow: hidden;
                white-space: nowrap;
                text-overflow: ellipsis;
            }

            .ivu-icon{
                position: absolute;
                top: 6px;
                right: 8px;
                cursor: pointer;
                font-size: 20px;
                transition: all 0.5s;


                &:hover{
                  transform: scale(1.2,1.2);
                  color: #993333;
                }
            }
        }
    }
</style>
