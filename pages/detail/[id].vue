<template>
  <div>
    <div v-if="loading">
      Sedang memuat
      <span class="loader"></span>
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
  display: inline-block;
  box-sizing: border-box;
  animation: rotation 1s linear infinite;
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
    kategori(id), rak(kode), cover
  `)

    .eq("id", id)
  if (data) {
    book.value = data[0]
    loading.value = false
  }
  if (error) throw error
}
</script>