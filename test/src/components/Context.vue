<template>
	<section>
		<p>{{ num }}</p>
		<p v-text="context.state"></p>
	</section>
</template>

<script lang="ts">
import { defineComponent, ref, reactive, onMounted } from 'vue';


export default defineComponent({
	name: 'Context',
	setup() {
		type IContext = {
			state: string
			formList: string[]
		}
		let num = ref(0); // Ref<number>
		let str = ref(''); // Ref<string>
		let context: IContext = reactive({
			state: 'common',
			formList: []
		})

		onMounted(() => {
			console.log(context.state)
			setTimeout(() => {
				context.state = 'context-test';
				num = 'num' // Type 'string' is not assignable to type 'Ref<number>'
				context.formList.push('formList first data')
				context.formList.push(new Date()) // Argument of type 'Date' is not assignable to parameter of type 'string'
				context.formList.push(1) // Argument of type 'number' is not assignable to parameter of type 'string'
			}, 1000 * 3)
		})
		return {
			num,
			context
		}
	}
})
</script>
