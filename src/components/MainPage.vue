<template>
  <div class="container">
    <div class="block-el">
      <div class="el" :class="{isVisible: isActive}" :style="styleObject"></div>
    </div>
    <div class="block-imp">
      <ul>
        <li v-for="(floor, index) in floors" :key="index">
          <p>{{floor}}</p>
          <button @click="callElevator(floor)"></button>
        </li>

      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainPage',
  data () {
    return {
      isActive: false,
      floors: [5, 4, 3, 2, 1],
      styleObject: {
        transition: 0,
        bottom: 0
      },
      isFloor: 1
    }
  },
  methods: {
    callElevator (f) {
      if (this.isFloor === f) {
        console.log('hi')
      }
      if (this.isFloor > f) {
        this.styleObject.transition = this.isFloor - f + 's'
        this.getBottom (f)
      }
      if (this.isFloor < f) {
        this.styleObject.transition = f - this.isFloor + 's'
        this.getBottom (f)
      }
      console.log(this.styleObject.bottom)
      console.log(this.styleObject.transition)
    },
    //изменение этажа
    getBottom (f) {
      this.styleObject.bottom = (f-1) + '00px'
      this.isFloor = f
      let current = 1
      let self = this
      setTimeout(function go() {
        self.isActive = !self.isActive
        if (current < 6) {
          setTimeout(go, 500);
        }
        current++;
      }, parseInt(this.styleObject.transition) * 1000);
    },

  }
}
</script>

<style scoped>
.container{
  display: flex;
  flex-wrap: wrap;
}
.block-el{
  display: flex;
  height: 500px;
  border: 1px solid black;

  align-items: flex-end;
}
.el{
  width: 100px;
  height: 100px;
  background: green;
  position: relative;
}

.block-imp{
  display: flex;
  height: 500px;
}
ul{
  display: flex;
  flex-direction: column;
  list-style: none;
  align-items: center;
  justify-content: space-around;
  margin: 0;
}
button{
  width: 30px;
  height: 30px;
  border: 1px solid blue;
  background: white;
  border-radius: 6px;
}
button:hover{
  background: blue;
}
p{
  margin: 0;
}
.isVisible{
  opacity: 0;
  transition: 0.5s;
}
</style>
