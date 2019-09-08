<template>
	<view>
		
		<!--图文条目-->
		<block v-for="(item,index) in list" v-bind:key="index">
			<index-list v-bind:item="item" v-bind:index="index"></index-list>
		</block>
		
	</view>
</template>

<script>
	// 引入子组件
	import indexList from "../../components/index/index-list.vue";
	export default {
		components:{
			indexList
		},
		data() {
			return {
				list:[
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						isguanzhu:false,
						title:"标题",
						type:"img",//img 图文 video 视频
						titlepic:"../../static/demo/banner1.jpg",
						playnum:200000,
						long:"2:47",
						infonum:{
							index:1, //0:没有顶,没有踩 1:顶  2:踩
							dingnum:10,
							cainum:10
						},
						commentnum:10,
						sharenum:10
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						isguanzhu:true,
						title:"标题",
						type:"video",//img 图文 video 视频
						titlepic:"../../static/demo/banner1.jpg",
						playnum:200000,
						long:"2:47",
						infonum:{
							index:2, //0:没有顶,没有踩 1:顶  2:踩
							dingnum:10,
							cainum:10
						},
						commentnum:10,
						sharenum:10
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						isguanzhu:true,
						title:"标题",
						type:"video",//img 图文 video 视频
						titlepic:"../../static/demo/banner1.jpg",
						playnum:200000,
						long:"2:47",
						infonum:{
							index:0, //0:没有顶,没有踩 1:顶  2:踩
							dingnum:10,
							cainum:10
						},
						commentnum:10,
						sharenum:10
					}
				]
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	
</style>
