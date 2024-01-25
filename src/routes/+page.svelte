<script>
	import { goto } from "$app/navigation";

    let buttonText = "Begin playing Buzzwords! 🐝";

    function goToGame() {
        goto("/game");
    }
</script>

<main>
    <div class="flex justify-center items-center h-screen">
        <button class="button" style="margin: 0 auto;" on:click={goToGame}>{buttonText}</button>
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