<style lang="less">
    @import '../../styles/common.less';
    @import './store.less';
</style>

<template>
    <div class="normal-box">
        <div class="page-action-pane">
                
        </div>

        <div class="normal-list">
            <div class="normal-header">
                <h1>广告</h1>
                <div class="pull-right">
                    <router-link to="/add-banner"><Button type="primary" icon="plus">新增广告</Button></router-link>
                </div>
            </div>
            <div class="normal-content">
                <div v-if="shop.length">

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
            shopType:[
                {
                    value: 'New York',
                    label: 'New York'
                },
                {
                    value: 'London',
                    label: 'London'
                }
            ],
            shop:[],
            model1:'',
            model2:'',
            model3:'',
            model4:''
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
