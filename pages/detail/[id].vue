<template>
  <div>
    <div v-if="loading">
      <span class="loader"></span>
      <h5 class="loading-text">Sedang memuat</h5>
    </div>
    <div v-else>
      <div class="container">
        <div class="cover">
          <img :src="book.cover" alt="">
        </div>
        <div class="text">
          <h4>{{ book.judul }}</h4>
          <p>Penulis : {{ book.penulis }}</p>
          <p>Penerbit : {{ book.penerbit }}</p>
          <p>Kategori : {{ book.kategori.nama }}</p>
          <p>Rak : {{ book.rak.kode }}</p>
          <a href="/"><button class="btn btn-primary" type="button">Kembali</button></a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
}

.cover {
  margin: 50px 40px 0px 0px;
  height: 35%;
  border-radius: 2rem;
}

.text {
  margin: 50px 10px 110px 0px;
  height: 35%;
  border-radius: 2rem;
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

img {
  border-radius: 1rem;
}
</style>

<script setup>
const router = useRoute()
const id = router.params.id
const supabase = useSupabaseClient()
const book = ref({})
const loading = ref(true)
onMounted(() => getData())

async function getData() {
  loading.value = true
  let { data, error } = await supabase
    .from('buku')
    .select(`
    id, judul, penulis, penerbit, 
    kategori(nama), rak(kode), cover
  `)

    .eq("id", id)
  if (data) {
    book.value = data[0]
    loading.value = false
  }
  if (error) throw error
}
</script>