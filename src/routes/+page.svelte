<script  lang="ts">
    import { onMount } from "svelte";
    import * as Accordion from "$lib/components/ui/accordion/index.js";

    let message = $state("Loading...");
    let name = $state("");
    function hello() {
        console.log("hello")
        fetch("/api/my/form/hello", {
            method: "POST",
            body: JSON.stringify({ name: name  }),
            headers: {
                "Content-Type": "application/json"
            }
        }).then((response) => response.json()).then((data) => {
            message = data.message
            name = ""
        });
    }
    onMount(hello)

</script>
<h1>{message}</h1>
<form>
<input type="input" bind:value={name} placeholder="Enter your name A" />
<button onclick={hello}>Send</button>
<Accordion.Root type="single">
  <Accordion.Item value="item-1">
    <Accordion.Trigger>Is it accessible?</Accordion.Trigger>
    <Accordion.Content>
      Yes. It adheres to the WAI-ARIA design pattern.
    </Accordion.Content>
  </Accordion.Item>
</Accordion.Root>
</form>