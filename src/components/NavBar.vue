<template>
  <nav class="navbar navbar-expand-lg bg-dark navbar-dark py-3">
      <div class="container">
        <!-- <a href="#" class="navbar-brand">Erwin Feld</a> -->

        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navmenu"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navmenu">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <!-- Add change ID from ancor tags -->
              <a href="#learn" class="nav-link">My Story</a>
            </li>
            <li class="nav-item">
              <a href="#questions" class="nav-link">Projects</a>
            </li>
            <li class="nav-item">
              <a href="#instructors" class="nav-link">CV</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
</template>

<script>
export default {
  name: "NavBar"

}
</script>