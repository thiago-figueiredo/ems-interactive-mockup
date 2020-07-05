<template>
  <div class="age-and-gender-and-hospital">
    <div class="age-and-gender">
      <input class="age" name="age" placeholder="Choose Age" type="number" />
      <div class="gender">
        <button
          class="gender-option"
          :class="{ 'gender-selected': genderSelected === 'M' }"
          @click="selectGender('M')"
        >
          <div class="gender-text">M</div>
          <span class="screen-reader-only">Male</span>
        </button>
        <button
          class="gender-option"
          :class="{ 'gender-selected': genderSelected === 'F' }"
          @click="selectGender('F')"
        >
          <div class="gender-text">F</div>
          <span class="screen-reader-only">Female</span>
        </button>
      </div>
    </div>
    <select class="hospital" name="hospital">
      <option>Choose Hospital</option>
      <option>Twiage Live Operations Center</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "age-and-gender-and-hospital",

  data() {
    return {
      genderSelected: null,
    };
  },

  methods: {
    selectGender(genderOption) {
      if (this.genderSelected === genderOption) {
        this.genderSelected = null;
        return;
      }

      this.genderSelected = genderOption;
    },
  },
};
</script>

<style scoped>
.age {
  display: block;
  font-size: 1.1rem;
  margin-right: 0.5rem;
  padding-left: 15px;
  width: 100%;
}

.age-and-gender {
  display: flex;
  grid-area: age-and-gender;
  width: 100%;
}

.age-and-gender-and-hospital {
  display: grid;
  grid-area: age-and-gender-and-hospital;
  grid-template-areas:
    "age-and-gender"
    "hospital";
}

.gender {
  border: 1px solid var(--nc-tx-2);
  border-radius: 4px;
  display: grid;
  font-size: 1.1rem;
  grid-area: gender;
  grid-template-columns: 1fr 1fr;
  height: 30px;
  width: 200px;
}

.gender-option {
  display: grid;
}

.gender-selected {
  background-color: var(--nc-tx-2);
  color: var(--nc-bg-1);
}

.gender-text {
  margin: auto;
}

.hospital {
  display: block;
  font-size: 1.1rem;
  grid-area: hospital;
  margin-bottom: 0;
  width: 100%;
}

.screen-reader-only {
  height: 1px;
  left: -10000px;
  overflow: hidden;
  position: absolute;
  top: auto;
  width: 1px;
}

select {
  color: gray;
}

select option:first-child {
  color: gray;
}

select option {
  color: var(--nc-tx-2);
}
</style>
