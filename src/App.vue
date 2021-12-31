<template>
  <div class="app">
    <header id="nav">
      <p class="logo">🐶 My Pup<strong>Dates</strong></p>
      <img class="dog-image" src="./assets/Milo.jpeg" alt="" />
      <p class="dog-name">What's <strong>Milo</strong> up to?</p>
      <nav>
        <router-link to="/">Schedule</router-link>
        <router-link to="/my-dog">My Dog</router-link>
        <router-link to="/logout">Logout</router-link>
      </nav>
    </header>
    <div class="page-container">
      <router-view />
    </div>
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  position: relative;
  display: flex;
  justify-content: space-between;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  max-height: 100vh;
  height: 100vh;
}

.page-container {
  width: 100%;
  margin-left: 270px;
  margin-right: 270px;
}

header {
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  max-height: 100vh;
  height: 100vh;
  min-height: 100vh;

  .dog-image {
    display: block;
    width: 100%;
    border-radius: 50%;
    width: 150px;
    height: 150px;
    object-fit: cover;
    margin: 0 auto 1rem auto;
  }

  .dog-name {
    font-size: 1.25em;
  }
}

#nav {
  max-width: 350px;
  background-color: rgb(226, 223, 223);
  padding: 30px;

  nav {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: space-between;
    margin: 2rem 0;
  }

  .logo {
    text-transform: uppercase;
    font-size: 2em;
    margin-bottom: 2rem;
  }

  a {
    font-weight: bold;
    color: #2c3e50;
    margin: 2rem 0;
    text-decoration: none;
    display: block;
    width: 100%;
    text-align: left;
    border-radius: 5px;
    padding: 1rem 2rem;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
