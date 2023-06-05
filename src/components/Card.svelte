<script lang="ts">
    import * as images from "../image";
    import { goto} from "$app/navigation"

    interface Quiz {
        id: number;
        name: string;
        imageUrl: keyof typeof images;
        questions: {
            id: number;
            question: string;
            answer: string;
            options: {
                id: number;
                label: string;
                text: string;
            } [];
        }[]
    }

    export let quiz: Quiz;

    const handleClick = () => {
        goto(`quiz/${quiz.id}`)
    }
</script>

<button 
    class="quiz-card shadow w-[250px] rounded overflow-hidden cursor-pointer m-2"
    on:click={handleClick}
>
    <img src={images[quiz.imageUrl]} alt="" class="h-44">
    <div class="flex items-center justify-between py-3 px-2">
        <h1 class="font-bold">{quiz.name}</h1>
        <p>{quiz.questions.length} Questions</p>
    </div>
</button>
