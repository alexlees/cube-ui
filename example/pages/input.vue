<template>
  <cube-page
    type="input-view"
    title="Input"
    class="option-demo">
    <div slot="content">
      <cube-input
        :type="type"
        placeholder="please type here..."
        :disabled="disabled"
        :readonly="readonly"
        :clearable="useClear"
        :autocomplete="true"
        :eye="eye"
        v-model="value"
      ></cube-input>
      <div class="value">value: {{value}}</div>
      <div class="options">
        <div class="option-list">
          <div class="group">
            <switch-option class="item" name="disabled" :value="disabled"
                            @update:value="updateDisabled"></switch-option>
          </div>
          <div class="group">
            <switch-option class="item" name="readonly" :value="readonly"
                            @update:value="updateReadonly"></switch-option>
          </div>
          <div class="group">
            <switch-option class="item" name="clearable" :value="useClear"
                            @update:value="updateUseClear"></switch-option>
          </div>
          <div class="group">
            <switch-option class="item" name="password" :value="isPwd"
                            @update:value="updatePwd"></switch-option>
            <switch-option class="item" name="show eye" :value="showEye"
                            @update:value="updateShowEye" v-if="isPwd"></switch-option>
            <switch-option class="item" name="password visible" :value="pwdVisible"
                            @update:value="updatePwdVisible" v-if="isPwd && showEye"></switch-option>
          </div>
        </div>
      </div>
    </div>
  </cube-page>
</template>

<script type="text/ecmascript-6">
  import CubePage from '../components/cube-page.vue'
  import SwitchOption from '../components/switch-option'

  export default {
    data() {
      return {
        type: 'password',
        value: '',
        disabled: false,
        useClear: true,
        readonly: false,
        isPwd: true,
        showEye: true,
        pwdVisible: true
      }
    },
    computed: {
      eye() {
        if (this.isPwd && this.showEye) {
          return {
            open: this.pwdVisible
          }
        } else {
          return false
        }
      }
    },
    methods: {
      updateDisabled(val) {
        this.disabled = val
      },
      updateReadonly(val) {
        this.readonly = val
      },
      updateUseClear(val) {
        this.useClear = val
      },
      updatePwd(val) {
        this.isPwd = val
        this.type = this.isPwd ? 'password' : 'text'
      },
      updateShowEye(val) {
        this.showEye = val
      },
      updatePwdVisible(val) {
        this.pwdVisible = val
      }
    },
    components: {
      CubePage,
      SwitchOption
    }
  }
</script>

<style lang="stylus">
.cube-page.option-demo.input-view .wrapper
  background-color: #efeff4
  .group
    background-color: white
  .value
    margin: 15px 5px
</style>
