<style lang="less">
    @import '../../styles/common.less';
    @import './shop.less';
</style>

<template>
    <div class="shop">
        <div class="page-action-pane">
            <div class="box">
                <div class="col-xs-4">
                    <div class="">
                        <div><label class="control-label">请输入关键词</label></div>
                        <Input v-model="model1" placeholder="请输入商品名称、商品 ID" style="width: 100%"></Input>
                    </div>
                    <div class="margin-top-20">
                        <div><label class="control-label">商品类型</label></div>
                        <Select v-model="model2" style="width:100%">
                            <Option v-for="item in shopType" :value="item.value" :key="item.value">{{ item.label }}</Option>
                        </Select>
                    </div>
                </div>
                <div class="col-xs-4">
                    <div>
                        <div><label class="control-label">所属货架</label></div>
                        <Input v-model="model3" placeholder="不限" style="width: 100%"></Input>
                    </div>
                </div>
                <div class="col-xs-4">  
                    <div>
                        <div><label class="control-label">商品类型</label></div>
                        <Select v-model="model4" style="width:100%">
                            <Option v-for="item in shopType" :value="item.value" :key="item.value">{{ item.label }}</Option>
                        </Select>
                    </div>
                    <div class="pull-right" style="margin-top:50px;">
                        <Button type="ghost">筛选</Button>
                        <Button type="ghost" disabled>导出商品</Button>
                    </div>
                </div>
            </div>
        </div>

        <div class="shop-list">
            <div class="shop-header">
                <h1>商品</h1>
                <div class="pull-right">
                    <router-link to="/add-shop"><Button type="primary" icon="plus">添加商品</Button></router-link>
                </div>
            </div>
            <div class="shop-content">
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
