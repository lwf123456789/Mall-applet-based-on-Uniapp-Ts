<script setup lang="ts">
	import { useMemberStore } from '@/stores'

	const memberStore = useMemberStore()
	// 退出登录
	const onLogout = () => {
		// 模态弹窗
		uni.showModal({
			content: '是否退出登录？',
			confirmColor: '#27BA9B',
			success: (res) => {
				if (res.confirm) {
					// 清理用户信息
					memberStore.clearProfile()
					// 返回上一页
					uni.navigateBack()
				}
			},
		})
	}
</script>

<template>
	<view class="viewport">
		<!-- 列表1 -->
		<view class="list" v-if="memberStore.profile">
			<navigator url="/pagesMember/address/address" hover-class="none" class="item arrow">
				我的收货地址
			</navigator>
		</view>
		<!-- #ifdef MP-WEIXIN -->
		<!-- 列表2 -->
		<view class="list">
			<button hover-class="none" class="item arrow" open-type="openSetting">授权管理</button>
			<button hover-class="none" class="item arrow" open-type="feedback">问题反馈</button>
			<button hover-class="none" class="item arrow" open-type="contact">联系我们</button>
		</view>
		<!-- #endif -->
		<!-- 列表3 -->
		<view class="list">
			<button hover-class="none" class="item arrow">关于在线商城</button>
		</view>
		<!-- 操作按钮 -->
		<view class="action" v-if="memberStore.profile">
			<view @tap="onLogout" class="button">退 出 登 录</view>
		</view>
	</view>
</template>

<style lang="scss">
	page {
		background-color: #f4f4f4;
	}

	.viewport {
		padding: 20rpx;
	}

	/* 列表 */
	.list {
		padding: 0 20rpx;
		background-color: rgba(231, 231, 231, 0.8);
		border-radius: 20rpx;
		margin-bottom: 20rpx;

		.item {
			line-height: 90rpx;
			padding-left: 10rpx;
			font-size: 30rpx;
			color: #333;
			border-top: 1rpx solid #ddd;
			position: relative;
			text-align: left;
			background-image: -webkit-linear-gradient(left, blue, #66ffff 10%, #cc00ff 20%, #CC00CC 30%, #CCCCFF 40%, #00FFFF 50%, #CCCCFF 60%, #CC00CC 70%, #CC00FF 80%, #66FFFF 90%, blue 100%);
			-webkit-text-fill-color: transparent;
			-webkit-background-clip: text;
			-webkit-background-size: 200% 100%;
			-webkit-animation: masked-animation 4s linear infinite;


			&::after {
				width: auto;
				height: auto;
				left: auto;
				border: none;
			}

			&:first-child {
				border: none;
			}

			&::after {
				right: 5rpx;
			}
		}

		.arrow::after {
			content: '\e6c2';
			position: absolute;
			top: 50%;
			color: #ccc;
			font-family: 'erabbit' !important;
			font-size: 32rpx;
			transform: translateY(-50%);
		}
	}

	/* 操作按钮 */
	.action {
		text-align: center;
		line-height: 90rpx;
		margin-top: 40rpx;
		font-size: 32rpx;
		font-weight: bold;
		color: #b9c7d5;
		text-shadow: 0 0 1px currentColor, -1px -1px 1px #000, 0 -1px 1px #000, 1px -1px 1px #000, 1px 0 1px #000, 1px 1px 1px #000, 0 1px 1px #000, -1px 1px 1px #000, -1px 0 1px #000;
		-webkit-filter: url(#diff1);
		filter: url(#diff1);

		.button {
			background-color: rgba(231, 231, 231, 0.8);
			margin-bottom: 20rpx;
			border-radius: 20rpx;
		}
	}
</style>