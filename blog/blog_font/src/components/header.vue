<template>
<nav class="nav">
    <h2>个人博客</h2>
        <el-menu theme="dark" :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
            <el-submenu v-for="(i,index) in datalist" :index="i.onedata.id" >
                <template slot="title">{{i.onedata.cnname}}</template>
                <el-menu-item v-for="(j,index2) in i.twodata" :index="j.id">{{j.cnname}}</el-menu-item>
            </el-submenu>
     </el-menu>
</nav>

</template>

<script>
    import {
        mapState,
        mapActions
    } from "vuex"
    import action_type from "../store/action_type"
    export default {
        name: 'header',
        data() {
            return {
                activeIndex: '1',
            };
        },
        computed: {
            ...mapState({
                datalist: (state) => state.headData
            })
        },
        methods: {
            ...mapActions({
                changeList: action_type.HEADCHANGEDATA.actions,
                // 二级分类点击后改变面包屑数组
                headbreadList: action_type.HEADBREADDATA.actions
            }),
            handleSelect(key, keyPath) {
                console.log(key)
                this.changeList(key)
                this.datalist.forEach(function(i) {
                    i.twodata.forEach(function(j) {
                        if (j.id == key) {
                            console.log(j)
                            var arr = [{
                                cnname: i.onedata.cnname,
                                oneId: i.onedata.id,
                                twoId: null
                            }, {
                                cnname: j.cnname,
                                oneId: j.parent_id,
                                twoId: j.id
                            }]
                            console.log(arr)
                            this.headbreadList(arr)
                        }
                    }.bind(this))
                }, this);
            }
        },
        mounted() {
            console.log(this.datalist)
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .el-menu-demo {
       background: #1abc9c;
       color: #fff;
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
    .nav{
         background: #1abc9c;
         z-index: 999;
         width: 100%;
         height: 60px;
    }
     h2{
        float: left;
        color: #fff;
        z-index: 999;
        line-height: 60px;
        padding-left: 30px;
    }
    .el-menu{
        float: right;
        background: #1abc9c;
    }
</style>