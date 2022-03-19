<template>

  {{ currentNoteType }}

  <div
    v-for="t in noteTypes"
    :key="t.identity.value"
  >
    <span @click="selectNoteType(t.identity.value)">
      {{ t.name.value }} ({{t.fields.all.length }})
      <span v-for="f in t.fields.all" :key="f.name.value">
        <span @click="renameField">{{f.name.value}}</span>
      </span>
    </span>
  </div>
  <div @click="createNewNoteType">Add new</div>
  <div @click="addField">Add field</div>
</template>

<script setup lang="ts">
// import { Identity } from '@sarasvati-platform/core/dist/core/models/entity'
import { NoteType, NoteTypeName, NoteField, NoteFieldName } from '@sarasvati-platform/core/dist/flashcards/models/index'
import { reactive, ref } from 'vue'
// const emptyObject = {}
const first = new NoteType(new NoteTypeName("123"))
const noteTypes = reactive<NoteType[]>([first])

let currentNoteType = ref<string>(first.identity.value)

function createNewNoteType() {
  noteTypes.push(
    new NoteType(
      new NoteTypeName('New Note Type')
  ))
}

function selectNoteType(noteTypeId: string) {
  console.log(noteTypeId)
  currentNoteType.value = noteTypeId
}

function addField() {
  const noteType = noteTypes.find(x => x.identity.value === currentNoteType.value)
  noteType?.fields.add(new NoteField(new NoteFieldName("llllaaaa" + new Date().toISOString())))
}

function renameField() {
  // const noteType = noteTypes.find(x => x.identity.value === currentNoteType.value)
  // noteType?.fields.all[0].name
}
</script>