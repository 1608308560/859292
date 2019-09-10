<template>
    <div class="navigation">
        <div class="content">
            <ul class="flex">
                <li @click="checkRouter(item,index)" :class="tabIndex==index?'active':''" v-for="(item,index) in routerList" :key='index'>
                    <a>{{item.routerName}} </a>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            tabIndex: 0,
            routerList: [{
                routerName: '网站首页',
                routerUrl: '/'
            },
            {
                routerName: '企业简介',
                routerUrl: '/introduction'
            },
            {
                routerName: '企业动态',
                routerUrl: '/dynamic'
            },
            {
                routerName: '产品中心',
                routerUrl: '/product'
            },
            {
                routerName: '供求信息',
                routerUrl: '/information'
            },
            {
                routerName: '在线留言',
                routerUrl: '/onlineMessage'
            },
            {
                routerName: '联系我们',
                routerUrl: '/contact'
            }]
        }
    },
    mounted() {


    },
    methods: {
        checkRouter(item, index) {
            this.tabIndex = index;
            this.$router.push(item.routerUrl)
        }
    }
}
</script >
<style  scoped>
.navigation {
    height: 45px;
    text-align: center;
    background: url('../assets/img/menubg.jpg') repeat-x left bottom;
}
.active{
    background: url(../assets/img/navabg.jpg) no-repeat left bottom;
}

.content {
    margin: auto;
    width: 1200px;
    height: 45px;
}

.content ul {
    list-style: none;
    margin-left: 100px;
}

.content ul li {
    display: inline;
    line-height: 45px;
    width: 120px;
    cursor: pointer;
}

.content ul li:hover {
    background: url(../assets/img/navabg.jpg) no-repeat left bottom;
}

.content ul li a {
    color: #fff;
    font-size: 14px;
}
</style>