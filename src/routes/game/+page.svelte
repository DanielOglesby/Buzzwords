<script lang="ts">
    import axios from 'axios';

    let data;
    let buttonText = "Start new round!";
    let letters: string = generateRandomLetters();
    let words: string[];

    async function fetchData() {
        letters = generateRandomLetters();
        console.log('randomletters', letters);
        
        try {
            const response = await axios.get(`https://8xxui291y1.execute-api.us-east-2.amazonaws.com/anagrams?letters=${letters}`);
            data = response.data.all;
            console.log('data', data);
            words = data;
        } catch (error) {
            console.error('Error fetching data', error);
        }
    }

    function generateRandomLetters(): string {
        let result = '';
        for (let i = 0; i < 6; i++) {
            const randomCharCode = Math.floor(Math.random() * 26) + 97;
            result += String.fromCharCode(randomCharCode);
        }
        return result;
    }
</script>

<main>
    <div class="flex justify-center items-center">
        <p class="text-8xl">{letters}</p>
    </div>
    <div class="flex justify-center items-center text-2xl">
        {#if words}
            {#each words as word}
                <p>{word}...</p>
            {/each}
        {/if}
    </div>
    <div class="flex justify-center items-center h-screen">
        <button class="button" style="margin: 0 auto;" on:click={fetchData}>{buttonText}</button>
    </div>
</main>

<style>
        .button {
        background-color: #333;
        color: white;
        padding: 10px 20px;
        border-radius: 5px;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2);
        cursor: pointer;
    }
</style>