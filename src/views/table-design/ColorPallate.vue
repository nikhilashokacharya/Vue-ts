<template>
  <div>
    <div class="buttonIn grid-design">
      <input type="text" id="enter" class="color-input"  :value="selectedValue"/>
      <button
        id="clear"
        :style="{height: '17px',
    padding: '0px',
    paddingLeft: '1px',
    paddingRight: '1px',
    border: '1px solid white',
    borderRightColor: 'gray',
    borderBottomColor: 'gray',
    borderLeftColor: 'lightgray',
    borderTopColor: 'lightgray',
    outline: 'none',
    marginLeft: '-2px'}"
        @click="clicked"
      >
        _
      </button>
    </div>
    <div class="grid-design1">
      <div></div>
      <div class="outer-border">
        <div
          class="tabs"
          style="margin: 0px 0px;float:right;margin-right:0px"
          v-if="clickedPallete"
        >
          <div class="tab">
            <input class="tabinput" type="radio" id="color-1" name="tab-color-1" checked />
            <label for="color-1">Palette</label>
            <div class="content">
              <div class="grid-container" >
                <div
                  class="grid-item1"
                  v-for="(color,i) in colors" :key="i"
                  @click="selectColor(color)"
                  :style="{backgroundColor:color.value}"
                ></div>
               
              </div>
            </div>
          </div>
          <div class="tab">
            <input class="tabinput" type="radio" id="color-2" name="tab-color-1" />
            <label for="color-2">System</label>
            <div class="content">
              <div class="gridcontainer">
                <div 
                 :style="{cursor:'context-menu'}"
                 v-for="(color,i) in colorSystem" :key="i" 
                @click="selectColor(color)">
                  <span class="griditem1" :style="{backgroundColor:color.value}"></span>{{color.displayName}}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { colors } from '../../models/colors';
import { colorSystem } from '../../models/colorSystem'
export default {
  data() {
    return {
      clickedPallete: false,
      clickedValue: false,
      colors: colors,
      colorSystem: colorSystem,
      selectedValue:""
    };
  },
  methods: {
    clicked() {
      console.log('clicked')
      this.clickedPallete = !this.clickedPallete;
    },
    selectColor(data) {
      console.log("Color:", data);
      this.selectedValue = data.name;
      this.clickedPallete = !this.clickedPallete;
    },

    blur(e, data) {
      this.clickedPallete=false;
      this.$emit("blur", e, data);
    },
  },
  // mounted(){
  //   console.log('colors',this.colors)
  // }
};
</script>

<style scoped>
.grid-design {
  display: grid;
  grid-template-columns: calc(100% - 15px) 15px;
  /* grid-template-columns: 0px 15px; */
  float: right;
}
grid-design1 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  background-color: rgb(238, 238, 238);
}
.color-input {
  border: none;
  outline: none;
  height: 14px;
}
.tabs {
  position: absolute;
  min-height: 174px;
  width: 204px;
  top: 18px;
  border: 1px solid gray;
  background-color: rgb(240, 240, 240);
  clear: both;
  align-self: right;
  /* margin: 25px 0; */
  z-index: 400;
  right: 0px;
  
}
.tab {
  float: left;
}
.tab label {
  background: rgb(238, 238, 238);
  height: 12px;
  border: 1px solid rgb(238, 238, 238);
  margin-left: -1px;
  position: relative;
  left: 1px;
  padding: 3px;
}
.tab [type="radio"] {
  display: none;
}
.content {
  position: absolute;
  top: 18px;
  left: 0;
  background: rgb(238, 238, 238);
  width: 200px;
  height: 152px;
  border: 1px solid rgb(238, 238, 238);
  box-shadow: 1px 1px gray;
  margin-top: 1px;
}
[type="radio"]:checked ~ label {
  background: ccc;
  box-shadow: 1px 0px gray;
  border-bottom: 1px solid ccc;
  border: 0.5px solid white;
  z-index: 2;
}
[type="radio"]:unchecked ~ label {
  border: 0.5px solid white;
}
[type="radio"]:checked ~ label ~ .content {
  z-index: 1;
}
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto auto auto auto auto auto;
  width: 10px;
  padding: 10px;
  /* position: fixed; */
}
.grid-item1 {
  /* background-color: rgb(255, 255, 255); */
  border: 1px solid rgba(0, 0, 0, 0.8);
  width: 14px;
  height: 14px;
}

/* System */
.gridcontainer {
  height: 150px;
  border: 1px solid gray;
  overflow-y: scroll;
  font-size: 12px;
}
.griditem1 {
  /* background-color: rgb(161, 161, 161); */
  border: 1px solid rgba(0, 0, 0, 0.8);
  width: 14px;
  height: 14px;
  text-align: center;
  margin: 1px;
  display: inline-block;
  cursor:none;
}

</style>