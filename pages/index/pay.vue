<template>
    <view>
        <view class="uni-list">
            <radio-group @change="applePriceChange">
                <label class="uni-list-cell uni-list-cell-pd" v-for="(item, index) in priceList" :key="index">
                    {{item.text}}
                    <radio :value="item.value" :checked="item.checked" />
                </label>
            </radio-group>
        </view>
		
        <view class="uni-padding-wrap">
            <button class="ipaPayBtn" @click="requestPayment" :loading="loading" :disabled="disabled">确认支付</button>
        </view>
    </view>
    </view>
</template>

<script>
    let iapChannel = null,
        productId = 'HelloUniappPayment1',
        productIds = ['HelloUniappPayment1', 'HelloUniappPayment6'];
    export default {
        data() {
            return {
                title: 'request-payment',
                loading: false,
                disabled: true,
                priceList: [{
                    value: 'HelloUniappPayment1',
                    text: '支付1元',
                    checked: true
                }, {
                    value: 'HelloUniappPayment6',
                    text: '支付6元',
                    checked: false
                }]
            }
        },
        onLoad: function() {
            plus.payment.getChannels((channels) => {
                console.log("获取到channel" + JSON.stringify(channels))
                for (var i in channels) {
                    var channel = channels[i];
                    if (channel.id === 'appleiap') {
                        iapChannel = channel;
                        this.requestOrder();
                    }
                }
                if(!iapChannel){
                    this.errorMsg()
                }
            }, (error) => {
                this.errorMsg()
            });
        },
        methods: {
            requestOrder() {
                uni.showLoading({
                    title:'检测支付环境...'
                })
                iapChannel.requestOrder(productIds, (orderList) => { //必须调用此方法才能进行 iap 支付
                    this.disabled = false;
                    console.log('requestOrder success666: ' + JSON.stringify(orderList));
                    uni.hideLoading();
                }, (e) => {
                    console.log('requestOrder failed: ' + JSON.stringify(e));
                    uni.hideLoading();
                    this.errorMsg()
                });
            },
            requestPayment(e) {
                this.loading = true;
                uni.requestPayment({
                    provider: 'appleiap',
                    orderInfo: {
                        productid: productId
                    },
                    success: (e) => {
                        uni.showModal({
                            content: "感谢您的赞助",
                            showCancel: false
                        })
                    },
                    fail: (e) => {
                        uni.showModal({
                            content: "支付失败,原因为: " + e.errMsg,
                            showCancel: false
                        })
                    },
                    complete: () => {
                        console.log("payment结束")
                        this.loading = false;
                    }
                })
            },
            applePriceChange(e) {
                productId = e.detail.value;
            },
            errorMsg(){
                uni.showModal({
                    content: "暂不支持苹果 iap 支付",
                    showCancel: false
                })
            }
        }
    }
</script>
