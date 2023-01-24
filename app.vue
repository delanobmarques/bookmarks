<script lang="ts" setup>
const newBookmark = ref("");
const { pending, data:bookmarks } = useAsyncData(async () => 
  $fetch("/api/bookmarks")
);
</script>

<template>
  <main>
    <form @submit.prevent>
      <label for="url">Add Bookmarks</label>
      <input v-model="newBookmark" type="url" name="url" id="url" required/>
      <button>Add</button>
    </form>

    <div>{{ newBookmark }}</div>

    <div v-if="pending">Loading...</div>
    <div v-else-if="bookmarks && bookmarks.length > 0">
      <ul>
        <li v-for="bookmark in bookmarks" :key="bookmark.id">
          {{  bookmark.url }}
        </li>
      </ul>
    </div>

    <div v-else>no bookmarks, yet ...</div>
  </main>
</template>
