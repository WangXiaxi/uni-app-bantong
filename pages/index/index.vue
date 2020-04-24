<template>
	<web-view :src="src">
	</web-view>
</template>

<script>
	import commonModel from '@/api/common.js'
	export default {
		data() {
			return {
				src: ''
			}
		},
		onLoad() {
			this.getUrl()
			const player = setInterval(() => {
				if (!this.src) {
					this.getUrl()
				} else {
					clearInterval(player)
				}
			}, 3000)
		},
		//点击导航栏 buttons 时触发
		onNavigationBarButtonTap(e) {
			const index = e.index
			if (index === 0) {
				const src = this.src
				this.src = ''
				this.$nextTick(() => {
					this.src = src
				})
			}
		},
		methods: {
			async getUrl() {
				const historyUrl = uni.getStorageSync('historyUrl')
				if(historyUrl) {
					this.src = historyUrl
				}
				const datas = await commonModel.getDFWebURL()
				if (datas.data.weburl !== this.src) {
					this.src = datas.data.weburl
					uni.setStorageSync('historyUrl', this.src)
				}
			}
		}
	}
</script>
<style>
</style>
