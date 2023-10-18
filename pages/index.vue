<template>
  <div>
    <NuxtLink to="/tambah">Isi Kunjungan</NuxtLink>
    <table border="1" width="50%">
      <thead>
        <tr>
          <th>#</th>
          <th>tgl dan waktu</th>
          <th>nama</th>
          <th>anggota</th>
          <th>keperluan</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pengunjung in visitors" :key="pengunjung.id">
          <td>{{ pengunjung.id }}</td>
          <td>{{ pengunjung.tanggal }}</td>
          <td>{{ pengunjung.nama }}</td>
          <td>{{ pengunjung.anggota }}</td>
          <td>{{ pengunjung.keperluan }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const client = useSupabaseClient()
const visitors = ref([])

async function getData() {
  const { data, error } = await client
    .from('pengunjung')
    .select('*')
    if(data) visitors.value = data
}


onMounted(() => getData())
</script>