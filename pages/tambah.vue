<template>
  <div class="content bg-secondary">
    <form @submit.prevent="addData()">
      <div>
        <h1 class="text-center mb-5">DATA PENGUNJUNG</h1>
        <div class="col mb-2">
          <input v-model="name" type="text" class="form-control form-control-lg" id="name" placeholder="Nama..." required />
        </div>
      </div>
      <div>
        <div class="col mb-3">
          <div class="row">
              <div class="col-sm-10">
                  <select v-model="kategori" class="form-select" id="kategori">
                          <option disabled value="">Kategori..</option>
                          <option>Guru</option>
                          <option>Siswa</option>
                          <option>Staf</option>
                          <option>Umum</option>
                  </select>                
                </div>
              </div>
              <div v-if="kategori == 'Siswa'" class="row ">
                <div class="col mb-4 mt-3">
                  <select v-model="tingkat" id="tingkat" class="form-select">
                          <option disabled value="">Tingkat..</option>
                          <option>X</option>
                          <option>XI</option>
                          <option>XII</option>
                  </select>
                </div>
                <div class="col mb-4 mt-3">
                  <select v-model="jurusan" id="jurusan" class="form-select">
                          <option disabled value="">Jurusan..</option>
                          <option>PPLG</option>
                          <option>TJKT</option>
                          <option>TBSM</option>
                          <option>DKV</option>
                          <option>TOI</option>
                  </select>                
                </div>
                <div class="col mb-5 mt-3">
                  <select v-model="kelas" id="kelas" class="form-select">
                          <option disabled value="">Kelas..</option>
                          <option>1</option>
                          <option>2</option>
                          <option>3</option>
                          <option>4</option>
                  </select>                
                </div>
              </div>
            </div>
          </div>

      <div>
        <div class="col mb-3">
          <input v-model="keperluan" type="text" class="form-control form-control-lg" id="keperluan" placeholder="Keperluan..." required />
        </div>
      </div>
      <button type="submit" class="btn btn-outlin-secondary">Submit</button>
      <NuxtLink to="/">kembali</NuxtLink>
    </form>
  </div>

  <div>
    <div class="showData">
      <H1 class="text-center mb-5">Riwayat Pengunjung</H1>
      <div class="table-responsive">
        <table class="table table-bordered table-striped">
          <thead class="table-dark">
            <tr>
              <th class="no">No</th>
              <th class="nama">Tanggal</th>
              <th class="kategori">Nama</th>
              <th class="keperluan">Kategori</th>
              <th class="kelas">Kelas</th>
              <th class="tanggal">Keperluan</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(dataPengunjung, index) in visitors" :key="dataPengunjung.id">
              <td>{{ index + 1 }}</td>
              <td>{{ dataPengunjung.tanggal }}</td>
              <td>{{ dataPengunjung.nama }}</td>
              <td>{{ dataPengunjung.kategori }}</td>
              <td>{{ dataPengunjung.kelas }}</td>
              <td>{{ dataPengunjung.keperluan }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const visitors = ref([]);
const name = ref("");
const kategori = ref("");
const tingkat = ref('')
const jurusan = ref('')
const kelas = ref('')
const kelasLengkap = ref('')
const keperluan = ref("");
async function getData() {
  const { data, error } = await supabase
  .from("dataPengunjung")
  .select()
  .order('no', { ascending: false })
  if (error) throw error;
  if (data) {
    visitors.value = data;
  }
}
onMounted(() => getData());
async function addData(){
  kelasLengkap.value = `${tingkat.value} ${jurusan.value} ${kelas.value}`
    const { error } = await supabase
    .from('dataPengunjung')
    .insert([{
        kategori: kategori.value,
        kelas: kelasLengkap.value,
        nama: name.value,
        keperluan: keperluan.value
    }])
    if (error) throw error
    else getData()
}
</script>
<style scope>
.content {
  background-image:"";
  width: 100%;
  height: 700px;
  padding-top: 150px;
  display: flex;
  justify-content: space-evenly;
  flex-direction: row;
  flex-wrap: wrap;
  align-content: center;
}
.btn {
  background: #ffffff;
  font-style: italic;
}
</style>