<template>
	<view class="site-list">
		<view class="site-list-item" @click="onClick">
			<slot name="header">
				<view class="item_header">
					<view v-if="showExtraIcon" class="item_icon"><u-icon :color="extraIcon.color" :size="extraIcon.size" :name="extraIcon.type" /></view>
				</view>
			</slot>
			
			<slot name="body">
				<view class="item_content" :class="{ 'item_content-center': showExtraIcon}">
					<view v-if="name || phone" class="item_content-title">
						<text class="item_content-title-main">{{ name || '' }}</text>
						<text class="item_content-title-sub">{{ phone || '' }}</text>
					</view>
					<view v-if="site" class="item_content-note">
						<text v-if="tag" class="tags">
							<text v-for="(item, index) in tag" :key="index" :class="{blue:item.text=='默认'}">{{ item.text }}</text>
						</text>
						<text :class="tag ? 'item_content-note-con-padding' :''" class="item_content-note-con">{{ site }}</text>
					</view>
				</view>
			</slot>
			
			<slot name="footer">
				<view v-if="rightIcon" class="item_extra" :class="rightIcon==[]?'width':''">
					<u-icon v-for="(item,index) in rightIcon" :index="index" :key="index" :size="item.size" class="item_extra-icon" :name="item.type" :color="item.color" @click="item.click" />
				</view>
			</slot>
			
			<uni-icons v-if="showArrow || link" :size="linkIcon.size" class="icon-wrapper" :type="linkIcon.type" :color="linkIcon.color" />
		</view>
	</view>
</template>
<script>

export default {
	name: 'SiteListItem',
	props: {
		showExtraIcon: {
			type: Boolean,
			default: false
		},
		extraIcon: {
			type: Object,
			default() {
				return {}
				// return {
				// 	type: 'map-fill',
				// 	color: 'rgba(78,72,178,1)',
				// 	size: '40rpx'
				// };
			}
		},
		name: {
			type: String,
			default: ''
		},
		phone: {
			type: String,
			default: ''
		},
		site:{
			type: String,
			default: ''
		},
		tag:{
			type: Array,
			default(){	
				return []
				//    text: "默认",
			}
		},
		rightIcon:{
			type: Array,
			default(){
				return []
				// return[{
				// 	type:"/static/shopping/icon_del@2x.png",
				// 	color: '#000000',
				// 	size: "36rpx"
				// },{
				// 	type:"/static/shopping/icon_bj@2x.png",
				// 	color: '#000000',
				// 	size: "36rpx"
				// }]
			}
		},
		showArrow: {
			type: Boolean,
			default: false
		},
		link: {
			type: [Boolean,String],
			default: false
		},
		linkIcon:{
			type:Object,
			default(){
				return{
					type:"arrowright",
					// color:"#33333",
					color: 'rgba(195,195,195,1)',
					size: '20rpx'
				}
			}
		}
		
	},
	data() {
		return {
			
		}
	},
	methods: {
		onClick() {
			if ( this.link ) {
				uni.navigateTo({
					url:this.link
				})
			}
		}
		
	}
}
</script>

<style lang="scss">
	.site-list{
		font-size: 28rpx;
		margin:30rpx;
		position: relative;
	}
	.site-list-item{
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex: 1;
		font-size: 26rpx;
		position: relative;
		justify-content: space-between;
		align-items: center;
		flex-direction: row;
		
		.item_header{
			/* #ifndef APP-NVUE */
			display: flex;
			/* #endif */
			flex-direction: row;
			align-items: center;
			margin-right: 20rpx;
			
			.item_icon {
				flex-direction: row;
				justify-content: center;
				align-items: center;
			}
			
		}
		.item_content{
			/* #ifndef APP-NVUE */
			display: flex;
			/* #endif */
			flex: 1;
			color: #fff;
			overflow: hidden;
			flex-direction: column;
			justify-content: space-between;
			overflow: hidden;
			
			.item_content-center {
				justify-content: center;
			}
			
			.item_content-title {
				font-size:28rpx;
				overflow: hidden;
				.item_content-title-main{
					max-width: 180rpx;
					overflow: hidden;
					white-space: nowrap;
				   text-overflow: ellipsis;
					float: left;
					margin-right:26rpx;
				}
			}
			
			.item_content-note {
				margin-top: 16rpx;
				font-size: 22rpx;
				overflow: hidden;
				text-overflow: ellipsis;
				white-space: nowrap;
				height:50rpx ;
				
				.tags {
					display: inline;
					font-weight: normal;
					align-items: center;
					
					text {
						display: inline-block;
						padding:0 20rpx;
						height: 40rpx;
						line-height: 40rpx;
						font-size: 20rpx;
						border-radius: 40rpx;
						text-align: center;
						margin-right: 10rpx;
						background-color:rgba(78,72,178,0.6);
					}
					.blue{
						background-color:rgba(78,72,178,1);
					}
				}
				
			}
			
		}
		.item_extra {
			/* #ifndef APP-NVUE */
			display: flex;
			/* #endif */
			align-items: center;
			overflow: hidden;
			padding-top:24rpx;
			
			.item_extra-icon{
				margin-left:30rpx
			}
		}
		.item_extra.width{
			width: 136rpx;
		}
		
	}
	.icon-wrapper {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		align-items: right;
	}
</style>
