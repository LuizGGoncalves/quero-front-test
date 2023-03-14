<template>
  <div class="header-container">
    <div class="header-contant-container">
      <div class="header-info">
      <font-awesome-icon icon="fa-solid fa-circle-info" size="2x" color="#18ACC4" />
      <div class="header-info-title"></div>
    </div>
    <div class="header-contact">
      <font-awesome-icon icon="fa-brands fa-whatsapp" size="2x" color="#0FA866" />
      <div class="contact-text-wrapper">
        <div class="header-contact-title">0800 123 2222</div>
        <div class="header-contact-description">Envie mensagem ou ligue</div>
      </div>
    </div>
    </div>
    <div class="header-logo">
      <img src="../assets/logo-querobolsa.svg" alt="Logo">
    </div>
    <div class="header-user-info">
      <div class="header-user-info-name"></div>
      <font-awesome-icon icon="fa-regular fa-circle-user" size="2x" color="#18ACC4" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'header'
}

</script>

<style lang="scss">
.header-container {
  align-items: center;
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
  margin-bottom: 15px;
  padding: 0 5%;
}

.header-contant-container{
  display: flex;
  gap:40%
}

.header-info {
  display: flex;
  align-items: center;
  width: 15%;
}

.header-contact {
  display: flex;
  align-items: center;
  width: 15%;
}

.header-logo {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 55%;
}

.header-logo img {
  width: 150px;
  height: 48px;
}

.header-user-info {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

.header-info-title {
  color: #007A8D;
  font-weight: bold;
  margin-left: 5px;
  margin-right: 10px;
  font-size: 15px;
  white-space: nowrap;
}

.header-info-title::before {
  content: 'Como funciona';
  align-self: center;
}

.header-contact-title {
  color: #007A8D;
  font-weight: bold;
  margin-left: 5px;
  font-size: 15px;
  white-space: nowrap;
}

.header-contact-description {
  font-size: 13px;
  margin-left: 5px;
  font-weight: bold;
  color: #007A8D;
  white-space: nowrap;
}

.header-user-info-name {
  color: #007A8D;
  margin-right: 5px;
  margin-left: 5px;
  font-weight: bold;
  white-space: nowrap;
}
.header-user-info-name::before {
  content:'Nome Sobrenome'
}

.contact-text-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

@media screen and (max-width: 770px) {

  .header-container {
  align-items: center;
  display: flex;
  justify-content:space-between;
  }

  .header-contact {
  display: none;
  }

  .header-info {
    flex-direction: column;
  }

  .header-info-title::before {
    content: "AJUDA";
  }

  .header-user-info {
  display: flex;
  flex-direction: column-reverse;
  justify-content: flex-end;
}

  .header-user-info-name::before {
  content:'Conta'
}
}
</style>