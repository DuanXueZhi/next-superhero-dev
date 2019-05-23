<template>
	<view class="page">
		<!-- 使用自定义组件 -->
		<helloComp :myval="myvalvalue"></helloComp>
		<p>{{myvalvalue}}</p>
		
		<!-- 轮播图 start -->
		<swiper class="carousel" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<!-- 
			* indicator-dots: 是否显示面板
			* autoplay: 是否自动切换
			* interval: 自动切换时间【5000】
			* duration: 滑动时长【500】
			*  -->7
			<swiper-item> <!-- 仅可放置在swiper组件中，宽高自动设置为100% -->
				<image src="http://www.pptok.com/wp-content/uploads/2012/08/xunguang-9.jpg" class="carousel"></image>
			</swiper-item>
			<swiper-item>
				<image src="http://www.pptok.com/wp-content/uploads/2012/08/xunguang-7.jpg" class="carousel"></image>
			</swiper-item>77
			<swiper-item>
				<image src="http://www.pptok.com/wp-content/uploads/2012/08/xunguang-6.jpg" class="carousel"></image>
			</swiper-item>
		</swiper>
		<!-- 轮播图 end -->
		
		<!-- 热门超英 start -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/logo.png" class="hot-ico"></image>
				<view class="hot-title">
					热门超英
				</view>
			</view>
		</view>
		<scroll-view scroll-x="true" class="page-block hot">
			<view class="single-poster" v-for="(superhero, index) in hotSuperheroList" :key="index">
				<view class="poster-wapper">
					<image :src="superhero.cover" class="poster"></image>
					<view class="movie-name">
						蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠
					</view>
					<!-- <view class="movie-score-wapper">
						<image src="../../static/logo.png" class="star-ico"></image>
						<image src="../../static/logo.png" class="star-ico"></image>
						<image src="../../static/logo.png" class="star-ico"></image>
						<image src="../../static/logo.png" class="star-ico"></image>
						<image src="../../static/logo.png" class="star-ico"></image>
						<view class="movie-score">
							9.1
						</view>
					</view> -->
					<trailerStar :innerScore="superhero.score" showNum="1"></trailerStar>
				</view>
			</view>
		</scroll-view>
		<!-- 热门超英 end -->

		<!-- 热门预告 start -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/logo.png" class="hot-ico"></image>
				<view class="hot-title">
					热门预告
				</view>
			</view>
		</view>
		<view class="hot-movies page-block">
			<video
					v-for="(trailer, index) in hotTrailerList"
					:src="trailer.trailer"
					:poster="trailer.poster"
					class="hot-movie-single"
					controls></video>
		</view>
		<!-- 热门预告 end -->

		<!-- 猜你喜欢 start -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/logo.png" class="hot-ico"></image>
				<view class="hot-title">
					猜你喜欢
				</view>
			</view>
		</view>

		<view class="page-block guess-u-like">
			<view class="single-like-movie" v-for="(guessMovieItem, guessMovieIndex) in guessULike" :key="guessMovieIndex">
				<image :src="guessMovieItem.image" class="like-movie"></image>
				<view class="movie-desc">
					<view class="movie-title">
						{{guessMovieItem.title}}
					</view>
					<trailerStar :innerScore="9.1" showNum="0"></trailerStar>
					<view class="movie-info">
						{{guessMovieItem.infoClass}}
					</view>
					<view class="movie-info">
						{{guessMovieItem.infoActor}}
					</view>
				</view>
				<view class="movie-oper" :data-guessMovieIndex="guessMovieIndex" @tap="praiseMe">
					<image src="../../static/logo.png" class="praise-ico"></image>
					<view class="praise-me">
						赞一下
					</view>
					<view :animation="animationData[guessMovieIndex]" class="praise-me animation-opacity">
						+1
					</view>
				</view>
			</view>
		</view>
		<!-- 猜你喜欢 end -->
	</view>
</template>

