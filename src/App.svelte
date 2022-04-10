<script>
  import "./global.css";
  import Message from "./lib/Message.svelte";
  import MessageContainer from "./lib/MessageContainer.svelte";
  import JSZip from "jszip";

  let txt = "";
  let fileInput;

  function passDownClick(e) {
    fileInput.click();
  }

  // const objectURL = window.URL.createObjectURL(selectedFile);
  // URL.revokeObjectURL(this.varName);

  function handleFile(data) {
    const selectedFile = this.files[0];
    const zip = new JSZip();
    zip.loadAsync(selectedFile).then(function (zip) {
      zip
        .file("_chat.txt")
        .async("string")
        .then((v) => {
          txt = v;
        }); // TODO: save the folder to storage and replace component
    });
  }
</script>

<input
  bind:this={fileInput}
  type="file"
  id="file"
  name="file"
  accept="application/x-zip-compressed"
  style="display:none"
  on:change={handleFile}
/>
<button id="fileSelect" on:click={passDownClick}>Select some files</button>

<MessageContainer reciever="Felix Krückel" bind:txt />
