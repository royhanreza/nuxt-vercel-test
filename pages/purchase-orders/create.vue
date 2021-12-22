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
        <product-add-form
          :form="form"
          :add-row="addRow"
          :remove-row="removeRow"
        />
      </a-form-model>
      <a-input-group compact>
        <a-input-number
          v-model="discount"
          :formatter="
            (value) => `${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')
          "
          :parser="(value) => value.replace(/\$\s?|(,*)/g, '')"
        />
        <a-select v-model="discountType" default-value="nominal">
          <a-select-option value="nominal"> Rp </a-select-option>
          <a-select-option value="percentage"> % </a-select-option>
        </a-select>
      </a-input-group>
      <strong>SUBTOTAL: {{ subtotal }}</strong
      ><br />
      <strong>DISKON PER LINE: {{ totalItemsDiscount }}</strong
      ><br />
      <strong>DISKON: {{ finalDiscount }}</strong
      ><br />
      <strong>PPN: {{ ppn }}</strong
      ><br />
      <strong>TOTAL: {{ total }}</strong>
    </div>
  </div>
</template>

<script>
import ProductAddForm from '~/components/purchase-orders/ProductAddForm.vue'

export default {
  name: 'PurchaseOrdersIndexPage',
  components: { ProductAddForm },
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
        items: [
          {
            product: '',
            description: '',
            qty: 0,
            unit: '',
            unitPrice: 0,
            discount: 0,
            tax: '',
            amount: 0,
            discountAllocation: 0,
          },
        ],
        discount: 0,
      },
      isAmountPriority: false,
      isPpnUpper: false,
      subtotal: 0,
      totalItemsDiscount: 0,
      discount: 0,
      finalDiscount: 0,
      discountType: 'nominal',
      ppn: 0,
      total: 0,
    }
  },
  computed: {
    changedItemsDiscount() {
      return {
        items: this.form.items,
        discount: this.discount,
        discountType: this.discountType,
      }
    },
  },
  watch: {
    // 'form.items': {
    changedItemsDiscount: {
      handler(items, oldItems) {
        const self = this
        let subtotal = 0
        let totalItemsDiscount = 0
        // let totalDiscountAllocation = 0;
        let ppn = 0

        this.form.items.forEach((item) => {
          const subtotalItem = Number(item.qty) * Number(item.unitPrice)
          const discount = subtotalItem * (Number(item.discount) / 100)
          const amount = subtotalItem - discount
          item.amount = amount

          subtotal += subtotalItem
          totalItemsDiscount += discount
        })

        const percentageDiscount =
          (subtotal - totalItemsDiscount) * (self.discount / 100)
        const finalDiscount =
          self.discountType === 'percentage'
            ? percentageDiscount
            : self.discount

        this.form.items.forEach((item) => {
          const discountAllocation =
            (Number(item.amount) / Number(subtotal)) * Number(finalDiscount)
          item.discountAllocation = discountAllocation

          // totalDiscountAllocation += discountAllocation;
        })

        this.form.items.forEach((item) => {
          let itemPpn = 0
          if (item.tax === 'ppn') {
            itemPpn =
              (Number(item.amount) - Number(item.discountAllocation)) *
              (10 / 100)
          }

          ppn += itemPpn
        })

        self.subtotal = subtotal
        self.totalItemsDiscount = totalItemsDiscount
        self.ppn = ppn
        self.finalDiscount = finalDiscount
      },
      deep: true,
    },
  },
  methods: {
    addRow() {
      this.form.items.push({
        product: '',
        description: '',
        qty: 0,
        unit: '',
        unitPrice: 0,
        discount: 0,
        tax: '',
        amount: '',
      })
    },
    removeRow(index) {
      this.form.items.splice(index, 1)
    },
    getItemsAmount(item) {
      const subtotal = Number(item.qty) * Number(item.unitPrice)
      const discount = subtotal * (Number(item.discount) / 100)
      const amount = subtotal - discount
      return amount
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
