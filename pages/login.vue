<template>
  <div id="AuthPage" class="w-full h-screen pt-32">
    <div class="w-full">
      <div class="w-full flex items-center justify-center gap-2.5 p-2">
        <img class="w-[35px]" src="/threads-logo.png" />
        <span class="font-bold text-2xl text-white">Threads</span>
      </div>

      <div class="max-w-[350px] mx-auto px-2 text-white">
        <div class="text-center mb-6 mt-4">Login / Register</div>

        <button
          @click="login('github')"
          class="flex items-center justify-center gap-3 p-1.5 w-full border rounded-full text-lg font-semibold"
        >
          <div class="flex items-center gap-2 justify-center">
            <img
              class="w-full max-w-[30px] rounded-full"
              src="/github-logo.png"
            />
            Github
          </div>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
useHead({
  title: "Login",
  meta: [
    {
      name: "description",
      content: "Login to Threads",
    },
  ],
});

const client = useSupabaseClient();
const user = useSupabaseUser();

watchEffect(() => {
  if (user.value) {
    return navigateTo("/");
  }
});

const login = async (prov: string) => {
  const { data, error } = await client.auth.signInWithOAuth({
    provider: prov,
    options: {
      redirectTo: `${window.location.origin}/confirm`,
    },
  });

  if (error) console.log(error);
};
</script>
