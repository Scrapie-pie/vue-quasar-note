<template>
  <q-page padding>
    <AppContainer>
      <h3>New Note</h3>

      <form @submit.prevent="submit">
        <q-input v-model="note.title" class="q-mt-sm" outlined label="Title" />

        <q-input
          class="q-mt-sm"
          outlined
          label="Description"
          v-model="note.description"
          dense
        />

        <q-card flat bordered class="q-mt-sm">
          <q-editor v-model="note.content" min-height="5rem" />
        </q-card>

        <div class="q-mt-md">
          <q-btn to="/" type="reset">Cancel</q-btn>
          <q-btn class="q-ml-sm" type="submit">Create</q-btn>
        </div>

      </form>
    </AppContainer>
  </q-page>
</template>

<script setup lang="ts">
import { reactive } from 'vue';
import { useRouter } from 'vue-router';
import { useLocalNotes } from 'src/helper';
import AppContainer from 'components/AppContainer.vue';

interface INote {
  title: string;
  description: string;
  content: string;
}

const router = useRouter();
const notes = useLocalNotes();

const note: INote = reactive({
  title: '',
  description: '',
  content: '',
});


const submit = () => {
  notes.value.unshift({
    ...note,
    createdAt: Date.now(),
    updatedAt: Date.now(),
  });

  router.push('/')

  note.title = '';
  note.description = '';
  note.content = '';
};
</script>
