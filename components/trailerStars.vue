<template name="trilerStars">
	<view class="movie-score-wapper">
<!--		<image src="../../static/logo.png" class="star-ico"></image>-->
<!--		<image src="../../static/logo.png" class="star-ico"></image>-->
<!--		<image src="../../static/logo.png" class="star-ico"></image>-->
<!--		<image src="../../static/logo.png" class="star-ico"></image>-->
<!--		<image src="../../static/logo.png" class="star-ico"></image>-->
<!--		<view class="movie-score">-->
<!--			9.1-->
<!--		</view>-->
		<img
				class="star-ico"
				:src="require('@/static/yellowStar.png')"
				v-for="yellow in yellowScore">
		<img
				v-for="gray in grayScore"
				src="../static/greyStar.png"
				class="star-ico">
<!--		<image-->
<!--				class="star-ico"-->
<!--				:src="require('@/static/yellowStar.png')"-->
<!--				v-for="yellow in yellowScore">-->

<!--		</image>-->
<!--		<image-->
<!--				class="star-ico"-->
<!--				src="../../static/greyStar.png"-->
<!--				v-for="yellow in yellowScore">-->
<!--		</image>-->
		<!-- <image></image>标签貌似src引导需要跳出两层 -->
		<view class="movie-score" v-if="showNum === '1'">
			{{innerScore}}
		</view>
	</view>
</template>

<script>
	export default {
		name: 'trailerStars',
		data() {
			return {
				yellowScore: 0,
				grayScore: 5
			}
		},
		props: {
			innerScore: 0, // 定义外部传入分数
			showNum: 0 // 是否需要显示具体的得分数
		},
		created () { // 相当于页面的noLoad，组建创建完成后调用
			let tempScore = 0
			if (this.innerScore !== null && this.innerScore !== undefined && this.innerScore !== '') {
				tempScore = this.innerScore
			}
			let yellowScore = parseInt(tempScore / 2) // 解析为十进制数
			let grayScore = 5 - yellowScore

			this.yellowScore = yellowScore
			this.grayScore = grayScore
			console.log(this.yellowScore)
		}
	}
</script>

<style>
	.movie-score-wapper{
		display: flex;
		flex-direction: row;
	}
	.star-ico{
		width: 20upx;
		height: 20upx;
		margin-top: 6upx;
	}
	.movie-score{
		font-size: 12px;
		color: grey;
		margin-left: 8upx;
	}
</style>
