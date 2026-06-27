<script setup lang="ts">
import { computed, ref } from 'vue'

// Demo-only client-side gate over mock data; this code is visible in the client bundle.
const ACCESS_CODE = 'harbor'

const enteredCode = ref('')
const unlocked = ref(false)
const showError = ref(false)

const canSubmit = computed(() => enteredCode.value.trim().length > 0)

const unlockDashboard = () => {
  if (enteredCode.value.trim().toLowerCase() === ACCESS_CODE) {
    unlocked.value = true
    showError.value = false
    return
  }
  showError.value = true
}
</script>

<template>
  <v-app>
    <v-main>
      <section v-if="!unlocked" class="gate-shell">
        <v-card class="gate-card pa-8" border>
          <p class="gate-eyebrow">Mercy General</p>
          <h1 class="gate-title">Clinical Operations Access</h1>
          <p class="gate-copy">Enter the access code to view the operational dashboard.</p>

          <v-text-field
            v-model="enteredCode"
            label="Access code"
            variant="outlined"
            density="comfortable"
            hide-details="auto"
            class="mt-4"
            @keydown.enter="unlockDashboard"
          />

          <v-alert
            v-if="showError"
            class="mt-4"
            type="error"
            variant="tonal"
            density="compact"
          >
            Access code is incorrect.
          </v-alert>

          <v-btn
            class="mt-6"
            color="primary"
            size="large"
            block
            :disabled="!canSubmit"
            @click="unlockDashboard"
          >
            Unlock
          </v-btn>
        </v-card>
      </section>

      <RouterView v-else />
    </v-main>
  </v-app>
</template>

<style scoped>
.gate-shell {
  min-height: 100svh;
  display: grid;
  place-items: center;
  padding: 1.5rem;
}

.gate-card {
  width: min(440px, 100%);
  background: #ffffff;
  border-color: #e2e6eb;
}

.gate-eyebrow {
  margin: 0;
  color: #0f766e;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.76rem;
  font-weight: 700;
}

.gate-title {
  margin: 0.35rem 0 0;
  color: #1b2733;
  font-size: 1.55rem;
  line-height: 1.15;
}

.gate-copy {
  margin: 0.6rem 0 0;
  color: #5d6a75;
}
</style>
