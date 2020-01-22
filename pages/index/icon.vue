<template>
	<view>
		<view class="list-bar">
			<view class="search-bar">
				<view class="icon-search sz-sm"></view>
				<input type="text" placeholder="search icon" confirm-type="search" @input="searchIcon" />
			</view>
		</view>
		<!-- 图标列表 -->
		<view class="grid-list">
			<view class="grid-item-col4" v-for="(item, index) in iconList" :key="index" v-if="item.isShow">
				<view :class="'icon-' + item.name" class="sz-big"></view>
				<view>{{ item.name }}</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			iconList: [
				{
					name: 'shangquan',
					isShow: true
				},
				{
					name: 'qingtie',
					isShow: true
				},
				{
					name: 'aixin',
					isShow: true
				},
				{
					name: 'bianji',
					isShow: true
				},
				{
					name: 'Dyanjing',
					isShow: true
				},
				{
					name: 'caidan',
					isShow: true
				},
				{
					name: 'anquan',
					isShow: true
				},
				{
					name: 'bangzhu',
					isShow: true
				},
				{
					name: 'buganxingqu',
					isShow: true
				},
				{
					name: 'bofangjilu',
					isShow: true
				},
				{
					name: 'chuangzuo',
					isShow: true
				},
				{
					name: 'chenggong',
					isShow: true
				},
				{
					name: 'ceshi',
					isShow: true
				},
				{
					name: 'dianhua',
					isShow: true
				},
				{
					name: 'dianzan',
					isShow: true
				},
				{
					name: 'dingwei',
					isShow: true
				},
				{
					name: 'diantong_guan',
					isShow: true
				},
				{
					name: 'dianying',
					isShow: true
				},
				{
					name: 'ditu',
					isShow: true
				},
				{
					name: 'diantong_kai',
					isShow: true
				},
				{
					name: 'dianyingpiao',
					isShow: true
				},
				{
					name: 'dingdan',
					isShow: true
				},
				{
					name: 'gengduo',
					isShow: true
				},
				{
					name: 'fanbei',
					isShow: true
				},
				{
					name: 'ertongpiao',
					isShow: true
				},
				{
					name: 'faxian',
					isShow: true
				},
				{
					name: 'ertongpiao',
					isShow: true
				},
				{
					name: 'gongyi',
					isShow: true
				},
				{
					name: 'hongbao',
					isShow: true
				},
				{
					name: 'fuzhi',
					isShow: true
				},
				{
					name: 'fenxiang',
					isShow: true
				},
				{
					name: 'huatifuhao',
					isShow: true
				},
				{
					name: 'huiyuan',
					isShow: true
				},
				{
					name: 'aliyu',
					isShow: true
				},
				{
					name: 'jiju',
					isShow: true
				},
				{
					name: 'jianshao',
					isShow: true
				},
				{
					name: 'kabao',
					isShow: true
				},
				{
					name: 'huati',
					isShow: true
				},
				{
					name: 'guanzhu',
					isShow: true
				},
				{
					name: 'maiyizengyi',
					isShow: true
				},
				{
					name: 'mima',
					isShow: true
				},
				{
					name: 'nan',
					isShow: true
				},
				{
					name: 'nv',
					isShow: true
				},
				{
					name: 'lihe',
					isShow: true
				},
				{
					name: 'paihangbang',
					isShow: true
				},
				{
					name: 'lipinka',
					isShow: true
				},
				{
					name: 'pengyouquan',
					isShow: true
				},
				{
					name: 'mingxinghuodong',
					isShow: true
				},
				{
					name: 'qupiao',
					isShow: true
				},
				{
					name: 'saoyisao',
					isShow: true
				},
				{
					name: 'rili',
					isShow: true
				},
				{
					name: 'pinglun',
					isShow: true
				},
				{
					name: 'qinghuiyuan',
					isShow: true
				},
				{
					name: 'riqian',
					isShow: true
				},
				{
					name: 'shandian',
					isShow: true
				},
				{
					name: 'shaixuan',
					isShow: true
				}
			]
		};
	},
	methods:{
		searchIcon(e) {
			let key = e.detail.value.toLowerCase();
			let list = this.iconList;
			for (let i = 0; i < list.length; i++) {
				let a = key;
				let b = list[i].name.toLowerCase();
				if (b.search(a) != -1) {
					list[i].isShow = true
				} else {
					list[i].isShow = false
				}
			}
			this.iconList = list
		}
	}
};
</script>

<style>
.sz-sm {
	font-size: 16px;
}
.sz-big {
	font-size: 40px;
}
</style>
