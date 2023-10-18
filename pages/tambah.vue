<template>
  <div>
    <h2>Isi Pengunjung</h2>
    <form>
      <input v-model="form.nama" type="text" placeholder="Nama..." required> <br>
      <select v-model="form.anggota">
        <option value="">Pilih Keanggotaan</option>
        <option v-for="a in anggota" :key="a.id" :value="a.id">{{ a.nama }}</option>
      </select> <br>
      <textarea  v-model="form.keperluan" cols="30" rows="10" placeholder="Keperluan ..."></textarea> <br>
      <button type="submit">Kirim</button> -
      <nuxt-link to="/">Kembali</nuxt-link>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const anggota = ref([])
const form = reactive({
  nama: "",
  anggota: "",
  keperluan: "",
})

async function getAnggota() {
  const { data, error } = await supabase.from('anggota').select() 
  if(data) anggota.value=data
}
async function SimpanKunjungan() {
  const { error } = await supabase.from('pengunjung').insert(from)
}

onMounted(() => getAnggota())
</script>