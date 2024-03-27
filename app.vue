<template>
  <UDashboardLayout>
    <UDashboardPanel>
      <UDashboardPanelContent>
        <UDashboardCard :title="title" :links="links">
          <UTable :loading="pending" :columns="columns" :rows="data?.products" />
        </UDashboardCard>
      </UDashboardPanelContent>
    </UDashboardPanel>
  </UDashboardLayout>
</template>

<script setup lang="ts">
interface product {
  id: number;
  title: string;
}
interface products {
	products: product[];
}

const title = ref("title")
const columns = [{key: 'id'}, {key: 'title'}]
const delayMS = 1000

const { data, pending, refresh } = await useFetch<products>(`https://dummyjson.com/products?delay=${delayMS}`)

const links = [{
	label: 'refresh',
	click: () => {
    console.log('refreshing');
    refresh(); },
	loading: pending.value,
	icon: 'i-material-symbols-refresh',
	variant: 'ghost',
}, {
	icon: 'i-material-symbols-download',
	disabled: pending.value,
	click: () => { alert("save") },
}]
</script>
