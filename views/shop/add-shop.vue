<style lang="less">
    @import '../../styles/common.less';
    @import './shop.less';
</style>

<template>
    <div class="add-shop">
        <div class="shop-info-box">
            <div class="">
                <Form :model="formItem" :label-width="80">
                    <div class="box">
                        <FormItem label="商品标题">
                            <Input v-model="formItem.input"></Input>
                        </FormItem>
                        <FormItem label="商品介绍">
                            <Input v-model="formItem.textarea" type="textarea" :autosize="{minRows: 2,maxRows: 5}" placeholder="Enter something..."></Input>
                        </FormItem>
                        <FormItem label="商品大图">
                            <div class="img-upload-list" v-for="item in uploadList">
                                <template v-if="item.status === 'finished'">
                                    <img :src="item.url">
                                    <div class="img-upload-list-cover">
                                        <Icon type="ios-eye-outline" @click.native="handleView(item.name)"></Icon>
                                        <Icon type="ios-trash-outline" @click.native="handleRemove(item)"></Icon>
                                    </div>
                                </template>
                                <template v-else>
                                    <Progress v-if="item.showProgress" :percent="item.percentage" hide-info></Progress>
                                </template>
                            </div>
                            <Upload
                                ref="upload"
                                :show-upload-list="false"
                                :default-file-list="defaultList"
                                :on-success="handleSuccess"
                                :format="['jpg','jpeg','png']"
                                :max-size="2048"
                                :on-format-error="handleFormatError"
                                :on-exceeded-size="handleMaxSize"
                                :before-upload="handleBeforeUpload"
                                multiple
                                type="drag"
                                action="//jsonplaceholder.typicode.com/posts/"
                                style="display: inline-block;width:58px;">
                                <div style="width: 58px;height:58px;line-height: 58px;">
                                    <Icon type="camera" size="20"></Icon>
                                </div>
                            </Upload>
                            <Modal title="View Image" v-model="visible">
                                <img :src="'https://o5wwk8baw.qnssl.com/' + imgName + '/large'" v-if="visible" style="width: 100%">
                            </Modal>
                        </FormItem>
                        <FormItem label="商品分类">
                            <CheckboxGroup v-model="formItem.checkbox">
                                <Checkbox label="Eat"></Checkbox>
                                <Checkbox label="Sleep"></Checkbox>
                                <Checkbox label="Run"></Checkbox>
                                <Checkbox label="Movie"></Checkbox>
                            </CheckboxGroup>
                        </FormItem>
                        <FormItem label="品牌">
                            <RadioGroup v-model="formItem.radio">
                                <Radio label="male">Male</Radio>
                                <Radio label="female">Female</Radio>
                            </RadioGroup>
                        </FormItem>
                        <FormItem label="商品详情">
                            <textarea id="articleEditor"></textarea>
                        </FormItem>
                        <FormItem label="商品参数">
                            <Input v-model="formItem.input"></Input>
                            <Input v-model="formItem.input"></Input>
                        </FormItem>
                        <FormItem>
                            <Row>
                                <Col span="12">
                                    <Button type="dashed" long @click="parameterAdd" icon="plus-round">Add item</Button>
                                </Col>
                            </Row>
                        </FormItem>
                    </div>

                    <div class="box">
                        <FormItem label="商品标题">
                            <Input v-model="formItem.input"></Input>
                        </FormItem>
                        <FormItem label="规格/库存">
                            <ul class="goods-norm">
                                <li>
                                    <div><label>规格名称</label></div>
                                    <Input v-model="formItem.input"></Input>
                                </li>
                                <li>
                                    <div><label>品牌价</label></div>
                                    <Input v-model="formItem.input"></Input>
                                </li>
                                <li>
                                    <div><label>折后价</label></div>
                                    <Input v-model="formItem.input"></Input>
                                </li>
                                <li>
                                    <div><label>库存</label></div>
                                    <Input v-model="formItem.input"></Input>
                                </li>
                            </ul>
                        </FormItem>
                        <!-- <FormItem label="物流/其他">
                            <RadioGroup v-model="formItem.radio">
                                <p><Radio label="same">统一运费</Radio> <Input v-model="formItem.input"></Input>元，“0”表示包邮</p>
                                <Radio label="different">运费模板</Radio>
                            </RadioGroup>
                            <p>每人限购 <InputNumber :max="1000" :min="0" v-model="value1"></InputNumber><span>不填或者"0"表示不限购</span></p>
                        </FormItem> -->
                    </div>
                    
                    <FormItem>
                        <Button type="primary">Submit</Button>
                        <Button type="ghost" style="margin-left: 8px">Cancel</Button>
                    </FormItem>
                </Form>
            </div>
        </div>
    </div>
