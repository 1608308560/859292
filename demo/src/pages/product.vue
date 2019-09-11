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
                    <div class="label_head " style="padding-left: 15px;font-weight:bold">产品中心</div>

                    <div class="link_more flex flex-hw">

                        <div class="list-details" v-for="(item,index) in productList.records" @click="rtproDet(item)" :key="index">
                            <div><img :src="item.image"></div>
                            <div class="list-name">
                                <a href="javascript"></a>{{item.name}}</div>
                        </div>

                    </div>
                    <el-pagination background layout="prev, pager, next" :total="rowCount" :page-size="pageSize" @current-change="currentChange">
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
            pageCurrent: 1,
            productList: [],
            rowCount: 0,
            pageSize: 10
        };
    },
    components: {
        connectUs
    },
    mounted() {
        this.rproList()
    },
    methods: {
        //商品详情
        rtproDet(item) {
            console.log(this.productList.pageCurrent, 'pageCurrent')
              console.log( item.id, 'id')
            this.$router.push({
                path: "productDetail",
                query: {
                    pageCurrent: this.productList.pageCurrent,
                    id: item.id
                }
            });
        },
        currentChange(val) {
            this.pageCurrent = val
            this.rproList()

        },
        rproList() {
            let that = this
            this.$axios.get('http://orcahrd.natapp1.cc/Orchard/product/findProduct.do', {
                params: {
                    pageCurrent: that.pageCurrent || (item && item.id)
                }
            })
                .then(function(res) {
                    that.productList = res.data.data
                    console.log(res.data.data)
                    that.rowCount = res.data.data.rowCount
                    that.pageSize = res.data.data.pageSize
                })
        }

    }

}
</script >
<style  scoped>
.my-dynamic {
    width: 1000px;
    margin: auto;
}

.left-box {
    width: 250px;
    font-size: 14px;
    text-align: left;
    line-height: 34px;
}

.el-pagination {
    text-align: center;
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

.list-details {
    border: 1px solid #58C102;
    width: 154px;
    margin: 10px;
    text-align: center;
    border-radius: 2px;
}

.list-details img {
    width: 152px;
}

.list-details .list-name {
    padding: 0 5px;
    font-size: 12px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
</style>