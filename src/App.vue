<template>
  <div id="app">

    <div class="layout">
        <Layout>
            <Header>
              <WisHeader 
                @goHome="goHome"
              />
            </Header>
            <Layout>
                <Sider hide-trigger :style="{background: '#fff'}">
                  <WisMenu 
                    :menuData="menuList"
                    @addMenuHandle="addMenuHandle"
                  />
                </Sider>
                <Layout class="wis-content-container" 
                  :style=" tabsArray ?
                    {background:'#fff',padding:'46px 0px 0px 0px'}:
                    {background:'#fff',padding:'0px 0px 0px 0px'}
                  "
                >
                    <div class="wis-tabs-container">
                      <WisTabs 
                        @changeTabs="changeTabs"
                        @goHome="goHome"
                      />
                    </div>
                    <Content 
                      v-show="showPlatform"
                      :style="{overflow:'auto',height:documentHeight+'px',padding: '8px 8px', minHeight: '280px', background: '#fff'}"
                    >
                        <div class="content-iframe">
                          <iframe 
                            v-for="(o,index) in menuList" 
                            :key="index"
                            :src="o.platformHttps" 
                            :ref="o.platformName"
                            :class="(showPlatform==o.platformName)?'show':''"
                            frameborder="0"
                          >
                          </iframe>
                      </div>
                    </Content>
                    <Content 
                      v-show="!showPlatform"
                      :style="{overflow:'auto',height:documentHeight+'px',padding: '8px 8px', minHeight: '280px', background: '#fff'}"
                    >
                      <keep-alive>
                        <router-view v-if='$route.meta.keepAlive'></router-view>
                      </keep-alive>
                      <router-view v-if='!$route.meta.keepAlive'></router-view>
                    </Content>
                </Layout>
            </Layout>
        </Layout>
    </div>
  </div>
</template>

<script>
import WisHeader from '@src/layout/header.vue';  // 头
import WisMenu from '@src/layout/menu.vue';  // 菜单
import WisTabs from '@src/layout/tabs.vue';  // tabs



