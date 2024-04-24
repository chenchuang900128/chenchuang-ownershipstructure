<template>




	<!-- 子视图 -->
	<view class="sonV" :style="{'borderColor': (subTreeData.investType ==  0) ? '#4473FF': '#41D380'}">

		<view style="width: 6px; height: 1px; margin-left: -9px; background-color: #C7C7C7;align-self: center;"></view>

		<view style="display: flex;">

			<image class="imgIcon" style="margin-left: 0px;" mode="aspectFit"> </image>

		</view>

		<view>

			<view style="line-height: 40px;margin-left: 8px;">{{subTreeData.investName}}</view>
			<view class="upView" style="margin-top: 2px;  height: 20px;">

				<!-- 自定义了一个data-id的属性,可以通过js获取到它的值!  hover-class 指定按下去的样式类-->
				<view class="cellView" v-for="(tagItem, index) in bindTag(subTreeData.label)"
					:style="{'color': bindColor(index),'backgroundColor':bindBgColor(index)}" :key="bindKey(index)">
					{{tagItem}}
				</view>


			</view>

			<view class="upView" style="height: 30px;">

				<view class="leftTextV">持股比例:</view>
				<view class="rightTextV">{{subTreeData.ratio}}</view>
				<view class="leftTextV">认缴金额:</view>
				<view class="rightTextV">{{subTreeData.amount}}</view>

			</view>

		</view>

	</view>


</template>

<script>
	export default {
		props: {

			subTreeData: {
				type: Object,
				default: function() {
					return {};
				}
			}



		},
		data() {
			return {

			}
		},
		methods: {
			bindKey(tag) {
				return 'basTree' + tag;
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

					let tmpArr = tmpStr.split("|");

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



	.imgIcon {

		width: 16px;
		height: 16px;
		justify-content: center;
		align-self: center;
		margin-left: 6px;
	}

	.sonV {

		display: flex;
		width: calc(100vw - 44px);
		height: auto;
		background: #FFFFFF;
		border-radius: 3px;
		margin-top: 12px;
		margin-left: 6px;
		border-left: 3px solid #FFFFFF;

	}

	.leftTextV {

		font-size: 12px;
		font-family: PingFangSC-Regular, PingFang SC;
		font-weight: 400;
		color: #999999;
		line-height: 24px;
		height: 36px;
		margin-left: 10px;
	}

	.rightTextV {

		font-size: 12px;
		font-family: PingFangSC-Medium, PingFang SC;
		font-weight: 500;
		color: #FF6A11;
		line-height: 24px;
		height: 36px;
		margin-left: 4px;


	}
</style>