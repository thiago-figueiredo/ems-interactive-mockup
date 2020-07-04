<template>
  <div id="app">
    <case-page />
  </div>
</template>

<script>
import "./new.min.css";
import "./night.css";
import "./styles.css";

import CasePage from "./components/case-page";

export default {
  name: "App",

  components: { CasePage },
};
</script>
