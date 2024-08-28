<template>
  <div id="app">
    <div class="form-container">
      <form @submit.prevent="handleSubmit">
        <div class="form-row">
          <label for="title">Título</label>
          <input v-model="formData.title" type="text" id="title" />
        </div>

        <hr class="gray-line" />

        <div class="form-row">
          <label for="emoji">Emoji</label>
          <select v-model="formData.emoji" id="emoji" class="emoji-select">
            <option value="👨‍💻">👨‍💻</option>
            <option value="👩‍💻">👩‍💻</option>
            <option value="💻">💻</option>
            <option value="🖥️">🖥️</option>
            <option value="🔧">🔧</option>
          </select>
        </div>

        <hr class="white-line" />

        <div class="form-row">
          <label>Apreciación</label>
          <div class="radio-group">
            <div v-for="option in appreciationOptions" :key="option">
              <input
                type="radio"
                :value="option"
                v-model="formData.appreciation"
                :id="option"
              />
              <label :for="option">{{ option }}</label>
            </div>
          </div>
        </div>

        <hr class="gray-line" />

        <div class="form-row">
          <label>Competencias aprendidas</label>
          <div class="checkbox-group">
            <div class="checkbox-row">
              <div v-for="(competence, index) in competenceOptions.slice(0, 2)" :key="competence">
                <input
                  type="checkbox"
                  :value="competence"
                  v-model="formData.competencies"
                  :id="competence"
                />
                <label :for="competence">{{ competence }}</label>
              </div>
            </div>
            <div class="checkbox-row">
              <div v-for="(competence, index) in competenceOptions.slice(2, 4)" :key="competence">
                <input
                  type="checkbox"
                  :value="competence"
                  v-model="formData.competencies"
                  :id="competence"
                />
                <label :for="competence">{{ competence }}</label>
              </div>
            </div>
            <div class="checkbox-row">
              <div v-for="(competence, index) in competenceOptions.slice(4, 5)" :key="competence">
                <input
                  type="checkbox"
                  :value="competence"
                  v-model="formData.competencies"
                  :id="competence"
                />
                <label :for="competence">{{ competence }}</label>
              </div>
            </div>
          </div>
        </div>

        <hr class="white-line" />

        <div class="form-row">
          <label for="opinion">Opinión</label>
          <textarea v-model="formData.opinion" id="opinion"></textarea>
        </div>
      </form>
    </div>

    <div class="result-container">
      <div class="icon">{{ formData.emoji }}</div>
      <h1>{{ formData.title }}</h1>
      <h2>Y me parece {{ formData.appreciation }}</h2>
      <h3>He aprendido:</h3>
      <h3>{{ formatCompetencies() }}</h3>
      <h3>Mi opinión hasta ahora del framework es:</h3>
      <h4 class="gray-text">{{ formData.opinion }}</h4>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        title: '',
        emoji: '👨‍💻',
        appreciation: 'Regular',
        competencies: [],
        opinion: ''
      },
      appreciationOptions: ['Regular', 'Bien', 'Muy bien', 'Increíble'],
      competenceOptions: [
        'Morfología de un componente',
        'Directivas',
        'One-Way y Two-Way data binding',
        'Estado',
        'El patrón de diseño MVVM'
      ]
    };
  },
  methods: {
    formatCompetencies() {
      return this.formData.competencies.length
        ? JSON.stringify(this.formData.competencies)
        : '';
    }
  }
};
</script>
<style scoped>
#app {
  display: flex;
  height: 100vh;
  font-family: Arial, sans-serif;
}

.form-container {
  width: 28rem;
  padding: 1.25rem;
  background-color: black;
  color: white;
  border-radius: 0.5rem;
  border: 0.125rem solid #6c6c6c;
  margin: 0.625rem;
}

.result-container {
  width: 72rem;
  padding: 1.25rem;
  border-radius: 0.5rem;
  border: 0.125rem solid #6c6c6c;
  margin: 0.625rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-row {
  margin-bottom: 1.25rem;
  display: flex;
  align-items: center;
  gap: 0.625rem;
}

label {
  margin-right: 0.625rem;
}

.radio-group {
  display: flex;
  gap: 0.625rem;
}

.checkbox-group {
  display: flex;
  flex-direction: column;
}

.checkbox-group .checkbox-row {
  display: flex;
  gap: 0.625rem;
}

.checkbox-group .checkbox-row:last-child {
  margin-top: 0.625rem;
}

hr.gray-line {
  border: 0;
  border-top: 0.0625rem solid gray;
  margin: 1.25rem 0;
}

hr.white-line {
  border: 0;
  border-top: 0.0625rem solid white;
  margin: 1.25rem 0;
}

textarea {
  width: 100%;
  height: 6.25rem;
}

.emoji-select {
  margin-left: 0.625rem;
}

.icon {
  font-size: 2rem;
  margin-bottom: 1.25rem;
}

.result-container h1,
.result-container h2,
.result-container h3,
.result-container h4 {
  margin: 1.25rem 0;
}

.gray-text {
  color: gray;
}
</style>
