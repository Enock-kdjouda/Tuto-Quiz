<template>
    <div class="Question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in randomChoices" :key="choice">
              <Answer 
                    :id="'answer${index}'"
                    :disabled="hasAnswer"
                    :value="choice"
                    @change="onAnswer"
                    v-model="answer"
                    :correctAnswer="question.correct_answer"
/>
            </li>
        </ul>
        <!-- <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button>
         -->
    </div>
</template>
<script setup>
    import { ref, computed, defineProps, defineEmits, onMounted, onUnmounted } from 'vue'
    import {shuffleArray} from '@/functions/array.js'
    import Answer from './Answer.vue'
 
    const props = defineProps({
        question: Object
    })
    const emits = defineEmits(['answer'])
    const answer = ref(null)
    const hasAnswer = computed(() => answer.value !== null)
    const randomChoices = computed(() => shuffleArray(props.question.choices))
    const onAnswer = (e) => {
        // Partie de time
        clearTimeout(timer)
        timer = setTimeout(() => {
            emits('answer', answer.value)
            
        },5_000)
    }

    let timer

    onMounted(() => {
        timer = setTimeout(() => {
            emits('answer', answer.value)
            
        },12_000)
    })
    onUnmounted(() => {
        clearTimeout(timer)
    })
    // Fin de la partie
</script>
<style>
   .Question {
        
        padding-top: 2rem;
    }
    .Question button{
        margin-left: auto;
        display: block;
    }
</style>