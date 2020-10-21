<template>
	<view>
		<!-- 翻页时钟组件end -->
		<view class="flip-container">
			<view class="flip-items" v-for="(unit,unitIndex) of timeArr" :key="unitIndex">
				<view class="item" v-for="(item,index) of unit.max + 1" :key="index" :class="{current: unit.current == index, past: unit.current - 1 == index || index==unit.max&&unit.current==0}">
					<view class="up">
						<view class="inner">{{index}}</view>
						<view class="shadow"></view>
					</view>
					<view class="down">
						<view class="inner">{{index}}</view>
						<view class="shadow"></view>
					</view>
				</view>
			</view>
		</view>
		<!-- 翻页时钟组件end -->
		
	<view class="main_wrap">
		<!-- 轮播图组件start -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="tag_wrap" circular="true">
			<swiper-item v-for="(item,index) in taskOfswiper" :key="index">
				<view class="swiper-item">
					<view class="alarm_time" style="display: flex;flex-direction: row;align-items: center;">
						<view class="cuIcon-time" style="margin-left: 20upx;margin-right: 10upx;"></view>
						<text>{{item.alarm_time}}</text>
					</view>
					<view class="alarm_thing">
						{{item.alarm_thing}}
					</view>
				</view>
			</swiper-item>
		</swiper>
		<!-- 轮播图组件end -->
		<!-- 三种功能start -->
		<view class="fucs_wrap">
			<view class="fucs_item">
				<view class="cuIcon-group" style="font-size: 40px;margin-bottom:20rpx">
				</view>
				<view>群组日程板导入</view>
			</view>
			<view class="fucs_item">
				<view class="cuIcon-addressbook" style="font-size: 40px;margin-bottom:20rpx">
				</view>
				<view>手动添加新日程</view>
			</view>
			<view class="fucs_item" style="border-right: 0px;">
				<view class="cuIcon-forward" style="font-size: 40px;margin-bottom:20rpx">
				</view>
				<view>剪切板一键导入</view>
			</view>
		</view>
		<!-- 三种功能end -->
		<!-- list start -->
		<view class="list">
			<view class="list_one" style="margin-bottom: 30rpx;">
				<view class="cuIcon-calendar">
				</view>
				<text>全部日程列表</text>
				<view class="cuIcon-right" style="position: absolute;right: 2rpx;">
				</view>
			</view>
			<view class="list_one">
				<view class="cuIcon-group_fill">
				</view>
				<text>我的群组列表</text>
				<view class="cuIcon-right" style="position: absolute;right: 2rpx;">
				</view>
			</view>
			<view class="list_one">
				<view class="cuIcon-friendaddfill">
				</view>
				<text>创建群组</text>
				<view class="cuIcon-right" style="position: absolute;right: 2rpx;">
				</view>
			</view>
			<view class="list_one" style="margin-top: 30rpx;">
				<view class="cuIcon-messagefill">
				</view>
				<text>我的消息</text>
				<view class="cuIcon-right" style="position: absolute;right: 2rpx;">
				</view>
			</view>
			<view class="list_one">
				<view class="cuIcon-warnfill">
				</view>
				<text>帮助</text>
				<view class="cuIcon-right" style="position: absolute;right: 2rpx;">
				</view>
			</view>
			<view class="list_one">
				<view class="cuIcon-repairfill">
				</view>
				<text>设置</text>
				<view class="cuIcon-right" style="position: absolute;right: 2rpx;">
				</view>
			</view>
		</view>
		<!-- list end -->
	</view>
	</view>
</template>

<script>
	function getTimeStr() {
		let time = new Date();
		let hour = ('00' + time.getHours()).slice(-2)
		let minute = ('00' + time.getMinutes()).slice(-2)
		let second = ('00' + time.getSeconds()).slice(-2)
		let timeStr = hour + minute + second
		return timeStr
	}
	export default {
		data() {
			return {
				timeStr: getTimeStr(),
				timeRunner: '',
				taskList:[{
					alarm_time:'2020年11月11日 星期二 07:35',
					alarm_thing:'学一210 参加单身派对'
				},{
					alarm_time:'2020年10月14日 星期三 08:00',
					alarm_thing:'学一210 参加大型舞会'
				},{
					alarm_time:'2022年01月01日 星期一 07:00',
					alarm_thing:'学一210 参加猛男舞团'
				}],
				taskOfswiper:[]//只放置三个元素 表示轮播图中的task
			}
		},
		computed: {
			timeArr() {
				return [...this.timeStr].map((unit, index) => {
					let max;
					if (index & 1 == 1) { //时分秒的个位
						max = 9
					} else if (index == 0) { //时十位
						max = 2
					} else if (index == 2) { //分十位
						max = 5
					} else if (index == 4) { //秒十位
						max = 5
					}
					return {
						max,
						current: Number(unit),
					}
				})
			}
		},
		methods: {
			setTimeRunner() {
				this.timeRunner = setInterval(() => {
					this.timeStr = getTimeStr()
				}, 1000)
			}
		},
		created() {
			this.setTimeRunner()
		},
		beforeDestroy() {
			clearInterval(this.timeRunner)
		},
		onShow() {
			//以下用来获取tasklist 并更新taskOfswiper轮播图中只会轮播tasklist按时间排序后的前三个事件
			
			this.taskOfswiper.push({
					alarm_time:'2020年10月14日 星期三 08:00',
					alarm_thing:'学一210 参加大型舞会'
				})
		}
	}
</script>

<style>
	@import url("index.css");
	.main_wrap {
		width: 100vw;
		height: 90vh;
		display: flex;
		flex-direction: column;
	}
	.tag_wrap{
		height: 300rpx;
		width: 94%;
		background-color: white;
		margin-left: 3%;
		border: 1px solid #999999;
		border-radius: calc(2%);
		box-shadow: 1rpx 1rpx #808080;
	}
	.alarm_time{
		height: 80rpx;
		border-bottom: 1px solid #808080;
		font-size: 18px;
		font-weight: bold;
	}
	.alarm_thing{
		font-size: 15px;
		padding: 20px;
	}
	.fucs_wrap{
		width: 94%;
		height: 250rpx;
		margin-top: 30rpx;
		margin-left: 3%;
		border-radius: calc(2%);
		background-color: white;
		display: flex;
		flex-direction: row;
		border:2px solid #39B54A;
		color: #39B54A;
		font-size: 13px;
		font-weight: 600;
	}
	.fucs_item{
		width: 35%;
		border-right: 2px solid #CCCCCC;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.list{
		display: flex;
		flex-direction: column;
		margin-top: 80rpx;
	}
	.list_one{
		width: 100vm;
		height: 100rpx;
		background-color: white;
		display: flex;
		flex-direction: row;
		padding: 30rpx;
		font-size: 16px;
		font-weight: 600;
		align-items: center;
	}
	.list_one text{
		margin-left: 30rpx;
	}
</style>
