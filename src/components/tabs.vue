<template>
  <div>
    <div class="tabs">
      <a
        class="tab"
        href="#complaints"
        :class="{ 'active-tab': activeTab === 'complaints' }"
        @click="setActiveTab('complaints')"
      >
        <span class="tab-text">Complaints</span>
      </a>
      <a
        class="tab"
        href="#media"
        :class="{ 'active-tab': activeTab === 'media' }"
        @click="setActiveTab('media')"
      >
        <span class="tab-text">Media</span>
      </a>
      <a
        class="tab"
        href="#chat"
        :class="{ 'active-tab': activeTab === 'chat' }"
        @click="setActiveTab('chat')"
      >
        <span class="tab-text">Chat</span>
      </a>
    </div>
    <div class="tabs-content" tabindex="0">
      <div
        class="tab-content snap-point"
        id="complaints"
        :class="{ 'active-tab-content': activeTab === 'complaints' }"
      >
        <slot name="complaints"></slot>
      </div>
      <div class="tabs-divider"></div>
      <div
        class="tab-content snap-point"
        id="media"
        :class="{ 'active-tab-content': activeTab === 'media' }"
      >
        <slot name="media"></slot>
      </div>
      <div class="tabs-divider"></div>
      <div
        class="tab-content snap-point"
        id="chat"
        :class="{ 'active-tab-content': activeTab === 'chat' }"
      >
        <slot name="chat"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "tabs",

  data() {
    return {
      activeTab: "complaints",
    };
  },

  methods: {
    setActiveTab(tabName) {
      this.activeTab = tabName;
      this.$emit("activeTabSet", tabName);
    },
  },
};
</script>

<style scoped>
.active-tab {
  background-color: var(--red);
}

.tab {
  flex: 1;
  font-size: 0.8rem;
  padding: 0.5rem;
  text-align: center;
  text-transform: uppercase;
  transition: background-color 0.2s;
}


.tab:focus {
  outline: none;
}

.tab:focus > .tab-text {
  outline: 1px dotted var(--nc-tx-2);
  outline-offset: 0.2rem;
}

.tabs {
  border: 1px solid var(--red);
  border-radius: 4px;
  display: flex;
  grid-area: tabs;
  margin-bottom: 0.5rem;
}

.tabs > a {
  color: var(--nc-tx-2);
  text-decoration: none;
}

.tab-content {
  flex-shrink: 0;
  height: 100%;
  width: 100%;
}

.tabs-content {
  display: flex;
  height: 100%;
  padding-bottom: 1rem;
  overflow-x: auto;
  scroll-behavior: smooth;
  scroll-snap-type: x mandatory;
  width: 100%;
}

.tabs-content:focus {
  outline: none;
}

.tabs-divider {
  flex-shrink: 0;
  width: 1rem;
}

.tabs-content > .snap-point {
  scroll-snap-align: start;
}
</style>
