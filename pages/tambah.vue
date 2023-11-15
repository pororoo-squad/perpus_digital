<template>
  <div class="row"></div>
  <div class="col"></div>
  <div>
    <h2 class="text-center">isi Pengunjung</h2>
    <div v-if="sukses" class="alert alert-succes">berhasil tersimpan</div>
    <form @submit.prevent="simpan()">
      <div class="mb-3">
        <input v-model="form.nama" type="text" class="form-control" placeholder="isi nama">
      </div>
      <div class="mb.3">
        <select v-model="form.anggota" class="form-control">
          <option value="">Pilih Keanggotaan</option>
          <option value="SISWA">siswa</option>
          <option value="GURU">guru</option>
          <option value="STAF">staf</option>
        </select>
      </div>
      <div v-if="form.anggota == 'SISWA'" class="mb-3">
      <input v-model="form.kelas" type="text" class="form-control" placeholder="kelas">
      </div>
      <div class="mb.3">
        <textarea  v-model="form.keperluan" cols="30" rows="3" placeholder="keperluan" class="from-control"></textarea>
      </div>
      <button type="submit" class="btn btn-outline-primary">Kirim</button> 
      <nuxt-link to="/">Kembali</nuxt-link>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const anggota = ref([])
const form = reactive({
  nama:"",
  anggota:"",
  keperluan:"",
})
const sukses = ref(false)

async function simpan() {
  sukses.value=false
  const {error}=await supabase
  .from('pengunjung')
  .insert(form)
  if(data){
    sukses.value=true
  }
}

async function SimpanKunjungan(){
  sukses.value=false
  const {error} = await supabase
  .from('pengunjung')
  .insert(from);
}
onMounted(() => getAnggota())
</script>