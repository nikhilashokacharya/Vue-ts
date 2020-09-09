<template>
  <div>
    <div class="box grid-design">
      <input type="text" id="enter" class="font-input" />
      <a href="#popup12">
        <button
          :style="{height: '17px',
    padding: '0px',
    paddingLeft: '1px',
    paddingRight: '2px',
    border: '1px solid white',
    borderRightColor: 'gray',
    borderBottomColor: 'gray',
    borderLeftColor: 'lightgray',
    borderTopColor: 'lightgray',
    outline: 'none',
    marginLeft: '-3px'}"
        >...</button>
      </a>
    </div>
    <div id="popup12" class="overlay">
      <div class="font-div popup">
        <div class="font-header">
          <span class="span-style">Font</span>
          <a class="close" href="#">
            <button class="ui-btn close">
              <svg viewBox="0 0 10 10">
                <polygon
                  points="10.2,0.7 9.5,0 5.1,4.4 0.7,0 0,0.7 4.4,5.1 0,9.5 0.7,10.2 5.1,5.8 9.5,10.2 10.2,9.5 5.8,5.1"
                />
              </svg>
            </button>
          </a>
        </div>
        <hr style="margin:0px" />
        <div class="font-body">
          <div class="wrapper">
            <div class="wrapper-1">
              <div>
                Font:
                <br />
                <input type="text" class="font-input-1" :value="this.font" />
                <br />
                <div class="font-first-frame">
                  <div
                    v-for="(value,i) of newFont"
                    :key="i"
                    @click="changeFont(i)"
                    :style="{'font-family':font}"
                  >{{i}}</div>
                </div>
              </div>
              <div>
                <div class="fieldset" style="height:70px;margin-top: 33px;">
                  <h1>
                    <span>Effects</span>
                  </h1>
                  <input
                    type="checkbox"
                    style="width:12px;margin-top: 0px;"
                    id="checkbox1"
                    name="StrikeOut"
                    value="StrikeOut"
                    @click="myFunction"
                  />
                  <label for="checkbox1">StrikeOut</label>
                  <br />
                  <input
                    type="checkbox"
                    id="checkbox2"
                    style="width:12px;margin-top: 0px;"
                    name="Underline"
                    value="Underline"
                    @click="myFunction"
                  />
                  <label for="checkbox2">Underline</label>
                </div>
              </div>
            </div>
            <div class="wrapper-2">
              <div class="wrapper-20">
                <div>
                  Font Style:
                  <br />
                  <input type="text" class="font-input-2" :value="fontStyle" />
                  <br />
                  <div class="font-second-frame" >
                    <div
                      v-for="(value,i) of temp"
                      :key="i"
                      :style="{'font-family':font,'font-weight':value.includes('Bold')?'bold':value.includes('Black')?'900':value.includes('Light')?'lighter':value.includes('SemiLight')?'300':value.includes('SemiBold')?'600':'','font-style':value.includes('Italic')?'italic':'','font-stretch':value.includes('Narrow')?'ultra-condensed':value.includes('SemiCondensed')?'semi-condensed':value.includes('Condensed')?'condensed':''}"
                      :ref="'fontStyleRef'.concat(value)"
                      :id="value"
                      @click="changeStyle(value)"
                    >{{value}}</div>
                  </div>
                </div>
                <div>
                  Size:
                  <br />
                  <input type="text" class="font-input-3" :value="this.size" />
                  <br />
                  <div class="font-third-frame">
                    <div v-for="size11 in size1" :key="size11">
                      <div @click="sizeValue(`${size11}`)">{{size11}}</div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="wrapper-21">
                <div class="fieldset" style="width:192px">
                  <h1>
                    <span>Sample</span>
                  </h1>
                  <div
                    :style="{'font-family':`${this.font}`,'font-size':`${this.size}`+'px','font-style':`${this.fontStyle1}`,'font-weight':`${this.fontWeight}`,'font-stretch':`${this.fontStretch}`,'text-decoration':`${this.dataDecorator}`}"
                  >AaBbYyZz</div>
                </div>
              </div>
              <div class="wrapper22">
                Script:
                <select style="width:210px;">
                  <option value="western">Western</option>
                  <option value="greek">Greek</option>
                  <option value="turkish">Turkish</option>
                  <option value="baltic">Baltic</option>
                  <option value="centralEuropean">CentralEuropean</option>
                  <option value="cyrillic">Cyrillic</option>
                  <option value="vietnamese">Vietnamese</option>
                </select>
              </div>
            </div>

            <div class="nested">
              <!-- <div></div> -->
              <div class="blank-div"></div>
              <div style="height:0px">
                <button
                  style="width:100%;border: 1px solid white;
    box-shadow: -1px -1px grey;"
                >OK</button>
              </div>
              <div>
                <button
                  style="width:100%;border: 1px solid white;
    box-shadow: -1px -1px grey;"
                >Cancel</button>
              </div>
              <div class="blank-div"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="ts">
