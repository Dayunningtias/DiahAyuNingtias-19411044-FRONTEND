<template>
<div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="form.namaKegiatan"
        label="Nama Kegiatan"
        :rules="[ val => val && val.length > 0 || 'Mohon isi nama kegiatan']"
      />
      <q-input
        filled
        v-model="form.deskripsi"
        label="Deskripsi Kegiatan"
        :rules="[ val => val && val.length > 0 || 'Mohon isi deskripsi kegiatan']"
      />
      <q-input
        filled
        v-model="form.waktu"
        label="waktu Kegiatan"
        :rules="[ val => val && val.length > 0 || 'Mohon isi waktu kegiatan']"
      />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
      </div>
    </q-form>

  </div>
</template>
<script>
export default {
  data () {
    return {
      form: {
        namaKegiatan: null,
        deskripsi: null,
        waktu: null
      }
    }
  },
  methods: {
    onSubmit () {
      this.$axios.post('kegiatan/insert', this.form)
        .then(res => {
          if (res.data.status) {
            this.$q.notify({
              message: res.data.pesan,
              color: 'positive'
            })
            this.$router.push({ name: 'dashboard' })
          } else {
            this.$q.notify({
              message: res.data.pesan,
              color: 'negative'
            })
          }
        })
    }
  }
}
</script>
