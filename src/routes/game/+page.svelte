<script lang="ts">
  import axios from "axios";
  import { Input } from "$lib/components/ui/input";
  import { Button } from "$lib/components/ui/button";

  let data;
  let buttonText = "Start new round!";
  let letters: string = generateRandomLetters();
  let words: string[];
  let foundWords: string[] = [];
  let inputText: string;

  fetchData();

  $: if (words && words.length < 10) {
    fetchData();
  }

  async function fetchData() {
    foundWords = [];
    letters = generateRandomLetters();
    console.log("randomletters", letters);

    try {
      const response = await axios.get(
        `https://8xxui291y1.execute-api.us-east-2.amazonaws.com/anagrams?letters=${letters}`,
      );
      data = response.data.all;
      console.log("data", data);
      words = data.filter((word) => word.length > 2);
    } catch (error) {
      console.error("Error fetching data", error);
    }
  }

  function generateRandomLetters(): string {
    let result = "";
    for (let i = 0; i < 6; i++) {
      const randomCharCode = Math.floor(Math.random() * 26) + 97;
      result += String.fromCharCode(randomCharCode);
    }
    return result;
  }

  function handleSubmit(event: KeyboardEvent | MouseEvent) {
    if (
      (event instanceof KeyboardEvent && event.key === "Enter") ||
      event instanceof MouseEvent
    ) {
      if (words.includes(inputText) && !foundWords.includes(inputText)) {
        foundWords = [...foundWords, inputText];
      }
      inputText = "";
      console.log(foundWords);
    }
  }
</script>

<main class="m-40">
  <div class="flex justify-center items-center">
    <p class="text-8xl">{letters}</p>
  </div>
  <div class="flex justify-center items-center text-2xl">
    {#if words}
      <p>Words Left:</p>
      {words.length - foundWords.length}
    {/if}
  </div>
  <div class="flex items-center h-screen flex-col gap-10 text-4xl text-center">
    {#if foundWords}
      <p>Correct Words:</p>
      {#each foundWords as word}
        <p>{word}</p>
      {/each}
    {/if}
    <div class="flex w-full max-w-sm items-center space-x-2">
      <Input
        on:keydown={handleSubmit}
        bind:value={inputText}
        placeholder="Enter a Buzzword!"
        class="bg-black text-white"
      />
      <Button type="submit" on:click={handleSubmit}>Submit</Button>
    </div>
    <button class="button" style="margin: 0 auto;" on:click={fetchData}
      >{buttonText}</button
    >
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
