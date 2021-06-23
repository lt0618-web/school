<template>
	<view>
		<view>
			<u-navbar
			back-text="" 
			title="收货地址" 
			back-icon-color="#fff"
			title-color="#fff"
			title-size="36"
			height="50" 
			:border-bottom="false"
			:background="navBackground">
			</u-navbar>
		</view>
		
		<view class="address">
			<view class="address-list" v-for='(item,index) in list' :key="index" :index="index">
				<SiteListItem 
				:showExtraIcon="item.showExtraIcon" :extraIcon="item.extraIcon" 
				:name="item.name" :phone="item.phone" :site="item.site" :tag="item.tag" 
				:rightIcon="rightIcon" :link="item.link"></SiteListItem>
			</view>
				
		</view>
		<view class="add">
			<view class="addSite" @tap="toAddSite">
				新建收货地址
			</view>
		</view>
	</view>
</template>

<script>
	import SiteListItem from "../components/site.vue";
	export default {
		components:{
			SiteListItem
		},
		data() {
			return {
				navBackground:{
					"background-color":"rgba(199,185,244,1)"
				}, 
				list:[{
					name: "莉莉娅",
					phone: "14574545741",
					tag: [{
						text: "默认",
					},{
						text: "公司",
					}],
					site:"北京市朝阳区万达广场2号楼2单元202室"
				},{
					name: "莉莉娅",
					phone: "14574545741",
					site:"北京市朝阳区万达广场2号楼2单元202室"
				}],
				rightIcon:[{
					type:"/static/shopping/icon_del@2x.png",
					color: '#000000',
					size: "36rpx",
					click(e){
						console.log(e)
					}
					},{
					type:"/static/shopping/icon_bj@2x.png",
					color: '#000000',
					size: "36rpx",
					click(e){
						console.log(e)
					}
				}]
			}
		},
		methods: {
			addressBtnClick(){
				console.log(index);
			},
			toAddSite(){
				uni.navigateTo({
				    url: '/pages/store/addSite'
				});
			}
		}
	}
</script>

<style lang="scss">
	page{
		background: #e8cfed;
		padding-bottom:190rpx
	}
	
	.address-list{
		margin:20rpx 0;
		background: rgba(199,185,244,0.6);
		overflow: hidden;
	}

	.add{
		background-color: #e8cfed;
		position:fixed;
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