import { newFont } from "../../models/newFont.ts";
import fontData from "../../models/fontData.json";
import { userFormData } from "../../models/UserFormData"
export default {
  data() {
    return {
      size: 8,
      font: "Arial",
      fontWeight: "bold",
      fontStyle: "Regular",
      fontStyle1:"",
      fontStretch: "condensed",
      dataDecorator: "",
      size1: [8, 10, 11, 12, 14, 16, 18, 20, 22, 24, 26, 28, 36, 48, 72],
      fontData: userFormData.ID_USERFORM1.properties.Font,
      newFont: newFont,
      temp: newFont["Arial"],
      data: ""
    };
  },
  methods: {
    sizeValue(data) {
      this.size = data;
      console.log(this.size);
    },
    fontValue(data) {
      this.font = data;
      console.log(this.font);
    },
    styleValue(data) {
      this.fontStyle = data;
      console.log(this.fontStyle);
    },
    myFunction() {
      const checkBox1 = document.getElementById("checkbox1");
      const checkBox2 = document.getElementById("checkbox2");

      if (checkBox1.checked === true && checkBox2.checked === true) {
        this.dataDecorator = "underline line-through";
      } else if (checkBox1.checked === true) {
        this.dataDecorator = "line-through";
        userFormData.ID_USERFORM1.properties.Font.FontStrikethrough = true;
      } else if (checkBox2.checked === true) {
        this.dataDecorator = "underline";
        userFormData.ID_USERFORM1.properties.Font.FontUnderline = true;
      } else {
        this.dataDecorator = "";
      }
    },
    changeFont(i) {
      this.temp = newFont[i];
      this.font = i;
    },
    changeStyle(value) {
      const refName = 'fontStyleRef'.concat(value);
      this.fontStyle = value;
      this.fontStyle1 = this.$refs[refName][0].style.fontStyle;
      this.fontWeight = this.$refs[refName][0].style.fontWeight;
      this.fontStretch = this.$refs[refName][0].style.fontStretch;
      userFormData.ID_USERFORM1.properties.Font.FontName = this.$refs[refName][0].style.fontFamily;
      userFormData.ID_USERFORM1.properties.Font.FontSize = this.size;
      userFormData.ID_USERFORM1.properties.Font.FontStyle = this.fontStyle;
    },
  },
  mounted() {
    this.font = this.fontData.FontName;
    this.fontStyle = this.fontData.FontStyle;
  },
};
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  /*   background: url(http://www.shukatsu-note.com/wp-content/uploads/2014/12/computer-564136_1280.jpg) no-repeat; */
  background-size: cover;
  height: 100vh;
}
.font-input {
  border: none;
  outline: none;
  height: 14px;
}
h1 {
  text-align: center;
  font-family: Tahoma, Arial, sans-serif;
  color: #06d85f;
  margin: 80px 0;
}

.span-style {
  position: absolute;
  left: 6px;
  top: 6px;
}

.box {
  display: grid;
  grid-template-columns: 90% 10%;
  background: rgba(255, 255, 255, 0.2);
  text-align: right;
}

.button {
  font-size: 1em;
  padding: 10px;
  color: #fff;
  border: 2px solid #06d85f;
  border-radius: 20px/50px;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.3s ease-out;
}
.button:hover {
  background: #06d85f;
}

.overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.7);
  transition: opacity 500ms;
  visibility: hidden;
  opacity: 0;
  z-index: 110;
}
.overlay:target {
  visibility: visible;
  opacity: 1;
}

.popup {
  margin: 70px auto;
  /* padding: 20px; */
  background: #fff;
  border-radius: 5px;
  width: 30%;
  position: relative;
  transition: all 5s ease-in-out;
}

