<template>
  <div  @contextmenu.prevent="$refs.ctxMenu.open">
    <label
      v-if="control"
      :key="control.name"
      :title="control.title"
      :tabindex="control.tabIndex"
      :style=" { 
        left: control.left,
        top: control.top,
        width: control.width,
        height: control.height,
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
        whiteSpace: control.whiteSpace,
      }"
      @mousedown="customLabelClick"
      @mouseup.stop
      :v-model="control.caption"
      :value="control.caption"
      :disabled="!control.enabled"
      @keyup.enter="trigger"
    >
      {{control.caption}}
      <!--  @contextmenu.prevent="$refs.menu.open($event, { foo: 'bar' })" -->
    </label>

    <context-menu id="context-menu" ref="ctxMenu">
      <li @click.self="subMenuClick">cut</li>
      <li class="disabled">paste</li>
      <li>copy</li>
    </context-menu>
  </div>
</template>



<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { Mutation, Getter } from "vuex-class";
import contextMenu from "vue-context-menu";
import { EventBus } from "./event-bus";
@Component({
  components: {
    contextMenu
  }
})
export default class CustomLabel extends Vue {
  @Prop() control!: any;
  @Prop() userFormKey!: any;
  @Prop() controlKey: string;

  @Getter getPrevControlIndex!: any;
 @Getter getCuttedControlList!: any
 @Getter getTreeData!: any

  @Mutation updatePrevControlIndex!: Function;
  @Mutation updateControlIndex!: Function;
  @Mutation activateControl!: Function;
  @Mutation cutSelectedControl!: Function;
  @Mutation cutControlList!: Function;
  @Mutation updateCuttedControlList!: Function

  subMenuClick(e: any) {
    this.updateCuttedControlList()
    console.log("event",e)
    this.cutControlList({
       controlKey: this.controlKey,
       control: this.control,
       userFormKey: this.userFormKey
    })
    this.cutSelectedControl({
       userFormKey: this.userFormKey,
        controlKey: this.controlKey,
    })
    console.log("list",this.getCuttedControlList)
  }

  customLabelClick() {
    this.updatePrevControlIndex(this.userFormKey);
    this.updateControlIndex({
      userFormKey: this.userFormKey,
      controlKey: this.controlKey
    });
    this.activateControl({
      controlKey: this.controlKey,
      userFormKey: this.userFormKey
    });
    console.log(this.getTreeData[this.userFormKey])
    //  EventBus.$emit("userFormClicked", this.getTreeData[this.userFormKey],this.control );
     EventBus.$emit("CallControl", this.getTreeData[this.userFormKey],this.control );
  }
}
</script>
<style scoped>
</style>