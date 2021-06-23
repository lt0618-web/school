<template>
		<view class="order">
			<view class="top">
				<u-icon name="/static/shopping/icon_dp@2x.png" :size="44" color="rgb(94,94,94)"></u-icon>
				<text>{{storeName}}</text>
			</view>
			<view class="cont">
				<view class="cont_info">
					<view class="info_img">
						<image :src="imgSrc" mode="widthFix"></image>
					</view>
					<view class="info_text">
						<view class="title">{{title}}</view>
						<view class="note">{{note}}</view>
						<view class="number">
							￥<text class="money">{{money}}</text>
							<text class="count">x{{count}}</text>
						</view>
					</view>
				</view>
				<view class="cont_sel">
					<view class="item">
						<view class="left">配送方式</view>
						<view class="right">{{mode}}</view>
					</view>
					<view class="item">
						<view class="left">运费</view>
						<view class="right">{{freight}}</view>
					</view>
					<view class="item address">
						<view class="left">订单备注</view>
						<input type="text" placeholder-class="line" placeholder="选填,请先和商家协商一致" />
					</view>
				</view>
			</view>
			<view class="foot">
				<text>共{{count}}件 小计：￥{{totalPrice(count,money,freight)}}</text>
			</view>
		</view>
</template>

<script>
	export default {
		name: 'orderItem',
		props:{
			storeName:{
				type:String,
				default:''
			},
			imgSrc:{
				type:String,
				default:''
			},
			title:{
				type:String,
				default:''
			},
			note:{
				type:String,
				default:''
			},
			money:{
				type:String,
				default:''
			},
			count:{
				type:String,
				default:''
			},
			mode:{
				type:String,
				default:''
			},
			freight:{
				type:String,
				default:''
			}
		},
		data() {
			return {
				allInfo:{
					toPrice:[],
					toNum:[]
				}
			}
		},
		computed: {
		},
		methods: {
			// 单个商品总价
			totalPrice(count,money,freight) {
					let price = 0;
					let monArr = money.split('.');
					let freArr = freight.split('.');
					if(monArr[1].length<2){
						monArr[1] = monArr[1] +'0'
					}
					if(freArr[1].length<2){
						freArr[1] = freArr[1] +'0'
					}
					let mon = parseInt(monArr[0] + monArr[1]);
					let fre = parseInt(freArr[0] + freArr[1])
					for(let i = 0; i<count; i++){
						price= price + mon;
					}
					let price2 = (price + fre ) +'';
					let len= price2.length - monArr[1].length;
					let decim = price2.substring(len);
					price2 = price2.split(decim)[0]+'.'+decim;
					return price2;
			}
		}
	}
</script>

<style lang="scss">
	.order{
		// background-color:rgba(199,185,244,0.6);
		margin:30rpx;
		color: #4e48b2;

		.top{
			font-size: 30rpx;
			line-height: 40rpx;
			overflow: hidden;
			display: flex;
			align-items: center;

			text{
				margin-left:20rpx;

			}

		}
		.cont{
			margin-top: 30rpx;

			.cont_info{
				margin-bottom:30rpx;
				overflow: hidden;
				display: flex;
				align-items: center;

				.info_img{
					width: 200rpx;
					height: 200rpx;
					margin-right:30rpx;
					image{
						width: 100%;
					}
				}
				.info_text{
					flex: 1;

					.title{
						height: 96rpx;
						line-height: 48rpx;
						font-size: 34rpx;
						display: -webkit-box;
						-webkit-box-orient: vertical;
						-webkit-line-clamp: 2;
						overflow: hidden;
					}
					.note{
						padding:20rpx 0;
						line-height: 30rpx;
						opacity: 0.3;
						font-size: 26rpx;
					}
					.number{
						font-size: 28rpx;
						line-height: 30rpx;
						overflow: hidden;
						display: flex;
						align-items: center;
						.money{
							font-size: 36rpx;
							flex: 1;
						}
						.count{
							width: 100rpx;
							text-align: right;
							font-size: 30rpx;
							opacity: 0.6;
						}
					}
				}
			}

			.cont_sel{
				.item{
					display: flex;
					align-items: center;
					line-height: 40rpx;
					padding:20rpx 0;
					color: #827ddd;

					.left{
						margin-right:20rpx;
						vertical-align: top;
					}
					.right{
						flex: 1;
						text-align: right;
					}
					input{
						flex: 1;
						font-size: 30rpx;
					}
				}
			}
		}
		.foot{
			font-size: 28rpx;
			text-align: right;
			line-height: 72rpx;
			padding-bottom:30rpx;
		}
		/deep/ .line {
			color: rgba(78,72,178,0.4);
			font-size: 28rpx;
		}

	}
</style>
