<template>
  <div>
    <a-page-header
      class="page-header"
      title="Pembelian"
      :breadcrumb="{ props: { routes } }"
      sub-title="Tambah Pesanan Pembelian"
      @back="() => null"
    />
    <div :style="{ padding: '24px', background: '#fff' }">
      <!-- <a-typography>
      <a-typography-title>Introduction</a-typography-title>
    </a-typography> -->
      <h1>Tambah Pesanan Pembelian</h1>
      <a-form-model :model="form">
        <a-form-model-item label="Kode Transaksi">
          <a-input v-model="form.code" />
        </a-form-model-item>
      </a-form-model>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PurchaseOrdersIndexPage',
  data() {
    return {
      routes: [
        {
          path: 'index',
          breadcrumbName: 'Home',
        },
        {
          path: 'first',
          breadcrumbName: 'Pesanan Pembelian',
        },
        {
          path: 'second',
          breadcrumbName: 'Tambah',
        },
      ],
      form: {
        code: '',
      },
    }
  },
  methods: {
    addRow() {
      this.rows.push({
        input: '',
      })
    },
  },
}
</script>

<style scoped>
.page-header {
  border: 1px solid rgb(235, 237, 240);
  margin-bottom: 20px;
  padding: 0px;
  border: none;
}
</style>
