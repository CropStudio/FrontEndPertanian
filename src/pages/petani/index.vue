<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <div class="q-pa-md">
        <q-table
                title="Petani" :data="data" :columns="columns" row-key="ktp" :loading="loading"
        >
            <template v-slot:top="props">
                <div class="col-4 q-table__title">Data Petani</div>
                <q-space/>
                <q-input rounded dense debounce="300" color="primary" v-model.trim="filter">
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
                        to="/petani/add"
                />
            </template>
            <template v-slot:body="props">
                <q-tr :props="props">
                    <q-td key="ktp" :props="props">
                        {{ props.row.ktp }}
                        <q-btn dense round flat :icon="props.expand ? 'arrow_drop_up' : 'arrow_drop_down'" @click="props.expand = !props.expand" />
                    </q-td>
                    <q-td key="nama" :props="props">{{ props.row.nama }}</q-td>
                    <q-td key="tempat_lahir" :props="props">{{ props.row.tempat_lahir }}</q-td>
                    <q-td key="tanggal_lahir" :props="props">{{ props.row.tanggal_lahir }}</q-td>
                    <q-td key="jenis_kelamin" :props="props">{{ props.row.jenis_kelamin }}</q-td>
                    <q-td key="pendidikan" :props="props">{{ props.row.pendidikan }}</q-td>
                    <q-td key="status_keluarga" :props="props">{{ props.row.status_keluarga }}</q-td>
                    <q-td key="alamat" :props="props">
                        <q-badge square color="amber">{{ props.row.alamat }}</q-badge>
                    </q-td>
                    <q-td key="no_hp" :props="props">{{ props.row.no_hp }}</q-td>
                    <q-td key="nama_kelompok_petani" :props="props">{{ props.row.nama_kelompok_petani }}</q-td>
                </q-tr>
                <q-tr v-show="props.expand" :props="props">
                    <q-td colspan="100%">
                        <div class="text-center q-gutter-sm">
                            <q-btn
                                    dense
                                    size="sm"
                                    class="bg-red text-white q-pl-sm q-pr-sm"
                                    icon="ion-trash"
                                    @click="del(props.row.NIS)"
                            >&nbsp;delete</q-btn>
                            <q-btn
                                    dense
                                    size="sm"
                                    class="bg-light-blue text-white q-pl-sm q-pr-sm"
                                    icon="ion-create"
                                    @click="edit(props.row.id)"
                            >&nbsp;edit</q-btn>
                        </div>
                    </q-td>
                </q-tr>
            </template>

        </q-table>
    </div>
</template>
<script>
export default {
  data () {
    return {
      text: '',
      selected: [],
      columns: [
        {
          name: 'ktp',
          required: true,
          label: 'Kartu Tanda Penduduk',
          align: 'left',
          field: row => row.ktp,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'nama', align: 'center', label: 'Nama Petani', field: 'nama', sortable: true },
        { name: 'tempat_lahir', label: 'Tempat Lahir', field: 'tempatlahir', sortable: true, style: 'width: 10px' },
        { name: 'tanggal_lahir', label: 'Tanggal Lahir', field: 'tanggallahir' },
        { name: 'jenis_kelamin', label: 'Jenis Kelamin', field: 'jeniskelamin' },
        { name: 'pendidikan', label: 'Pendidikan', field: 'pendidikan' },
        { name: 'status_keluarga', label: 'Status keluarga', field: 'statuskeluarga', sortable: true },
        { name: 'alamat', label: 'Alamat', field: 'alamat', sortable: true },
        { name: 'no_hp', label: 'No HP', field: 'nohp', sortable: true },
        { name: 'nama_kelompok_petani', label: 'Nama Kelompok Tani', field: 'nama_kelompok_petani', sortable: true }
      ],
      data: [],
      loading: false
    }
  },
  methods: {
    loadData () {
      this.loading = true
      this.$axios.get('petani').then(({ data }) => {
        this.loading = false
        if (data.status) {
          this.data = data.message
          console.log(data)
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
