<template>
	<h3>this is tabs component</h3>
  <el-tabs type="card" @tab-click="handleClick">
    <el-tab-pane label="User">User</el-tab-pane>
    <el-tab-pane label="Config">Config</el-tab-pane>
    <el-tab-pane label="Role">Role</el-tab-pane>
    <el-tab-pane label="Task">Task</el-tab-pane>
  </el-tabs>
	<section>
		<component :is="activeComponent"></component>
	</section>
</template>
<script>
import { ref, reactive, defineAsyncComponent, markRaw } from 'vue';
export default {
	data() {
		return {
			activeIndex: 0,
			activeComponent: markRaw(defineAsyncComponent(() => import('@/components/TabContent1.vue')))
		}
	},
	watch: {
		activeIndex() {
			switch (this.activeIndex) {
				case 0:
				case 2:
					this.activeComponent = markRaw(defineAsyncComponent(() => import('@/components/TabContent1.vue')));
					break;
				case 1:
				case 3:
					this.activeComponent = markRaw(defineAsyncComponent(() => import('@/components/TabContent2.vue')));
					break;
				default:
					break;
			}
		}
	},
	methods: {
		handleClick(tab, event) {
			console.log(tab, event)
			console.log(tab.index)
			this.activeIndex = tab.index - 0
		}
	}
}
</script>
