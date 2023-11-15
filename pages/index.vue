<template>
  <h2 class="text-center">Riwayat Kunjungan</h2>
  <NuxtLink to="/tambah">Isi Kunjungan</NuxtLink>
<div>
  <table class="table">
<thead class="table-primary">
  <tr>
          <th>#</th>
          <th>tgl </th>
          <th>nama</th>
          <th>anggota</th>
          <th>keperluan</th>
          <th>kelas</th>
        </tr>
</thead>
<tbody>
  <tr v-for="pengunjung in visiters" :key="pengunjung.id">
        <td>{{pengunjung.id}}</td>
        <td>{{pengunjung.nama}}</td>
        <td>{{pengunjung.anggota}}</td>
        <td>{{pengunjung.keperluan}}</td>
        <td>{{pengunjung.kelas}}</td>
  </tr>
</tbody>
  </table>
</div>
</template>
<script setup>
const client = useSupabaseClient()
const visitors = ref([])

async function getData() {
  const {data, error} = await client
    .from("pengunjung")
    .select("*")
    if (data)visitors.value = data
}
onMounted(() => getData())
</script>