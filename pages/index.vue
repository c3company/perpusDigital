<template>
  <div>
    <!-- Cari  -->
    <!-- <Search /> -->

    <div class="row bg-primary py-3">
      <div class="col-lg-12">
        <!-- <span class="input-group-text rounded-pill" id="basic-addon1"><i class="bi bi-search"></i></span> -->
        <form @submit.prevent="getData" class="px-4">
          <input v-model="keyword" type="search" class="form-control rounded-pill" placeholder="Cari Buku">
        </form>
      </div>
    </div>


    <div class="row mt-5">
      <div v-if="loading">
        <span class="loader"></span>
        <h1 class="loading-text">Loading</h1>
      </div>
      <div v-else>
        <div v-if="books.length > 0" class="col-lg-12">
          <div class="row">
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
        </div>
        <div v-else>
          <h3 class="loading-text">Maaf Buku Yang Anda Cari Tidak Ada</h3>
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

.loader {
  width: 48px;
  height: 48px;
  border: 5px solid #FFF;
  border-bottom-color: #008cff;
  border-radius: 50%;
  box-sizing: border-box;
  display: flex;
  margin: auto;
  align-items: center;
  margin-top: 100px;
  animation: rotation 1s linear infinite;
}

.loading-text {
  text-align: center;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}
</style>

<!-- js -->
<script setup>
const supabase = useSupabaseClient()
const books = ref([])
const keyword = ref('');
const loading = ref(true)

onMounted(() => getData())

async function getData() {
  loading.value = true
  let { data, error } = await supabase
    .from('buku')
    .select(`
    id, judul, penulis, penerbit, 
    kategori(id), rak(kode), cover
  `)

    .ilike('judul', `%${keyword.value}%`)
  if (data) {
    books.value = data
    loading.value = false
  }
  if (error) throw error
}
</script>