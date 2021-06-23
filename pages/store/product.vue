<template>
	<view>
		<view>
			<u-navbar
			back-text="" 
			title="商品详情" 
			back-icon-color="#fff"
			title-color="#fff"
			title-size="36"
			height="50" 
			:border-bottom="false"
			:background="navBackground">
			<view slot="right" class="slot-wrap" style="margin-right:30rpx">
					<u-icon name="share" color="#fff" size="36" @click="onShare"></u-icon>	
				</view>
			</u-navbar>
		</view>
		<view class="pro-img">
			<u-swiper 
			class="p-swiper" 
			:list="proDetail.imgList" 
			mode="dot"
			height="750"
			border-radius="0rpx"
			:autoplay="false"
			img-mode="widthFix"></u-swiper>
			<view class="pro-tex">
				<text class="tex-num">￥<strong>{{this.proDetail.textNum}}</strong></text>
				<text class="tex-val">{{this.proDetail.textVal}}</text>
				<text class="tex-peo">{{this.proDetail.textPeo}} 已购买</text>
			</view>
		</view>
		<view class="pro-list">
			<uni-list>
				<uni-list-item title="参数" rightText="查看全部" link @click="paramShow =true" :rightIcon="{color:'rgba(78,72,178,0.5)'}" ></uni-list-item>
				<uni-list-item title="规格" rightText="查看全部" link @click="modelSpecBtn" :rightIcon="{color:'rgba(78,72,178,0.5)'}" ></uni-list-item>
				<uni-list-item title="宝贝评价" rightText="查看全部" link to="/pages/store/reciewList" :rightIcon="{color:'rgba(78,72,178,0.5)'}"></uni-list-item>
				<reviewItem :revlist='revlist' class="rev-list"></reviewItem>
			</uni-list>
		</view>
		
		<view class="pro-detail">
			<view class="deta-tit">
				<text class="title">商品详情</text>
				<!-- <u-divider color="#fa3534">长河落日圆</u-divider> -->
			</view>
			<view class="deta-img">
				<image v-for="(item,index) in detailList" :index="index" :key="index" :src="item.url" mode="widthFix"></image>
			</view>
		</view>
		
		<view class="pro-bot-nav">
			<uni-goods-nav :fill="true"  :options="options" :buttonGroup="buttonGroup"  @click="onClick" @buttonClick="buttonClick" />
				
		</view>
		
		
		<view class="popup-dom">
			
			<view class="param-minute">
				<u-popup v-model="paramShow" mode="bottom" :closeable="true" close-icon-color="#000" close-icon-size="24" border-radius="40">
					<view>
						<text class="title">商品参数</text>
						<view class="content">
							<scroll-view scroll-y="true" style="height: 600rpx;">
								<view>
									<text v-for="(item,index) in paramList" class="minute" :key="index" :index="index"><strong>{{item.title}}：</strong>{{item.text}}</text>
								</view>
							</scroll-view>
						</view>
					</view>
				</u-popup>
			</view>
			
			<view class="popup-spec">
				<u-popup v-model="modelSpec" mode="bottom" :closeable="true" close-icon-color="#000" close-icon-size="24" border-radius="40">
					<view class="content">
						<scroll-view scroll-y="true" style="height: 600rpx;">
							<view class="cont-dom">
								<view class="uni-comment-list">
								    <view class="uni-comment-img">
								        <image :src="popupProd.img" mode="widthFix"></image>
								    </view>
								    <view class="uni-comment-body">
								        <view class="uni-comment-number">
								            <text>￥{{popupProd.number}}</text>
								        </view>
								        <view class="uni-comment-text">
								            <text>已选：“{{popupProd.default.color.text}},{{popupProd.default.diameter.text}}”</text>
								        </view>  
								    </view>
								</view>
								<text class="title"><strong>颜色</strong></text>
								<text class="title"><strong>颜色</strong></text>
							   <view class="btn-list">
									<u-button
									 size="mini"
									 v-for="(item,index) in popupProd.color"
									 :key="index"
									 :index="index"
									 :hair-line="false"
									 :disabled="item.disabled"
									 :custom-style="item.disabled ? customStyleDis : item.selected ? customStyleAct : customStyleDef"
									 hover-class="none"
									 @click="colorBtn(index)"
									>{{item.text}}</u-button>
						
								  </view>
								  <text class="title"><strong>伞内直径</strong></text>
								  <view class="btn-list">
									<u-button
									 size="mini"
									 v-for="(item,index) in popupProd.diameter"
									 :key="index"
									 :index="index"
									 :hair-line="false"
									 :disabled="item.disabled"
									 :custom-style=" item.disabled ? customStyleDis : item.selected ? customStyleAct : customStyleDef"
									 hover-class="none"
									 @click="diameterBtn(index)"
									>{{item.text}}</u-button>
							   </view>
								<view class="number">
									<text class="title"><strong>购买数量</strong>库存{{popupProd.count}}件</text>
									<u-number-box 
									v-model="numberValue" 
									@change="valChange" 
									:min="1" 
									:max="100"
									size="30"
									input-width="100"
									input-height="60"
									bg-color="rgba(242,242,242,1)"></u-number-box>
								</view>
								
							</view>
						</scroll-view>
						<view class="navs">
							<uni-goods-nav :fill="true" :options="[]" :buttonGroup="popupButtonGroup"  @buttonClick="popupButtonClick" />
						</view>
					</view>
				</u-popup>
			</view>
		</view>
		
	</view>
