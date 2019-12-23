<template>
  <div class="retirement_plan">
    <Stack type="vertical" align="center">
      <Title
        text="How much do you need to retire?"
        :additionalClasses="['padding--x4']"
      ></Title>
      <Logo />
    </Stack>
    <Stack
      type="vertical"
      align="center"
      :additionalCalsses="['required_input_section']"
    >
      <InputField
        align="center"
        :width="'380px'"
        :additionalClasses="['required_input', 'padding__top--x4']"
        placeholder="When do you want to retire?"
        v-model="retirmentAgeText"
      />
      <InputField
        v-for="ageInput in ageInputs"
        :key="ageInput.title"
        align="center"
        :width="'380px'"
        :additionalClasses="['required_input', 'padding__top--x4']"
        :placeholder="ageInput.title"
        v-model="ageInputsData[ageInput.decade]"
      />
    </Stack>
  </div>
</template>

<script>
import MeosDesign from "meos_design";
import Logo from "../components/Logo";

export default {
  name: "retiremen_plan",
  components: {
    Title: MeosDesign.components.Title,
    Stack: MeosDesign.components.Stack,
    InputField: MeosDesign.components.InputField,
    Logo: Logo
  },
  data() {
    return {
      retirmentAgeText: "",
      expectedDeathText: "110",
      ageInputsData: {}
    };
  },
  methods: {
    setAgeInputs(startingDecade, lastDecade) {
      const range = (start, end) => {
        return [...Array(1 + end - start).keys()].map(v => start + v);
      };
      const decades = range(startingDecade, lastDecade);
      decades.forEach(decade => {
        this.ageInputsData[decade] = this.ageInputsData[decade] || "";
      });
    }
  },
  watch: {
    // retirmentAgeText() {
    //   this.setAgeInputs();
    // },
    // expectedDeathText() {
    //   this.setAgeInputs();
    // }
  },
  mounted() {
    this.setAgeInputs(0, 30);
  },
  computed: {
    expectedDeath() {
      return Number(this.expectedDeathText);
    },
    retirmentAge() {
      return Number(this.retirmentAgeText);
    },
    ageInputs() {
      console.log(this.ageInputsData);
      if (this.retirmentAge === 0 || this.expectedDeath === 0) {
        return [];
      }
      const range = (start, end) => {
        return [...Array(1 + end - start).keys()].map(v => start + v);
      };
      const startingDecade = Math.floor(this.retirmentAge / 10);
      const lastDecade = Math.ceil(this.expectedDeath / 10);
      const decades = range(startingDecade, lastDecade);
      return decades.map(decade => {
        return {
          decade: decade,
          title: `What monthly income do you wan in your ${decade}0's`,
          value: this.ageInputsData[decade] || ""
        };
      });
    }
  },
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.placeholder {
  width: max-content;
}
.retirement_plan {
  width: 100%;
}

.required_input_section {
  width: 100%;

  .required_input {
    width: 300px;
  }
}
</style>
