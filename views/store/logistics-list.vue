<style lang="less">
    @import '../../styles/common.less';
    @import './store.less';
</style>

<template>
    <div class="logistics normal-box">
        <div class="page-action-pane">
            <div class="box search-box">
                <div class="search-text"><label>搜索</label></div>
                <div class="inline-block"><Input v-model="search" placeholder="请输入模板名称"></Input></div>
                <Button type="ghost">筛选</Button>
            </div>
        </div>

        <div class="normal-list">
            <div class="normal-header">
                <h1>运费模板</h1>
                <div class="pull-right">
                    <router-link to="/add-logistics"><Button type="primary" icon="plus">新增模板</Button></router-link>
                </div>
            </div>
            <div class="normal-content">
                <div v-if="logistics.length">

                </div>
                <div v-else class="empty">
                    <i class="empty__icon"></i><h4 class="m-t-20">暂无数据</h4>
                </div>
            </div>  
        </div>
    </div>
</template>

<script>
import Cookies from 'js-cookie';
export default {
    data () {
        return {
            logistics:[],
            search: ''
        };
    },
    computed: {
        avatorPath () {

        }
    },
    methods: {
        
    }
};
</script>

<style>

</style>
