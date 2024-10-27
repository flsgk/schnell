<!-- javascript 를 작성하는 부분 -->
<script>
  import Login from "./pages/Login.svelte";
  import Main from "./pages/Main.svelte";
  import NotFound from "./pages/NotFound.svelte";
  import Signup from "./pages/Signup.svelte";
  import Router from "svelte-spa-router";
  import PlayHard from "./pages/PlayHard.svelte";
  import "./CSS/main.css";

  const routes = {
    "/": Main,
    "/playhard": PlayHard,
    "/login": Login,
    "/signup": Signup,
    "/*": NotFound,
  };
</script>

<Router {routes}></Router>
<!-- Router 라는 컴포넌트에 routes 라는 속성을 전달하여 특정 URL 경로와 해당 컴포넌트를 연결해주는 역할을 한다. -->

<!-- html을 작성하는 부분 -->
<main></main>

<!-- CSS 를 작성하는 부분 -->
<style>
</style>
