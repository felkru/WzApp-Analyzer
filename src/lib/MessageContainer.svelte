<script>
  import Message from "./Message.svelte";

  export let reciever;

  // TODO: Make txt property required, remove default value
  export let txt;

  function parseTxtToJson(txt) {
    let chunks = txt.split(/^\[(\d\d\.\d\d\.\d\d, \d\d\:\d\d\:\d\d)\](.*?):/m);
    let data = [];
    for (let i = 3; i < chunks.length; i += 3) {
      const date = chunks[i - 2];
      const author = chunks[i - 1].trim();
      let content = chunks[i].trim();
      let msgType = "Text";
      if (content === "Bild weggelassen") {
        msgType = "Image";
        content = "";
      }
      data.push({
        date,
        author,
        content,
        msgType,
      });
    }
    console.log(data);
    return data;
  }

  $: data = parseTxtToJson(txt);
</script>

<div class="flex-container">
  {#each data as { date, author, content, msgType }}
    {#if msgType === "Image"}
      <Message
        content="<img src='svelte.png' alt='default image'>"
        {date}
        {author}
        {reciever}
      />
    {:else}
      <Message {content} {date} {author} {reciever} />
    {/if}
  {/each}
</div>

<style>
  .flex-container {
    display: flex;
    flex-direction: column;
  }
</style>
