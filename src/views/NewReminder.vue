<script setup lang="ts">
import Modal from "../components/Modal.vue";
import { ref} from "vue";


const reminder = ref('');
const date = ref('');
const color = ref('');
const city = ref('');
const error = ref('');


const handleCloseModal = () => {
  error.value = '';
  reminder.value = '';
  date.value = '';
  color.value = '';
  city.value = '';
  props.closeModal();
}

const submitForm = (event: any) => {

  event.preventDefault();


  if (!reminder.value || !date.value || !color.value || !city.value) {
    error.value = 'Por favor, rellena todos los campos';
    return;
  }

  if (reminder.value.length > 30) {
    error.value = 'El reminder es demasiado largo';
    return;
  }

  error.value = '';

  const data = {
    reminder: reminder.value,
    date: date.value,
    color: color.value,
    city: city.value,
  };

  console.log('valor de formulario', data)

  // TODO: Add reminder


  handleCloseModal();
};

</script>

<template>
  <Modal>

    <template #header>
      <div>
        <h2>New reminder</h2>
      </div>
    </template>
    <template #content>

        <form @submit.prevent="submitForm">

          <div class="form-control">
            <label class="form-label" for="reminder">Reminder</label>
            <textarea class="text-area" id="reminder" rows="3" v-model="reminder" />
          </div>

          <div class="form-control">
            <label class="form-label" for="date">Date and time</label>
            <input class="input-text" type="datetime-local" id="date" v-model="date" />
          </div>

          <div class="form-control">
            <label class="form-label" for="color-picker">Selecciona un color:</label>
            <input class="input-color" type="color" id="color-picker" name="color-picker"
            v-model="color">
          </div>

          <div class="form-control">
            <label class="form-label" for="city">Select city:</label>
            <select class="select"  id="city" name="city" v-model="city">
              <option value="">Select</option>
              <option value="Cajica">Cajica</option>
              <option value="Chia">Chia</option>
              <option value="Bogota">Bogota</option>
            </select>
          </div>

          <div class="error-message">
            {{ error }}
          </div>


          <div class="pt-2 text-right" >
            <button type="button" class="btn btn-secondary" @click="handleCloseModal">Cancel</button>
            <button type="submit" class="btn btn-primary ml-1">Save</button>
          </div>

        </form>

    </template>
    <template #footer>
    </template>
  </Modal>
</template>

<style scoped>

</style>