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
  </div>
</template>

<script>
export default {
  name: "complaint-set",

  data() {
    return {
      complaintSet: [
        { name: "Cardiac Arrest", priority: 1 },
        { name: "STEMI", priority: 1 },
        { name: "Stroke", priority: 1 },
        { name: "Resp. Distress", priority: 1 },
        { name: "Sepsis", priority: 1 },
        { name: "Other Adult", priority: 1 },
        { name: "Other PEDI", priority: 1 },
        { name: "Chest Pain", priority: 2 },
        { name: "Psych/Tox", priority: 2 },
        { name: "Urgent", priority: 2 },
        { name: "Routine", priority: 3 },
        { name: "ColorComplaint", priority: 3, color: "#301aff" },
        { name: "Elite Alert", priority: 1 },
        { name: "LEYLA!", priority: 3 },
        { name: "OWEN!", priority: 1 },
        { name: "Trauma", priority: 1 },
      ],
    };
  },

  methods: {
    setComplaint(complaintName) {
      alert(`You selected ${complaintName}!`);
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

.complaint-item-text {
  margin: auto;
  text-align: center;
}

.complaint-set {
  display: grid;
  grid-area: main;
  grid-gap: 0.5rem;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: auto auto auto auto auto auto;
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
</style>
