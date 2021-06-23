<template>
	<view>
		<view>
			<u-navbar
			back-text=""
			title="订单详情"
			back-icon-color="#fff"
			title-color="#fff"
			title-size="36"
			height="50"
			:border-bottom="false"
			:background="navBackground">
			</u-navbar>
		</view>

		<view class="address">
			<SiteListItem
			:showExtraIcon="address.showExtraIcon" :extraIcon="address.extraIcon"
			:name="address.name" :phone="address.phone" :site="address.site"
			:link="address.link"></SiteListItem>
		</view>
		<view>
		<orderItem :productInfo="productInfo" :parice.sync='moneyInfo.parice' :count.sync='moneyInfo.count'></orderItem>
		</view>
		<view class="footer">
			<text>共{{moneyInfo.count}}件，小计：<strong>￥{{moneyInfo.parice}}</strong></text>
			<u-button shape="circle" @click="sumberBtn" :hair-line="false" hover-class="none" :custom-style="customStyleAct">提交订单</u-button>
			<view class="btn" ></view>
		</view>
	</view>
</template>

<script>
	import SiteListItem from "../components/site.vue";
	import orderItem from "../components/order2.vue";
	export default {
		components:{
			SiteListItem,
			orderItem
		},
		data() {
			return {
				navBackground:{
					"background-color":"rgba(199,185,244,1)"
				},
				customStyleAct:{
					"background-color":"rgba(78,72,178,1)",
					"margin":"15rpx 30rpx",
					"color":"#fff"
				},
				address:{
					showExtraIcon:true,
					extraIcon: {
						type: 'map-fill',
						color: 'rgba(78,72,178,1)',
						size: '40rpx'
					},
					name: "莉莉娅",
					phone: "14574545741",
					site:"北京市朝阳区万达广场2号楼2单元202室",
					link:"/pages/store/address"
				},
				productInfo:[{
					storeName:"新夏晴雨伞",
					imgSrc:"/static/shopping/img_spt2@3x.png",
					title:"插画全自动雨伞折叠女晴雨两 用太阳伞防晒防紫外线学生",
					note:"浅蓝，120cm",
					money:"29.90",
					count:"10",
					mode:"物流配送",
					freight:"0.00"
				},{
					storeName:"新夏晴雨伞",
					imgSrc:"/static/shopping/img_spt2@3x.png",
					title:"插画全自动雨伞折叠女晴雨两 用太阳伞防晒防紫外线学生",
					note:"浅蓝，120cm",
					money:"9.90",
					count:"6",
					mode:"物流配送",
					freight:"1.25"
				}],
				moneyInfo:{
						parice:'',
						count:''
				}
			}
		},
		methods: {
			sumberBtn(){
				console.log(this);
			},

		}
	}
</script>

<style lang="scss">
	page{
		background: #e8cfed;
		padding-bottom:120rpx;
	}

	.address{
		margin-bottom:10rpx;
		background: rgba(199,185,244,0.6);
		overflow: hidden;
		/deep/.item_content{
			color:rgba(78,72,178,1) ;
		}
	}
	.order-dom{
		margin-bottom:10rpx;
		background: rgba(199,185,244,0.6);
		overflow: hidden;
	}
	.footer{
		position: fixed;
		bottom:0;
		background: #fff;
		width: 100%;
		height: 100rpx;
		line-height: 100rpx;
		display: flex;
		box-shadow: 0 3rpx 15rpx #e7e6f8;

		text{
			flex: 1;
			text-align: right;
			font-size: 26rpx;
			color: #333;
			strong{
				font-size: 34rpx;
				color: rgba(255,82,82,1);
			}
		}
	}
</style>
