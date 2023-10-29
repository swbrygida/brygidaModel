<template>
    <main>
        <div class="belka">
        <NuxtLink to="/">Kościół Rektoralny pw. Wniebowzięcia 
        Najświętszej Marii Panny Zwycięskiej w Lublinie</NuxtLink><br>
        <NuxtLink class="linkBelki" to="/">Zewnątrz </NuxtLink>
        <NuxtLink class="linkBelki" to="/wnetrze">Wewnątrz </NuxtLink>
        <NuxtLink class="linkBelki onlyBig" to="/firstperson" >Spacer</NuxtLink>
        
        
        </div>
    </main>
  </template>
  <style>
  @import url("https://fonts.googleapis.com/css2?family=Inknut+Antiqua:wght@300;800&display=swap");

  .belka {
    width: 90vw;
    height: auto;
    padding: 1em 5vw;
    border-bottom: 2px solid #f4f4f4;
    text-align: center;
    font-size: large;
    font-weight: 800;
    position: absolute;
    top: 0;
    left: 0;
    font-family: "Inknut Antiqua", serif;
    line-height: 1.8rem
  }
  a {
    color: #000;
    text-decoration: none;
  }
  a:hover {
    text-decoration: underline;
  }

  @media (orientation: portrait) {
    .onlyBig {
      display: none;
    }
    .linkBelki {
      padding: 0 1em ;
      text-decoration: underline;
    }
    .belka a {
      font-size: small;
      font-weight: 300;
    }
  }
  @media (orientation: landscape) {
    .linkBelki {
      padding: 1em 3em;
      margin: 1em;
    }
  }

 </style>