<template>
  <div class="container-fluid">
    <div class="row bg-dark text-light">
      <div class="col-lg-1">
        <img src="~/assets/img/logo.jpeg"
        alt=""
        width="80"
        height="80"
        class="d-inline-block align-text-top left-20"/>
      </div>
      <div class="col-lg">
        <h1>BUKU PENGUNJUNG PERPUSTAKAAN</h1>
        <P>
          JL.DEPOK,SUKAMENAK,KEC.PURBARATU,KAB.TASIKMALAYA,JAWA BARAT
        </P>
      </div>
      <div class="col-lg-1">
        <img src="~/assets/img/logo.pororo.png"
        alt=""
        width="80"
        height="80"
        class="d-inline-block align-text-top right-20"/>
      </div>
    </div>
    <slot />
  </div>
</template>