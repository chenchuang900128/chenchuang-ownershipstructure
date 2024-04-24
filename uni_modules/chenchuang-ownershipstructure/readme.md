# chenchuang-ownershipstructure

#### 使用方法

```使用方法
<!-- treeName：树形结构的主题名称 treeData: 树形结构的填充数据  目前支持三级树形结构-->
<chenchuang-ownershipstructure v-if="(curTreeName.length > 0)" :treeName="curTreeName" :treeData="curTreeData">
</chenchuang-ownershipstructure>
```

#### HTML代码实现部分
```html
<template>
	<view class="content">

		<!-- treeName：树形结构的主题名称 treeData: 树形结构的填充数据 -->
		<chenchuang-ownershipstructure v-if="(curTreeName.length > 0)" :treeName="curTreeName" :treeData="curTreeData">
		</chenchuang-ownershipstructure>

	</view>
</template>

<script>
	export default {

		data() {
			return {
				title: 'Hello',
				curTreeName: '',
				curTreeData: []
			}
		},
		onLoad() {


			this.curTreeName = "广州汽车集团股份有限公司";

			let tmpArr = [];
			for (let i = 0; i < 4; i++) {

				// 模拟企业控股数据
				let s = {
					'ratio': '20%',
					'amount': '1000000万',
					'label': '广州｜先进制造业｜高新技术',
					'investName': '广州汽车工业集团有限公司' + i,
					'investType': '0',
					'invests': [{
							'ratio': '20%',
							'amount': '100000万',
							'label': '广州｜汽车｜高新技术',
							'investName': '广汽丰田股份有限公司',
							'investType': '0',
						},
						{
							'ratio': '10%',
							'amount': '90000万',
							'label': '广州｜工业｜高新技术',
							'investName': '中国机械工业集团有限公司',
							'investType': '0',
						},

						{
							'ratio': '10%',
							'amount': '900万',
							'label': '股东',
							'investName': '曾庆洪',
							'investType': '1',
						},
						{
							'ratio': '10%',
							'amount': '900万',
							'label': '股东',
							'investName': '吴松',
							'investType': '1',
						}
					]

				};


				let tmpDict = Object.assign(s, {
					"isOpen": false
				});
				tmpArr.push(tmpDict);

			}

			// 模拟个人控股数据
			let t = {
				'ratio': '10%',
				'amount': '900万',
				'label': '股东',
				'investName': '曾庆洪',
				'investType': '1',
				'invests': []

			};
			let tmpDict = Object.assign(t, {
				"isOpen": false
			});
			tmpArr.push(tmpDict);

			this.curTreeData = tmpArr;
		},
		methods: {

		}
	}
</script>


<!-- /*

*/ -->
<style>
	page {
		background-color: #f6f6f6;

	}

	.content {
		display: flex;
		flex-direction: column;

	}
</style>






```