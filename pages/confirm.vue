<template>
  <div class="w-full overflow-auto">
    <div class="mx-auto max-w-[500px] overflow-hidden">
      <div class="px-4 max-w-[600px] mx-auto">
        <div>
          <div class="mt-20 w-full flex items-center justify-center mx-auto">
            <div
              class="text-white mx-auto flex flex-col items-center justify-center"
            >
              <Icon
                name="eos-icons:bubble-loading"
                size="50"
                class="text-white"
              />
              <div class="w-full mt-2">Redirecting....</div>
            </div>
          </div>
        </div>

        <div class="mt-60" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
useHead({
  title: "Confirm",
  meta: [
    {
      name: "description",
      content: "Confirm your account",
    },
  ],
});

const user = useSupabaseUser();

watch(
  user,
  () => {
    if (user.value) {
      return navigateTo("/");
    }
  },
  { immediate: true }
);
</script>
