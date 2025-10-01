<script>
  let title = $state('');
  let message = $state('');

  async function sendNotification() {
    if (!("Notification" in window)) {
      alert("Browser unterstützt keine Notifications.");
      return;
    }

    let permission = Notification.permission;
    if (permission !== "granted") {
      permission = await Notification.requestPermission();
    }
    if (permission !== "granted") {
      alert("Keine Berechtigung für Notifications.");
      return;
    }
    new Notification(title || "Benachrichtigung", {
      body: message || "Keine Nachricht angegeben."
    });
  }
</script>

<main class="max-w-md mx-auto mt-12 p-6 bg-white shadow-lg rounded-2xl space-y-4">
  <h1 class="text-2xl font-bold text-center">Notification Übung</h1>

  <div>
    <label for="title" class="block text-sm font-medium mb-1">Title</label>
    <input
      id="title"
      type="text"
      bind:value={title}
      placeholder="Titel eingeben"
      class="w-full rounded-lg border border-gray-300 px-3 py-2 focus:ring-2 focus:ring-blue-500 focus:outline-none"
    />
  </div>

  <div>
    <label for="message" class="block text-sm font-medium mb-1">Message</label>
    <textarea
      id="message"
      bind:value={message}
      placeholder="Nachricht eingeben"
      class="w-full rounded-lg border border-gray-300 px-3 py-2 min-h-[100px] focus:ring-2 focus:ring-blue-500 focus:outline-none"
    ></textarea>
  </div>

  <button
    on:click={sendNotification}
    class="w-full bg-blue-600 text-white py-2 rounded-lg font-semibold hover:bg-blue-700 transition-colors"
  >
    Send
  </button>
</main>
