<template>
    <h1>Récapitulatif</h1>
    <p>
        {{ hasWon ? quiz.success_message : quiz.failure_message }}
    </p>
    <p>
        Score : {{ score }}/{{  score_total }}
    </p>
    <!-- {{ quiz.questions.length }} -->
</template>

<script setup>
import { computed } from 'vue'
    const props = defineProps({
        quiz: Object,
        answers: Array
    })
    const score_total = 20
    const score = computed(() => {
        return props.quiz.questions.reduce((acc,question,k) =>{
            if(question.correct_answer === props.answers[k]){
                return acc + 0.5
            }
            return acc
        }, 0)
    })
    const hasWon = computed(() => score.value >= props.quiz.minimum_score)
</script>