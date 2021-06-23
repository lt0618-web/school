<template>
	<view>
		<view class="uni-goods-wrap">
			<u-grid :col="2" align="center" :border="false" >
				<u-grid-item v-for="(item,index) in goodsList" :key="index" :index="index" @click="click" bg-color="rgb(255,255,255,0)" :custom-style="listStyle"
				>
					<view class="l-dom">
						<image :src="item.imgurl" class="l-img" mode="widthFix"></image>
						<text class="l-text">{{item.title}}</text>
						<view class="l-number">
							<text class="l-num">￥<strong>{{item.num}}</strong></text>
							<text class="l-peo">{{item.people}}人付款</text>
						</view>
					</view>
				</u-grid-item>
			</u-grid>
		</view>
	</view>
</template>

<script>
    export default {
		 name: 'goodsItem',
		 props:{
			goodsList:{
				type:Array,
				default() {
					return[{
					url:'/static/shopping/img_spt1@3x.png',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					url:'/static/shopping/img_spt1@3x.png',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					url:'/static/shopping/img_spt1@3x.png',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				},{
					url:'/static/shopping/img_spt1@3x.png',
					imgurl:'/static/shopping/img_spt2@3x.png',
					title:'汉尚华莲枫灵原创汉服 女明制交领衫搭褶裙汉尚华莲枫',
					num:'199',
					people:'312'
				}]
						 
				}
			} 
		 },
		 data(){
			 return {
				 listStyle:{
					"padding":"5rpx",
				}
			}
		 },
		 methods:{
			 click(index){
				 var linkUrl = '/pages/store/product?productId='+this.goodsList[index].productId;
				 if(this.goodsList[index].url){
					 linkUrl = this.goodsList[index].url;
				 }
				uni.navigateTo({
					url:linkUrl
				})
				console.log(index)
			}
		 }
		 
    }
</script>

<style lang="scss">
    /* comment */
    page {
        background-color: rgba(199,185,244,0.3);
    }

    view {
        font-size: 28rpx;
    }
    .uni-goods-wrap {
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
        /deep/.u-grid-item{
        	background:none;
        	.l-dom{
        		background-color: rgba(199,185,244,0.6);
        		overflow: hidden;
        		margin: 0 9rpx;
        		border-radius: 15rpx;
        	}
        }
        .l-img{
        	width: 100%;
        	height: auto;
        	display: block;
        }
        .l-text{
        	height: 72rpx;
        	opacity: 1;
        	font-size: 28rpx;
        	font-family: PingFang SC Medium, PingFang SC Medium-Medium;
        	font-weight: 500;
        	text-align: left;
        	color: #4e48b2;
        	line-height: 36rpx;
        	display: -webkit-box;
        	-webkit-box-orient: vertical;
        	-webkit-line-clamp: 2;
        	overflow: hidden;
        	margin:20rpx;
        }
        .l-number{
        	line-height: 36rpx;
        	height: 36rpx;
        	margin-bottom: 20rpx;
        	width: 100%;
        	overflow: hidden;
        	color: #4e48b2;
        	.l-num{
        		margin-left: 23rpx;
        		font-size: 24rpx;
        		font-family: PingFang SC Bold, PingFang SC Bold-Bold;
        		font-weight: 700;
        		text-align: left;
        		strong{
        			font-size: 34rpx;
        		}
        	}
        	.l-peo{
        		text-align: right;
        		float: right;
        		margin-right: 23rpx;
        		opacity: 0.6;
        		font-size: 20rpx;
        		font-family: PingFang SC Medium, PingFang SC Medium-Medium;
        		font-weight: 500;
        	}
        }
    }

</style>