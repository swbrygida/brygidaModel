<template>
  <main>
    <div class="stopka">
      <NuxtLink  target="_blank"  to="/info">
      <img src="../public/icons/mkidn-logo.png"  class="logotypMKiDN" alt="Logotyp Ministerstwa Kultury i
    Dziedzictwa Narodowego"></NuxtLink>
      <p>
        <NuxtLink  target="_blank"  to="/info"
          >Dofinansowano ze środków Funduszu Promocji Kultury</NuxtLink
        >
      </p>
    </div>
  </main>
</template>
<style>
@import url("https://fonts.googleapis.com/css2?family=Inknut+Antiqua:wght@300;800&display=swap");

.stopka {
  width: 90vw;
  height: auto;
  padding: 0 5vw;
  border-top: 2px solid #f2f2f2;
  background-color: #fff;
  text-align: center;
  font-size: normal;
  font-weight: 800;
  position: fixed;
  bottom: 0; left: 0;
  font-family: "Inknut Antiqua", serif;
  line-height: 1.8rem;
  display: flex;
  flex-wrap: wrap;
  
  align-items: center;
  justify-content: center;
}


img.logotypMKiDN {
  height: 4em!important;
  width: auto;
  margin: 0 2em;
}

</style>
