<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log(this)
			this.phoneWidth = this.$el.clientWidth
			this.phoneHeight = this.$el.clientHeight
			// Vue.component('phoneWidth',this.$el.clientWidth)
			// console.log(phoneWidth)
			// console.log(phoneHeight)
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
</style>
