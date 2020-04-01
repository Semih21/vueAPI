<template>
  <div id="app">
    <div class="fixed-top">
      <b-navbar type="dark" variant="primary">
        <b-navbar-nav>
          <b-nav-item to="/">Home</b-nav-item>

          <!-- Navbar dropdowns -->
          <b-nav-item-dropdown text="Categories" right>
            <b-dropdown-item to="/categories/business">Business</b-dropdown-item>
            <b-dropdown-item to="/categories/health">Health</b-dropdown-item>
            <b-dropdown-item to="/categories/technology">Technology</b-dropdown-item>
            <b-dropdown-item to="/categories/science">Science</b-dropdown-item>
          </b-nav-item-dropdown>

          <b-nav-item to="/random">Random</b-nav-item>
        </b-navbar-nav>
      </b-navbar>
    </div>
    <router-view />

    <footer>
      <p>
        &copy; 2020 Copyright:
        <span>NewsApi</span>
      </p>
      <ul class="footer-nav">
        <li>
          <b-link href="/">Home</b-link>
        </li>
        <li>
          <b-link href="/random">Random</b-link>
        </li>
      </ul>
    </footer>
  </div>
</template>
export default{ categoryLists=["Business","Health","Technology","Science"] }
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}
.footer-nav {
  display: flex;
  justify-content: center;
  list-style-type: none;
}
.footer-nav li {
  margin: 5px;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
