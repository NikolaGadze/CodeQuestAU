<template>
  <div class="home">
    <div class="background-image"></div>
    <div class="content">
      <h1>Welcome to <span class="codequest-text">CodeQuest</span>!</h1>
      <p class="bold-text">Learn programming in a fun and interesting way.</p>
      <router-link to="/courses">
        <button>
          Let's go
          <i class="fas fa-rocket"></i>
        </button>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView'
}
</script>

<style scoped>
.home {
  text-align: center;
  position: relative;
  padding: 50px;
  font-size: 1.2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  font-family: "Courier New", monospace;
}

.background-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url(https://img.freepik.com/free-photo/website-html-code-browser-view-printed-white-paper-closeup-view_211682-164.jpg?w=996&t=st=1713802143~exp=1713802743~hmac=79a947dfcc5b7e7df825a47f3d1d33f9487be6757b54227881332b3e09e422f8);
  background-size: cover;
  background-position: center;
  z-index: -1;
  opacity: 0.5;
}

.content {
  z-index: 1;
  color: rgb(0, 0, 0);
  background-color: rgba(255, 255, 255, 0.8);
  padding: 20px;
}

h1, p, button {
  margin: 20px 0;
}

button {
  background-color: #0c0c0c;
  color: white;
  padding: 1rem 2rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: #1b1a1a;
}

.codequest-text {
  font-family: "Courier New", monospace;
}

.bold-text {
  font-weight: bold;
}
</style>
