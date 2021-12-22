<template>
  <div>
    <a-button type="primary" icon="plus" @click="addRow"
      >Tambah Barang</a-button
    >
    <table>
      <thead>
        <tr>
          <th>Produk</th>
          <th>Deskripsi</th>
          <th>Qty</th>
          <th>Satuan</th>
          <th>Harga</th>
          <th>Diskon</th>
          <th>Pajak</th>
          <th>Amount</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in form.items" :key="index" class="item-row">
          <td>
            <a-form-model-item>
              <a-select
                show-search
                placeholder="Select a person"
                option-filter-prop="children"
                style="width: 200px"
                :filter-option="filterOption"
              >
                <a-select-option value="jack"> Jack </a-select-option>
                <a-select-option value="lucy"> Lucy </a-select-option>
                <a-select-option value="tom"> Tom </a-select-option>
              </a-select>
            </a-form-model-item>
          </td>
          <td>
            <a-form-model-item>
              <a-input v-model="item.description" />
            </a-form-model-item>
          </td>
          <td>
            <a-form-model-item>
              <a-input-number
                v-model="item.qty"
                :formatter="
                  (value) => `${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')
                "
                :parser="(value) => value.replace(/\$\s?|(,*)/g, '')"
              />
            </a-form-model-item>
          </td>
          <td>
            <a-form-model-item>
              <a-select
                v-model="item.unit"
                show-search
                placeholder="Pilih Satuan"
                option-filter-prop="children"
                style="width: 200px"
                :filter-option="filterOption"
              >
                <a-select-option value="pcs"> Pcs </a-select-option>
              </a-select>
            </a-form-model-item>
          </td>
          <td>
            <a-form-model-item>
              <a-input-number
                v-model="item.unitPrice"
                :formatter="
                  (value) => `${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')
                "
                :parser="(value) => value.replace(/\$\s?|(,*)/g, '')"
              />
            </a-form-model-item>
          </td>
          <td>
            <a-form-model-item>
              <a-input-number
                v-model="item.discount"
                :formatter="
                  (value) => `${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')
                "
                :parser="(value) => value.replace(/\$\s?|(,*)/g, '')"
              />
            </a-form-model-item>
          </td>
          <td>
            <a-form-model-item>
              <a-select
                v-model="item.tax"
                show-search
                placeholder="Pilih Pajak"
                option-filter-prop="children"
                style="width: 100px"
                :filter-option="filterOption"
              >
                <a-select-option value="ppn">PPN</a-select-option>
              </a-select>
            </a-form-model-item>
          </td>
          <td>
            <a-form-model-item>
              <a-input-number
                v-model="item.amount"
                :formatter="
                  (value) => `${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')
                "
                :parser="(value) => value.replace(/\$\s?|(,*)/g, '')"
              />
            </a-form-model-item>
          </td>
          <td>
            <a-form-model-item v-if="form.items.length > 1">
              <a-button
                type="danger"
                shape="circle"
                icon="delete"
                @click="removeRow(index)"
              />
            </a-form-model-item>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    form: {
      type: Object,
      required: true,
    },
    addRow: {
      type: Function,
      required: true,
    },
    removeRow: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {}
  },
  methods: {
    filterOption(input, option) {
      return (
        option.componentOptions.children[0].text
          .toLowerCase()
          // eslint-disable-next-line unicorn/prefer-includes
          .indexOf(input.toLowerCase()) >= 0
      )
    },
  },
}
</script>

<style scoped>
.item-row {
  background: #fafafa;
}
</style>
