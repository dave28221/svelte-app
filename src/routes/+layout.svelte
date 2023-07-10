<script>
    import "../app.css";
    import { onMount, onDestroy } from "svelte";
  
    let theCurrentTime = new Date();
  
    onMount(() => {
      const interval = setInterval(() => {
        theCurrentTime = new Date();
      }, 1000);
  
      onDestroy(() => {
        clearInterval(interval);
      });
    });
  </script>

<nav class="theNav">
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/sign-up">Sign Up</a>
    <p>the current time is : {theCurrentTime.toLocaleDateString()}</p>
</nav>

<slot />

<footer>
    <p>the Footer</p>
    <p class="theDate" />
</footer>

<style>
    /*global styles */

    .theNav {
        margin: 0 auto;
        display: flex;
        place-content: center;
        background-color: rgb(69, 66, 66);
    }
    .theNav a {
        padding: 20px;
        text-decoration: none;
        color: #ffffff;
        font-size: 17px;
        background-color: rgb(69, 66, 66);
    }

    .theNav a:hover {
        /* create animation here */
    }

    footer {
        background-color: rgb(69, 66, 66);
        height: 200px;
    }
</style>
