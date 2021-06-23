<template>
	<view>
		<view>
			<u-navbar
			back-text="" 
			title="分类商品" 
			back-icon-color="#fff"
			title-color="#fff"
			title-size="36"
			height="50" 
			:border-bottom="false"
			:background="navBackground">
			</u-navbar>
		</view>
		<view>
			<u-sticky>
				<u-tabs 
					:list="tabList" 
					:current="current" 
					@change="change" 
					height="70"
					font-size="30"
					active-color="#fff"
					inactive-color="rgba(255,255,255,0.5)"
					gutter="30"
					bg-color="rgba(199,185,244,1)"
					:show-bar="false"
					:bole="false">
				</u-tabs>
			</u-sticky>
		</view>
		<view class="list-dom">
			<goods :goodsList="comList"></goods>
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
				current: 0,
				navBackground:{
					"background-color":"rgba(199,185,244,1)"
				},
				listStyle:{
					"padding":"10rpx 0"
				},
				tabList:[{
					name:"百货"
				},{
					name:"衣服"
				},{
					name:"鞋子"
				},{
					name:"饰品"
				},{
					name:"帽子"
				},{
					name:"衣服"
				},{
					name:"饰品"
				}],
				comList:[],
				comList1:[{
					productId:'6',
					imgurl:'/static/shopping/img_spt1@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					productId:'6',
					imgurl:'/static/shopping/img_spt1@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					imgurl:'/static/shopping/img_spt1@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					productId:'6',
					url:'/static/shopping/img_spt1@3x.png',
					imgurl:'/static/shopping/img_spt1@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				}],
				comList2:[{
					productId:'6',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					productId:'6',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					productId:'6',
					url:'/static/shopping/img_spt2@3x.png',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					productId:'6',
					url:'/static/shopping/img_spt2@3x.png',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				}]
			}
		},
		onLoad(option) {
			var id = option.id ? option.id : 0;
			var tabCur = id < this.tabList.length-1;
				this.comList = tabCur ? (/^(11)*$/.test('1'.repeat(id)) ? this.comList1 : this.comList2) : this.comList1;
				this.current = tabCur ? id :0;
		},
		methods: {
			change(index){
				this.current = index;
				this.comList = /^(11)*$/.test('1'.repeat(index)) ? this.comList1 : this.comList2;
			}
			
		}
	}
</script>

<style lang="scss">
	@import 'uview-ui/index.scss';

	page {
		min-height: 100%;
		background-color:#ecd5f2;
	}
	
	.list-dom{
		margin:10rpx;
	}
	
</style>