<script>
	import common from '../../common/common.js'
	
	// 导入自定义组件
	import helloComp from '../../components/helloComp'
	import trailerStar from '../../components/trailerStars.vue'
	
	export default {
		components: {
			helloComp,
			trailerStar
		},
		data() {
			return {
				title: 'Hello',
				carouselList: [],
				myvalvalue: 'hello Next~~',
				hotSuperheroList: [
					{
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 9.1
                    },
                    {
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 6.1
                    },
                    {
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 7.1
                    },
                    {
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 1.1
                    },
                    {
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 3.1
                    },
                    {
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 8.1
                    },
                    {
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 5.1
                    },
                    {
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 7.1
                    },
                    {
                        cover: '../../static/logo.png',
                        name: '蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠',
                        score: 8.1
                    },
				],
                hotTrailerList: [
					{
                        trailer: require('../../static/video/8.7.mp4'),
                        poster: require('../../static/logo.png')
					},
                    {
                        trailer: require('../../static/video/8.7.mp4'),
                        poster: require('../../static/logo.png')
                    },
                    {
                        trailer: require('../../static/video/8.7.mp4'),
                        poster: require('../../static/logo.png')
                    },
                    {
                        trailer: require('../../static/video/8.7.mp4'),
                        poster: require('../../static/logo.png')
                    }
				],
				guessULike: [ // 猜你喜欢
					{
					    image: require('../../static/logo.png'),
						title: '蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战',
						infoClass: '2018 / 美国 / 科幻 动作',
						infoActor: '本·安抚克莱 / 亨利·卡维尔 / 艾米·亚当斯 / 盖尔·加朵',
					},
                    {
                        image: require('../../static/logo.png'),
                        title: '蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战',
                        infoClass: '2018 / 美国 / 科幻 动作',
                        infoActor: '本·安抚克莱 / 亨利·卡维尔 / 艾米·亚当斯 / 盖尔·加朵',
                    },
                    {
                        image: require('../../static/logo.png'),
                        title: '蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战',
                        infoClass: '2018 / 美国 / 科幻 动作',
                        infoActor: '本·安抚克莱 / 亨利·卡维尔 / 艾米·亚当斯 / 盖尔·加朵',
                    },
                    {
                        image: require('../../static/logo.png'),
                        title: '蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战',
                        infoClass: '2018 / 美国 / 科幻 动作',
                        infoActor: '本·安抚克莱 / 亨利·卡维尔 / 艾米·亚当斯 / 盖尔·加朵',
                    },
                    {
                        image: require('../../static/logo.png'),
                        title: '蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战',
                        infoClass: '2018 / 美国 / 科幻 动作',
                        infoActor: '本·安抚克莱 / 亨利·卡维尔 / 艾米·亚当斯 / 盖尔·加朵',
                    },
                    {
                        image: require('../../static/logo.png'),
                        title: '蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战蝙蝠侠超人大战',
                        infoClass: '2018 / 美国 / 科幻 动作',
                        infoActor: '本·安抚克莱 / 亨利·卡维尔 / 艾米·亚当斯 / 盖尔·加朵',
                    }
                ],

				animationData: {},
				animationDataArr: [
					{}, {}, {}, {}, {}, {}
				]
			}
		},

		onLoad() {
			let vm = this

			// #ifdef APP-PLUS || MP-WEIXIN
			// 在页面创建的时候，创建一个临时动画对象
			this.animation = uni.createAnimation()
			// #endif

			// 获取common.js中的服务器地址
			let serverUrl = common.serverUrl
			
			// 请求轮播图
			uni.request({
				url: serverUrl + '/index/carousel/list',
				method: 'POST',
				success: (res) => {
					// console.log(res.data)
					
					// 获取真实数据之前，务必判断状态是否为200
					if (res.data.status === 200) {
						vm.carouselList = carouselList
					}
				}
			})
			
			// 查询热门预告
			uni.request({
				url: serverUrl + '/index/movie/hot?type=trailer',
				method: 'POST',
				success: (res) => {
					// console.log(res.data)
					// 获取真实数据之前，务必判断状态是否为200
					if (res.data.status === 200) {
						vm.hotTrailerList = res.data.data
					}
				}
			})

            // 查询热门超英
            uni.request({
                url: serverUrl + '/index/movie/hot?type=superhero',
                method: 'POST',
                success: (res) => {
                    // console.log(res.data)

                    // 获取真实数据之前，务必判断状态是否为200
                    if (res.data.status === 200) {
                        vm.hotSuperheroList = res.data.data
                    }
                }
            })

            // 查询猜你喜欢
            uni.request({
                url: serverUrl + '',
                method: 'POST',
                success: (res) => {
                    // console.log(res.data)

                    // 获取真实数据之前，务必判断状态是否为200
                    if (res.data.status === 200) {
                        vm.guessULike = res.data.data
                    }
                }
            })
		},
		methods: {
			// 实现点赞动画
            praiseMe (e) {
                // #ifdef APP-PLUS || MP-WEIXIN
                let gIndex = e.currentTarget.dataset.guessmoiveindex
				console.log(gIndex)
                return
                // 构建动画数据，并且通过step表示动画的完成
                this.animation
					.translateY(-60)
					.opacity(1)
					.step({duration: 400}) // 建立动画

				// 导出动画数据到view组件，实现组建的动画效果
				// this.animationData = this.animation.export()
				this.animationData = this.animation.export()
				this.animationDataArr[gIndex] = this.animationData.export()

				// 还原动画
				setTimeout(function () {
					this.animation
						.translateY(0)
						.opacity(0)
						.step({duration: 0})
				}.bind(this), 500)
                // this.animationData = this.animation.export()
                this.animationDataArr[gIndex] = this.animationData.export()
            	// #endif
            }
		},
		onUnload () {
		    // 页面卸载时候清除动画数据
		    this.animationData = {}
		}
	}
</script>

<style>
	@import url("index.css");
</style>
