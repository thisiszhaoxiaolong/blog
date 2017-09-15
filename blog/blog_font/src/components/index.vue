<template>
  <div class="index">
   <headertop></headertop>
<!--面包屑-->
<main>
<div id="ww">
        <div class="row">
            <div>
                <img src="../assets/img/user.png">
                <h1>Hi,三岁先生</h1>
                <p>文凭不过是一张火车票，清华的是软卧，本科的是硬卧，专科的是硬座，民办的是站票，成教的在厕所挤着。火车到站，都下车找工作，才发现老板并不太关心你是怎么来的，只关心你会干什么。</p>
            </div>
        </div>
    </div>
  <breadcast></breadcast>
<!--主内容区-->
<el-row :gutter="24">
    <el-col :span="17">
        <router-view  class="grid-content"></router-view>
    </el-col>
    <el-col :span="7">
        <div class="grid-content ">
            <search></search>
            <top></top>
            <news></news>
        </div>
    </el-col>
</el-row>  
</main>

<footers></footers>
</div>
</template>

<script>
    import breadcast from "./breadcast";
    import header from "./header"
    import search from "./search"
    import top from "./top"
    import news from "./new"
    import detail from "./detail"
    import footers from "./footer"

    import action_type from "../store/action_type"

    import {
        mapState,
        mapActions
    } from "vuex"
    export default {
        name: 'hello',
        data() {
            return {
                activeIndex: '1',
                datalist: [{
                    one: 12,
                    two: [
                        1, 2, 3, 4
                    ]
                }]
            };
        },
        methods: {
            handleSelect(key, keyPath) {
                console.log(key, keyPath);
            }

        },
        computed: {
            ...mapState({
                headData: (state) => state.headData
            })
        },
        components: {
            breadcast: breadcast,
            headertop: header,
            search: search,
            top: top,
            news: news,
            detail: detail,
            footers: footers

        },
        beforeRouteEnter: (to, from, next) => {

            next(vm => {
                console.log(vm.headData)
                if (!vm.headData) {
                    vm.$router.push({
                        path: "/"
                    })
                }

            })
        },
        mounted() {

        }


    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .index {
        width: 1200px;
        margin: 0 auto;
    }
    
    .borderR {
        border-radius: 10px;
    }
    
    .breadCrumb {
        height: 40px;
        line-height: 40px;
        /*background: lightblue;*/
        padding-left: 20px;
    }
    
    .el-row {
        margin-bottom: 20px;
        &:last-child {
            margin-bottom: 0;
        }
    }
    
    .el-col {
        border-radius: 4px;
    }
    
    .bg-purple-dark {
        background: #99a9bf;
    }
    
    .bg-purple {
        background: #d3dce6;
    }
    
    .bg-purple-light {
        background: #e5e9f2;
    }
    
    .grid-content {
        border-radius: 4px;
        min-height: 36px;
    }
    
    .row-bg {
        padding: 10px 0;
        background-color: #f9fafc;
    }
      
    #ww {
        width: 100%;
        background: #f2f2f2;
    }
    
    #ww .row {
        width: 80%;
        text-align: center;
        padding: 60px 0;
        margin-left: 10%;
    }
    
    #ww .row p {
        line-height: 35px;
    }
    main{
        background:#fff;
    }
    
</style>