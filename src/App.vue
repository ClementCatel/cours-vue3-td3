<script setup>
import { ref, computed } from "vue";

const text = ref("");
const trimmedText = computed(() => text.value.trim());

const posts = ref([]);

function addPost() {
  const newPost = {
    id: Math.random().toString(36).substring(2),
    content: trimmedText.value,
    createdAt: new Date(),
    author: {
      id: Math.random().toString(36).substring(2),
      username: "Clem",
      avatarUrl: "data:image/jpeg;base64,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"
    }
  }
  posts.value.push(newPost);
  text.value = "";
}
</script>

<template>
  <main>
    <div class="container">
      <form class="card" @submit.prevent="addPost">
        <textarea name="post" id="post" placeholder="Quoi de neuf ?" maxlength="200" v-model="text"></textarea>
        <button type="submit" :disabled="!trimmedText">Publier</button>
      </form>

      <p v-if="!posts.length">Pas de post pour le moment.</p>

      <article v-for="(post, index) in posts" :key="index" class="card">
        <div class="post-header">
          <img :src="post.author.avatarUrl" alt="avatar" width="36" height="36" class="user-image">
          <a>{{ post.author.username }}</a>
        </div>
        <p>{{ post.content }}</p>
      </article>
    </div>
  </main>
</template>

<style scoped>
.container {
  height: 100vh;
  margin: 0 auto;
  max-width: 640px;
}
.card {
  background-color: var(--color-bg-secondary);
  border-radius: 10px;
  border: 1px solid var(--color-border);
  margin-bottom: 1rem;
}

form {
  display: flex;
  flex-direction: column;
  margin-top: 1rem;
  padding: 1rem 1.5rem;
  width: 100%;
}
textarea {
  background: none;
  border: none;
  color: var(--color-text-primary);
  flex: 1;
  margin-bottom: 1rem;
  outline: none;
  padding: 0.5rem 0;
  resize: none;
  field-sizing: content;
}
button {
  align-self: flex-end;
  background: none;
  border-radius: 10px;
  border: 1px solid var(--color-border);
  color: var(--color-text-primary);
  cursor: pointer;
  font-size: 1rem;
  height: 40px;
  padding: 0 1rem;
}
button:disabled {
  cursor: not-allowed;
  opacity: 0.4;
}

article {
  padding: 0.75rem 1.5rem;
  overflow: hidden;
}
article p {
  white-space: pre-wrap;
}

.user-image {
  border-radius: 50%;
  object-fit: cover;
}

.post-header {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1rem;
}
</style>
