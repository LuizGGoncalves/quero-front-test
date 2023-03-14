<template>
  <footer class="footer-container">
    <div class="first-section">
      <div class="pops">
        <font-awesome-icon icon="fa-brands fa-whatsapp" size="2x" color="white"/>
        <div class="text-wrapper">
          <div class="footer-title">0800 123 2222</div>
          <div class="footer-description">Seg - Sex 8h-22h</div>
        </div>
      </div>
      <div class="pops">
        <font-awesome-icon icon="fa-regular fa-comments" size="2x" color="white"/>
        <div class="text-wrapper">
          <div class="footer-title">Chat ao vivo</div>
          <div class="footer-description">Seg - Sex 8h-22h</div>
        </div>
      </div>
      <div class="pops">
        <font-awesome-icon icon="fa-regular fa-envelope" size="2x" color="white"/>
        <div class="text-wrapper">
          <div class="footer-title">Mande um e-mail</div>
          <div class="footer-description">respondemos rapidinho</div>
        </div>
      </div>
      <div class="pops">
        <font-awesome-icon icon="fa-solid fa-circle-info" size="2x" color="white"/>
        <div class="text-wrapper">
          <div class="footer-title">Central de ajuda</div>
          <div class="footer-description">Encontre todas as respostas</div>
        </div>
      </div>
    </div>
    <div class="second-section">
      <span>Feito com muito amor</span>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<style>

.footer-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.first-section {
  margin-top: 1%;
  background-color: #007A8D;
  display: flex;
  justify-content: space-between;
  padding: 2% 5%;
  gap: 10%;
}

.pops {
  display: flex;
  align-items: center;
}

.pops-last {
  display: flex;
  align-items: center;
  width: 100%;
}

.text-wrapper {
  margin-left: 10px;
  margin-right: 5px;
}

.footer-title {
  color: white;
  font-weight: bold;
}

.footer-description {
  color: white
}

.second-section {
  background-color: #18ACC4;
  justify-content: center;
  display: flex;
  padding: 2% 5%
}
</style>