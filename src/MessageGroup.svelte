<script lang="ts">
  export let avatar: string;
  export let name: string;
  export let time: Date;
  export let messages: string[];
</script>

<div class="message-group">
  <img src={avatar} alt="profile" />
  <div>
    <p class="name">{name}<span class="time">{time.toLocaleString()}</span></p>
    {#each messages as m}
      <p class="content">{m}</p>
    {/each}
  </div>
</div>

<style>
  .message-group {
    display: flex;
    text-align: left;
  }

  img {
    width: 40px;
    height: 40px;
    margin-top: 4px;
    margin-right: 8px;
  }

  .name {
    margin: 0;
    vertical-align: top;
    font-weight: 600;
  }

  .time {
    margin-left: 8px;
    font-size: 10pt;
    font-weight: 400;
  }

  .content {
    margin: 0;
    padding-top: 4px;
  }
</style>
