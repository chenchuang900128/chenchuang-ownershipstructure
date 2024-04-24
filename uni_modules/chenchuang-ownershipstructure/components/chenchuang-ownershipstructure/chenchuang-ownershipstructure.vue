<template>

	<!-- 父视图竖线 -->
	<view style="width: 1px; padding-bottom: 0px; margin-left: 12px; background-color: #C7C7C7;position: absolute;">

		<!-- 父视图 -->
		<view class="fatherV" style="margin-left: -4px; z-index: 99;">

			<image class="imgIcon" style="width: 0px;" mode="aspectFit"> </image>

			<view class="fatherTextV"> {{ treeName }} </view>

		</view>


		<view v-if="true" v-for="(item, index) in treeData" :key="bindKey(100 + index)">

			<CCBCashSubTree @click="openChange" :tag="index" :subTreeData="item">
			</CCBCashSubTree>

			<!-- 父视图竖线 -->
			<view v-if="(item.invests.length > 0 && item.isOpen)"
				:style="{'height': bindSubLineHeight(item.invests) + 'px'}" class="subLineV">
			</view>

			<view v-if="item.isOpen" style="margin-top: 10px; margin-left: 10px;">

				<!--  otherIndex 修复小程序bug -->
				<view style="margin-left: 0px;" v-for="(subitem, otherIndex) in item.invests" :key="bindKey(200 + index)">

					<CCBCashBasTree :subTreeData="subitem"></CCBCashBasTree>


				</view>
			</view>



		</view>

		<!-- 遮挡底部多出线条 -->
		<view style="margin-left: -4px; margin-top: -46px; width: 8px; height: 60px; background-color: #F3F4F6;">
		</view>

	</view>









</template>

<script>
	import CCBCashSubTree from './CCBCashSubTree.vue'
	import CCBCashBasTree from './CCBCashBasTree.vue'

	export default {
		props: {

			treeName: {
				// 上拉的状态：more-loading前；loading-loading中；noMore-没有更多了
				type: String,
				default: '--'
			},

			treeData: {
				type: Array,
				default: []
			}


		},
		components: {

			CCBCashSubTree,
			CCBCashBasTree

		},
		data() {
			return {

			}
		},
		methods: {
			bindKey(tag) {

				return 'tree' + tag;
			},
			openChange(item, index) {

				console.log("点击成功 = " + JSON.stringify(item));
				console.log("点击成功 index = " + JSON.stringify(index));
				// 获取子组件传值
				item.isOpen = !item.isOpen;

				// 父组件数据更新
				this.treeData[index] = item;

				// 重新刷新组件 修复微信小程序
				this.$forceUpdate();

				console.log("treeData = ", JSON.stringify(this.treeData[index]));


				// console.log('data原始数据 = ', JSON.stringify(this.treeData));


			},

			bindSubLineHeight(item) {

				if (item.length > 1) {

					return 48 + (item.length - 1) * 104
				}
				return 48;

			},
			ZJValidString(obj) {

				let str = '';
				if (typeof(obj) == "undefined" || (obj) == null) {
					return str;
				}
				return obj + '';
			},
			bindTag(tagStr) {

				let tmpStr = this.ZJValidString(tagStr);
				if (tmpStr.length > 1) {

					let tmpArr = tmpStr.split(",");

					return (tmpArr);

				} else {

				}
				return []


			},
			bindColor(index) {

				let colorArr = ["#4473FF", "#FFA01B", "#41D380"];
				return colorArr[index % 3];
			},
			bindBgColor(index) {

				let bgColorArr = ["#F1F4FA", "#FFF5E8", "#ECFAF2"];
				return bgColorArr[index % 3];
			},
		}
	}
</script>

<style lang="scss" scoped>
	.upView {
		display: flex;
		flex-direction: row;
		height: 26px;


	}


	.cellView {
		margin-top: -4px;
		margin-left: 8px;
		height: 18px;
		line-height: 18px;
		text-align: center;
		border-radius: 2px;
		padding: 0px 4px !important;
		font-size: 10px;

		background-color: #F5F5F5;
		color: #818183;

	}

	.fatherV {

		display: flex;
		width: calc(100vw - 16px);
		height: 48px;
		margin-left: 8px;
		background: #FFFFFF;
		border-radius: 3px;
		border-left: 3px solid #FFFFFF;
		border-color: #4473FF;
	}

	.fatherTextV {

		font-size: 18px;
		font-family: PingFang-SC-Semibold, PingFang-SC;
		font-weight: 600;
		color: #000000;
		margin-left: 10px;
		align-self: center;

	}

	.imgIcon {

		width: 16px;
		height: 16px;
		justify-content: center;
		align-self: center;
		margin-left: 8px;
	}

	.subLineV {

		width: 1px;
		height: 0px;
		margin-left: 10px;
		padding-top: 10px;
		padding-bottom: -30px;
		background-color: #C7C7C7;
		position: absolute;
	}
</style>