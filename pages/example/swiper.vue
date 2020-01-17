<template>
	<view>
		<view class="list-bar">全屏轮播</view>
		<swiper class="screen-swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="true" :circular="true"
		 :autoplay="true" interval="5000" duration="500">
			<swiper-item v-for="(item,index) in swiperList" :key="index">
				<image :src="item.url" mode="aspectFill"></image>
			</swiper-item>
		</swiper>
		<view class="list-bar">卡片轮播</view>
		<swiper class="card-swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="true" :circular="true"
		 :autoplay="true" interval="5000" duration="500" @change="cardSwiper" >
			<swiper-item v-for="(item,index) in swiperList" :key="index" :class="cardCur==index?'cur':''">
				<view class="swiper-item">
					<image :src="item.url" mode="aspectFill"></image>
				</view>
			</swiper-item>
		</swiper>
		<view class="list-bar">堆叠轮播</view>
		<view class="tower-swiper" @touchmove="TowerMove" @touchstart="TowerStart" @touchend="TowerEnd">
			<view class="tower-item" :class="item.zIndex==1?'none':''" v-for="(item,index) in swiperList" :key="index" :style="[{'--index': item.zIndex,'--left':item.mLeft}]" :data-direction="direction">
				<view class="swiper-item">
					<image :src="item.url" mode="aspectFill"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cardCur: 0,
				swiperList:[{
					id:0,
					url:"https://game.gtimg.cn/images/yxzj/coming/v2/skins/image/20191230/f2785fd14af2b9c10e3c77445f6d1eaa.jpg"
				},{
					id:1,
					url:"https://game.gtimg.cn/images/yxzj/coming/v2/skins/image/20191230/9b2be2bc107e76bfa55e36e935ca4488.jpg"
				},{
					id:2,
					url:"https://game.gtimg.cn/images/yxzj/coming/v2/skins/image/20191213/fc7c09f1ff283762836d27e4442f295b.jpg"
				},{
					id:3,
					url:"https://game.gtimg.cn/images/yxzj/coming/v2/skins/image/20191226/e5e5eaf3e8ac9cfd4b07bea36bdb65b7.jpg"
				},{
					id:4,
					url:"https://game.gtimg.cn/images/yxzj/coming/v2/skins/image/20191223/f68a50a1137f2c41d50dc0e68f5c215b.jpg"
				},{
					id:5,
					url:"https://game.gtimg.cn/images/yxzj/coming/v2/skins/image/20191212/3296e8d25d0b69ada6e9cab0d408aebd.jpg"
				}],
				dotStyle: false,
				towerStart: 0,
				direction: ''
			};
		},
		onLoad() {
			this.TowerSwiper('swiperList');
			// 初始化towerSwiper 传已有的数组名即可
		},
		methods: {
			DotStyle(e) {
				this.dotStyle = e.detail.value
			},
			// cardSwiper
			cardSwiper(e) {
				this.cardCur = e.detail.current
			},
			// towerSwiper
			// 初始化towerSwiper
			TowerSwiper(name) {
				let list = this[name];
				for (let i = 0; i < list.length; i++) {
					list[i].zIndex = parseInt(list.length / 2) + 1 - Math.abs(i - parseInt(list.length / 2))
					list[i].mLeft = i - parseInt(list.length / 2)
				}
				this.swiperList = list
			},

			// towerSwiper触摸开始
			TowerStart(e) {
				this.towerStart = e.touches[0].pageX
			},

			// towerSwiper计算方向
			TowerMove(e) {
				this.direction = e.touches[0].pageX - this.towerStart > 0 ? 'right' : 'left'
			},

			// towerSwiper计算滚动
			TowerEnd(e) {
				let direction = this.direction;
				let list = this.swiperList;
				if (direction == 'right') {
					let mLeft = list[0].mLeft;
					let zIndex = list[0].zIndex;
					for (let i = 1; i < this.swiperList.length; i++) {
						this.swiperList[i - 1].mLeft = this.swiperList[i].mLeft
						this.swiperList[i - 1].zIndex = this.swiperList[i].zIndex
					}
					this.swiperList[list.length - 1].mLeft = mLeft;
					this.swiperList[list.length - 1].zIndex = zIndex;
				} else {
					let mLeft = list[list.length - 1].mLeft;
					let zIndex = list[list.length - 1].zIndex;
					for (let i = this.swiperList.length - 1; i > 0; i--) {
						this.swiperList[i].mLeft = this.swiperList[i - 1].mLeft
						this.swiperList[i].zIndex = this.swiperList[i - 1].zIndex
					}
					this.swiperList[0].mLeft = mLeft;
					this.swiperList[0].zIndex = zIndex;
				}
				this.direction = ""
				this.swiperList = this.swiperList
			},
		}
	}
</script>

<style>
	.screen-swiper {
		min-height: 375upx;
	}
	
	.screen-swiper image,
	.screen-swiper video,
	.swiper-item image,
	.swiper-item video {
		width: 100%;
		display: block;
		height: 100%;
		margin: 0;
		pointer-events: none;
	}
	
	.card-swiper {
		height: 560upx !important;
	}
	
	.card-swiper swiper-item {
		width: 610upx !important;
		left: 70upx;
		box-sizing: border-box;
		padding: 40upx 0upx 70upx;
		overflow: initial;
	}
	
	.card-swiper swiper-item .swiper-item {
		width: 100%;
		display: block;
		height: 100%;
		border-radius: 10upx;
		transform: scale(0.9);
		transition: all 0.2s ease-in 0s;
		overflow: hidden;
	}
	
	.card-swiper swiper-item.cur .swiper-item {
		transform: none;
		transition: all 0.2s ease-in 0s;
	}
	
	
	.tower-swiper {
		height: 420upx;
		position: relative;
		max-width: 750upx;
		overflow: hidden;
	}
	
	.tower-swiper .tower-item {
		position: absolute;
		width: 300upx;
		height: 380upx;
		top: 0;
		bottom: 0;
		left: 50%;
		margin: auto;
		transition: all 0.2s ease-in 0s;
		opacity: 1;
	}
	
	.tower-swiper .tower-item.none {
		opacity: 0;
	}
	
	.tower-swiper .tower-item .swiper-item {
		width: 100%;
		height: 100%;
		border-radius: 6upx;
		overflow: hidden;
	}
	.tower-swiper .tower-item {
		transform: scale(calc(0.5 + var(--index) / 10));
		margin-left: calc(var(--left) * 100upx - 150upx);
		z-index: var(--index);
	}
</style>
