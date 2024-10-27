<script>
  import { onMount } from "svelte"; // onMount 임포트

  onMount(() => {
    //Svelte에서 여러 요소에 이벤트 리스너를 추가할 때는 onMount 안에 모든 로직을 포함시키는 것이 좋음
    const signUp = document.querySelector(".signup-btn");
    const logIn = document.querySelector(".login-btn");

    const handleSignup = () => {
      window.location.href = "/#/signup";
    };

    const handleLogin = () => {
      window.location.href = "/#/login";
    };

    signUp.addEventListener("click", handleSignup);
    logIn.addEventListener("click", handleLogin);

    return () => {
      signUp.removeEventListener("click", handleSignup);
      logIn.removeEventListener("click", handleLogin);
    };
  });
</script>

<header>
  <div class="title"><h1>SCHNELL</h1></div>
  <div class="new-btn">
    <button class="signup-btn">회원가입</button>
    <button class="login-btn">로그인</button>
  </div>
</header>

<main>
  <div class="level-btn">
    <button class="hard-btn">상</button>
    <button class="normal-btn">중</button>
    <button class="easy-btn">하</button>
  </div>
</main>

<footer></footer>
