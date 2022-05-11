<script>
  import {browser} from "$app/env";

  let counter;
  let increment;
  let decrement;

  if(browser) {
    const socket = new WebSocket("wss://ktor-todo-backend-stream.herokuapp.com/")

    socket.onopen = function (_) {
      console.log("connected to server")
    };

    socket.onmessage = (event) => {
        console.log(event.data)
        counter = JSON.parse(event.data).count
    }

    increment = () => socket.send("increment")
    decrement = () => socket.send("decrement")
  }

</script>

<h1>Counter : {counter ?? "Loading..."}</h1>
<button on:click={increment}>
    INCREMENT
</button>
<button on:click={decrement}>
    DECREMENT
</button>
