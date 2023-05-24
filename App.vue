<script>
	export default {
		onLaunch: function() {
			// console.log('App Launch')
		},
		onShow: function() {
			// console.log('App Show')
		},
		onHide: function() {
			// console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import "uview-ui/index.scss";
	@import "static/css/common.css";
	
	@font-face {
		font-family: "PF";
		src: url('https://ttf.appldkj.com/PingFangMedium.ttf');
	}
	
	p,text,label,textarea,span,view{
		font-family: "PF";
	}	
</style>
