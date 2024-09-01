<template>
  <div id="IndexPage" class="w-full overflow-auto">
    <div class="mx-auto max-w-[500px] overflow-hidden">
      <div id="Posts" class="px-4 max-w-[600px] mx-auto">
        <div v-if="isPosts">
          <div v-for="post in posts" :key="post">
            <PostMain
              :post="post"
              @isDeleted="posts = userStore.getAllPosts()"
            />
          </div>
        </div>
        <div v-else>
          <div
            v-if="isLoading"
            class="mt-20 w-full flex items-center justify-center mx-auto"
          >
            <div
              class="text-white mx-auto flex flex-col items-center justify-center"
            >
              <Icon
                name="eos-icons:bubble-loading"
                size="50"
                class="text-white"
              />
              <div class="w-full mt-1">Loading...</div>
            </div>
          </div>
          <div
            v-if="!isLoading"
            class="mt-20 w-full flex items-center justify-center mx-auto"
          >
            <div
              class="text-white mx-auto flex flex-col items-center justify-center"
            >
              <Icon name="tabler:mood-empty" size="50" class="text-white" />
              <div class="w-full">Make the first post!</div>
            </div>
          </div>
        </div>
        <div class="mt-60" />
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({
  title: "Home",
  meta: [
    {
      name: "description",
      content: "Threads - A place to share your thoughts",
    },
  ],
});

const userStore = useUserStore();

let posts = ref([]);
let isPosts = ref(false);
let isLoading = ref(false);

onBeforeMount(async () => {
  try {
    isLoading.value = true;
    await userStore.getAllPosts();
    isLoading.value = false;
  } catch (error) {
    console.log(error);
  }
});

onMounted(() => {
  watchEffect(() => {
    if (userStore.posts && userStore.posts.length >= 1) {
      posts.value = userStore.posts;
      isPosts.value = true;
    }
  });
});

watch(
  () => posts.value,
  () => {
    if (userStore.posts && userStore.posts.length >= 1) {
      posts.value = userStore.posts;
      isPosts.value = true;
    }
  },
  { deep: true }
);
</script>