export default {
  name: 'App',
  components: { 
    WisHeader, 
    WisMenu,
    WisTabs
  },
  data(_this) {
    return {
      showPlatform:'',  // 显示的 platform
      menuList:[],  // 菜单
      isRefresh:true,  // 刷新
      documentHeight:document.documentElement.clientHeight-(_this.tabsArray?116:68),  // 窗口高度
    }
  },
  computed: {
    tabsArray(){
      return this.$store.state.storeTabs.tbasList["length"];
    }     
  },   
  watch:{
    // 监听 tabs
    "$store.state.storeTabs.tbasList"(val){
      this.updataWindow();
    },
  },   
  created(){
    var that=this;
    
    this.menuInit();   // 菜单初始化
    // this.$router.push({name:'home',params:{}});

    window.onresize = function(){ 
      that.updataWindow();
    };

    /**
     * 页面跳转 监听
     */
    // this.$router.beforeEach((to, from, next) => {
    //     let tabsList=that.$store.state.storeTabs.tbasList;
    //     let action=tabsList.filter(o=>o["name"]==to['name']);

    //     // 已存在 
    //     if(action["length"]){
    //       that.$store.dispatch("selectTabs",to["name"]);
    //     }else{
    //       that.$store.dispatch("addTabs",{
    //         _this:that,
    //         label:(to["meta"]||{})["title"]||"未命名",
    //         name:to["name"],
    //         icon:"ios-bookmark-outline",
    //         params:to["params"]
    //       });      
    //     }

    //     // 刷新
    //     if( (to["params"]||{})["refresh"] ){
    //       that.isRefresh=false;
    //       that.$nextTick(()=>{
    //         that.isRefresh=true;
    //       });
    //     }
        
    //     next();
    // });

  },
  mounted(){

  },  
  methods:{
    /**
     * 到首页
    */
    goHome: function(){
      this.showPlatform="";
    },
    /**
     * 菜单 初始化
     */
    menuInit: function(){
      setTimeout(()=>{
          this.menuList=[
            {
              id: "1",
              name: "SRM平台",
              platformName:'srm',
              platformHttps:"http://139.224.2.42:10011/main.html?isLogin=false",
              children: [
                {
                    id:"1-1",
                    name: "供应商管",
                    platformName:'srm',
                    platformHttps:"http://139.224.2.42:10011/main.html?isLogin=false",
                    pathURL:"#AtpApp.custom_pp.supplierInfo.supplier.controller.Supplier",
                    icon:"logo-buffer",                   
                },
                {
                    id:"1-2",
                    name: "采购项目管理",
                    platformName:'srm',
                    platformHttps:"http://139.224.2.42:10011/main.html?isLogin=false",
                    pathURL:"#AtpApp.custom_pp.project.purchaseproject.controller.Project",
                    icon:"logo-buffer",   
                },
              ]
            },
            {
              id: "2",
              name: "vue 平台",
              platformName:'vue',
              platformHttps:"http://182.168.1.221/vuePlatform",
              children: [
                  {
                      id:"2-1",
                      name: "vue页面1", 
                      platformName:'vue',
                      platformHttps:"http://182.168.1.221/vuePlatform",
                      pathURL:"/platform/page1",            
                      icon:"logo-buffer",
                  },
                  {
                      id:"2-2",
                      name: "vue页面2", 
                      platformName:'vue',
                      platformHttps:"http://182.168.1.221/vuePlatform",
                      pathURL:"/platform/page2",            
                      icon:"logo-buffer",
                  },
                  {
                      id:"2-3",
                      name: "vue页面3", 
                      platformName:'vue',
                      platformHttps:"http://182.168.1.221/vuePlatform",
                      pathURL:"/platform/page3",            
                      icon:"logo-buffer",
                  },                                    
              ]
            },  
            {
              id: "3",
              name: "无路由的平台",
              platformName:'w3c',
              platformHttps:"https://www.w3school.com.cn/index.html",
              children: [
                  {
                      id:"3-1",
                      name: "html", 
                      platformName:'w3c',
                      platformHttps:"https://www.w3school.com.cn/index.html",
                      pathURL:"https://www.w3school.com.cn/html/index.asp",   
                      notRouter: true,         
                      icon:"logo-buffer",
                  },
                  {
                      id:"3-2",
                      name: "css", 
                      platformName:'w3c',
                      platformHttps:"https://www.w3school.com.cn/index.html",
                      pathURL:"https://www.w3school.com.cn/css/index.asp",  
                      notRouter: true,         
                      icon:"logo-buffer",
                  },                                   
              ]
            },                      
          ];

          this.$nextTick(()=>{
            this.iframeInit();
          });
      },300);
    },
    /**
     * tabs 切换
     */
    changeTabs: function(option){
      this.platformLink(option);
    },
    /**
     * iframe 初始化
     */
    iframeInit: function(){
      // console.log(123);
    },
    /**
     * 刷新 窗口
     */
    updataWindow: function(){
      this.documentHeight=document.documentElement.clientHeight-(this.tabsArray?116:68);  // 窗口高度
    },
    /**
     * add 菜单
     */
    addMenuHandle: function(option){
      let that=this;
      this.$store.dispatch("addTabs",{
        _this:that,
        label:option["name"],
        name:option["pathURL"],
        icon:option["icon"],
        menuObj:option
      });

      this.platformLink(option);
    },
    /**
     * 平台 跳转
     */
    platformLink: function(option){
      console.log("页面切换");
      console.log(option);

      this.showPlatform=option["platformName"];  // 显示 iframe      


      // 有路由的页面
      if(!option["notRouter"]){
        // 平台页面跳转   option["platformHttps"]
        this.$refs[option.platformName][0].contentWindow.postMessage(option,"*");  // 向 iframe 传消息
      }else{
        this.$refs[option.platformName][0].src=option["pathURL"];  // 跳转页面
      }

    }
  },
}
</script>

<style lang="scss">
  .wis-content-container{
    width: 100%;
    position: relative;
    
    .wis-tabs-container{
      width: 100%;
      position: absolute;
      top: 0px;
      left: 0px; 
      height: 46px;
    }

    .content-iframe{
        height: 100%;
        position: relative;

        iframe{
          position: absolute;
          visibility: hidden;
          width: 100%;
          height: 100%;

          &.show{
            visibility: inherit;
          }
        }
    }
  }
</style>