.popup h2 {
  margin-top: 0;
  color: #333;
  font-family: Tahoma, Arial, sans-serif;
}
.popup .close {
  position: absolute;
  /* top: 20px; */
  right: 0px;
  transition: all 200ms;
  /* font-size: 30px; */
  font-weight: bold;
  text-decoration: none;
  color: #333;
}
.popup .close:hover {
  color: #06d85f;
}
.popup .content {
  max-height: 30%;
  overflow: auto;
}

@media screen and (max-width: 700px) {
  .box {
    width: 70%;
  }
  .popup {
    width: 70%;
  }
}

.wrapper {
  display: grid;
  grid-template-columns: 1fr 3fr 1fr;
  grid-gap: 1em;
  padding-left: 10px;
  padding-top: 20px;
}
.wrapper-1 {
  margin-left: 0px;
  grid-template-columns: 1fr;
  font-style: bold;
}
.wrapper2 {
  grid-template-columns: 1fr 1fr;
  display: grid;
  /* grid-template-columns: repeat(2, 1fr); */
}

.wrapper-3 {
  margin-right: 10px;
}
.wrapper-20 {
  display: grid;
  grid-template-columns: 1fr 2fr;
  grid-gap: 1em;
}
.wrapper-21 {
  grid-row: 2/3;
  margin-top: 33px;
}
.nested {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 12px 29px;
  margin-right: 10px;
}
.nested > button {
  height: 25px;
}
.font-div {
  height: 360px;
  width: 480px;
  border: 1px solid gray;
  background: rgb(238, 238, 238);
}
.font-header {
  background-color: rgb(255, 255, 255);
  height: 25px;
}
.font-body {
  /* background-color:rgb(173, 170, 170); */
  font-size: 12px;
}
.font-input-1 {
  height: 13px;
  width: 147px;
  border: 1px solid white;
  box-shadow: -1px -1px grey;
  margin-left: 1px;
  margin-bottom: 3px;
}
.font-input-2 {
  width: 127px;
  height: 13px;
  border: 1px solid white;
  box-shadow: -1px -1px grey;
  margin-left: 1px;
  margin-bottom: 3px;
}
.font-input-3 {
  width: 57px;
  height: 13px;
  border: 1px solid white;
  box-shadow: -1px -1px grey;
  margin-left: 1px;
  margin-bottom: 3px;
}
.font-first-frame {
  width: 150px;
  border: 1px solid white;
  box-shadow: -1px -1px grey;
  background: white;
  height: 88px;
  overflow-y: scroll;
  margin-left: 1px;
}
.font-second-frame {
  width: 130px;
  border: 1px solid white;
  box-shadow: -1px -1px grey;
  background: white;
  height: 88px;
  overflow-y: scroll;
  margin-left: 1px;
}
.font-third-frame {
  width: 60px;
  border: 1px solid white;
  box-shadow: -1px -1px grey;
  background: white;
  height: 88px;
  overflow-y: scroll;
  margin-left: 1px;
}

/* fieldSet */
.fieldset {
  border: 0.5px groove threedface;
  border-top: none;
  padding: 0.5em;
  margin: 1em 2px;
}
.fieldset > h1 {
  font: 1em normal;
  margin: -1em -0.5em 0;
  grid-column: 2/4;
}
.fieldset > h1 > span {
  float: left;
  color: black;
}
.fieldset > h1:before {
  border-top: 2px groove threedface;
  content: " ";
  float: left;
  margin: 0.5em 2px 0 -1px;
  width: 0.75em;
}
.fieldset > h1:after {
  border-top: 2px groove threedface;
  content: " ";
  display: block;
  height: 1.5em;
  left: 2px;
  margin: 0 1px 0 0;
  overflow: hidden;
  position: relative;
  top: 0.5em;
}

.ui-btn {
  /* margin: 2px; */
  margin: 0;
  width: 33px;
  height: 25px;
  border: 0;
  outline: 0;
  background: transparent;
}
.ui-btn:hover {
  background: rgba(255, 255, 255, 0.1);
}
.ui-btn.close {
  background: white;
}
.ui-btn:hover {
  background: #e81123;
  color: white;
}
.ui-btn svg path,
.ui-btn svg rect,
.ui-btn svg polygon {
  fill: white;
}
.ui-btn svg {
  width: 10px;
  height: 10px;
  stroke: gray;
}
.ui-btn svg:hover {
  width: 10px;
  height: 10px;
  stroke: white;
}
</style>