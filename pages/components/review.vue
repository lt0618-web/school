<template>
	<view>
		<view class="uni-padding-wrap" v-for="(item,index) in revlist" :index="index" :key="index">
			
			<view class="uni-comment">
				
				<view class="uni-comment-list">
				    <view class="uni-comment-face">
				        <image :src="item.icon" mode="widthFix"></image>
				    </view>
				    <view class="uni-comment-body">
				        <view class="uni-comment-top">
				            <text>{{item.name}}</text>
				        </view>
				        <view class="uni-comment-date">
				            <text>{{item.date}}</text>
				        </view>  
				    </view>
				</view>
				
				<view class="uni-comment-content"><text>{{item.text}}</text></view>
				
				<view class="uni-comment-img">
					<u-grid :col="4" :border='false'>
							<u-grid-item v-for="(item2,index2) in item.imgList" :key="index2" :index="index2" bg-color="rgba(199,185,244,0)" :custom-style="listStyle">
								<image :src="item2.url" mode="widthFix"></image>
							</u-grid-item>
					</u-grid>
				</view>  
				
			</view>
		</view>
	</view>
</template>

<script>
    export default {
		 name: 'reviewItem',
		 props:{
			revlist:{
				type:Array,
				default() {
					return[{
						icon:"/static/shopping/icon_mz@3x.png",
						name:"热心网友",
						date:"08/12  23:30",
						text:"挺好的，收到后立刻装上，非常满意。强烈推荐推荐！挺好的，收到后立刻装上，非常满意。强烈推荐推荐！挺好的，收到后立刻装上，非常满意。强烈推荐推荐！",
						imgList:[{
							url:"/static/shopping/img_spt2@3x.png"
						}]
					}]
						 
				}
			} 
		 },
		 data(){
			 return {
				 listStyle:{
					"padding":" 0",
				}
			}
		 }
		 
    }
</script>

<style lang="scss">
    /* comment */
    page {
        background-color: rgba(199,185,244,1);
    }

    view {
        font-size: 28rpx;
    }
    .uni-padding-wrap {
        padding: 30rpx 0;
		  color: #4e48b2;
		  font-size: 28rpx;
		  
		  .uni-comment {
		      display: flex;
		      flex-grow: 1;
		      flex-direction: column;
		  }
		  
		  .uni-comment-list {
		      flex-wrap: nowrap;
		      width: 100%;
		      display: flex;
				padding:0 30rpx;
		  }
		  
		  .uni-comment-face {
		      width: 60rpx;
		      height: 60rpx;
		      border-radius: 100%;
		      margin-right: 20rpx;
		      flex-shrink: 0;
		      overflow: hidden;
		  }
		  
		  .uni-comment-face image {
		      width: 100%;
		      border-radius: 100%;
		  }
		  
		  .uni-comment-body {
		      width: 100%;
		  }
		  .uni-comment-top{
			  height: 26rpx;			 
			  line-height: 26rpx;
			  font-family: PingFang SC Bold, PingFang SC Bold-Bold;
			  font-weight: 700;
			  text{
				color: #4e48b2;
			  }
		  }
		  .uni-comment-date{
			  height: 15rpx;
			  font-size: 20rpx;
			  font-family: Alibaba PuHuiTi-R, Alibaba PuHuiTi-R-PuHuiTi-R;
			  font-weight: PuHuiTi-R;
			  color: #7973d6;
		  }
		  .uni-comment-content{
				padding:0 30rpx;
			  line-height: 36rpx;
			  opacity: 1;
			  font-family: PingFang SC Medium, PingFang SC Medium-Medium;
			  font-weight: 500;
		  }
		  .uni-comment-img{
				padding:20rpx;
			  width: 100%;
			  .u-grid-item{
				   padding:0 10rpx;
			  }
			  image{
				  width: 100%;
			  }
		  }
    }

</style>