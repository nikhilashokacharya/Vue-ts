<template>
  <div  @contextmenu.prevent="$refs.ctxMenu.open">
    <button
      v-if="control"
      :key="control.name"
      @mousedown="customButtonClick"
      @mouseup.stop
      :style="{
        left: control.left,
        top: control.top,
        width: control.width,
        height:control.height,
        zIndex: control.zIndex,
        border: control.border,
        backgroundColor: control.backColor,
        borderColor: control.borderColor,
        fontFamily: control.font,
        color: control.foreColor,
        textAlign: control.textAlign,
        cursor: control.mousePointer,
        boxShadow: control.specialEffect,
        wordWrap: control.wordWrap,
        overflow: control.overflow,
        whiteSpace:control.whiteSpace,
        borderStyle: 'solid'
      }"
      :title="control.title"
      :tabindex="control.tabindex"
      :v-model="control.caption"
      :value="control.caption"
      :disabled="!control.enabled"
      @keyup.enter="trigger"
    >{{control.caption}}</button>


      <context-menu id="context-menu" ref="ctxMenu">
      <li >cut</li>
      <li class="disabled">paste</li>
      <li>copy</li>
    </context-menu>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { Getter, Mutation } from "vuex-class";
import { EventBus } from "./event-bus";
import contextMenu from "vue-context-menu";

@Component({
  components: {
    contextMenu
  }
})
export default class CustomButton extends Vue {
  @Prop() control!: any;
  @Prop() userFormKey!: any;
  @Prop() controlKey: string;
  @Getter getTreeData!: any

  
  @Getter getPrevControlIndex!: any;
  
  @Mutation updatePrevControlIndex!: Function;
  @Mutation updateControlIndex!: Function;
  @Mutation activateControl!: Function;

  customButtonClick() {
       this.updatePrevControlIndex(this.userFormKey);
    this.updateControlIndex({userFormKey:this.userFormKey,controlKey:this.controlKey});
     this.activateControl({
      controlKey: this.controlKey,
      userFormKey: this.userFormKey
    });
    // EventBus.$emit("userFormClicked",  this.getTreeData[this.userFormKey],this.control);
    EventBus.$emit("CallControl", this.getTreeData[this.userFormKey],this.control );
  }
}
</script>
<style scoped>
</style>