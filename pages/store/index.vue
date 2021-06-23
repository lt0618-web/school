<template>
	<view>
		<u-navbar 
		back-text="" 
		title="商城" 
		back-icon-color="#fff"
		title-color="#fff"
		title-size="36"
		:title-bold="true"
		height="50" 
		:border-bottom="false"
		:background="navBackground">
		</u-navbar>
		<view class="search-dom">
			<u-search 
				placeholder="關鍵字搜索商品" 
				placeholder-color="#fff"
				v-model="keyword"
				shape="round"
				search-icon="/static/shopping/icon_search@3x.png"
				search-icon-color="#fff"
				height="80"
				color="#fff"
				:input-style="{'background-color':'rgb(78,72,178,0)'}"
				:show-action="false"
				bg-color="rgb(78,72,178,0.2)"
				:disabled="true"
				@tap="toSearch">
			</u-search>
		</view>
		<view class="grid-dom">
			<swiper class="swiper" @change="swiperChange">
				<swiper-item>
					<u-grid :col="5" align="center" :border="false">
						<u-grid-item v-for="(item,index) in list" :key="index" :index="index" bg-color="rgb(255,255,255,0)" @click="xmlClick">
							<image :src="item.icon" class="badge-icon"></image>
							<text class="grid-text">{{item.text}}</text>
						</u-grid-item>
					</u-grid>
				</swiper-item>
				<swiper-item>
					<u-grid :col="5" align="center" :border="false">
						<u-grid-item v-for="(item,index) in list" :key="index" :index="index" bg-color="rgb(255,255,255,0)" @click="xmlClick">
							<image :src="item.icon" class="badge-icon"></image>
							<text class="grid-text">{{item.text}}</text>
						</u-grid-item>
					</u-grid>
				</swiper-item>
				<swiper-item>
					<u-grid :col="5" align="center" :border="false">
						<u-grid-item v-for="(item,index) in list" :key="index" :index="index" bg-color="rgb(255,255,255,0)" @click="xmlClick">
							<image :src="item.icon" class="badge-icon"></image>
							<text class="grid-text">{{item.text}}</text>
						</u-grid-item>
					</u-grid>
				</swiper-item>
			</swiper>
			<view class="indicator-dots" >
				<view class="indicator-dots-item" :class="[current == 0 ? 'indicator-dots-active' : '']">
				</view>
				<view class="indicator-dots-item" :class="[current == 1 ? 'indicator-dots-active' : '']">
				</view>
				<view class="indicator-dots-item" :class="[current == 2 ? 'indicator-dots-active' : '']">
				</view>
			</view>
		</view>
		<view class="list-dom">
			<text class="l-title">猜你喜欢</text>
			<goods :goodsList="comList" ></goods>
		</view>
		
	</view>
</template>

<script>
	import goods from "../components/goods.vue";
	export default {
    components: {
		 goods
		 },
		data() {
			return {
				keyword:'',
				current: 0,
				navBackground:{
					"background-color":"rgba(199,185,244,1)"
				},
				listStyle:{
					"padding":"10rpx 0"
					
				},
				list: [{
					icon:'/static/shopping/iocn_bh@3x.png',
					text:'百貨'
					},{
					icon:'/static/shopping/icon_yf@3x.png',
					text:'衣服'
					},{
					icon:'/static/shopping/icon_xz@3x.png',
					text:'鞋子'
					},{
					icon:'/static/shopping/icon_sp@3x.png',
					text:'飾品'
					},{
					icon:'/static/shopping/icon_mz@3x.png',
					text:'帽子'
					},{
					icon:'/static/shopping/iocn_bh@3x.png',
					text:'百貨'
					},{
					icon:'/static/shopping/icon_yf@3x.png',
					text:'衣服'
					},{
					icon:'/static/shopping/icon_xz@3x.png',
					text:'鞋子'
					},{
					icon:'/static/shopping/icon_sp@3x.png',
					text:'飾品'
					},{
					icon:'/static/shopping/icon_mz@3x.png',
					text:'帽子'
				}],
				comList:[{
					productId:'3',
					imgurl:'/static/shopping/img_spt1@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					productId:'4',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					productId:'5',
					imgurl:'/static/shopping/img_spt1@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					productId:'6',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				}]
			}
		},
		onLoad() {
		},
		methods: {
			swiperChange(item){
				this.current = item.detail.current;
			},
			xmlClick(index){				
				uni.navigateTo({
					url:'/pages/store/list?id=' + index
				})
				console.log(index)
			},
			productClick(index){
				uni.navigateTo({
					url:'/pages/store/product?productId='+this.comList[index].productId
				})
				console.log(index)
			},
			toSearch(e){
				console.log(e)
				// uni.navigateTo({
				// 	url: '/pages/store/search'
				// }) 
			}
		}
	}
</script>

<style lang="scss">
	@import 'uview-ui/index.scss';

	page {
		min-height: 100%;
		background-color:rgba(199,185,244,1);
	}
	.search-dom,.grid-dom{
		padding:20rpx 30rpx;
	}
	
	.search-dom{
		/deep/.u-content{
			background-color: rgba(78,72,178,0.2) ;
		}
	}
	.grid-dom{
		.badge-icon {
			width: 86rpx;
			height: 86rpx;
		}
			
		.grid-text {
			font-size: 26rpx;
			margin-top: 4rpx;
			color: #4E48B2;
		}
		.swiper {
			height: 370rpx;
		}
		.indicator-dots {
			margin-top: 10rpx;
			display: flex;
			justify-content: center;
			align-items: center;
		}
		/deep/.indicator-dots-item {
			background-color: rgba(78,72,178,0.2);
			height: 10rpx;
			width: 50rpx;
		}
		
		/deep/.indicator-dots-active {
			background-color: rgba(78,72,178,1);
		}
		/deep/.u-grid-item{
			background: none;
			.span{
				display: block;
			}
		}
	}
	
	
	.list-dom{
		margin:0 23rpx 40rpx;
		.l-title{
			display: block;
			height: 34rpx;
			opacity: 1;
			font-size: 36rpx;
			font-family: PingFang SC Bold, PingFang SC Bold-Bold;
			font-weight: 700;
			text-align: left;
			color: #4e48b2;
			line-height: 36rpx;
			padding:0 31rpx;
			margin-bottom:  30rpx;
		}
		// /deep/.u-grid-item{
		// 	background:none;
		// 	.l-dom{
		// 		background-color: rgba(199,185,244,0.6);
		// 		overflow: hidden;
		// 		margin: 0 9rpx;
		// 		border-radius: 15rpx;
		// 	}
		// }
	}
	
</style>
