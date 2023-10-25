<template>
  <div>
    <h3 class="text-center mt-5">Rekomendasi</h3>
    <div class="d-flex justify-content-center">
      <div class="container-fluid d-flex">
        <div class="card" style="width: 10rem;">
          <NuxtLink to="/detail"><img src="~/assets/img/cover1.jpg" class="card-img-top" alt="..."></NuxtLink>
          <div class="card-body">
            <p class="card-text text-center">Judul Buku</p>
          </div>
        </div>
        <div class="card" style="width: 10rem;">
          <img src="~/assets/img/cover2.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <p class="card-text text-center">Judul Buku</p>
          </div>
        </div>
        <div class="card" style="width: 10rem;">
          <img src="~/assets/img/cover3.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <p class="card-text text-center">Judul Buku</p>
          </div>
        </div>
        <div class="card" style="width: 10rem;">
          <img src="~/assets/img/cover4.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <p class="card-text text-center">Judul Buku</p>
          </div>
        </div>
        <div class="card" style="width: 10rem;">
          <img src="~/assets/img/cover5.jpg" class="card-img-top" alt="...">
          <div class="card-body">
            <p class="card-text text-center">Judul Buku</p>
          </div>
        </div>
      </div>
    </div>
    <div class="container-card"></div>
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

.container-card {
  border-bottom: 2px solid #000;
  margin: 50px 0px 50px 0px;
}
</style>