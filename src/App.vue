<template>
  <nav class="navbar">
    <div class="container">
      <router-link to="/" class="logo">
        <!-- Umjesto slike, dodajte tekst "CodeQuest" -->
        <span class="brand-text">CodeQuest</span>
      </router-link>
      
    </div>
  </nav>
  <router-view/>
  <footer class="footer">
    <div class="container">
      <p>&copy; 2024 CodeQuest. All Rights Reserved.</p><br>
      <!-- Dodajte klasu "social-icons" za grupiranje ikonica -->
      <div class="social-icons">
        <i class="fab fa-facebook-f"></i>
        <i class="fab fa-twitter"></i>
        <i class="fab fa-linkedin-in"></i>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.navbar {
  background-color: #dbdbdbb3;
  padding: 15px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.container {
  display: flex;
  align-items: center;
}

.logo {
  flex: 1;
}

/* Stilovi za tekst "CodeQuest" */
.brand-text {
  font-family: 'Courier New', sans-serif; /* Postavite željeni font */
  font-size: 24px; /* Postavite željenu veličinu fonta */
  font-weight: bold; /* Postavite željenu debljinu fonta */
  font-style: italic; /* Postavite tekst na nakrivljeni font */
  color: #0c0c0c; /* Postavite željenu boju teksta */
  margin-right: 10px; /* Dodajte marginu desno kako biste dodali razmak */
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

nav li {
  display: inline-block;
  margin-right: 20px;
}

nav a {
  color: #333;
  text-decoration: none;
  font-weight: bold;
}

nav a.router-link-exact-active {
  color: #191919;
}

.social-icons {
  display: flex;
}

.social-icons li {
  margin-left: 10px;
}

.social-icons a {
  color: #333;
}

.social-icons i {
  font-size: 20px;
}

/* Postavljanje ikonica na desni kraj */
.container ul {
  margin-left: auto;
}

.footer {
  background-color: #dbdbdbb3; 
  padding: 15px 20px;
  /* text-align: center; Uklonite ovu liniju */
  display: flex; /* Koristimo flexbox */
  justify-content: center; /* Centriramo sadržaj horizontalno */
}

.footer p {
  margin: 0; /* Remove default margin */
}

.social-icons {
  display: flex;
  justify-content: flex-end; /* Stavite ikonice u desni kraj */
}

.social-icons i {
  font-size: 20px;
  margin-left: 10px; /* Dodajte razmak između ikonica */
}

/* Font Awesome icons (replace with your icons if needed) */
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css");
</style>
