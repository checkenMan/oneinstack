<script setup lang="ts">
import System from '@/utils/System'

interface Props {
  currentActive?: 'login' | 'register'
  loading?: boolean
}

withDefaults(defineProps<Props>(), {
  currentActive: 'login',
  loading: false
})
</script>

<template>
  <div v-loading="loading" class="login-container">
    <div class="login-content-left">
      <img class="login-content-left__logo" src="/static/images/login-logo.webp" alt="" />
      <div class="login-content-left__btn">
        <button
          class="login-content-left__btn-login"
          :class="{ active: currentActive === 'login' }"
          @click="System.router.push('/login')"
        >
          登录
        </button>
      </div>
    </div>
    <div class="login-content-right">
      <div class="login-content-right__main">
        <slot
          :className="{
            loginBtn: 'login-content-right__main-login-btn',
            other: 'login-content-right__main-other',
            formItemGap: 'login-content-right__main-form-item-gap'
          }"
        />
      </div>
    </div>
  </div>
</template>

<style scoped lang="less">
@primary-color: #f7911c;
@error-color: #ff4848;
@font-gray: #a2a2a2;
@border-gray: #e3e3e3;
@bg-color: #f5f5f5;

.login-container {
  width: 100%;
  height: 100vh;
  background-color: @bg-color;
  display: flex;
  justify-content: center;
  align-items: center;

  .login-content-left {
    padding: 32px 42px;
    width: 657px;
    height: 100%;
    background: url('/static/images/login-bg.webp') no-repeat;
    background-size: 100% 100%;
    position: relative;

    &__btn {
      position: absolute;
      top: 50%;
      right: 0;
      transform: translate(0, -50%);
      width: 163px;
      height: 210px;
      display: flex;
      flex-direction: column;
      justify-content: center;

      &-login,
      &-register {
        flex: 0.5;
        border-radius: 30px 0 0 30px;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 24px;
        color: #fff;

        &.active {
          font-weight: 500;
          background-color: #fff;
          color: #f75f1c;
        }
      }
    }
  }

  .login-content-right {
    flex: 1;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;

    &__main {
      width: 434px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      :deep(.login-content-right__main-login-btn) {
        margin-top: 48px;
        width: 100%;
        height: 58px;
        background: linear-gradient(180deg, @primary-color 0%, #ff4848 100%);
        border-radius: 10px;
        font-weight: 500;
        font-size: 20px;
        color: #ffffff;
        cursor: pointer;
        transition: box-shadow 0.3s;

        &:hover,
        &:focus {
          box-shadow: 0 0 10px @primary-color;
        }
      }

      :deep(.login-content-right__main-form-item-gap) {
        margin-bottom: 50px;
      }

      :deep(.login-content-right__main-other) {
        margin-top: 53px;
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;

        &-title {
          font-size: 16px;
          color: @font-gray;
        }
      }
    }
  }
}

:deep(.el-input) {
  --el-input-focus-border-color: @primary-color;
  --el-input-bg-color: transparent;
  --el-input-height: 50px;
  --el-input-placeholder-color: @font-gray;
  --el-input-border-color: @border-gray;
  --el-input-border-radius: 0;
  font-size: 16px;
  outline: none;
  box-shadow: none;

  &__wrapper {
    box-shadow: none;
    border-bottom: 1px solid @border-gray;
    transition: border 0.3s;
    padding-left: 0;

    &.is-focus {
      border-bottom: 1px solid @primary-color;
    }
  }
}

:deep(.el-checkbox) {
  --el-checkbox-text-color: @font-gray;
  --el-checkbox-border-radius: 3px;
  --el-checkbox-bg-color: transparent;
  --el-checkbox-checked-text-color: @primary-color;
  --el-checkbox-checked-bg-color: @primary-color;
  --el-checkbox-input-border-color-hover: @primary-color;
  --el-checkbox-checked-input-border-color: @primary-color;

  &__input {
    zoom: 1.85;
  }

  &__label {
    padding-left: 22px;
  }
}

:deep(.el-link) {
  --el-link-font-size: 14px;
  --el-link-text-color: @font-gray;
  --el-link-font-weight: 400;
  --el-link-hover-text-color: @primary-color;
}

:deep(.el-form-item.is-error) {
  .el-input__wrapper {
    box-shadow: none;
    border-bottom: 1px solid @error-color;
  }
}

:deep(.el-divider__text) {
  font-size: 16px;
  color: @font-gray;
  background-color: @bg-color;
}
</style>
