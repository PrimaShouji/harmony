<script lang="ts">
  import MessageGroup from "./MessageGroup.svelte";
  import _ from "lodash";

  export let name: string;

  interface Message {
    userId: string;
    avatar: string;
    name: string;
    time: Date;
    message: string;
  }

  const messages: Message[] = [
    {
      userId: "382970947527454396",
      avatar:
        "https://cdn.discordapp.com/avatars/128581209109430272/acb5a845a8221b50e523a763c000765a.webp?size=40",
      name: "Name",
      time: new Date(1651343949442),
      message: "message",
    },
    {
      userId: "382970947527454396",
      avatar:
        "https://cdn.discordapp.com/avatars/128581209109430272/acb5a845a8221b50e523a763c000765a.webp?size=40",
      name: "Name",
      time: new Date(1651343949442),
      message: "message2",
    },
    {
      userId: "382970947527454396",
      avatar:
        "https://cdn.discordapp.com/avatars/128581209109430272/acb5a845a8221b50e523a763c000765a.webp?size=40",
      name: "Name",
      time: new Date(1651342949442),
      message: "message0",
    },
  ];

  function aggregateMessages(arr: Message[]) {
    const grouped = _.groupBy(arr, (m) => {
      const reducedDate = new Date(m.time);
      reducedDate.setMinutes(0);
      return m.userId + reducedDate.valueOf();
    });
    return _.sortBy(
      _.map(Object.keys(grouped), (k) =>
        _.reduce(
          grouped[k],
          (agg, next) => {
            agg.messages.push(next.message);
            return {
              avatar: next.avatar,
              name: next.name,
              time: next.time,
              messages: agg.messages,
            };
          },
          {
            avatar: "",
            name: "",
            time: new Date(),
            messages: [] as string[],
          }
        )
      ),
      (m) => m.time
    );
  }
</script>

<main>
  <h1>Hello, {name}!</h1>
  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
    how to build Svelte apps.
  </p>
</main>
<div>
  {#each aggregateMessages(messages) as m}
    <div class="message-group">
      <MessageGroup
        avatar={m.avatar}
        name={m.name}
        time={m.time}
        messages={m.messages}
      />
    </div>
  {/each}
</div>

<style>
  .message-group {
    margin-bottom: 16px;
  }

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