</template>

<script>
	import reviewItem from "../components/review.vue";
	export default {
    components: {
		 reviewItem
		 },
		data() {
			return {
				navBackground:{
					"background-color":"rgba(199,185,244,1)"
				}, 
				customStyleDef:{
					"background-color":"rgba(153,153,153,1)",
					"margin-right":"20rpx",
					"color":"#fff"
				},
				customStyleAct:{
					"background-color":"rgba(78,72,178,1)",
					"margin-right":"20rpx",
					"color":"#fff"
				},
				customStyleDis:{
					"background-color":"rgba(242,242,242,1)",
					"margin-right":"20rpx",
					"color":"#999"
				},
				numberValue:1,
				store:false,
				paramShow: false,
				modelSpec:false,
				proDetail:{
					textNum:"20.00",
					textVal:"插画全自动雨伞折叠女晴雨两用太阳伞防晒防 紫外线学生ins遮阳伞",
					textPeo:"123,445",
					
					imgList:[{
						image:"/static/shopping/img_spt1@3x.png"
					},{
						image:"/static/shopping/img_spt1@3x.png"
					},{
						image:"/static/shopping/img_spt1@3x.png"
					},{
						image:"/static/shopping/img_spt1@3x.png"
					},{
						image:"/static/shopping/img_spt1@3x.png"
					}],
				},
				detailList:[{
					url:"/static/shopping/img_spxq@2x.png"
				},{
					url:"/static/shopping/img_spxq@2x.png"
				}],
				paramList:[{
					title:'材质',
					text:'钢架/绸布',
					},{
					title:'产地',
					text:'江苏徐州铜山区铜山万达广场',
					},{
					title:'颜色分类',
					text:'蓝色、绿色、黑色',
					},{
					title:'材质',
					text:'钢架/绸布',
					},{
					title:'产地',
					text:'江苏徐州铜山区铜山万达广场',
					},{
					title:'颜色分类',
					text:'蓝色、绿色、黑色',
					},{
					title:'材质',
					text:'钢架/绸布',
					},{
					title:'产地',
					text:'江苏徐州铜山区铜山万达广场',
					},{
					title:'颜色分类',
					text:'蓝色、绿色、黑色',
				}],
				options: [{
					icon: 'shop',
					iconColor:'rgba(78,72,178,1)',
					text: '店铺',
					size:'21'
				}, {
					icon: 'headphones',
					iconColor:'rgba(78,72,178,1)',
					text: '客服',
					size:'21'
				}, {
					icon: 'star',
					iconColor:'rgba(78,72,178,1)',
					text: '收藏',
					size:'22'
				}],
				 buttonGroup: [{
				   text: '加入购物车',
				   backgroundColor: '#fff',
				   color: 'rgba(78,72,178,1)',
					border:'1rpx solid rgba(78,72,178,1)'
				 },
				 {
				   text: '立即购买',
				   backgroundColor: 'rgba(78,72,178,1)',
				   color: '#fff',
					border:'1rpx solid rgba(78,72,178,1)'
				 }
				 ],
				 popupButtonGroup:[],
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
					 }
				 ],
				 popupProd:{
					 img:"/static/shopping/img_spt2@3x.png",
					 number:"29.00",
					 count:"258795",
					 default:{
					  color:{
						text:"浅蓝"
					  },
					  diameter:{
						text:"120cm"
					  }
					 },
					 color:[{
					  text:"浅蓝",
					  disabled: false,
					  selected: true
					  },{
					  text:"卡其",
					  disabled: true,
					  selected: false
					  },{
					  text:"米白",
					  disabled: false,
					  selected: false
					}],
					diameter:[{
					  text:"106cm",
					  disabled: true,
					  selected: false
					  },{
					  text:"120cm",
					  disabled: false,
					  selected: true
					  },{
					  text:"190cm",
					  disabled: false,
					  selected: false
					}],
				}
				
			}
		},
		onLoad() {
			this.popupButtonGroup = this.buttonGroup;
		},
		methods: {
			onClick(e) {
				var index = e.index;
				if(index == 2){
					if(this.store){
						this.options[index].icon='star';
						this.options[index].iconColor='rgba(78,72,178,1)';
						this.store = false;
					}else{
						this.options[index].icon='star-filled';
						this.options[index].iconColor='rgba(255,77,77,1)';
						this.store = true;
					}
				}else{
					
					index == 0?
					uni.navigateTo({
						url:'#'//店铺地址
					})	:
					uni.navigateTo({
						url:'#'//客服地址
					});
				}
			},
			buttonClick(e) {
				var text =this.buttonGroup[e.index].text;
				this.popupButtonGroup = [{
				   text: text,
				   backgroundColor: 'rgba(78,72,178,1)',
				   color: '#fff',
					border:'1rpx solid rgba(78,72,178,1)'
				}];
				this.modelSpec=true;
				
				console.log(e.index);
			},
			modelSpecBtn(){
				this.popupButtonGroup = this.buttonGroup;
				this.modelSpec=true;
			},
		colorBtn(index){
		    this.popupProd.color[index].selected = true;
		    this.popupProd.default.color.text = this.popupProd.color[index].text;
		    for(let key in this.popupProd.color) {
		     let nowbtn = this.popupProd.color[key];
		     if(key != index) {
		      this.popupProd.color[key].selected = false
		     }
		    }
		   },
		   diameterBtn(index){
		    this.popupProd.diameter[index].selected = true;
		    this.popupProd.default.diameter.text = this.popupProd.diameter[index].text;
		    for(let key in this.popupProd.diameter) {
		     let nowbtn = this.popupProd.diameter[key];
		     if(key != index) {
		      this.popupProd.diameter[key].selected = false;
		     }
		    }
		   },
			popupButtonClick(e){
				 this.modelSpec=false;
				 if(this.popupButtonGroup[0].text == this.buttonGroup[1].text){
					 uni.navigateTo({
					 	url: '/pages/store/orderDetails'
					 })
				 }
			},
			valChange(e) {
				console.log('当前值为: ' + e.value)
			},
			onShare(){
				
			}
		}
	}
