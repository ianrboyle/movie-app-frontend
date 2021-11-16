<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  data: function () {
    return {
      message: "Welcome to my movie app.",
    };
  },
};
</script>
