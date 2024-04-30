<template>
  <nav>
    <div class="container">
      <a href="#" class="logo">CodeQuest</a>
      <ul>
        <li><a href="#">Početna</a></li>
        <li><a href="#">Kursevi</a></li>
        <li><a href="#">Zadaci</a></li>
        <li><a href="#">Kontakt</a></li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar'
}
</script>

<style scoped>
nav {
  background-color: #f5f5f5;
  padding: 20px;
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 20px;
  font-weight: bold;
}

a {
  color: #333;
  text-decoration: none;
  margin: 0 10px;
}

a:hover {
  color: #007bff;
}
</style>