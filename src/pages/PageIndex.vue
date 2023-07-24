<template>
  <q-page padding>
    <AppContainer>
      <div class="row items-center justify-between">
        <h3>Your notes</h3>
        <div>
          <q-btn round color="positive" icon="add" to="/new" />
        </div>
      </div>

      <AppNoteCard
        v-for="({ title, description }, idx) in notes"
        :key="idx"
        :title="title"
        :description="description"
        @click="router.push(`/note/${idx}`)"
      />
      <div v-if="!notes.length">You have not created any notes.</div>
    </AppContainer>
  </q-page>
</template>

<script setup lang="ts">
import { useLocalNotes } from 'src/helper';
import { useRouter } from 'vue-router';
import AppContainer from 'components/AppContainer.vue';
import AppNoteCard from 'components/AppNoteCard.vue';

const notes = useLocalNotes();
const router = useRouter();
</script>
