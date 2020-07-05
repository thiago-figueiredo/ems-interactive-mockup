<template>
  <div class="container" style="position: relative;">
    <div class="back">Close Case</div>
    <div class="header">#000001</div>
    <div class="forward">
      <img class="messages-icon" src="../assets/messages.svg" />
    </div>
    <age-and-gender-and-hospital />
    <tabs style="grid-column: 1 / span 3;" @activeTabSet="onActiveTabSet">
      <template v-slot:complaints>
        <complaint-set />
      </template>
      <template v-slot:media>
        <media />
      </template>
      <template v-slot:chat>
        <chat />
      </template>
    </tabs>
  </div>
</template>

<script>
import AgeAndGenderAndHospital from "./age-and-gender-and-hospital";
import ComplaintSet from "./complaint-set";
import Chat from "./chat";
import Media from "./media";
import Tabs from "./tabs";

export default {
  name: "case-page",

  components: { AgeAndGenderAndHospital, Chat, ComplaintSet, Media, Tabs },

  data() {
    return {
      tabName: "complaints",
    };
  },

  methods: {
    onActiveTabSet(tabName) {
      this.tabName = tabName;
    },
  },
};
</script>

<style scoped>
.back {
  color: var(--red);
  grid-area: back;
  margin: auto auto auto 0;
}

.container {
  display: grid;
  grid-gap: 0.5rem 0;
  grid-template-areas:
    "back header forward"
    "age-and-gender-and-hospital age-and-gender-and-hospital age-and-gender-and-hospital"
    "tabs tabs tabs";
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: auto auto 451px;
}

.forward {
  grid-area: forward;
  margin: auto 0 auto auto;
}

.header {
  grid-area: header;
  margin: auto;
}

.messages-icon {
  margin-bottom: 0;
  width: 35px;
}
</style>
