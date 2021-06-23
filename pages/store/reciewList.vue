<template>
	<view>
		<view>
			<u-navbar
			back-text="" 
			title="全部评价" 
			back-icon-color="#fff"
			title-color="#fff"
			title-size="36"
			height="50" 
			:border-bottom="false"
			:background="navBackground">
			</u-navbar>
		</view>
		
		<view class="review-list">
			<review :revlist='revlist'></review>
		</view>
	</view>
</template>

<script>
	import review from "../components/review.vue";
	export default {
    components: {
		 review
		 },
		data() {
			return {
				navBackground:{
					"background-color":"rgba(199,185,244,1)"
				}, 
				 revlist:[
					 {
					 	icon:"/static/shopping/iocn_bh@3x.png",
					 	name:"热心网友",
					 	date:"08/12  23:30",
					 	text:"挺好的，收到后立刻装上，非常满意。强烈推荐推荐!",
					 	imgList:[{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	}]
					 },{
					 	icon:"/static/shopping/iocn_bh@3x.png",
					 	name:"热心网友",
					 	date:"08/12  23:30",
					 	text:"挺好的，收到后立刻装上，非常满意。强烈推荐推荐!",
					 	imgList:[{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	}]
					 },{
					 	icon:"/static/shopping/iocn_bh@3x.png",
					 	name:"热心网友",
					 	date:"08/12  23:30",
					 	text:"挺好的，收到后立刻装上，非常满意。强烈推荐推荐!",
					 	imgList:[{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	}]
					 },{
					 	icon:"/static/shopping/iocn_bh@3x.png",
					 	name:"热心网友",
					 	date:"08/12  23:30",
					 	text:"挺好的，收到后立刻装上，非常满意。强烈推荐推荐!",
					 	imgList:[{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	},{
					 		url:"/static/shopping/img_spt2@3x.png"
					 	}]
					 }
				 ]
				
			}
		},
		onLoad() {
		},
		methods: {
		}
	}
</script>

<style lang="scss">
	@import 'uview-ui/index.scss';

	page {
		min-height: 100%;
		background-color:#ecd5f2;
		padding-bottom:20rpx;
	}
	.review-list{
		/deep/.uni-padding-wrap {
			margin: 10rpx 0;
			background-color: rgba(199,185,244,0.6);
		}
		
		/deep/.uni-comment-content{
			padding-left: 110rpx;
		}
		/deep/.uni-comment-img{
			padding-left: 100rpx;
		}
		
	}
	
</style>
