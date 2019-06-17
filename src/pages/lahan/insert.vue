<template>
    <q-page padding>
        <q-form
                @submit="onSubmit"
                @reset="onReset"
                class="q-gutter-md"
        >
            <q-input
                    filled
                    v-model="ktp"
                    label="Kartu Tanda Penduduk"
                    hint="No KTP"
                    lazy-rules
                    :rules="[ val => val && val.length > 0 || 'Please type your NPM']"
            />
            <q-input
                    filled
                    v-model="alamat_lahan"
                    label="Alamat Lahan"
                    hint="ALAMAT LAHAN"
            />
            <q-select filled v-model="kepemilikan" :options="options" label="Kepemilikan" />
            <q-input
                    filled
                    v-model="jenis_lahan"
                    label="Jenis Lahan"
                    hint="JENIS LAHAN"
            />
            <q-input
                    filled
                    v-model="luas_lahan"
                    label="Luas Lahan"
                    hint="LUAS LAHAN"
            />
            <q-input
                    filled
                    v-model="peruntukan"
                    label="Peruntukan"
                    hint="PERUNTUKAN"
            />

            <q-toggle v-model="accept" label="I accept the license and terms" />

            <div>
                <q-btn label="Submit" type="submit" color="primary"/>
                <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
            </div>
        </q-form>
    </q-page>
</template>

<script>
export default {
  data () {
    return {
      data: ' ',
      ktp: ' ',
      alamat_lahan: ' ',
      kepemilikan: ' ',
      jenis_lahan: ' ',
      luas_lahan: ' ',
      peruntukan: ' ',

      model: null,
      options: [
        'Sewa', 'Bagi Hasil', 'Gadai', 'Waris', 'Titisari', 'Pribadi'
      ]
    }
  },
  methods: {
    onSubmit () {
      if (this.accept !== true) {
        this.$q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'fas fa-exclamation-triangle',
          message: 'You need to accept the license and terms first'
        })
      } else {
        this.$q.notify({
          color: 'green-4',
          textColor: 'white',
          icon: 'fas fa-check-circle',
          message: 'Submitted'
        })
      }
    },

    onReset () {
      this.ktp = null
      this.alamat_lahan = null
      this.kepemilikan = null
      this.jenis_lahan = null
      this.luas_lahan = null
      this.peruntukan = null
      this.accept = false
    }
  }
}
</script>
