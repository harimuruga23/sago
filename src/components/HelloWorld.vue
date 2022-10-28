<template>
  <div class="pa-10 wrap">
    <v-text-field
      outlined
      v-model="muthal_idai"
      label="முதல் எடை"
      :dense="dense"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-md"
      outlined
      v-model="irandam_idai"
      label="இரண்டாம் எடை"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-lg"
      filled
      v-model="nigara_idai"
      label="நிகர எடை"
      :dense="dense"
      readonly
    ></v-text-field>
    <v-text-field
      class="mt-xl"
      outlined
      v-model="man_kazhivu_sadhaveedham"
      label="மண் கழிவு சதவீதம்"
      :dense="dense"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-md"
      filled
      v-model="man_kazhivu"
      label="மண் கழிவு"
      :dense="dense"
      readonly
    ></v-text-field>
    <v-text-field
      class="mt-lg"
      filled
      v-model="motha_idai"
      label="மொத்த எடை"
      :dense="dense"
      readonly
    ></v-text-field>
    <v-text-field
      class="mt-xl"
      outlined
      v-model="point"
      label="point"
      :dense="dense"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-md"
      outlined
      v-model="point_vilai"
      label="point விலை"
      :dense="dense"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-md"
      filled
      v-model="oru_ton_vilai"
      label="ஒரு டன்னிற்க்கான விலை"
      :dense="dense"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-lg"
      filled
      v-model="pattiyal_1"
      label="பட்டியல் 1"
      :dense="dense"
      readonly
    ></v-text-field>
    <v-text-field
      v-model="iraku_koozhi"
      class="mt-md"
      filled
      label="இறக்கு கூலி"
      :dense="dense"
      readonly
    ></v-text-field>
    <!-- @keyup="calc()" -->
    <v-text-field
      class="mt-lg"
      filled
      v-model="pattiyal_2"
      label="பட்டியல் 2"
      :dense="dense"
      readonly
    ></v-text-field>
    <v-text-field
      class="mt-xl"
      standout="bg-teal text-white"
      outlined
      v-model="vadagai_vettukoozhi"
      label="வாடகை + வெட்டுக்கூலி"
      :dense="dense"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-md"
      standout="bg-teal text-white"
      outlined
      v-model="idhara_selavu"
      label="இதர செலவுகள்"
      :dense="dense"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-md"
      standout="bg-teal text-white"
      outlined
      v-model="advance"
      label="advance"
      :dense="dense"
      @keyup="calc()"
    ></v-text-field>
    <v-text-field
      class="mt-lg"
      filled
      v-model="this.motha_patiyal_thogai"
      label="மொத்த பட்டியல் தொகை"
      :dense="dense"
      readonly
      background-color="light-green lighten-1"
    ></v-text-field>
  </div>
</template>

<script>
export default {
  data() {
    return {
      muthal_idai: "",
      irandam_idai: "",
      nigara_idai: "",
      man_kazhivu_sadhaveedham: "",
      man_kazhivu: "",
      motha_idai: "",
      point: "",
      point_vilai: "",
      oru_ton_vilai: "",
      pattiyal_1: "",
      iraku_koozhi: 358,
      pattiyal_2: "",
      vadagai_vettukoozhi: "",
      idhara_selavu: "",
      advance: "",
      motha_patiyal_thogai: "",
      dense: false,
    };
  },
  methods: {
    calc() {
      this.output_1();
      this.man_kazhivuf();
      this.output_3();
      this.output_4();
    },
    output_1() {
      this.nigara_idai = Math.ceil(this.muthal_idai - this.irandam_idai);
    },
    man_kazhivuf() {
      this.man_kazhivu = Math.ceil(
        this.nigara_idai * (this.man_kazhivu_sadhaveedham / 100)
      );
      this.motha_idai = Math.ceil(this.nigara_idai - this.man_kazhivu);
    },

    output_3() {
      this.oru_ton_vilai = Math.ceil(this.point * this.point_vilai);
      this.pattiyal_1 = Math.ceil(
        (this.motha_idai * this.oru_ton_vilai) / 1000
      );
      this.iraku_koozhi = Math.ceil((this.motha_idai * 3) / 100);
      this.pattiyal_2 = Math.ceil(this.pattiyal_1 - this.iraku_koozhi);
    },

    output_4() {
      this.motha_patiyal_thogai = Math.ceil(
        this.pattiyal_2 -
          this.vadagai_vettukoozhi -
          this.idhara_selavu -
          this.advance
      );
    },
  },
};
</script>

<style scoped>
.wrap {
  background-color: whitesmoke;
}
</style>
