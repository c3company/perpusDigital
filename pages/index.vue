<template>
  <div>
    <!-- Cari  -->
    <!-- <Search /> -->
    <nav class="navbar bg-primary p-3">
      <form class="container">
        <div class="input-group">
          <!-- <span class="input-group-text rounded-pill" id="basic-addon1"><i class="bi bi-search"></i></span> -->
          <form @submit.prevent="getData">
            <input v-model="keyword" type="search" class="form-control search rounded-pill" placeholder="Cari Buku"
              aria-label="Cari Buku" aria-describedby="basic-addon1">
          </form>
        </div>
      </form>
    </nav>
    <!-- untuk menampilkan componen rekomendasi -->

    <!-- <RekomendasiBuku /> -->

    <div class="row mt-5">
      <div v-for="book in books" :key="book.id" class="col-2">
        <div class="card">
          <div class="card-header">
            <NuxtLink :to="`/detail/${book.id}`">
              <img :src="book.cover" alt="cover" class="cover">
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>

    <!-- table -->
    <!-- <div class="container">
      <table class="table table-striped table-light mt-4">
        <thead>
          <tr>
            <td>COVER</td>
            <td>JUDUL</td>
            <td>PENULIS</td>
            <td>PENERBIT</td>
            <td>KATEGORI</td>
            <td>RAK</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="book in books" :key="book.id">
            <td><img :src="book.cover" alt=""></td>
            <td>{{ book.judul }}</td>
            <td>{{ book.penulis }}</td>
            <td>{{ book.penerbit }}</td>
            <td>{{ book.kategori.nama }}</td>
            <td>{{ book.rak.kode }}</td>
          </tr>
        </tbody>
      </table>
    </div> -->


  </div>
</template>

<style scoped>
.card img {
  height: 100%;
  width: 100%;
}

.card {
  margin: auto;
}

.search {
  width: 100%;
}
</style>

<!-- js -->
<script setup>
const supabase = useSupabaseClient()
const books = ref([])
const keyword = ref('');

onMounted(() => getData())

async function getData() {
  let { data, error } = await supabase
    .from('buku')
    .select(`
    id, judul, penulis, penerbit, 
    kategori(id), rak(kode), cover
  `)

    .ilike('judul', `%${keyword.value}%`)
  if (data) books.value = data
  if (error) throw error
}
</script>