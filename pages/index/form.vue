<template>
	<view class="container">
		<form>
			<view class="list-bar">文本输入</view>
			<view class="w-form">
				<view class="title">标题</view>
				<input name="input" placeholder="请输入文本" />
			</view>
			<view class="w-form">
				<view class="title">输入地址</view>
				<input name="input" placeholder="请确定位置" />
				<view class="icon-dingwei"></view>
			</view>
			<view class="w-form">
				<view class="title">验证码</view>
				<input name="input" placeholder="请输入验证码" />
				<button type="primary" class="w-btn">验证码</button>
			</view>
			<view class="w-form">
				<view class="title">手机号码</view>
				<input name="input" placeholder="请输入手机号码" />
				<view class="w-cup">
					<view class="w-tag bg-grey">+86</view>
					<view class="w-tag line-grey w-border">中国大陆</view>
				</view>
			</view>
			<view class="list-bar">选择器</view>
			<view class="w-form">
				<view class="title">单列选择</view>
				<picker :value="pickerIndex" :range="picker" @change="PickerChange">
					<view>{{ picker[pickerIndex] }}</view>
				</picker>
			</view>
			<view class="w-form">
				<view class="title">多列选择</view>
				<picker mode="multiSelector" :value="multiIndex" @columnchange="MultiColumnChange" :range="multiArray" @change="MultiChange">
					<view>{{ multiArray[0][multiIndex[0]] }}，{{ multiArray[1][multiIndex[1]] }}，{{ multiArray[2][multiIndex[2]] }}</view>
				</picker>
			</view>
			<view class="w-form">
				<view class="title">时间选择</view>
				<picker mode="time" :value="time" start="09:01" end="21:01" @change="TimeChange">
					<view class="picker">
						{{time}}
					</view>
				</picker>
			</view>
			<view class="w-form">
				<view class="title">日期选择</view>
				<picker mode="date" :value="date" start="2015-09-01" end="2020-09-01" @change="DateChange">
					<view class="picker">
						{{date}}
					</view>
				</picker>
			</view>
			<view class="w-form">
				<view class="title">地址选择</view>
				<picker mode="region" @change="RegionChange" :value="region">
					<view class="picker">
						{{region[0]}}，{{region[1]}}，{{region[2]}}
					</view>
				</picker>
			</view>
			<view class="w-form">
				<view class="title">文本框</view>
				<textarea maxlength="-1" :disabled="modalName!=null" @input="textareaBInput" placeholder="多行文本输入框"></textarea>
			</view>
			<view class="w-form">
				<view class="title">开关选择</view>
				<switch @change="SwitchA" color="#2C2C2C"></switch>
			</view>
			<view class="w-form">
				<view class="title">单选选择</view>
				<radio-group @change="RadioChange">
					<label>
						<radio :value="china" /><text>中国</text>
						<radio :value="japan" /><text>美国</text>
					</label>
				</radio-group>
			</view>
			<view class="w-form">
				<view class="title">多项选择</view>
				<checkbox-group name="">
					<label>
						<checkbox :value="guangdong" /><text>广东</text>
						<checkbox :value="jiangsu" /><text>江苏</text>
						<checkbox :value="zhejiang" /><text>浙江</text>
					</label>
				</checkbox-group>
			</view>
		</form>
	</view>
</template>

<script>
export default {
	data() {
		return {
			pickerIndex: 1,
			multiIndex: [0, 0, 0],
			picker: ['王大头', '王大合', '王大脸'],
			multiArray: [['无脊柱动物', '脊柱动物'], ['扁性动物', '线形动物', '环节动物', '软体动物', '节肢动物'], ['猪肉绦虫', '吸血虫']],
			time: '12:01',
			date: '2018-12-25',
			region: ['广东省', '深圳市', '盐田区'],
		};
	},
	methods: {
		PickerChange(e) {
			this.pickerIndex = e.detail.value;
		},
		MultiChange(e) {
			this.multiIndex = e.detail.value;
		},
		MultiColumnChange(e) {
			let data = {
				multiArray: this.multiArray,
				multiIndex: this.multiIndex
			};
			data.multiIndex[e.detail.column] = e.detail.value;
			switch (e.detail.column) {
				case 0:
					switch (data.multiIndex[0]) {
						case 0:
							data.multiArray[1] = ['扁性动物', '线形动物', '环节动物', '软体动物', '节肢动物'];
							data.multiArray[2] = ['猪肉绦虫', '吸血虫'];
							break;
						case 1:
							data.multiArray[1] = ['鱼', '两栖动物', '爬行动物'];
							data.multiArray[2] = ['鲫鱼', '带鱼'];
							break;
					}
					data.multiIndex[1] = 0;
					data.multiIndex[2] = 0;
					break;
				case 1:
					switch (data.multiIndex[0]) {
						case 0:
							switch (data.multiIndex[1]) {
								case 0:
									data.multiArray[2] = ['猪肉绦虫', '吸血虫'];
									break;
								case 1:
									data.multiArray[2] = ['蛔虫'];
									break;
								case 2:
									data.multiArray[2] = ['蚂蚁', '蚂蟥'];
									break;
								case 3:
									data.multiArray[2] = ['河蚌', '蜗牛', '蛞蝓'];
									break;
								case 4:
									data.multiArray[2] = ['昆虫', '甲壳动物', '蛛形动物', '多足动物'];
									break;
							}
							break;
						case 1:
							switch (data.multiIndex[1]) {
								case 0:
									data.multiArray[2] = ['鲫鱼', '带鱼'];
									break;
								case 1:
									data.multiArray[2] = ['青蛙', '娃娃鱼'];
									break;
								case 2:
									data.multiArray[2] = ['蜥蜴', '龟', '壁虎'];
									break;
							}
							break;
					}
					data.multiIndex[2] = 0;
					break;
			}
			this.multiArray = data.multiArray;
			this.multiIndex = data.multiIndex;
		},
		TimeChange(e) {
			this.time = e.detail.value
		},
		DateChange(e) {
			this.date = e.detail.value
		},
		RegionChange(e) {
			this.region = e.detail.value
		}
		
	}
};
</script>

<style>
.container {
	background-color: #c0c4cc;
}
</style>
