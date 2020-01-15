<template>
	<view>
		<view class="list-bar">滑动导航</view>
		<scroll-view scroll-x class="nav" scroll-with-animation :scroll-left="scrollLeft">
			<view class="nav-item" :class="index==TabCur?' cur':''" v-for="(item,index) in 10" :key="index" @tap="tabClick" :data-id="index">
				Tab{{index}}
			</view>
		</scroll-view>
		<view class="list-bar">居中导航</view>
		<scroll-view scroll-x class="nav text-center">
			<view class="nav-item" :class="index==TabCur?' cur':''" v-for="(item,index) in 3" :key="index" @tap="tabClick" :data-id="index">
				Tab{{index}}
			</view>
		</scroll-view>
		<view class="list-bar">平分导航</view>
		<scroll-view scroll-x class=" nav">
			<view class="flex text-center">
				<view class="nav-item flex-sub" :class="index==TabCur?' cur':''" v-for="(item,index) in 4" :key="index" @tap="tabClick" :data-id="index">
					Tab{{index}}
				</view>
			</view>
		</scroll-view>
		<view class="list-bar">背景导航</view>
		<scroll-view scroll-x class="nav-bg text-center">
			<view class="bg-item" :class="index==TabCur?'text-white cur':''" v-for="(item,index) in 3" :key="index" @tap="tabClick" :data-id="index">
				Tab{{index}}
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				TabCur: 0,
				scrollLeft: 0
			};
		},
		methods: {
			tabClick(e) {
				this.TabCur = e.currentTarget.dataset.id;
				this.scrollLeft = (e.currentTarget.dataset.id - 1) * 60
			}
		}
	}
</script>

<style lang="scss">
	.list-bar {
		display: flex;
		position: relative;
		align-items: center;
		min-height: 100upx;
		justify-content: space-between;
		color:#2c2c2c;
	}
	.nav {
		background-color: #ffffff;
		white-space: nowrap;
		.nav-item {
			height: 90upx;
			display: inline-block;
			line-height: 90upx;
			margin: 0 10upx;
			padding: 0 20upx;
			color:#c0c4cc
		}
		.cur{
			border-bottom: 4upx solid;
			color:#2c2c2c;
		}
	}
	.text-center {
		text-align: center;
	}
	.nav-bg {
		background-color: #fadbd9;
		white-space: nowrap;
		.bg-item {
			height: 90upx;
			display: inline-block;
			line-height: 90upx;
			margin: 0 10upx;
			padding: 0 20upx;
			color:#e54d42
		}
		.cur{
			border-bottom: 4upx solid;
			color:#e54d42;
		}
	}
</style>
