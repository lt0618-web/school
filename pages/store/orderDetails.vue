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
			<view class="order-dom" v-for="(item,index) in productInfo" :key="index" :index="index">
				<orderItem
				:storeName="item.storeName"
				:imgSrc="item.imgSrc"
				:title="item.title"
				:note="item.note"
				:money="item.money"
				:count="item.count"
				:mode="item.mode"
				:freight="item.freight"
				></orderItem>
			</view>
		</view>
		<view class="footer">
			<text>共{{orderCountAll(productInfo)}}件，小计：<strong>￥{{orderMoneyAll(productInfo)}}</strong></text>
			<u-button shape="circle" @click="sumberBtn" :hair-line="false" hover-class="none" :custom-style="customStyleAct">提交订单</u-button>
			<view class="btn" ></view>
		</view>
	</view>
</template>

<script>
	import SiteListItem from "../components/site.vue";
	import orderItem from "../components/order.vue";
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
				}]
			}
		},
		methods: {
			sumberBtn(){
				console.log(this);
			},
			orderCountAll(data){
				let count = 0;
				for(let i=0; i<data.length;i++){
					count=count + parseInt(data[i].count);
				}
				return count;
			},
			orderMoneyAll(data){
				let money = 0;
				for(let i=0; i<data.length;i++){
					let price = 0;
					let monArr = data[i].money.split('.');
					let freArr = data[i].freight.split('.');
					if(monArr[1].length<2){
						monArr[1] = monArr[1] +'0'
					}
					if(freArr[1].length<2){
						freArr[1] = freArr[1] +'0'
					}
					let mon = parseInt(monArr[0] + monArr[1]);
					let fre = parseInt(freArr[0] + freArr[1])
					for(let j = 0; j<data[i].count; j++){
						price= price + mon;
					}
					price = price + fre ;
					money = money + price;
					console.log(data)
				}

				money = money + '';
				let len= money.length - 2;
				let decim = money.substring(len);
				money = money.split(decim)[0]+'.'+decim;
				return money;
			}

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
