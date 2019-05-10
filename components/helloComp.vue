<template name="helloComp"> <!-- 定义组件名称 -->
	<view>
		{{msg}}
		<input type="text" :value="myval"  class="txt"/>
	</view>
</template>

<script>
	export default {
		// 定义组件名称
		name: 'helloComp',
		data() {
			return {
				msg: '你好，这是自定义组件----'
			}
		},
		props: {
			// 自定义一个变量，用户接收父组件（首页或者其他页面）传入的参数值
			myval: {
				type: String // 定义这个参数的类型
			}
		}
	}
</script>

<style>
	.txt{
		color: red;
	}
</style>
