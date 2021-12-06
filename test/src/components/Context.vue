<template>
	<section>
		<p @click="add">{{ num }}</p>
		<p v-text="context.state"></p>
	</section>
</template>

<script lang="ts">
import { defineComponent, ref, reactive, onMounted, onUpdated } from 'vue';

export default defineComponent({
	name: 'Context',
	setup() {
		interface IContext {
			state: string
			formList: string[]
		}
		let num = ref(0); // Ref<number>
		let str = ref(''); // Ref<string>
		let context: IContext = reactive({
			state: 'common',
			formList: []
		})

		function getTestData() {
			return new Promise((resolve, reject) => {
				setTimeout(() => {
					resolve('this is test content')
				}, 1000 * 8)
			})
		}

		function add() {
			num.value = num.value + 1;
		}

		onMounted(() => {
			console.log(context.state)
			getTestData().then(res => {
				console.log(res)
			});

			setTimeout(() => {
				context.state = 'context-test';
				// num = 'num' // Type 'string' is not assignable to type 'Ref<number>'
				context.formList.push('formList first data')
				// context.formList.push(new Date()) // Argument of type 'Date' is not assignable to parameter of type 'string'
				// context.formList.push(1) // Argument of type 'number' is not assignable to parameter of type 'string'
			}, 1000 * 3)
		})

		return {
			num,
			context,
			add
		}
	}
})
</script>
