<template>
	<el-main>
		<el-row :gutter="15">
			<el-col :lg="12">
				<el-card shadow="never">
					<el-alert title="试试右键表格行看看. 支持多级菜单, 动态菜单等等等..." type="success" style="margin-bottom:20px;"></el-alert>
					<el-table ref="table" :data="tableData" highlight-current-row @row-contextmenu="rowContextmenu">
						<el-table-column type="expand">
							<template #default="props">
								<el-empty :description="props.row.id + ' 自定义扩展行'" :image-size="60"></el-empty>
							</template>
						</el-table-column>
						<el-table-column prop="id" label="ID" width="50"></el-table-column>
						<el-table-column prop="name" label="NAME" width="220"></el-table-column>
						<el-table-column prop="date" label="DATE"></el-table-column>
						<el-table-column prop="state" label="STATE"></el-table-column>
					</el-table>
				</el-card>
			</el-col>
			<el-col :lg="12">
				<el-card shadow="never" @contextmenu.prevent="openMenu">
					<div style="height:500px;display: flex;flex-direction: column;align-items: center;justify-content: center;color: #999;">
						试试看在上下左右四个角落右键，看看边缘位置修正效果
					</div>
				</el-card>
			</el-col>
		</el-row>
	</el-main>

	<hl-contextmenu ref="contextmenu" @command="handleCommand" @visible-change="visibleChange">
		<hl-contextmenu-item command="a" title="返回(B)" suffix="Alt+←"></hl-contextmenu-item>
		<hl-contextmenu-item command="b" title="重新加载(R)" suffix="Ctrl+R" icon="el-icon-refresh"></hl-contextmenu-item>
		<hl-contextmenu-item title="切换兼容性模式" divided>
			<hl-contextmenu-item command="c1" title="二级菜单1"></hl-contextmenu-item>
			<hl-contextmenu-item title="二级菜单2">
				<hl-contextmenu-item command="c2-1" title="三级菜单1"></hl-contextmenu-item>
				<hl-contextmenu-item command="c2-2" title="三级菜单2"></hl-contextmenu-item>
				<hl-contextmenu-item command="c2-3" title="三级菜单3"></hl-contextmenu-item>
			</hl-contextmenu-item>
			<hl-contextmenu-item command="c3" title="二级菜单3"></hl-contextmenu-item>
		</hl-contextmenu-item>
		<hl-contextmenu-item  command="d" title="属性(P)" divided :disabled="row&&row.state==0"></hl-contextmenu-item>
		<hl-contextmenu-item  command="e" title="设置state=1" v-if="row&&row.state==0"></hl-contextmenu-item>
	</hl-contextmenu>

</template>

<script>
	import scContextmenu from '@/components/hlContextmenu'
	import scContextmenuItem from '@/components/hlContextmenu/item'
	export default {
		name: 'contextmenu',
		components: {
			scContextmenu,
			scContextmenuItem
		},
		data() {
			return {
				row: null,
				tableData: [
					{
						id: '1',
						name: 'huala-fun',
						date: '2021-10-10',
						state: 1
					},
					{
						id: '2',
						name: 'Lolowan(此行右键属性禁用)',
						date: '2021-10-09',
						state: 0
					},
					{
						id: '3',
						name: 'Ali',
						date: '2021-10-08',
						state: 1
					}
				]
			}
		},
		mounted() {

		},
		methods: {
			rowContextmenu(row, column, event){
				this.row = row
				this.$refs.table.setCurrentRow(row);
				this.$refs.contextmenu.openMenu(event)
			},
			openMenu(e){
				this.row = null
				this.$refs.contextmenu.openMenu(e)
			},
			handleCommand(command){
				this.$message('click on item ' + command)
				if(command == 'e'){
					this.row.state = 1
				}
			},
			visibleChange(visible){
				if(!visible){
					this.$refs.table.setCurrentRow();
				}
			}
		}
	}
</script>

<style scoped>
</style>
