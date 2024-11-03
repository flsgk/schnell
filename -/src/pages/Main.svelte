<script>
  import { onMount } from "svelte"; // onMount 임포트

  onMount(() => {
    //Svelte에서 여러 요소에 이벤트 리스너를 추가할 때는 onMount 안에 모든 로직을 포함시키는 것이 좋음
    const signUp = document.querySelector(".signup-btn");
    const logIn = document.querySelector(".login-btn");
    const playHard = document.querySelector(".hard-btn");
    const playNormal = document.querySelector(".normal-btn");
    const playEasy = document.querySelector(".easy-btn");

    const handleSignup = () => {
      window.location.href = "/#/signup";
    };
    const handleLogin = () => {
      window.location.href = "/#/login";
    };
    const handleHard = () => {
      window.location.href = "/#/playhard";
    };
    const handleNormal = () => {
      window.location.href = "/#/playnormal";
    };
    const handleEasy = () => {
      window.location.href = "/#/playeasy";
    };

    signUp.addEventListener("click", handleSignup);
    logIn.addEventListener("click", handleLogin);
    playHard.addEventListener("click", handleHard);
    playNormal.addEventListener("click", handleNormal);
    playEasy.addEventListener("click", handleEasy);

    return () => {
      signUp.removeEventListener("click", handleSignup);
      logIn.removeEventListener("click", handleLogin);
      playHard.removeEventListener("click", handleHard);
      playNormal.removeEventListener("click", handleNormal);
      playEasy.removeEventListener("click", handleEasy);
    };
  });
</script>

<div class="button-container">
  <header>
    <div class="title">✨ SCHNELL ✨</div>
    <div class="new-btn">
      <button class="signup-btn">Signup</button>
      <button class="login-btn">Log in</button>
    </div>
  </header>

  <main>
    <div class="level-btn">
      <div class="level">Select level</div>
      <button class="hard-btn">HARD</button>
      <button class="normal-btn">NORMAL</button>
      <button class="easy-btn">EASY</button>
    </div>
  </main>

  <img src="src/assets/_.gif" alt="" />
</div>

<style>
  :root {
    font-family: "Jersey 10", sans-serif;
    font-weight: 400;
    font-style: normal;
    font-size: 20px;
  }

  .button-container {
    display: flex;
    flex-direction: column; /* 수직 방향으로 배치 */
    align-items: center; /* 수평 중앙 정렬 */
    justify-content: center; /* 수직 중앙 정렬 */
    height: 100vh; /* 화면 전체 높이 사용 */
    width: 100%; /* 전체 너비 사용 */
  }

  .title {
    font-size: 50px;
    margin-bottom: 20px;
  }

  .signup-btn {
    border: none;
    font-family: "Jersey 10", sans-serif;
    font-weight: 400;
    font-style: normal;
    font-size: 30px;
    width: 100px;
    height: 50px;
    border-radius: 10px;
    background-color: palevioletred;
    cursor: pointer;
  }

  .login-btn {
    border: none;
    font-family: "Jersey 10", sans-serif;
    font-weight: 400;
    font-style: normal;
    font-size: 30px;
    width: 100px;
    height: 50px;
    border-radius: 10px;
    background-color: palevioletred;
    cursor: pointer;
  }

  .level-btn {
    margin-top: 40px;
    display: flex; /* 수평으로 배치 */
    gap: 20px; /* 버튼 간격 설정 */
  }

  .hard-btn {
    border: none;
    border-radius: 10px;
    font-family: "Jersey 10", sans-serif;
    font-weight: 400;
    font-style: normal;
    font-size: 30px;
    background-color: rgb(248, 210, 216);
    width: 200px;
    height: 50px;
  }

  .normal-btn {
    border: none;
    border-radius: 10px;
    font-family: "Jersey 10", sans-serif;
    font-weight: 400;
    font-style: normal;
    font-size: 30px;
    background-color: rgb(248, 210, 216);
    width: 200px;
    height: 50px;
  }

  .easy-btn {
    border: none;
    border-radius: 10px;
    font-family: "Jersey 10", sans-serif;
    font-weight: 400;
    font-style: normal;
    font-size: 30px;
    background-color: rgb(248, 210, 216);
    width: 200px;
    height: 50px;
  }

  img {
    width: 100px;
    height: 100px;
  }
</style>
