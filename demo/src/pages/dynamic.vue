<template>
    <div>
        <div class="my-dynamic flex">
            <div class="left-box">
                <div class="info_head">企业简介</div>
                <div class="info_content">
                    <div class="label_content">
                        <h1>
                            <a>
                                <span>服务流程</span>
                            </a>
                        </h1>
                    </div>
                </div>
                <connect-us/>
            </div>
            <div class="right-box">
                <div class="label">
                    <div class="label_head " style="padding-left: 15px;">新闻动态</div>

                    <div class="link_more">
                        <div v-for="(item, index) in listday" :key="index" class="title-nav flex">
                            <div class="list-content">{{item.title}}</div>
                            <div class="list-day">{{utils.transformTime(item.update_time)}}</div>
                        </div>
                    </div>
                    <el-pagination background layout="prev, pager, next" :total="rowCount" @current-change="currentChange">
                    </el-pagination>
                </div>
            </div>
        </div>
    </div>
</template> 

<script>
import connectUs from '../components/connectUs'
export default {
    data() {
        return {
            listday: [],
            pageCurrent: 1,
            pageSize: 10,
            rowCount:100
        };
    },
    components: {
        connectUs
    },
    methods: {
        currentChange(val) {
            console.log(val)
            this.pageCurrent = val
            this.findEnterpriseDynamic()

        },
        findEnterpriseDynamic() {
            let that = this
            let params = {
                pageSize: this.pageSize,
                pageCurrent: this.pageCurrent
            }
            this.$axios.get('http://orcahrd.natapp1.cc/Orchard/enterprise/findEnterpriseDynamic.do', params)
                .then(function(res) {
                    console.log(res.data.dynamicList)
                    that.listday = res.data.dynamicList
                    that.rowCount=res.data.dynamicList.rowCount
                })
                .catch(function(err) {
                    console.log(err)
                });
        }
    },
    mounted() {
        this.findEnterpriseDynamic()
    },

}
</script >
<style  scoped>
.my-dynamic {
    width: 1000px;
    margin: auto;
}

.el-pagination {
    text-align: center;
}

.left-box {
    width: 250px;
    font-size: 14px;
    text-align: left;
    line-height: 34px;
}

.label_content h1 {
    font-size: 12px;
    height: 25px;
    line-height: 25px;
    padding-left: 25px;
    background: url(../assets/img/article_arrow_1.jpg) no-repeat;
    background-position: 10px 10px;
}

.right-box {
    width: 730px;
    margin-left: 20px
}

.link_more {
    padding: 0 15px;
    line-height: 33px;
    text-align: left;
}

.list-content {
    width: 630px;
}

.title-nav {
    border-bottom: 1px dashed #66CC66;
}
</style>