<template>
  <nav>
    <ul class="nav-bar">
      <li><a href="#">Minha conta</a></li>
      <li><a href="#">Pré-matrículas</a></li>
      <li><a href="#">Bolsas favoritas</a></li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
}


</script>

<style>
nav {
  background-color: #18ACC4;
  color: #fff;
  display: flex;
  padding: 0 5%;
}

.nav-bar {
  list-style-type: none;
  display: flex;
  width: 100%;
  gap: 3%;
  margin: 0;
  padding: 0;
  align-items: center;
}

.nav-bar li {
  height: 100%;
  padding: 1% 0%;
}

.nav-bar li a {
  color: white;
  font-weight: bold;
  display: flex;
  align-items: center;
  text-decoration: none;
  width: 100%;
  height: 100%;
  padding-right: 10%;
}

.nav-bar li a:hover {
  background-color: #007A8D;
  color: #fff;
  width: 100%;
  height: 100%;
}

</style>