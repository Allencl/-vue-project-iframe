<template>
    <div style="height:100%">
        <Menu
            width="auto"
            style="height:100%"
            @on-select="selectHandle"
        >
            <menu-sun :menus="menuData"/>
        </Menu>
    </div>
</template>
<script>
import MenuSun from "@src/layout/menuList.vue";
export default {
    components: {
        MenuSun
    },
    data() {
        return {
            // 菜单 数据
            // menuList: [
            //     {
            //         name: "SRM平台",
            //         id: "1",
            //         children: [
            //             {
            //                 id:"1-1",
            //                 name: "页面1", 
            //                 platform:'',
            //                 icon:"logo-buffer",
            //                 pathURL:"page1/qwqwq"            
            //             },
            //         ]
            //     },
            //     {
            //         name: "质量平台",
            //         id: "2",
            //         children: [
            //             {
            //                 id:"2-1",
            //                 name: "页面22", 
            //                 platform:'',
            //                 icon:"logo-buffer",
            //                 pathURL:"page2/qwqwq"            
            //             },
            //         ]
            //     },                
            //     // {
            //     //     name: "一级菜单",
            //     //     id: "1",
            //     //     children: [
            //     //         {
            //     //             id:"1-1",
            //     //             name: "表单示例", 
            //     //             icon:"logo-buffer",
            //     //             pathName:"page1"            
            //     //         },
            //     //         {
            //     //             name: "二级菜单",
            //     //             id: "1-2",
            //     //             children: [
            //     //                 {
            //     //                     name: "跳转示例1", 
            //     //                     id: "1-2-1",
            //     //                     icon:"ios-analytics",
            //     //                     pathName:"page2"            
            //     //                 }
            //     //             ]
            //     //         },
            //     //         {
            //     //             id:"1-3",
            //     //             name: "跳转示例2", 
            //     //             icon:"logo-buffer",
            //     //             pathName:"page3"            
            //     //         },
            //     //     ]
            //     // }
            // ]
        };
    },
    methods:{
        /**
         * 菜单 点击
         */
        selectHandle: function(option){
            this.$emit("addMenuHandle",option);
        }
    },
    props:{
        menuData:{
            type: Array,
            default:()=>[]
        }
    }
};
</script>