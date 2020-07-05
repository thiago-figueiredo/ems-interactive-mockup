<template>
  <div class="complaint-set">
    <div
      class="complaint-item"
      role="button"
      tabindex="0"
      v-for="complaint in complaintSet"
      v-on:click="setComplaint(complaint.name)"
      v-on:keydown.enter="setComplaint(complaint.name)"
      :class="{ ['priority-' + complaint.priority]: true }"
      :key="complaint.name"
      :style="{
        backgroundColor: complaint.color
          ? `${complaint.color} !important`
          : false,
      }"
    >
      <span class="complaint-item-text">{{ complaint.name }}</span>
    </div>
    <div class="first-legend-item legend-item">
      <span class="priority-1"></span><span>Priority 1</span>
    </div>
    <div class="legend-item">
      <span class="priority-2"></span><span>Priority 2</span>
    </div>
    <div class="legend-item">
      <span class="priority-3"></span><span>Priority 3</span>
    </div>
    <div
      class="complaint-header"
      role="button"
      tabindex="0"
      v-on:click="unsetComplaint()"
      v-on:keydown.enter="unsetComplaint()"
      :class="{ 'complaint-header-on': complaintSelected.name }"
    >
      <div>
        <div class="complaint-header-name">{{ complaintSelected.name }}</div>
        <div class="complaint-header-priority">
          Priority {{ complaintSelected.priority }}
        </div>
      </div>
      <div
        class="complaint-header-color"
        :class="{ ['priority-' + complaintSelected.priority]: true }"
      ></div>
    </div>
    <div
      class="complaint-tag-groups"
      :class="{ 'complaint-tag-groups-on': complaintSelected.name }"
    >
      <div
        class="complaint-tags-group"
        v-for="(value, property) in complaintSelected.tags"
        :key="value.join()"
      >
        <div class="complaint-tags-group-name">{{ property }}</div>
        <div class="complaint-tags">
          <button
            class="complaint-tag-item"
            v-for="tag in value"
            v-on:click="setTag(tag, $event)"
            :class="{
              ['priority-' + complaintSelected.priority]: isTagSelected(tag),
            }"
            :key="tag"
          >
            {{ tag }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const tags = () => ({
  onset: ["ALS On Board", "Adv Airway"],
  symptons: [
    "SECURITY",
    "Vtach",
    "Vfib",
    "PEA",
    "Asystole",
    "STEMI",
    "Trauma",
    "Critical Bleed",
    "Hypoxia",
    "OD/Tox",
  ],
  location: ["There"],
  vitals: ["PEDIATRIC", "ROSC", "T<96", "HR<40", "HR>120"],
  interventions: ["CPR", "Shock", "Pacing", "Epi", "Amio", "Atropine", "IV"],
});

export default {
  name: "complaint-set",

  data() {
    return {
      complaintSelected: {},

      complaintSet: [
        { name: "Cardiac Arrest", priority: 1, tags: tags() },
        { name: "STEMI", priority: 1, tags: tags() },
        { name: "Stroke", priority: 1, tags: tags() },
        { name: "Resp. Distress", priority: 1, tags: tags() },
        { name: "Sepsis", priority: 1, tags: tags() },
        { name: "Other Adult", priority: 1, tags: tags() },
        { name: "Other PEDI", priority: 1, tags: tags() },
        { name: "Chest Pain", priority: 2, tags: tags() },
        { name: "Psych/Tox", priority: 2, tags: tags() },
        { name: "Urgent", priority: 2, tags: tags() },
        { name: "Routine", priority: 3, tags: tags() },
        { name: "ColorComplaint", priority: 3, tags: tags(), color: "#301aff" },
        { name: "Elite Alert", priority: 1, tags: tags() },
        { name: "LEYLA!", priority: 3, tags: tags() },
        { name: "OWEN!", priority: 1, tags: tags() },
        { name: "Trauma", priority: 1, tags: tags() },
      ],

      tagsSelected: [],
    };
  },

  methods: {
    isTagSelected(tag) {
      return this.tagsSelected.includes(tag);
    },

    setComplaint(complaintName) {
      this.complaintSelected = this.complaintSet.find(
        (complaint) => complaint.name === complaintName
      );
      console.log(`You selected ${complaintName}!`);
    },

    setTag(tagName, event) {
      event.stopPropagation();
      console.log(tagName);
      const tagExistsAt = this.tagsSelected.findIndex((tag) => tag === tagName);
      if (tagExistsAt > -1) {
        this.tagsSelected.splice(tagExistsAt, 1);
        return;
      }

      this.tagsSelected.push(tagName);
    },

    unsetComplaint() {
      this.complaintSelected = {};
      this.tagsSelected = [];
    },
  },
};
</script>

<style scoped>
.complaint-item {
  border-radius: 4px;
  display: grid;
  font-size: 1.1rem;
  font-weight: bold;
  height: 4rem;
  padding: 0rem 0.5rem;
}

.complaint-item:focus {
  outline: none;
}

.complaint-item:focus > .complaint-item-text {
  outline: 1px dotted var(--nc-tx-2);
  outline-offset: 0.2rem;
}

.complaint-item-text {
  margin: auto;
  text-align: center;
}

.complaint-set {
  display: grid;
  grid-gap: 0.5rem;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: auto auto auto auto auto auto;
  height: 451px;
  overflow-y: hidden;
  position: relative;
}

.legend-item {
  align-items: center;
  display: flex;
  font-size: 0.8rem;
  text-transform: uppercase;
}

.first-legend-item {
  grid-column-start: 1;
}

.legend-item span:first-child {
  display: inline-block;
  height: 16px;
  margin-right: 0.3rem;
  width: 16px;
}

.complaint-header {
  align-items: center;
  background-color: var(--nc-bg-3);
  border-bottom: 1px solid var(--nc-bg-1);
  box-sizing: border-box;
  display: flex;
  height: 69px;
  padding: 1rem;
  position: absolute;
  top: -70px;
  transition: top 0.3s;
  width: 100%;
}

.complaint-header-on {
  top: 0px;
}

.complaint-header-name {
  font-size: 1.1rem;
  font-weight: bold;
}

.complaint-header-priority {
  font-size: 0.8rem;
  text-transform: uppercase;
}

.complaint-header-color {
  height: 50px;
  margin-left: auto;
  width: 50px;
}

.complaint-tag-groups {
  background-color: var(--nc-bg-3);
  bottom: -381px;
  box-sizing: border-box;

  height: 381px;
  overflow-y: auto;
  padding: 1rem;
  position: absolute;
  transition: bottom 0.3s;
  width: 100%;
}

.complaint-tag-groups-on {
  bottom: 0px;
}

.complaint-tags-group {
  margin-bottom: 1rem;
}

.complaint-tags-group:last-of-type {
  margin-bottom: 0;
}

.complaint-tags-group-name {
  font-size: 0.8rem;
  margin-bottom: 0.5rem;
  text-transform: uppercase;
}

.complaint-tags {
  display: flex;
  flex-wrap: wrap;
}

.complaint-tag-item {
  border: 1px solid var(--nc-tx-2);
  margin: 0px 0.5rem 0.5rem 0rem;
  padding: 0.5rem;
}
</style>
