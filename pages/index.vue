<template>
  <h2 class="text-center">Riwayat Kunjungan</h2>
  <NuxtLink to="/tambah">Isi Buku Tamu</NuxtLink>
<div>
  <table class="table">
    <thead class="table-secondary">
  <tr>
          <th>#</th>
          <th>tgl dan waktu</th>
          <th>nama</th>
          <th>anggota</th>
          <th>kelas</th>
          <th>keperluan</th>
        </tr>
</thead>
<tbody>
  <tr v-for="pengunjung in visiters" :key="pengunjung.id">
        <td>{{pengunjung.id}}</td>
        <td>{{pengunjung.anggota}} {{ pengunjung.waktu }}</td>
        <td>{{pengunjung.nama}}</td>
        <td>{{pengunjung.keperluan}}</td>
        <td>{{pengunjung.anggota.nama}}</td>
        <td>
          <span v-if="pengunjung.kelas">{{ pengunjung.kelas }}</span>
          <span v-else>-</span>
        </td>
        <td>{{ pengunjung.keperluan }}</td>
  </tr>
</tbody>
  </table>
</div>
</template>
<script setup>
const client = useSupabaseClient()
const visitors = ref([]);

async function getData() {
  const { data, error } = await client.from("pengunjung").select(`id, tanggal, waktu, nama, anggota(nama),kelas, keperluan`);
  if (data) visitors.value = data;
}

onMounted(() => getData());
</script>