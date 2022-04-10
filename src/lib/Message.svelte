<script>
  export let content;
  export let date;
  export let author;
  export let reciever;
</script>

<div class="box {author === reciever ? 'send' : 'recieved'}">
  <!-- TODO: implement a different heading color for each author -->
  {#if author !== reciever}<span style="color: #fa6533; font-weight: 500;"
      >{author}</span
    >{/if}
  <p class="text">{@html content}</p>
  <div class="time-spacer">{date}</div>
  <div class="time">{date}</div>
  <div class="arrow">
    <svg viewBox="0 0 8 13" width="8" height="13" class="">
      <path
        fill="currentColor"
        d="M5.188 0H0v11.193l6.467-8.625C7.526 1.156 6.958 0 5.188 0z"
      />
    </svg>
  </div>
</div>

<style>
  .box {
    position: relative;
    padding: var(--single-padding);
    color: white;
    margin-bottom: var(--single-padding);
    max-width: 95%;
  }

  .send {
    background-color: var(--send-msg-color);
    align-self: flex-end;
    border-radius: var(--single-padding) 0px var(--single-padding)
      var(--single-padding);
  }

  .send .arrow {
    right: -8px;
    color: var(--send-msg-color);
  }

  .recieved {
    background-color: var(--recieved-msg-color);
    align-self: flex-start;
    border-radius: 0px var(--single-padding) var(--single-padding)
      var(--single-padding);
  }

  .recieved .arrow {
    color: var(--recieved-msg-color);
    left: -8px;
    transform: scaleX(-1);
  }

  .time {
    position: absolute;
    color: rgba(255, 255, 255, 0.6);
    font-size: 13px;
    right: var(--single-padding);
    bottom: var(--single-padding);
  }

  .arrow {
    position: absolute;
    top: 0;
    padding: 0;
  }

  .arrow svg {
    display: block;
  }

  .time-spacer {
    visibility: hidden;
    font-size: 13px;
    margin: 0px;
  }

  p {
    color: white;
    margin: 0;
  }
</style>
