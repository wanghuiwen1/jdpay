<template>
    <div class="hello">
        <form action="https://h5pay.jd.com/jdpay/saveOrder" method="post" id="batchForm" style="height: 0">
            <input type="hidden" name="version" v-model="payOrderInfo.version"><br/>
            <input type="hidden" name="merchant" v-model="payOrderInfo.merchant"><br/>
            <input type="hidden" name="device" v-model="payOrderInfo.device" ><br/>
            <input type="hidden" name="tradeNum" v-model="payOrderInfo.tradeNum" ><br/>
            <input type="hidden" name="tradeName" v-model="payOrderInfo.tradeName"><br/>
            <input type="hidden" name="tradeDesc" v-model="payOrderInfo.tradeDesc" value="${}"><br/>
            <input type="hidden" name="tradeTime" v-model="payOrderInfo.tradeTime" ><br/>
            <input type="hidden" name="amount" v-model="payOrderInfo.amount" ><br/>
            <input type="hidden" name="currency" v-model="payOrderInfo.currency" ><br/>
            <input type="hidden" name="note" v-model="payOrderInfo.note"><br/>
            <input type="hidden" name="callbackUrl" v-model="payOrderInfo.callbackUrl"><br/>
            <input type="hidden" name="notifyUrl" v-model="payOrderInfo.notifyUrl"><br/>
            <input type="hidden" name="ip" v-model="payOrderInfo.ip" ><br/>
            <input type="hidden" name="userType" v-model="payOrderInfo.userType" ><br/>
            <input type="hidden" name="userId" v-model="payOrderInfo.userId" ><br/>
            <input type="hidden" name="expireTime" v-model="payOrderInfo.expireTime" ><br/>
            <input type="hidden" name="orderType" v-model="payOrderInfo.orderType" ><br/>
            <input type="hidden" name="industryCategoryCode" v-model="payOrderInfo.industryCategoryCode" ><br/>
            <input type="hidden" name="specCardNo" v-model="payOrderInfo.specCardNo" /><br/>
            <input type="hidden" name="specId" v-model="payOrderInfo.specId" ><br/>
            <input type="hidden" name="specName" v-model="payOrderInfo.specName" ><br/>
            <input type="hidden" name="payChannel" v-model="payOrderInfo.payChannel" ><br/>
            <input type="hidden" name="sign" v-model="payOrderInfo.sign" ><br/>
            <input type="hidden" name="cert" v-model="payOrderInfo.cert" /><br/>
            <input type="hidden" name="vendorId" v-model="payOrderInfo.vendorId" ><br/>
            <input type="hidden" name="goodsInfo" v-model="payOrderInfo.goodsInfo" ><br/>
            <input type="hidden" name="orderGoodsNum" v-model="payOrderInfo.orderGoodsNum" ><br/>
            <input type="hidden" name="receiverInfo" v-model="payOrderInfo.receiverInfo" ><br/>
            <input type="hidden" name="termInfo" v-model="payOrderInfo.termInfo" ><br/>
            <input type="hidden" name="riskInfo" v-model="payOrderInfo.riskInfo" ><br/>
        </form>
        <button @click="createOrder">0.1购买</button>
        <button>0.5购买</button>
        <button>1购买</button>
    </div>
</template>

<script>
    import axios from 'axios'
    import qs from 'qs'

    export default {
        name: 'HelloWorld',
        data() {
            return {
                payOrderInfo: {}
            }
        },
        mounted(){
            axios.interceptors.request.use(
                config => {
                    config.headers['Authorization'] = 'Bearer eyJhbGciOiJIUzUxMiJ9.eyJleHAiOjE1Njk3OTUwMTEsInN1YiI6ImFkbWluc2hpdHUiLCJjcmVhdGVkIjoxNTY5MTkwMjExMTU4fQ.FvvylJq35KL6Z5XxOAu0_KAF9iHoagZvcbekxiMRSiWYFdcL3-jxLQeqLdVLS0lzM-_CznEJw7NoZ-A4sWdFLA'
                    return config
                }
            )
            axios
            .post('http://127.0.0.1:8081/paper/online/pay')
            .then(response => {
                window.console.log(response.data.data)
                this.payOrderInfo = response.data.data

                window.console.log(this.payOrderInfo)
                window.console.log(document.getElementById("batchForm"))
            })
            .catch(function (error) { // 请求失败处理

            });
        },
        methods: {
            createOrder() {
                setTimeout(document.getElementById("batchForm").submit(),1000)

            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
