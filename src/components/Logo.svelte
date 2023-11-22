<script>
  export let size = 1
  $: width = size * 128
  $: font = size * 4
  $: margin = size * 1.5
</script>

<div class="logo">
  <svg style:width height="108" viewBox="0 0 128 108" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path
      d="M50.2 107C50.9 107.1 51.6 107.2 52.3 107.2C63.2 102.3 72.5 94.3 78.9 83.9C85.2 73.8 88.2 62.4 88 50.8L76.1 38.9C81 64.1 71.4 90.8 50.2 107Z"
      fill="#C0C2C3"
    />
    <path d="M46 106.4C46.1 106.4 46.2 106.4 46.3 106.5C69 90.3 78.8 61.9 72.4 35.9L55.4 18.9C69 46.7 66.3 80.9 46 106.4Z" fill="#C0C2C3" />
    <path
      d="M103.6 64.8C100.7 77.8 93.8 89.5 83.6 98.3C80.6 100.9 77.4 103.2 74.1 105.1C90.8 100.2 104.3 87.7 110.5 71.6L103.6 64.8Z"
      fill="#C0C2C3"
    />
    <path
      d="M100.9 62.9L91.1 53.1C90.9 64.3 87.8 75.3 81.7 85.1C75.8 94.7 67.6 102.3 57.9 107.4C60.1 107.4 62.3 107.3 64.5 107C82.9 99.5 96.9 83.1 100.9 62.9Z"
      fill="#C0C2C3"
    />
    <path d="M47.4 11.7L35.7 0C14.9 8 0 28.3 0 51.8C0 77.8 18.1 99.7 42.2 105.7C64.8 78.4 66 40.2 47.4 11.7Z" fill="#E8E221" />
    <path d="M128 61.1C128 30.5 103 5.5 72.4 5.5C65.4 5.5 58.7 6.8 52.5 9.2L124.2 80.9C126.7 74.8 128 68.1 128 61.1Z" fill="#76CC3E" />
  </svg>
  <p style:font-size={`${font}rem`} style:margin-left={`${margin}rem`}>CLSX</p>
</div>

<style>
  .logo {
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }
  p {
    font-size: 3.5rem;
    font-weight: 700;
    margin-left: 1.5rem;
    color: var(--dark-grey);
  }
</style>
