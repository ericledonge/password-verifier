<script setup>
import { ref, onMounted } from 'vue'

const digit_1 = ref(null)
const digit_2 = ref(null)
const digit_3 = ref(null)
const digit_4 = ref(null)

const verification_1 = ref(null)
const verification_2 = ref(null)
const verification_3 = ref(null)
const verification_4 = ref(null)

onMounted(() => {
  verification_1.value.focus()
})

const handleInput = () => {
  if (digit_1.value !== null) {
    verification_2.value.focus()
  }
  if (digit_2.value !== null) {
    verification_3.value.focus()
  }
  if (digit_3.value !== null) {
    verification_4.value.focus()
  }
}

const handlePaste = (event) => {
  const pasted = event.clipboardData.getData('text')
  if (pasted.length === 4) {
    digit_1.value = pasted[0]
    digit_2.value = pasted[1]
    digit_3.value = pasted[2]
    digit_4.value = pasted[3]
  }
}

const handleVerify = (e) => {
  console.log(`${digit_1.value}${digit_2.value}${digit_3.value}${digit_4.value}`)
}
</script>

<template>
  <div class="wrapper" @paste="handlePaste">
    <h1>Authorization Code</h1>
    <p>Please enter the code that we sent to (***) *** - 2819.</p>
    <form @submit.prevent="handleVerify">
      <div class="fields">
        <input type="text" maxlength="1" v-model="digit_1" ref="verification_1" @input="handleInput" />
        <input type="text" maxlength="1" v-model="digit_2" ref="verification_2" @input="handleInput" />
        <input type="text" maxlength="1" v-model="digit_3" ref="verification_3" @input="handleInput" />
        <input type="text" maxlength="1" v-model="digit_4" ref="verification_4" @input="handleInput" />
      </div>
      <button>Verify</button>
    </form>
  </div>
</template>
