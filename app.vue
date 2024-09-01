<template>
  <div>
    <NuxtPwaManifest />
    <div class="bg-black fixed w-[calc(100%+1px)] h-full">
      <NuxtLayout>
        <NuxtPage />
      </NuxtLayout>

      <CreatePost
        :class="[
          {
            'max-h-[100vh] transition-all duration-200 ease-in visible':
              userStore.isMenuOverlay,
          },
          {
            'max-h-0 transition-all duration-200 ease-out invisible':
              !userStore.isMenuOverlay,
          },
        ]"
      />

      <ModalLogout
        :class="[
          {
            'max-h-[100vh] transition-all duration-200 ease-in visible':
              userStore.isLogoutOverlay,
          },
          {
            'max-h-0 transition-all duration-200 ease-out invisible':
              !userStore.isLogoutOverlay,
          },
        ]"
      />
    </div>
  </div>
</template>

<script setup>
useHead({
  titleTemplate: (titleChunk) => {
    return titleChunk ? `${titleChunk} - Threads` : "Threads";
  },
  meta: [
    {
      name: "description",
      content: "Threads - A place to share your thoughts",
    },
  ],
});

const userStore = useUserStore();
</script>
