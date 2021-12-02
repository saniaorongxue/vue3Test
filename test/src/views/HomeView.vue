<template>
  <div class="home">
		<Tab />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Tab from '@/components/Tabs.vue';

export default defineComponent({
  name: 'HomeView',
  components: {
		Tab
  },
});
</script>