</template>

<script>
import Cookies from 'js-cookie';
import tinymce from 'tinymce';
export default {
    data () {
        return {
            formItem: {
                input: '',
                textarea: '',
                select: '',
                radio: 'male',
                checkbox: [],
                switch: true,
                date: '',
                time: '',
                slider: [20, 50],
                textarea: ''
            },
            index: 1,
            formDynamic: {
                items: [
                    {
                        value: '',
                        index: 1,
                        status: 1
                    }
                ]
            },
            defaultList: [
                {
                    'name': 'a42bdcc1178e62b4694c830f028db5c0',
                    'url': 'https://o5wwk8baw.qnssl.com/a42bdcc1178e62b4694c830f028db5c0/avatar'
                },
                {
                    'name': 'bc7521e033abdd1e92222d733590f104',
                    'url': 'https://o5wwk8baw.qnssl.com/bc7521e033abdd1e92222d733590f104/avatar'
                }
            ],
            imgName: '',
            visible: false,
            uploadList: []
        };
    },
    computed: {
        avatorPath () {

        }
    },
    methods: {
        handleView (name) {
            this.imgName = name;
            this.visible = true;
        },
        handleRemove (file) {
            const fileList = this.$refs.upload.fileList;
            this.$refs.upload.fileList.splice(fileList.indexOf(file), 1);
        },
        handleSuccess (res, file) {
            file.url = 'https://o5wwk8baw.qnssl.com/7eb99afb9d5f317c912f08b5212fd69a/avatar';
            file.name = '7eb99afb9d5f317c912f08b5212fd69a';
        },
        handleFormatError (file) {
            this.$Notice.warning({
                title: 'The file format is incorrect',
                desc: 'File format of ' + file.name + ' is incorrect, please select jpg or png.'
            });
        },
        handleMaxSize (file) {
            this.$Notice.warning({
                title: 'Exceeding file size limit',
                desc: 'File  ' + file.name + ' is too large, no more than 2M.'
            });
        },
        handleBeforeUpload () {
            const check = this.uploadList.length < 5;
            if (!check) {
                this.$Notice.warning({
                    title: 'Up to five pictures can be uploaded.'
                });
            }
            return check;
        },
        parameterAdd () {
            this.index++;
            this.formDynamic.items.push({
                value: '',
                index: this.index,
                status: 1
            });
        },
        parameterRemove (index) {
            this.formDynamic.items[index].status = 0;
        }
    },
    mounted () {
        this.uploadList = this.$refs.upload.fileList;
        tinymce.init({
            selector: '#articleEditor',
            branding: false,
            elementpath: false,
            height: 600,
            language: 'zh_CN.GB2312',
            menubar: 'edit insert view format table tools',
            theme: 'modern',
            plugins: [
                'advlist autolink lists link image charmap print preview hr anchor pagebreak imagetools',
                'searchreplace visualblocks visualchars code fullscreen fullpage',
                'insertdatetime media nonbreaking save table contextmenu directionality',
                'emoticons paste textcolor colorpicker textpattern imagetools codesample'
            ],
            toolbar1: ' newnote print fullscreen preview | undo redo | insert | styleselect | forecolor backcolor bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | link image emoticons media codesample',
            autosave_interval: '20s',
            image_advtab: true,
            table_default_styles: {
                width: '100%',
                borderCollapse: 'collapse'
            }
        });
    },
    destroyed () {
        tinymce.get('articleEditor').destroy();
    }
};
</script>

<style>

</style>
