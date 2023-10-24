<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<div>
    {#each messages as message}
    <p>{message.author}: {message.message}</p>
    {/each}
</div>
<script lang="ts">
    import { Socket, io } from "socket.io-client"; 
    type Message = {
        author: string,
        message: string,
        server: {
            online: number,
            userList: string[]
        }
    }
    const socket = io("sockets.hosted.coasterfan5.com");
    let messages: Message[] = []
    socket.on("message", (message) => {
        messages = [...messages, message]
    })
    let message = '';
    function submit() {
        socket.emit("setName", "Daniel");
        socket.emit("message", message);
        message = '';
    }
</script>
<input bind:value={message} />
<button on:click={submit}>Submit</button>
