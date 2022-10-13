<script setup lang="ts">
import Modal from './components/Modal.vue'
import '@/assets/styles.css'
import { ref } from 'vue'

const showModal = ref(false)
const selectedFruit = ref('')
const selectedFoodItem = ref('')
const favoriteFood = ref('')
const budgetNumber = ref('')

const fruitOptions = ref([
  {text: 'Watermelon', value: 'watermelon'},
  {text: 'Orange', value: 'orange'},
  {text: 'Banana', value: 'banana'},
  {text: 'Kiwi', value: 'kiwi'}
])
const foodItemOptions = ref([
  {foodGroup: 'Vegetables', foods: [{value: 'Lettuce'}, {value: 'Cucumber'}, {value: 'Cabbage'}, {value: 'Broccoli'}]},
  {foodGroup: 'Fruits', foods: [{value: 'Apple'}, {value: 'Orange'}, {value: 'Watermelon'}, {value: 'Banana'}]},
])

function formatBudgetNumber(num: number) {
  const options = {style: 'currency', currency: 'USD'}
  const number = new Intl.NumberFormat('en-US', options)
  return number.format(num)
}

</script>

<template>
  <main class="lp">
    <a href="#" class="btn btn-primary" data-open-modal="exModal" @click="showModal = true">Show Modal</a>
      <Modal class="modal modal-sm" id="exModal" v-if="showModal" @close="showModal = false">

        <template v-slot:header>
          <div class="ly-row ly-spacebetween-center mb-1">
            <h3 class="m-0">Supermarket Survey!</h3>
          </div>
        </template>

        <template v-slot:body>
          <div class="input-wrapper">
            <label for="selectedFruit">Select a Fruit</label>
            <select v-model="selectedFruit" id="selectedFruit">
              <option disabled selected hidden value="">Select option</option>
              <option v-for="option in fruitOptions" :value="option.value">
                {{option.text}}
              </option>
            </select>
          </div>

          <div>
            <label for="selectedFoodItem">Select a Food Item</label>
            <select v-model="selectedFoodItem" id="selectedFoodItem">
              <option disabled selected hidden value="">Select one</option>
              <optgroup v-for="option in foodItemOptions" :label="option.foodGroup">
                <option v-for="food in option.foods" :value="food.value">{{food.value}}</option>
              </optgroup>
            </select>
          </div>

          <div>
            <label for="favoriteFood">Favorite Food</label>
            <textarea rows="1" id="favoriteFood" maxlength="80" v-model="favoriteFood"></textarea>
            <div>
              <p>E.g Seafood Pizza</p>
              <span id="count">{{favoriteFood.length}}/80</span>
            </div>
          </div>

          <div>
            <label for="budget">Food Budget</label>
            <input type="text" v-model.number="budgetNumber" id="budget" @focusout="budgetNumber = formatBudgetNumber(Number(budgetNumber))" />
          </div>
        </template>

        <template v-slot:footer>
          <a href="" class="btn lpi-close">Cancel</a>
          <a href="" class="btn btn-primary">Submit</a>
        </template>
      </Modal>
  </main>
</template>

<style scoped>
  .input-wrapper {
    display: 'flex'
  }
</style>
