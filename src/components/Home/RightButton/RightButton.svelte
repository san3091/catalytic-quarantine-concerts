<script>
  import { onMount } from 'svelte'
  import anime from 'animejs/lib/anime.es.js'
	import homeTransitions from '../../../transitions/home'


  export let delay
  export let initialVisit
  export let homeWidth

  let width, clicked

  onMount(() => {
    const letters = document.querySelectorAll('.button-letter')
    if (initialVisit) {
      anime({
        targets: '.button-container',
        translateX: [width + 20, 0],
        delay: delay,
        easing: 'easeOutExpo',
      })

      anime({
        targets: letters,
        translateX: [width + 20, 0],
        opacity: [0, 1],
        delay: anime.stagger(50, {start: delay, from: 'center'}),
        easing: 'easeOutExpo'
      })
    }
  })
</script>

<div class='button-container' class:clicked>
  <button on:click={() => {clicked = true; homeTransitions.outro(homeWidth, width)}}
    class='right-button' 
    bind:clientWidth={width}>
    {#each "LINEUP".split("") as letter }
      <h3 class='button-letter'>{letter}</h3>
    {/each}
  </button> 
  <div class='hover-background-buffer'>
  </div>
</div>
  
<style>
  .button-container {
    position: absolute;
    right: -20px;
    height: 100%;
    overflow: hidden;
    display: flex;
    transition: right 0.3s ease-in-out;
  }

  .right-button {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex: 1;
    margin: 0;
    border: none;
    border-left: 5px solid aliceblue;
    background-color: rgba(0, 0, 0, 35%);
    transition: background-color 0.3s ease-in-out;
  }

  .button-letter {
    margin: 10px 30px;
    color: aliceblue;
    font-family: var(--mono-1);
    transition: color 0.3s ease-in-out;
  }

  .hover-background-buffer {
    background: aliceblue;
    width: 20px;
    flex: 1;
    transition: opacity 0.3s ease-in-out;
  }
  
  .button-container:hover {
    right: 0px;
  }

  .button-container:hover .right-button, 
  .button-container.clicked .right-button {
    background-color: aliceblue;
  }
  
  .button-container:hover .button-letter, 
  .button-container.clicked .button-letter {
    color: black;
    text-shadow: none;
  }
  
  .button-container.clicked {
    right: -20px;
  }

  .button-container.clicked .hover-background-buffer {
    opacity: 0;
  }
</style>