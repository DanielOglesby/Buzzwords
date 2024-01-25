<script lang="ts">
    import axios from 'axios';

    let data;

    let buttonText = "Start new round!";

    let letters: string[] = generateRandomLetters();
    let words = data;

    async function fetchData() {
        generateRandomLetters();
        
        try {
            const response = await axios.get(`http://www.anagramica.com/all/${letters}`);
            data = response.data;
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

    console.log(letters);
    console.log(words);

</script>

<main>
    <div class="flex justify-center items-center">
        <p class="text-8xl">{letters}</p>
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