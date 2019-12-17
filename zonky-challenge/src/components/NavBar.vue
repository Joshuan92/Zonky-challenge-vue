<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="#">Search flights </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown text="Language">
            <b-dropdown-item href="#">EN</b-dropdown-item>
            <b-dropdown-item href="#">CZ</b-dropdown-item>
            <b-dropdown-item href="#">DE</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<style scoped>
.centered {
  width: 40%;
  margin-left: 30%;
  margin-right: 30%;
  text-align: center !important;
}
.centered-btn {
  text-align: center;
}
</style>
