<template>
    <div class="enterprise flex">
        <div class="left-label">
            <div class="info_head ">在线留言</div>
            <div class="info_content">
                <div class="label_content">
                    <h1>
                        <a>
                            <span>服务流程</span>
                        </a>
                    </h1>
                    <h1>
                        <a>
                            <span>企业文化</span>
                        </a>
                    </h1>
                    <h1>
                        <a>
                            <span>联系我们</span>
                        </a>
                    </h1>
                    <h1>
                        <a>
                            <span>公司简介</span>
                        </a>
                    </h1>
                </div>
            </div>
            <connect-us/>
        </div>
        <div class="right-label">
            <div class="product-detail">湖北通山葡萄园、湖北黄石葡萄园</div>
            <div class="prodct-day grey">更新时间：2019/8/16 14:54:28</div>
            <div class="prodct-content">
                <img src="http://img3.jqw.com/2017/01/17/1744317/product/b201908161454271880.jpg">
            </div>
            <div class="prodct-bot">
                <el-button type="primary" @click="buy()">立即购买</el-button>
                <el-button type="primary">加入购物车</el-button>
            </div>

            <div class="moreDetail">信息描述：
                <p></p>
                <p>孕妇能吃桑葚吗？医生：吃桑葚需要注意这3点！
                </p>
                <p>
                </p>
                <p>桑葚能降低血脂，防止血管硬化，适用于阴血不足、头晕目眩、盗汗及津伤口渴、消渴、肠燥便秘等症。桑葚具有免疫促进作用，可以防癌抗癌。
                </p>
                <p>
                </p>
                <p>常吃桑葚能显著提高人体免疫力，具有延缓衰老，美容养颜，乌发的功效。</p>
                <p><br></p>
                <p></p>
            </div>
            <div class="page-rl flex">
                <div class="page-l flex1">上一页</div>
                <div class="page-r flex1">下一页</div>
            </div>
        </div>
        <div id="weixin"></div>
        <el-dialog title="购买" :visible.sync="dialogVisible" width="600px" :before-close="handleClose">
            <div>
                <span class="lebel">价格：</span>￥{{price}}</div>
            <div class="marT20">
                <span class="lebel">数量：</span>
                <el-input-number v-model="num" @change="handleChange" :min="1" :max="10" label="描述文字"></el-input-number>
            </div>
            <div class="flex flex-vc marT20">
                <span class="lebel">收货地址：</span>
                <el-input v-model="adress" placeholder="请输入收货地址"></el-input>
            </div>
            <span slot="footer" class="dialog-footer">
                <el-button @click="handleClose()">取 消</el-button>
                <el-button type="primary" @click="comfirm()">确 定</el-button>
            </span>
        </el-dialog>
    </div>
</template>

<script>
import connectUs from '../components/connectUs'
export default {
    data() {
        return {
            dialogVisible: false,
            price: '10',
            num: 1,
            adress: ''

        };
    },
    components: {
        connectUs
    },
    methods: {
        // 微信授权登录
        setWxerwma() {
            const s = document.createElement('script')
            s.type = 'text/javascript'
            s.src = 'https://res.wx.qq.com/connect/zh_CN/htmledition/js/wxLogin.js'
            const wxElement = document.body.appendChild(s)
            const el = document.getElementById('#weixin')

            wxElement.onload = function() {
                var obj = new WxLogin({
                    id: el, // 需要显示的容器id
                    appid: 'wx77a0e06751d42ca0', // 公众号appid wx*******（需去微信公众平台申请）
                    scope: 'snsapi_login', // 网页默认即可
                    redirect_uri: encodeURIComponent('http://localhost:8080/#/'), // 授权成功后回调的url
                    state: Math.ceil(Math.random() * 1000), // 可设置为简单的随机数加session用来校验
                    style: 'black', // 提供"black"、"white"可选。二维码的样式
                    href: '' // 外部css文件url，需要https
                })
            }
        },
        // 点击购买
        buy() {
            if (!sessionStorage.getItem('token')) {
                // this.setWxerwma();
                this.showModal()
            } else {
                this.showModal()
            }

        },
        // 确认
        comfirm() {
            // 调取后台购买接口
            let data = {
                price: this.price,
                num: this.num,
                adress: this.adress
            }
            console.log(data, 'data222')
        },
        //清空弹窗内容
        resetModal() {

        },
        // 打开弹窗
        showModal() {
            this.dialogVisible = true
        },
        // 关闭弹窗
        handleClose(done) {
            this.$confirm('确认关闭？')
                .then(_ => {
                    this.dialogVisible = false

                })
                .catch(_ => { });
        },
        // 切换数量
        handleChange(value) {
            console.log(value, 'value');
            let price = 10;
            this.price = price * value
        }
    },
}
</script >
<style  scoped>
.left-label {
    width: 250px;
}

.el-input {
    width: 400px;
}

.lebel {
    display: inline-block;
    width: 80px;
    text-align: right;
}

.enterprise {
    width: 1000px;
    margin: auto;
}

.label_content h1 {
    font-size: 12px;
    height: 25px;
    line-height: 25px;
    padding-left: 25px;
    background: url(../assets/img/article_arrow_1.jpg) no-repeat;
    background-position: 10px 10px;
}

.right-label {
    margin: 0 0 0 20px;
    width: 730px;
    border: 1px solid #ccc;
}

.product-detail {
    text-align: center;
    height: 51px;
    margin-top: 10px;
    font-size: 20px;
}

.prodct-day {
    text-align: center;
    font-size: 12px;
    height: 20px;
    line-height: 20px;
    border-top: 1px solid #CCCCCC;
}

.prodct-content {
    padding: 10px;
    text-align: center;
}

.prodct-bot {
    text-align: center;
}

.prodct-bot .el-button {
    background-color: gray;
    padding: 8px 10px;
}


.moreDetail {
    font-weight: bold;
    padding: 4px 0 4px 8px;
    text-align: left;
}

.moreDetail p {
    border-top: 1px dashed;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    margin-top: 10px;
    padding-top: 10px;
}

.page-l {
    text-align: left;
}

.page-rl {
    padding: 10px 15px;
}

.page-r {
    text-align: left;
}
</style>