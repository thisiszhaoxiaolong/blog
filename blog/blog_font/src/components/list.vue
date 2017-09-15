<template>
<div>
    

<el-row class="rowall">
    <el-col :span="24" style="border-radius: 4px;">
        <el-row class="classrowone">
            <el-col :span="6">标题</el-col>
            <el-col :span="6">分类</el-col>
            <el-col :span="6">作者</el-col>
            <el-col :span="6">发布时间</el-col>
        </el-row>
        <el-row v-for="i in everypage" class="classrow">
            <router-link :to="{name:'detail',params:{id:i.id,onedata:{cnname:i.cnname_one,oneId:i.oneId,twoId:null},twodata:{cnname:i.cnname_two,oneId:i.oneId,twoId:i.twoId}}}">
                <el-col :span="6">{{i.article_name}}</el-col>
                <el-col :span="6">{{i.cnname_one}}</el-col>
                <el-col :span="6">{{i.editer}}</el-col>
                <el-col :span="6">{{i.time}}</el-col>
            </router-link>
        </el-row>
    </el-col>
</el-row>
  <div class="page">
        <el-pagination 
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange" 
        :current-page="currentPage4" 
        :page-sizes="[5, 10, 15, 20]" 
        :page-size="5"
        layout="total, sizes, prev, pager, next, jumper" 
        :total="alldata.length">
        </el-pagination>
    </div>
</div> 
</template>

<script>
    import {
        mapState,
        mapActions
    } from "vuex"
    export default {
        name: 'header',
        data() {
            return {
                activeIndex: '1',
                everypagelist: 5,
                everypage: null,
                alldata: [],
                id: null,
                currentPage4: 0
            }
        },
        computed: {
            ...mapState({
                datalist: (state) => state.articleList
            })
        },
        methods: {
            handleSelect(key, keyPath) {
                console.log(key, keyPath);
            },
            handleSizeChange(val) {
                this.everypagelist = val
            },
            handleCurrentChange(val) {
                this.everypage = this.alldata.slice(this.everypagelist * (val - 1), this.everypagelist * val)
                    // console.log(this.everypage)
            },
        },
        mounted(){
            console.log(this.datalist)
        },
        created(){
            this.alldata=this.datalist;
            this.everypage = this.alldata.slice(this.everypagelist * 0, this.everypagelist)
        }
    }
</script>  

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .classrow {
        height: 40px;
        /*background:#8cc7b2;*/
        border-bottom: 1px solid #000;
        line-height: 40px;
        margin: 10px 20px;
        border-radius: 5px;
        padding: 0 10px;
    }
    
    .classrowone {
        height: 40px;
        background: #44d39f;
        line-height: 40px;
        margin: 10px 20px;
        border-radius: 5px;
        padding: 0 10px;
        color: #fff;
        font-size:20px;
    }
    
    .rowall {
        background: #fff;
        min-height: 100%;
    }
    .page{
        text-align: center;
        margin-top: 70px;
    }
</style>