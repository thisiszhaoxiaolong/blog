<template>
    <el-row class="rowall">
        <el-col :span="24" style="border-radius: 4px;">
        
        <h2 class="classrowone">
            最新文章
        </h2>
            <el-row v-for="(i,index) in datalist" class="classrow" :span="24">
<!-- {{i.id}} -->
                <router-link :to="{name:'detail',params:{id:i.id,onedata:{cnname:i.cnname_one,oneId:i.oneId,twoId:null},twodata:{cnname:i.cnname_two,oneId:i.oneId,twoId:i.twoId}}}">
                    <el-col :span="2" class="classrow1">{{index+1}}</el-col>
                    <el-col :span="14" class="classrow2">{{i.article_name}}</el-col>
                    <el-col :span="6" class="classrow3">{{i.TIME}}</div></el-col>
                </router-link>
            </el-row>
        </el-col>
    </el-row>
</template>


<script>
    import {
        mapActions,
        mapState
    } from "vuex"
    export default {
        data() {
            return {

            }
        },
        computed: {
            ...mapState({
                datalist: (state) => state.newlist
            })
        },
        mounted(){
            console.log()
        }
    }
</script>
<style scoped>
    .rowall {
        background: #fff ;
        padding: 5px;
        border-radius: 5px;
    }
    
    .classrowone {
        background: #1abc9c;
        margin-bottom: 10px;
        text-align: center;
        color: white;
        padding: 2px 0;
        font-weight: 300;
    }
    
    .classrow {
        margin: 5px 0;
        border-bottom: 1px solid #ccc;
    }
    
    .classrow1 {
        border-radius: 50%;
        width: 20px;
        height: 20px;
        text-align: center;
        line-height: 20px;
        background: red;
        margin-right: 10px;
        font-size: 12px;
    }
    
    .classrow2 {
        /*background: lightblue;*/
        /*margin-right: 10px*/
    }
    
    .classrow3 {
        /*background: lightgreen;*/
        font-size: 14px;
        width: 90px;
    }
</style>