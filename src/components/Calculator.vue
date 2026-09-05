<template>
    <v-container class="fill-height d-flex flex-column justify-center" max-width="1100">
        <div>
            <v-row>
                <v-col cols="12" md="3">
                    <v-card class="pt-8 px-4" height="225">
                        <v-text-field v-model="numberOfLbs" label="Number of lbs of animal" variant="outlined"
                            class="px-4" />

                        <v-divider :thickness="10" />

                        <v-text-field v-model="oneLb" label="One lb" :disabled="true" variant="outlined"
                            class="px-4 py-4" />
                    </v-card>
                </v-col>

                <v-col cols="12" md="3">
                    <v-card class="pt-8 px-4" height="225">
                        <v-text-field v-model="oneKg" label="One kg" :disabled="true" variant="outlined" class="px-4" />

                        <v-divider :thickness="10" />

                        <v-text-field v-model="lbsToKg" label="lbsToKgs" :disabled="true" variant="outlined"
                            class="px-4 py-4" />
                    </v-card>
                </v-col>

                <v-col cols="12" md="3">
                    <v-card class="pt-8 px-4" height="225">
                        <v-text-field v-model="numberOfMg" label="Number of mg" variant="outlined" class="px-4" />

                        <v-divider :thickness="10" />

                        <v-text-field v-model="oneKg" label="One kg" :disabled="true" variant="outlined"
                            class="px-4 py-4" />
                    </v-card>
                </v-col>
                <v-col cols="12" md="3">
                    <v-card class="pt-8 px-4" height="225">
                        <v-text-field v-model="oneMl" label="One ml" variant="outlined" :disabled="true" class="px-4" />

                        <v-divider :thickness="10" />

                        <v-text-field v-model="mgPerMl" label="mg per ml" variant="outlined" class="px-4 py-4" />
                    </v-card>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12" md="12" class="d-flex justify-center mt-6">
                    <v-btn color="primary" class="mr-4 mt-2" @click="calculateDosage">Calculate</v-btn>
                    <v-card-text class="result">
                        {{ result }} {{ measurement }}
                    </v-card-text>
                </v-col>
            </v-row>
        </div>
    </v-container>
    <v-footer> <v-row class="justify-center">
            <v-col class="text-center">
                {{ new Date().getFullYear() }} —
                <strong>Made with
                    <v-icon icon="mdi-heart" color="secondary"></v-icon> by
                    NinjaPanda47</strong>
            </v-col>
        </v-row></v-footer>
</template>

<script setup lang="ts">

import { ref, reactive, computed } from 'vue'

const numberOfLbs = ref('')
const oneLb = ref('1')
const lbsToKg = ref('2.2')
const oneKg = ref('1')
const numberOfMg = ref('')
const oneMl = ref('1')
const mgPerMl = ref('')
let result = ref(0)

const measurement = computed(() => {
    return mgPerMl.value === '' ? 'mg' : 'ml'
})

function calculateDosage() {
    const includeMl = mgPerMl.value !== ''
    const lbs = Number(numberOfLbs.value)
    const mgsToKgs = Number(numberOfMg.value)
    const mgsToMls = Number(mgPerMl.value)
    if (includeMl) {
        result.value = (lbs * mgsToKgs) / (2.2 * mgsToMls)
    } else {
        result.value = (lbs * mgsToKgs) / 2.2
    } console.log(result)
}
</script>

<style scoped>
.result {
    font-size: 20px;
}
</style>