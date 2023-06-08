<script>
	import quizzes from '../data.json';
	import Card from '../components/Card.svelte';
</script>

{#each quizzes as quiz (quiz.id)}
	<Card {quiz} />
{/each}

<style lang="postcss">
</style>
