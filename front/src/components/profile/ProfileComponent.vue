<template>
	<div class="profile-container">
		<div class="menu">
			<p 
				style="padding-top: 30%;" 
				@click="showProfile"
				:class="{ ispick: route.name === 'profile-update' }"
				>프로필 수정</p>
			<p @click="showProducts" :class="{ ispick: route.name === 'profile-accession' }">찜한 상품들</p>
			<p @click="aiPick" :class="{ ispick: route.name === 'profile-ai' }">맞춤 상품 추천</p>
		</div>
		<div style="width: 100%;">
			<RouterView/>
		</div>
	</div>
</template>

<script setup>
	import { RouterView, useRouter, useRoute } from 'vue-router';

	const router = useRouter()
	const route = useRoute();

	const showProfile = () => {
		router.push({name:'profile-update'})
	}

	const showProducts = () => {
		router.push({name:'profile-accession'})
	}

	const aiPick = () => {
		router.push({name: 'profile-ai'})
	}
</script>

<style lang="scss" scoped>
@use '@/assets/styles/utils/variables' as *;

.profile-container {
	display: flex;
	min-height: 100vh; /* Ensure the container takes at least full viewport height */
}

.menu {
	flex: 0 0 200px;
	border-right: solid 1px $gray-300;
	border-left: solid 1px $gray-300;
	margin-right: 70px;
}

p {
	font-family: $font-base;
	font-size: $font-size-lg;
	font-weight: 600;
	color: $gray-500;
	margin-bottom: 35px;
	padding-left: 34px;
	cursor: pointer;
}

.ispick {
	color: $primary-500;
}



</style>
