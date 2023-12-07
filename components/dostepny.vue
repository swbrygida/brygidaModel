<template>
  <main>
    <div class="dost">
      <p @click="plus"><img src="../public/icons/plus.svg" alt="zwiększ wielkość liter"/></p>
      <p @click="minus"><img src="../public/icons/minus.svg" alt="zmniejsz wielkość liter"/></p>
      <p @click="kontrast"><img src="../public/icons/kontrast.svg" alt="zwiększ kontrast czytania"/></p>
      <p @click="antykontrast"><img src="../public/icons/antykontrast.svg" alt="odwróć kontrast czytania"/></p>
      <p @click="normal"><img src="../public/icons/normal.svg" alt="normalny kontrast czytania"/></p>
      
    </div>
  </main>
</template>
<script setup>
const plus = function() {
  console.log('plus')
  const calak = document.querySelectorAll('a') 
  calak.forEach((element) => element.style.fontSize = "2em");   
  const calak2 = document.querySelectorAll('p') 
  calak2.forEach((element) => element.style.fontSize = "2em");  
  const calak3 = document.querySelectorAll('h2') 
  calak3.forEach((element) => element.style.fontSize = "2rem");  
  const calak4 = document.querySelector('.dof')
  calak4.style.fontSize = ".5em"
  const calak5 = document.querySelector('.logotypMKiDN')
  calak5.style.fontSize = ".5em"
  
}
const minus = function() {
  console.log('minus')
  const calak = document.querySelectorAll('a') 
  calak.forEach((element) => element.style.fontSize = "1em");  
  const calak2 = document.querySelectorAll('p') 
  calak2.forEach((element) => element.style.fontSize = "1em");   
  const calak3 = document.querySelectorAll('h2') 
  calak3.forEach((element) => element.style.fontSize = "1rem");  
  const calak4 = document.querySelector('.dof')
  calak4.style.fontSize = "1em"
  const calak5 = document.querySelector('.logotypMKiDN')
  calak5.style.fontSize = "1em"
}
const kontrast = function() {
  console.log('kontrast')
  const calak = document.querySelector('body')
  calak.style.color = 'yellow'
  calak.style.backgroundColor = 'black'
  const calak2 = document.querySelectorAll('a') 
  calak2.forEach((element) => element.style.color = "yellow");  
}

const antykontrast = function() {
  console.log('antykontrast')
  const calak = document.querySelector('body')
  calak.style.color = 'black'
  calak.style.backgroundColor = 'yellow'
  const calak2 = document.querySelectorAll('a') 
  calak2.forEach((element) => element.style.color = "black");  
}    

const normal = function() {
  console.log('normal')
  const calak = document.querySelector('body')
  calak.style.color = 'black'
  calak.style.backgroundColor = 'white'
  const calak2 = document.querySelectorAll('a') 
  calak2.forEach((element) => element.style.color = "black"); 
}

</script>
<style>
.dost {
  padding: 0 .5em;
  width: auto;
  height: auto;
  min-height: 14em;
  position: absolute;
  top: 6em;
  left: 0;
  background-color: #fff;
  
  text-align: center;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px,
      rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
}
.dost p {
  height: 2em;
  font-size: 1em;
  line-height: 1em;
  margin: .5em 0;
}
.dost p img {
  width: 2em;
  height: 2em;
}
</style>