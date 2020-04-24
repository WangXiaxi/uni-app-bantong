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
		},
		methods: {
			async getUrl() {
				const datas = await commonModel.getDFWebURL()
				this.src = datas.data.weburl
			}
		}
	}
</script>
<style>
</style>
