<template>
  <nav :class="['navbar', { transparent: isHome, fixed: isHome, bordered: !isHome }]">
    <div
      class="container"
      style="display: flex"
    >
      <div class="left-section">
        <RouterLink
          to="/"
          class="logo-link"
        >
          <div class="logo">MoneyUp</div>
        </RouterLink>

        <ul class="nav-links">
          <li><RouterLink to="/product">상품</RouterLink></li>
          <li><RouterLink to="/spotAsset">현물</RouterLink></li>
          <li><RouterLink to="/map">지도</RouterLink></li>
          <li><RouterLink to="/article">커뮤니티</RouterLink></li>
          <li><RouterLink to="/searchproduct">관심종목검색</RouterLink></li>
        </ul>
      </div>
      <template v-if="store.isLogin">
        <img
          style="margin-left: auto; cursor: pointer"
          @click="onclick"
          src="@/assets/icon/basicprofile.png"
          alt=""
        />
        <BaseButton
          style="margin-left: 20px"
          @click="store.logOut()"
          >로그아웃</BaseButton
        >
      </template>
      <template v-else>
        <BaseButton
          style="margin-left: auto"
          to="/login"
          >로그인</BaseButton
        >
        <BaseButton
          style="margin-left: 20px"
          to="/signup"
          variant="secondary"
          >가입하기</BaseButton
        >
      </template>
      <div class="right-section"></div>
    </div>
  </nav>
</template>

<script setup>
import BaseButton from '@/components/base/BaseButton.vue'
import { useAccountStore } from '@/stores/accounts'
import { computed } from 'vue'
import { RouterLink, useRoute, useRouter } from 'vue-router'

const route = useRoute()

const isHome = computed(() => route.path === '/')

const store = useAccountStore()
const router = useRouter()

const onclick = () => {
  router.push({ name: 'profile-update' })
}
</script>

<style scoped lang="scss">
@use '@/assets/styles/utils/variables' as *;

img {
  width: 40px;
  height: 40px;
}

.navbar {
  width: 100%;
  background-color: white;
  font-family: $font-base;
  z-index: 1000;

  &.transparent {
    background-color: rgba(255, 255, 255, 0.3);
    box-shadow: none;
  }

  &.fixed {
    position: fixed;
    top: 0;
    left: 0;
  }

  &.bordered {
    border-bottom: 1px solid #dee2e6;
  }
}

.wrapper {
  max-width: 1280px;
  margin: 0 auto;
  height: 60px;
  padding: 0 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.left-section {
  display: flex;
  align-items: center;
  gap: 40px;
}

.logo {
  font-weight: 900;
  font-size: 24px;
  line-height: 36px;
  color: $primary-500;
}

.logo-link {
  text-decoration: none;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 24px;
  margin: 0;
  padding: 0;
}

.nav-links li {
  cursor: pointer;
  font-weight: 600;
  font-size: 16px;
  color: $primary-500;
}

.nav-links a {
  text-decoration: none;
  color: inherit;
}

.right-section {
  display: flex;
  gap: 12px;
  align-items: center;
}
</style>
