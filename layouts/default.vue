<template>
  <div id="MainLayout" class="h-screen">
    <div class="w-full max-w-[500px] mx-auto">
      <div
        id="TopMenu"
        class="w-full flex items-center justify-center px-2 h-10 my-2"
      >
        <img class="w-[35px]" src="/threads-logo.png" />
      </div>
    </div>

    <div class="flex w-full max-w-[500px] mx-auto h-screen">
      <slot />
    </div>

    <div
      id="BottomNav"
      class="fixed z-50 bottom-0 flex w-full h-[70px] border-t border-t-gray-700 bg-black"
    >
      <div
        class="flex w-full max-w-[500px] mx-auto items-center justify-around"
      >
        <button @click="navigateTo('/')" class="w-full h-full">
          <Icon
            name="material-symbols:home-outline"
            size="35"
            class="text-white"
          />
        </button>
        <button @click="userStore.isMenuOverlay = true" class="w-full h-full">
          <Icon
            class="mb-1 text-white"
            name="material-symbols:edit-square-outline-rounded"
            size="32"
          />
        </button>
        <button @click="userStore.isLogoutOverlay = true" class="w-full h-full">
          <Icon class="mb-1 text-white" name="ph:sign-out" size="32" />
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
const userStore = useUserStore();

const client = useSupabaseClient();
const user = useSupabaseUser();
</script>
