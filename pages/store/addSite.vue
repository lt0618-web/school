<template>
	<view>
		<view>
			<u-navbar
			back-text="" 
			title="新增收货地址" 
			back-icon-color="#fff"
			title-color="#fff"
			title-size="36"
			height="50" 
			:border-bottom="false"
			:background="navBackground">
			</u-navbar>
		</view>
		<view class="wrap">
			<view class="top">
				<view class="item">
					<view class="left">收货人</view>
					<input type="text" placeholder-class="line" placeholder="请填写收货人姓名" />
				</view>
				<view class="item">
					<view class="left">手机号码</view>
					<input type="text" placeholder-class="line" placeholder="请填写收货人手机号" />
				</view>
				<view class="item" @tap="showRegionPicker">
					<view class="left">所在地区</view>
					<input disabled type="text" placeholder-class="line" placeholder="省市区县、乡镇等" />
				</view>
				<view class="item address">
					<view class="left">详细地址</view>
					<textarea type="text" placeholder-class="line" placeholder="街道、楼牌等" />
				</view>
			</view>
			<view class="bottom">
				<view class="tag">
					<view class="left">标签</view>
					<view class="right">
						<text class="tags">家</text>
						<text class="tags">公司</text>
						<text class="tags">学校</text>
						<view class="tags plus"><u-icon size="22" name="plus"></u-icon></view>
					</view>
				</view>
				<view class="default">
					<view class="left">
						<view class="set">设置默认地址</view>
						<view class="tips">提醒：每次下单会默认推荐该地址</view>
					</view>
					<view class="right"><switch color="#4e48b2" @change="setDefault" /></view>
				</view>
			</view>
			<u-picker mode="region" ref="uPicker" v-model="show" />
		</view>
		<view class="add">
			<view class="addSite" @tap="toAddSite">
				新建收货地址
			</view>
		</view>
	</view>
	</template>

<script>
export default {
	data() {
		return {
			show: false,
			navBackground:{
				"background-color":"rgba(199,185,244,1)"
			}, 
		};
	},
	methods: {
		setDefault() {},
		showRegionPicker() {
			this.show = true;
		},
		toAddSite(){
			console.log(11111)
		}
	}
};
</script>

<style lang="scss" scoped>
	page{
		background: #e8cfed;
		padding-bottom:190rpx
	}
/deep/ .line {
	color: rgba(78,72,178,0.4);
	font-size: 28rpx;
}
.wrap {
	background-color: #fbf3fe;
	color:rgba(78,72,178,1);
	.top {
		background-color: rgba(199,185,244,0.2);
		border-top: solid 2rpx #fff;
		padding: 22rpx;
		.item {
			display: flex;
			font-size: 32rpx;
			line-height: 100rpx;
			align-items: center;
			border-bottom: solid 2rpx #fff;
			.left {
				width: 180rpx;
			}
			input {
				text-align: left;
			}
		}
		
		.address {
			padding: 20rpx 0;
			textarea {
				// width: 100%;
				height: 150rpx;
				background-color: rgba($color: #fff, $alpha: 0.7);
				line-height: 60rpx;
				margin: 40rpx auto;
				padding: 20rpx;
				color:rgba(78,72,178,1);
			}
		}
		.site-clipboard {
			padding-right: 40rpx;
			textarea {
				// width: 100%;
				height: 150rpx;
				background-color: rgba($color: #fff, $alpha: 0.7);
				line-height: 60rpx;
				margin: 40rpx auto;
				padding: 20rpx;
			}
			.clipboard {
				display: flex;
				justify-content: center;
				align-items: center;
				font-size: 26rpx;
				color: #fff;
				height: 80rpx;
				.icon {
					margin-top: 6rpx;
					margin-left: 10rpx;
				}
			}
		}
	}
	.bottom {
		margin-top: 20rpx;
		padding: 40rpx;
		padding-right: 0;
		background-color: rgba(199,185,244,0.2);
		font-size: 28rpx;
		.tag {
			display: flex;
			.left {
				width: 160rpx;
			}
			.right {
				display: flex;
				flex-wrap: wrap;
				.tags {
					width: 140rpx;
					padding: 16rpx 8rpx;
					border: solid 2rpx #4e48b2;
					text-align: center;
					border-radius: 50rpx;
					margin: 0 10rpx 20rpx;
					display: flex;
					font-size: 28rpx;
					align-items: center;
					justify-content: center;
					color:#4e48b2;
					line-height: 1;
				}
				.plus {
					//padding: 10rpx 0;
				}
				.tags.active {
					background-color:#4e48b2;
					border: solid 2rpx #fff;
					color:#fff;
				}
			}
		}
		.default {
			margin-top: 50rpx;
			display: flex;
			justify-content: space-between;
			border-bottom: solid 2rpx #4e48b2;
			line-height: 64rpx;
			.tips {
				font-size: 24rpx;
			}
			.right {
			}
		}
	}
}
.add{
	background-color: #e8cfed;	position:fixed;
	bottom:0;
	width:100%;
	height: 130rpx;
	.addSite {
		display: flex;
		justify-content: space-around;
		width: 690rpx;
		line-height: 90rpx;
		position: absolute;
		bottom: 20rpx;
		left: 30rpx;
		background-color: rgba(78,72,178,1);
		border-radius: 90rpx;
		font-size: 34rpx;
		color: #ffffff;
	}
}

</style>
