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
