<!-- 话题详情页面 -->
<template>
	<view>
		<topic-info :info="info"></topic-info>
		<!-- 分割线 -->
		<view class="divider"></view>
	</view>
</template>

<script>
	import topicInfo from '@/components/topic-detail/topic-info.vue'
	export default {
		components:{
			topicInfo
		},
		data() {
			return {
				info: {
					"title": "淘宝记录簿",
					"titlepic": "../../static/demo/topicpic/13.jpeg",
					"desc": "120斤到85斤 我的反转人生",
					"totalnum": 20,
					"todaynum": 15
				}

			}
		},
		onLoad(e) {
			if (e.detail) {
				let res = JSON.parse(e.detail);
				console.log(JSON.stringify(res));
			}
		},
		methods: {

		}
	}
</script>

<style lang="scss">
	.divider{
		height: 20rpx;
		background-color: #EEEEEE;
	}
</style>
