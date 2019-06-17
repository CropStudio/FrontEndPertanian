<template>
    <q-page padding>
        <q-form
                @submit="onSubmit"
                @reset="onReset"
                class="q-gutter-md"
        >
            <q-input standout="bg-teal text-white" v-model="text" label="Custom standout" :dense="dense" />
            <q-input
                    filled
                    v-model="ktp"
                    label="KTP"
                    hint="Kartu tanda Penduduk"
                    lazy-rules
                    :rules="[ val => val && val.length > 0 || 'Please type your KTP']"
            />
            <q-input
                    filled
                    v-model="nama"
                    label="NAMA"
                    hint="NAMA"
            />
            <q-input
                    filled
                    v-model="tempatlahir"
                    label="Tempat Lahir"
                    hint="Tempat Lahir"
            />
            <q-input
                    filled
                    v-model="tanggallahir"
                    hint="Tanggal Lahir"
                    type="date"
            />
            <q-input
                    filled
                    v-model="jeniskelamin"
                    label="Jenis Kelamin"
                    hint="Jenis Kelamin"
            />
            <q-input
                    filled
                    v-model="pendidikan"
                    label="Pendidikan"
                    hint="Pendidikan"
            />
            <q-input
                    filled
                    v-model="statuskeluarga"
                    label="Status Keluarga"
                    hint="Status Keluarga"
            />
            <q-input
                    filled
                    v-model="alamat"
                    label="Alamat"
                    hint="Alamat"
            />
            <q-input
                    filled
                    v-model="nohp"
                    label="No Handphone"
                    hint="No Handphone"
            />
            <q-input
                    filled
                    v-model="namakelompoktani"
                    label="Nama Kelompok Tani"
                    hint="Nama Kelompok Tani"
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
      data: ''
    }
  }
}
</script>
