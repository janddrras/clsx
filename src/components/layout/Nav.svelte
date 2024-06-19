<script>
  import { fade, fly } from "svelte/transition"
  import { onMount } from "svelte"
  import Logo from "./Logo.svelte"
  import { quartOut } from "svelte/easing"

  export let page
  let color = page === "large" ? "white" : "var(--dark-grey)"

  let isOpen = false
  let y
  let fullHeight
  let windowHeight

  onMount(() => {
    fullHeight = document.body.scrollHeight
    windowHeight = window.innerHeight
  })
</script>

<svelte:window bind:scrollY={y} />

<header class="container">
  <div class="main-menu">
    <a href="/"><Logo {color} /></a>
    <button class="menu-button" on:click={() => (isOpen = !isOpen)}>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        width="50%"
        height="50%"
        stroke="#1f1f1f"
        stroke-width="2"
        stroke-linecap="round"
      >
        <path d="M3 12h18M3 6h18M3 18h18" />
      </svg>
    </button>
  </div>

  {#if y > windowHeight / 2 && y < fullHeight - windowHeight}
    <div class="second-menu" transition:fade={{ duration: 500 }}>
      <a href="/"><Logo isSmall /></a>
      <button class="menu-button" on:click={() => (isOpen = !isOpen)}>
        {#if isOpen}
          <svg width="40%" height="40%" style="" viewBox="0 0 7 7" fill="#1f1f1f" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M6.85979 7H5.75379L3.56979 4.116L1.38579 7H0.279785L3.02379 3.374L0.461785 0H1.56779L3.56979 2.646L5.57179 0H6.67779L4.12979 3.374L6.85979 7Z"
            />
          </svg>
        {:else}
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            width="50%"
            height="50%"
            stroke="#1f1f1f"
            stroke-width="2"
            stroke-linecap="round"
          >
            <path d="M3 12h18M3 6h18M3 18h18" />
          </svg>
        {/if}
      </button>
      <div class="second-menu-overlay" />
    </div>
  {/if}

  {#if isOpen}
    <nav>
      <div class="menu-grid" transition:fly={{ y: "-100%", duration: 1000, easing: quartOut }}>
        <a href="/" on:click={() => (isOpen = false)}>
          <div class="menu-link" in:fly={{ y: "80%", duration: 800, delay: 100, easing: quartOut }}>
            <p class="background-letter">C</p>
            <span>Home</span>
            <img src="/arrow_outward.svg" alt="arrow icon" />
          </div>
        </a>
        <a href="/about" on:click={() => (isOpen = false)}>
          <div class="menu-link" in:fly={{ y: "80%", duration: 800, delay: 300, easing: quartOut }}>
            <p class="background-letter">L</p>
            <span>About</span>
            <img src="/arrow_outward.svg" alt="arrow icon" />
          </div>
        </a>
        <a href="/gallery" on:click={() => (isOpen = false)}>
          <div class="menu-link" in:fly={{ y: "80%", duration: 800, delay: 400, easing: quartOut }}>
            <p class="background-letter">S</p>
            <span>Gallery</span>
            <img src="/arrow_outward.svg" alt="arrow icon" />
          </div>
        </a>
        <a href="/contact" on:click={() => (isOpen = false)}>
          <div class="menu-link no-border" in:fly={{ y: "80%", duration: 800, delay: 500, easing: quartOut }}>
            <p class="background-letter">X</p>
            <span>Contact</span>
            <img src="/arrow_outward.svg" alt="arrow icon" />
          </div>
        </a>
      </div>

      <div class="second-grid" transition:fly={{ y: "-400%", duration: 1000, delay: 200, easing: quartOut }}>
        <div class="second-grid-link" in:fly={{ y: "80%", duration: 600, delay: 900, easing: quartOut }}>
          <p>
            <a href="mailto:office@office.com" on:click={() => (isOpen = false)}> Mail Us </a>
          </p>
          <img src="/arrow_outward.svg" alt="arrow icon" />
        </div>
        <div class="social">
          <a
            href="https://instagram.com"
            target="_blank"
            on:click={() => (isOpen = false)}
            in:fly={{ y: "80%", duration: 800, delay: 900, easing: quartOut }}
          >
            <img src="/instagram.svg" alt="instagram icon" />
          </a>
          <a
            href="https://linkedin.com"
            target="_blank"
            on:click={() => (isOpen = false)}
            in:fly={{ y: "80%", duration: 800, delay: 1000, easing: quartOut }}
          >
            <img src="/linkedin.svg" alt="linkedin icon" />
          </a>
          <button
            class="close-button"
            on:click={() => (isOpen = false)}
            in:fly={{ y: "80%", duration: 800, delay: 1100, easing: quartOut }}
          >
            x
          </button>
        </div>
      </div>
      <div class="menu-backdrop" on:click={() => (isOpen = false)} aria-hidden="true" transition:fade />
    </nav>
  {/if}
</header>

<style>
  header {
    position: relative;
    z-index: 3;
  }
  .main-menu {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-top: 1.5rem;
  }
  .second-menu {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 2rem;
    position: fixed;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%);
    height: 70px;
    padding: 5px;
    border-radius: 25px;
    margin: auto;
    z-index: 4;
    overflow: hidden;
  }
  .second-menu-overlay {
    backdrop-filter: blur(1rem);
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(223, 239, 255, 0.35);
    z-index: -1;
  }
  button {
    border: none;
    background-color: transparent;
    cursor: pointer;
  }
  .menu-button {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 50px;
    height: 50px;
    background-color: var(--yellow);
    border-radius: 50%;
    transition: all 0.6s ease-in-out;
  }
  .menu-button:hover {
    background-color: var(--grey);
  }
  .menu-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    backdrop-filter: blur(1.5rem);
    background-color: rgba(0, 0, 0, 0.6);
    z-index: 2;
    cursor: pointer;
  }
  .menu-grid {
    max-width: var(--max-width);
    margin: auto;
    position: fixed;
    top: 1.2rem;
    left: 1.2rem;
    right: 1.2rem;
    min-height: 25rem;
    background: var(--gradient);
    z-index: 4;
    border-radius: 1rem;
    opacity: 0.97;
    backdrop-filter: blur(2px);
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    overflow: hidden;
  }
  .second-grid {
    margin: auto;
    max-width: var(--max-width);
    position: fixed;
    top: calc(1.2rem + 25rem + 0.8rem);
    left: 1.2rem;
    right: 1.2rem;
    min-height: 5rem;
    background: var(--gradient);
    z-index: 4;
    border-radius: 1rem;
    opacity: 0.97;
    backdrop-filter: blur(2px);
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    overflow: hidden;
  }
  .second-grid-link {
    grid-column: 1 / span 3;
    border-right: 1px solid var(--black);
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    padding: 0 2rem 0;
    color: var(--black);
    font-weight: 400;
    font-size: 1.4rem;
    text-decoration: none;
    transition: all 0.6s ease-in-out;
    cursor: pointer;
  }
  .social {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    align-items: center;
    justify-content: center;
  }
  .social a {
    margin: auto;
    padding-top: 0.5rem;
  }
  .social a img {
    width: 1.5rem;
    height: 1.5rem;
  }
  .close-button {
    border: none;
    background-color: var(--bright-yellow);
    cursor: pointer;
    font-size: 2.4rem;
    font-weight: 400;
    color: var(--black);
    height: 100%;
  }
  .menu-link {
    position: relative;
    height: 100%;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    padding: 80% 2rem 0;
    color: var(--black);
    font-weight: 400;
    font-size: 1.8rem;
    text-decoration: none;
    border-right: 1px solid var(--black);
    transition: all 0.4s ease-in-out;
  }
  .no-border {
    border-right: none;
  }
  .menu-link:hover {
    opacity: 1;
    background-color: var(--yellow);
  }
  .menu-link img,
  .second-grid-link img {
    width: 2rem;
    height: 2rem;
    opacity: 0.8;
  }
  .background-letter {
    position: absolute;
    color: black;
    top: 1rem;
    left: 50%;
    transform: translateX(-50%);
    font-size: 15rem;
    font-weight: 700;
    opacity: 0.05;
    z-index: 2;
  }
</style>
