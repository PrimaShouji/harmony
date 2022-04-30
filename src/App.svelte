<script lang="ts">
  import MessageGroup from "./MessageGroup.svelte";

  export let name: string;

  const messages = [
    {
      avatar:
        "https://cdn.discordapp.com/avatars/128581209109430272/acb5a845a8221b50e523a763c000765a.webp?size=40",
      name: "Name",
      time: new Date(),
      message: "message",
    },
  ];
</script>

<main>
  <h1>Hello, {name}!</h1>
  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
    how to build Svelte apps.
  </p>
</main>
<div>
  {#each messages as m}
    <MessageGroup
      avatar={m.avatar}
      name={m.name}
      time={m.time}
      messages={[m.message]}
    />
  {/each}
</div>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
