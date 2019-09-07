<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import './common/css/uni.css';
	/*引入自己的图标库*/
	@import './common/css/iconfont.css';
	/*引入animate.css动画库*/
	@import './common/css/animate.css';
</style>
