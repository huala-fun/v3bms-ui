<template>
	<el-main>
		<el-alert title="封装el-select支持异步获取数据,以及根据字典名获取数据,继承el-select全部的属性和事件" type="success" style="margin-bottom:20px;"></el-alert>

		<el-row :gutter="15">
			<el-col :lg="12">
				<el-card shadow="never" header="异步单选">
					<hl-select v-model="value" :apiObj="$API.system.dic.get" clearable filterable style="width: 100%;"></hl-select>
				</el-card>
			</el-col>
			<el-col :lg="12">
				<el-card shadow="never" header="异步多选">
					<hl-select v-model="value2" :apiObj="$API.system.dic.get" clearable filterable multiple style="width: 100%;"></hl-select>
				</el-card>
			</el-col>
			<el-col :lg="12">
				<el-card shadow="never" header="字典选择器">
					<hl-select v-model="value3" dic="notice" clearable filterable style="width: 100%;"></hl-select>
				</el-card>
			</el-col>
			<el-col :lg="12">
				<el-card shadow="never" header="自定义模板">
					<hl-select v-model="value4" dic="notice" clearable filterable placeholder="自定义placeholder" style="width: 100%;">
						<template #option="{data}">
							<span style="float: left">{{ data.label }}</span>
							<span style="float: right; color: #999; font-size: 13px">{{ data.value }}</span>
						</template>
					</hl-select>
				</el-card>
			</el-col>
		</el-row>
	</el-main>
</template>

<script>
	export default {
		name: 'scselect',
		data() {
			return {
				value: '3',
				value2: ['1', '3'],
				value3: '',
				value4: ''
			}
		},
		mounted() {

		},
		methods: {

		}
	}
</script>

<style>
</style>
