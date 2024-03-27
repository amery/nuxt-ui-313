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
interface product {}
interface products {
	products: product[];
}

const title = ref("title")
const columns = [{key: 'id'}, {key: 'title'}]

const { data, pending, refresh } = await useFetch<products>('https://dummyjson.com/products')

const links = [{
	label: 'refresh',
	click: refresh,
	loading: pending,
	icon: 'i-material-symbols-refresh',
	variant: 'ghost',
}, {
	icon: 'i-material-symbols-download',
	disabled: pending,
	click: () => { alert("save") },
}]
</script>
