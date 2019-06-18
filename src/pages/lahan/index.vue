<template>
    <q-page padding>
        <q-table title="Petani" :data="data" :columns="columns" row-key="ktp" :loading="loading">
            <template v-slot:top>
                <q-space/>
                <q-input outlined dense debounce="300" color="primary" v-model.trim="filter">
                    <template v-slot:append>
                        <q-icon name="search"/>
                    </template>
                </q-input>
                <q-btn
                        icon="add"
                        unelevated
                        label="Tambah"
                        size="sm"
                        class="q-ml-xs q-mr-xs q-pa-sm bg-green-5 text-white"
                        dense
                        to="/lahan/add"
                />
            </template>
        </q-table>
    </q-page>
</template>
<script>
export default {
  data () {
    return {
      filter: '',
      columns: [
        {
          name: 'ktp',
          field: 'ktp',
          label: 'No KTP',
          align: 'left',
          sortable: true
        },
        {
          name: 'alamat_lahan',
          field: 'alamatlahan',
          label: 'Alamat lahan Petani',
          align: 'center',
          sortable: true
        },
        {
          name: 'kepemilikan',
          field: 'kepemilikan',
          label: 'Kepemilikan Lahan',
          align: 'center',
          sortable: true
        },
        {
          name: 'jenis_lahan',
          field: 'jenis_lahan',
          label: 'Jenis Lahan',
          align: 'center',
          sortable: true
        },
        {
          name: 'luas_lahan',
          field: 'luas_lahan',
          label: 'Luas Lahan',
          align: 'center',
          sortable: true
        },
        {
          name: 'peruntukan',
          field: 'peruntukan',
          label: 'Peruntukan',
          align: 'center',
          sortable: true
        },
        {
          name: 'action',
          field: 'action',
          label: 'Action',
          align: 'center',
          sortable: true
        }
      ],
      data: [],
      loading: false
    }
  },
  methods: {
    loadData () {
      this.loading = true
      this.$axios.get('datapetani').then(({ data }) => {
        this.loading = false
        if (data.status) {
          this.data = data.message
        } else {
          this.$q.notify({
            message: 'Gagal load data/tidak ada data!',
            color: 'negative',
            icon: 'close'
          })
        }
      })
    }
  },
  mounted () {
    this.loadData()
  }
}
</script>
