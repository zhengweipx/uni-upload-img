<template>
	<view>
		<view class="feedback-title" style="background-color: #efeff4;">
			<text>{{ title }}</text>
		</view>
		<view class="feedback-body feedback-uploader">
			<view class="uni-uploader">
				<view class="uni-uploader-head">
					<view class="uni-uploader-title">点击预览图片</view>
					<view class="uni-uploader-info">{{ dataList.length }}/{{ num }}</view>
				</view>
				<view class="uni-uploader-body">
					<view class="uni-uploader__files">
						<block v-for="(image, index) in dataList" :key="index">
							<view class="uni-uploader__file" style="position: relative; width: 198rpx; height: 198rpx;">
								<image class="uni-uploader__img" style="width: 198rpx; height: 198rpx;" :src="image" @tap="_previewImage(index)"></image>
								<view class="close-view" @tap="_close(index)">x</view>
							</view>
						</block>
						<view class="uni-uploader__input-box" style="width: 196rpx; height: 196rpx;" v-if="dataList.length < num">
							<view class="uni-uploader__input" style="width: 196rpx; height: 196rpx;" @tap="_chooseImg()"></view>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: 'ZwUploadImg',
	props: {
		title: {
			type: String,
			default: '图片(选填,提供问题图片,总大小10M以下)'
		},
		num: {
			type: Number,
			default: 9
		},
		dataList: {
			type: Array,
			default() {
				return [];
			}
		}
	},
	data() {
		return {};
	},
	methods: {
		_previewImage(index) {
			//预览图片
			uni.previewImage({
				urls: this.dataList,
				current: this.dataList[index]
			});
		},
		_chooseImg() {
			this.$emit('chooseImg');
		},
		_close(index) {
			this.dataList.splice(index, 1);
			this.$emit('close', this.dataList);
		}
	}
};
</script>

<style>
.close-view {
	text-align: center;
	line-height: 24rpx;
	height: 32rpx;
	width: 32rpx;
	border-radius: 50%;
	background: #ff5053;
	color: #ffffff;
	position: absolute;
	top: -12rpx;
	right: -8rpx;
	font-size: 24rpx;
}
</style>
