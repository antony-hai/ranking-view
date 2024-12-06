<template>
  <view class="container-resigter">
    <div class="title">
      <div>注册</div>
    </div>
    <nut-form ref="formRef" class="form">
      <nut-form-item label="手机号">
        <nut-input v-model="formData.mobile" />
      </nut-form-item>
      <div class="divide"></div>
      <nut-form-item label="密码">
        <nut-input type="password" v-model="formData.password" />
      </nut-form-item>
      <div class="divide"></div>
      <nut-form-item label="确认密码">
        <nut-input type="password" v-model="formData.confirmPassword" />
      </nut-form-item>
      <div class="divide"></div>
      <div class="submit">
        <div class="button">立即注册</div>
      </div>
    </nut-form>
  </view>
</template>

<script setup>
import { ref } from "vue";

const formData = ref({ mobile: "", password: "", confirmPassword: "" });
const formRef = ref(null);
</script>

<style lang="less">
@primary-color: #0abab5;
.container-resigter {
  background: #dde5f4;
  min-height: 100%;

  .title {
    padding: 130px 0;
    div {
      margin: 0 auto;
      background-color: @primary-color;
      color: white;
      border-radius: 50%;
      text-align: center;
      width: 180px;
      height: 180px;
      font-size: 70px;
      line-height: 180px;
    }
  }
  .form {
    padding: 20px 50px;
    background: transparent;
    .nut-cell-group__wrap {
      background-color: transparent;
      box-shadow: none;

      .nut-cell {
        border-radius: 16px;
        line-height: 48px;
        padding: 30px 36px;
      }
      .nut-form-item__label {
        font-size: 32px;
      }
      .nut-input .input-text {
        font-size: 32px;
      }
    }
  }
  .submit {
    .button {
      text-align: center;
      font-weight: 600;
      color: #ffffff;
      height: 100px;
      font-size: 32px;
      line-height: 100px;
      background-color: @primary-color;
      border-radius: 25px;
    }
  }
  .divide {
    height: 60px;
  }
}
</style>
