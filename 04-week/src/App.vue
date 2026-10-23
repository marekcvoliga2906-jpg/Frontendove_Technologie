<script setup>
import { computed, ref } from 'vue'

const students = ref([
  { id: 1, name: 'Anna Nováková', grade: 92 },
  { id: 2, name: 'Martin Kováč', grade: 78 },
  { id: 3, name: 'Lucia Horváthová', grade: 85 }
])
const name = ref('')
const grade = ref('')
const formError = ref('')

const averageGrade = computed(() => {
  if (students.value.length === 0) return null
  const total = students.value.reduce((sum, student) => sum + student.grade, 0)
  return total / students.value.length
})

function addStudent() {
  const trimmedName = name.value.trim()
  const normalizedGrade = grade.value.trim().replace(',', '.')

  if (trimmedName.length <= 2) {
    formError.value = 'Meno musí mať viac ako 2 znaky.'
    return
  }
  if (/\d/.test(trimmedName)) {
    formError.value = 'Meno nesmie obsahovať čísla.'
    return
  }
  if (!/^\d+(\.\d+)?$/.test(normalizedGrade)) {
    formError.value = 'Známka musí obsahovať iba číslo.'
    return
  }

  const numericGrade = Number(normalizedGrade)
  if (numericGrade < 0 || numericGrade > 100) {
    formError.value = 'Známka musí byť v rozsahu od 0 do 100.'
    return
  }

  students.value.push({ id: Date.now(), name: trimmedName, grade: numericGrade })
  name.value = ''
  grade.value = ''
  formError.value = ''
}

function removeStudent(id) {
  students.value = students.value.filter((student) => student.id !== id)
}
</script>

<template>
  <main class="page">
    <section class="card" aria-labelledby="title">
      <p class="eyebrow">Samostatný projekt</p>
      <h1 id="title">Evidencia študentov</h1>

      <form class="student-form" @submit.prevent="addStudent">
        <label>
          Meno študenta
          <input v-model="name" type="text" placeholder="Napr. Jana Nováková" autocomplete="name">
        </label>
        <label>
          Známka (0 – 100)
          <input v-model="grade" type="text" inputmode="decimal" placeholder="Napr. 85">
        </label>
        <button type="submit">Pridať študenta</button>
      </form>

      <p v-if="formError" class="form-error" role="alert">{{ formError }}</p>

      <div class="table-wrapper">
        <table v-if="students.length">
          <thead>
            <tr>
              <th scope="col">Meno študenta</th>
              <th scope="col">Známka</th>
              <th scope="col"><span class="sr-only">Akcia</span></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="student in students" :key="student.id">
              <td>{{ student.name }}</td>
              <td>{{ student.grade }}</td>
              <td><button class="remove-button" type="button" @click="removeStudent(student.id)">Vymazať</button></td>
            </tr>
          </tbody>
          <tfoot>
            <tr>
              <th scope="row">Priemerná známka</th>
              <td colspan="2">{{ averageGrade.toFixed(2) }}</td>
            </tr>
          </tfoot>
        </table>
        <p v-else class="empty-state">Nenašli sa žiadni študenti.</p>
      </div>
    </section>
  </main>
</template>

<style scoped>
:global(*) { box-sizing: border-box; }
:global(body) { margin: 0; background: #f2f5f9; color: #1d2939; font-family: Arial, sans-serif; }
.page { display: grid; min-height: 100vh; place-items: center; padding: 24px; }
.card { width: min(100%, 720px); padding: 32px; background: #fff; border-radius: 16px; box-shadow: 0 12px 36px #172b4d1a; }
.eyebrow { margin: 0 0 6px; color: #4f46e5; font-size: .85rem; font-weight: 700; text-transform: uppercase; letter-spacing: .08em; }
h1 { margin: 0 0 28px; font-size: clamp(1.8rem, 4vw, 2.5rem); }
.student-form { display: grid; grid-template-columns: 1fr 180px auto; gap: 16px; align-items: end; }
label { display: grid; gap: 6px; font-weight: 600; }
input { min-width: 0; padding: 10px 12px; border: 1px solid #cbd5e1; border-radius: 8px; font: inherit; }
input:focus { outline: 3px solid #c7d2fe; border-color: #4f46e5; }
button { padding: 11px 16px; border: 0; border-radius: 8px; background: #4f46e5; color: white; font: inherit; font-weight: 700; cursor: pointer; }
button:hover { background: #4338ca; }
.form-error { margin: 16px 0 0; color: #b42318; font-weight: 600; }
.table-wrapper { margin-top: 28px; overflow-x: auto; }
table { width: 100%; border-collapse: collapse; text-align: left; }
th, td { padding: 14px 12px; border-bottom: 1px solid #e2e8f0; }
thead { background: #f8fafc; }
tfoot { background: #eef2ff; }
.remove-button { padding: 7px 10px; background: #b42318; }
.remove-button:hover { background: #8f1b13; }
.empty-state { margin: 0; padding: 24px; text-align: center; color: #475467; background: #f8fafc; border-radius: 8px; }
.sr-only { position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px; overflow: hidden; clip: rect(0, 0, 0, 0); white-space: nowrap; border: 0; }
@media (max-width: 640px) { .card { padding: 24px 18px; } .student-form { grid-template-columns: 1fr; } }
</style>
