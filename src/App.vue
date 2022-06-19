<template>
  <div id="app">
    <Header
      :pickedColorHeader="this.colorHeaderVar"
      :mensaje="mensajeDisplay"
    />
    <Navigator
      @isHard="isHardNavigator = $event"
      @numero="colorCount = $event"
      :mensaje="this.mensajeDisplay"
    />
    <Container
      :ishardContainer="isHardNavigator"
       @isHard="isHardNavigator = $event"
       @color="color = $event"
       :colors="colors"
      :pickedColor="colorHeaderVar"
      @mensajeDisplay="mensajeDisplay = $event"
    />
  </div>
</template>

<script>
import Container from "./components/ContainerC.vue";
import Header from "./components/HeaderC.vue";
import Navigator from "./components/NavigatorC.vue";
export default {
  name: "App",
  components: {
    Container,
    Header,
    Navigator,
  },
  data() {
    return {
      isHardNavigator: true,
      colors: [],
      colorCount: 6,
      mensajeDisplay: "",
      colorHeaderVar: "",
      color: "",
    };
  },
  created() {
    this.init();
    this.colorHeader();
  },
updated() {
    this.isHardNavigator ? this.setColor() : this.reset();
  },
  methods: {
    init() {
      this.colors =
        this.colorCount == 6
          ? this.createNewColors(this.colorCount)
          : this.createNewColors(this.colorCount)
    },
    setColor() {
      if (this.colors.length != this.colorCount && this.isHardNavigator) {
        this.colors = this.createNewColors(this.colorCount);
      }   
    },
    colorHeader() {
      this.colorHeaderVar = this.colors[this.PickColor()].backgroundColor;
    },
    PickColor() {
      var quantity;
      if (this.isHardNavigator) {
        quantity = 6;
      } else {
        quantity = 3;
      }
      return Math.floor(Math.random() * quantity);
    },
    randomInt() {
      return Math.floor(Math.random() * 256);
    },
    createRandomStringColor() {
      var newColor =
        "rgb(" +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ")";
      return newColor;
    },
     reset() {

     if (!this.isHardNavigator) {
     this.mensajeDisplay = ""
     this.colors = this.createNewColors(6)
      this.colorHeader();
     this.isHardNavigator = true
      console.log("entro");
     }
    },
    createNewColors(numbers) {
      var arr = [];
      for (var i = 0; i < numbers; i++) {
         arr.push({
          id: i,
          backgroundColor: this.createRandomStringColor() },
        );
      }
      return arr;
    },
  },
};
</script>

<style>
body {
  background: #232323;
  margin: 0;
  font-family: "Montserrat", "Avenir";
}
h1 {
  font-weight: normal;
  line-height: 1.1;
  padding: 20px 0;
}
</style>
