<script>
// No script needed if just links, but you can manage state here if needed
</script>

<nav>
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/essay">Essay</a></li>
        <li><a href="/exam">Exam</a></li>
    </ul>
</nav>


<style>

img {
  width: 100%;
  height: auto;
  margin: 0;
  padding: 0;
  display: block;
}

nav {
  width: 100%;
  position: sticky;
  top: 0;
  z-index: 1000;  /* Ensure it's on top of other content */
}

nav ul {
  display: flex;
  position: sticky;
  top: 0;
  list-style-type: none;
  margin: 0;
  padding: 0;

  background-color: #333;
  z-index: 1000; /* Ensure it's on top of other content */
}

nav ul li {
  float: left;
}

nav ul li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

nav ul li a:hover {
  background-color: #111;
}
</style>

