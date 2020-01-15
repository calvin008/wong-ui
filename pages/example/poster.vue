<template>
	<view class="container">
		<button style="color: white;background: linear-gradient(to left, #f58365, #ff188a);" @click="openPost">打开海报</button>
		<poster v-if="posterShow"></poster>
	</view>
</template>

<script>
	import poster from '@/components/wongPoster.vue';
	export default {
		components: {
			poster
		},
		data() {
			return {
				posterShow:false
			}
		},
		onLoad() {
			
		},
		methods: {
			openPost(){
				this.posterShow = true
			}
		}
	}
</script>

<style>
	.container{
		height: 100vh;
		width: 100vw;
		display: flex;
		align-items: center;
		justify-content: center;
		}
</style>
