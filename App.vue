<script>
	export default {
		onLaunch: function() {
			// console.log('App Launch')
			// #ifdef MP-WEIXIN
			wx.loadFontFace({
			  family: 'wxPF',
			  source: 'url("https://ttf.appldkj.com/PingFangMedium.ttf")',
			  success: console.log
			})
			// #endif
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
	
	// @import "@/static/css/stylesheet.css";
	
	@font-face {
		font-family: "PF";
		src: url(@/static/PingFangMedium.ttf);
	}
	@font-face {
		font-family: "PF";
		src: url('https://ttf.appldkj.com/PingFangMedium.ttf');
	}
	
	p,text,label,textarea,span,view{
		font-family: "PF";
	}	
</style>