</script>

<style lang="scss">
	@import 'uview-ui/index.scss';

	page {
		min-height: 100%;
		background-color:#ecd5f2;
		padding-bottom:130rpx;
	}
	
	.pro-img {
		background-color: rgba(199,185,244,0.6);
		
		/deep/.u-indicator-item-dot{
			width: 20rpx;
			height: 20rpx;
			margin: 10rpx 20rpx;
			background-color: rgba(255,255,255,0.5);
		}
		/deep/.u-indicator-item-dot-active{
			background-color: rgba(140,144,213,1);
			
		}
		
		.pro-tex{
			padding:20rpx 36rpx;
			font-family: PingFang SC Bold, PingFang SC Bold-Bold;
			line-height: 48rpx;
			color: #4e48b2;
			
			.tex-num{
				font-weight: 700;
				font-size: 30rpx;
				strong{
					font-size: 48rpx;
				}
				display: block;
			}
			.tex-val{
				font-size: 34rpx;
				margin: 10rpx 0;
				height:96rpx;
				display: -webkit-box;
				-webkit-box-orient: vertical;
				-webkit-line-clamp: 2;
				overflow: hidden;
			}
			.tex-peo{
				text-align: right;
				display: block;
				color:rgba(78,72,178,0.5);
				font-size: 28rpx;
			}
		}
	}
	
	.pro-list{
		padding-top:10rpx;
		margin-bottom: 10rpx;
		background-color: #fff;
		
		.rev-list{
			background-color: rgba(199,185,244,0.6);
			/deep/.uni-padding-wrap{
				padding-top:0;
			}
		}
		.uni-list-item{
			height: 100rpx;
			background-color: rgba(199,185,244,0.6);
			
			/deep/.uni-list-item__content-title,
			/deep/.uni-list-item__extra-text{
				font-size: 28rpx;
				color:rgba(120,114,221,1);
			}
			/deep/.uni-list-item__extra-text{
				opacity: 0.5;
			}
			.uni-icon-wrapper{
				color:rgba(120,114,221,1);
				
			}
		}
		/deep/.uni-list::before{
			height: 0;
		}
		/deep/.uni-list::after{
			height: 0;
		}
		/deep/.uni-list--border:after{
			background-color:rgba(255,255,255,1);
		}
		/deep/.uni-list--border-top{
			background-color:rgba(255,255,255,1);
		}
		/deep/.uni-list--border-bottom{
			background-color:rgba(199,185,244,0);
		}
	}
	
	.pro-detail{
		.deta-tit{
			height: 130rpx;
			padding: 40rpx 0;
			text-align: center;
			position: relative;
			background-color: #fff;
			.title{
				font-size: 32rpx;
				font-family: PingFang SC Medium, PingFang SC Medium-Medium;
				font-weight: 500;
				text-align: center;
				color: #4e48b2;
				line-height: 50rpx;
				height:50rpx;
			}
			.title::before,
			.title::after{
				display: block;
				content: '';
				position: absolute;
				width: 86rpx;
				height: 2rpx;
				background-color: rgba(199,185,244,1);
			}
			.title::before{
				left: 40%;
				margin-left: -100rpx;
				margin-top: 24rpx;
			}
			.title::after{
				margin-top: -24rpx;
				right: 40%;
				margin-right: -100rpx;
			}
		}
		.deta-img{
			/deep/.uni-padding-wrap .uni-comment-img .u-grid-item{
				padding:10rpx;
		  }
			image{
				display: block;
				margin: 0;
				width: 100%;
			}
		}
		
	}
	.pro-bot-nav{
		position: fixed;
		bottom: 0;
		width: 100%;
	}
	
	/deep/.uni-tab__right{
		border-radius: 40rpx;
		border: 2rpx solid rgba(78,72,178,1);
		overflow: hidden;
	}
	/deep/.uni-tab__text{
		color:rgba(78,72,178,1);
	}
	
	
	
	.popup-dom{
		text{
			display: block;
		}
		.param-minute{
			/deep/.u-close--top-right{
				 top:40rpx;
				 right:30rpx
			}
			.title{
				margin-top: 10rpx;
				padding:30rpx 0;
				line-height: 40rpx;
				font-size: 30rpx;
				text-align: center;
				color: #333333;
				position: relative;
			}
			.title::after{
				 position: absolute;
				 z-index: 10;
				 right: 0;
				 bottom: 0;
				 left: 0;
				 height: 1px;
				 content: '';
				 -webkit-transform: scaleY(.5);
				 transform: scaleY(.5);
				 background-color: #f2f2f2;
			}
				
			.minute{
				line-height: 40rpx;
				padding:30rpx 0;
				margin: 0 30rpx;
				position: relative;
				font-size: 28rpx;
				color:rgba(153,153,153,1);
				strong{
					color:rgba(51,51,51,1);
				}
			}
			.minute::after{
				 position: absolute;
				 z-index: 10;
				 right: 0;
				 bottom: 0;
				 left: 0;
				 height: 1px;
				 content: '';
				 -webkit-transform: scaleY(.5);
				 transform: scaleY(.5);
				 background-color: #f2f2f2;
			}
		}
		.popup-spec{
			overflow: hidden;
			.content{
				padding:30rpx;
				margin-bottom: 100rpx;
			}
			.uni-comment-list{
				padding-bottom:30rpx;
				position: relative;
				.uni-comment-img{
					width: 240rpx;
					height: 240rpx;
					margin-right: 30rpx;
					border-radius: 0;
					flex-shrink: 0;
					overflow: hidden;
					image{
						width: 100%;
					}
				}
				.uni-comment-number{
					margin-top: 130rpx;
					line-height: 35rpx;
					font-size: 48rpx;
					color: #fe2c55;
					text-indent: -10rpx;
				}
				.uni-comment-text{
					margin-top: 25rpx;
					line-height: 27rpx;
					font-size: 28rpx;
					color: #333333;
				}
			}
			.uni-comment-list::after{
				 position: absolute;
				 z-index: 10;
				 right: 0;
				 bottom: 0;
				 left: 0;
				 height: 1px;
				 content: '';
				 -webkit-transform: scaleY(.5);
				 transform: scaleY(.5);
				 background-color: #f2f2f2;
			}
			.title{
				line-height: 30rpx;
				font-size: 24rpx;
				color: #999999;
				padding:30rpx 0;
				strong{
					line-height: 30rpx;
					font-size: 32rpx;
					color: #333333;
					display: inline-block;
					padding-right: 15rpx;
				}
			}
			.number{
				overflow: hidden;
				margin-bottom: 30rpx;
				.title{
					float: left;
				}
				.u-numberbox{
					float: right;
					margin:20rpx 0;
					
					/deep/.u-icon-minus{
						border-radius:5rpx;
					}
					/deep/.u-number-input{
						border-radius:5rpx;
					}
					/deep/.u-icon-plus{
						border-radius:5rpx;
					}
				}
			}
			.btn-list{
				padding-bottom:30rpx ;
				position: relative;
			}
			.btn-list::after{
				 position: absolute;
				 z-index: 10;
				 right: 0;
				 bottom: 0;
				 left: 0;
				 height: 1px;
				 content: '';
				 -webkit-transform: scaleY(.5);
				 transform: scaleY(.5);
				 background-color: #f2f2f2;
			}
			.navs{
				position: fixed;
				bottom: 0;
				left:0;
				width: 100%;
				padding:20rpx 30rpx 10rpx;
				overflow: hidden;
				box-shadow: 0 0 10rpx 1rpx #f4f4f4 ;
				background-color: #fff;
				z-index: 14;
			}
		}
	}
	
</style>
