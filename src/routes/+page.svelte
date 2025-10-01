<script>
  let text = $state();
  let title = $state();

  async function notify() {
    let permission = Notification.permission;
    if (permission !== 'granted') {
      permission = await Notification.requestPermission();
    }
    if (permission === 'granted') {
      new Notification(`${title}`, {
        body: `${text}`,
        icon: "/icon.png"
      });
    }
  }
</script>
<div class="min-h-screen flex items-center justify-center bg-gray-100 p-4">
  <div class="w-full max-w-xl">
    <input  bind:value={title}  type="text" class="border p-2 w-full mb-4"/>
    <textarea bind:value={text} class="border p-2 w-full mb-4 h-32"></textarea>
    <button onclick={notify} class="bg-blue-500 text-white px-4 py-2">Benachrichtigung senden</button>
  </div>
</div>
