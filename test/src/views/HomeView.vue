<template>
  <div class="home">
		<Tab />
		<Context />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Tab from '@/components/Tabs.vue';
import Context from '@/components/Context.vue';

export default defineComponent({
  name: 'HomeView',
  components: {
		Tab,
		Context
  },
});
</script>
