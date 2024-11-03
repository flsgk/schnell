<script>
  import { onMount } from "svelte";
  import { words } from "../normalword.js";

  let randomWords = Array(50).fill(""); //50개의 빈 문자열로 초기화
  let matchedWord = new Set(); // 맞춘 단어를 누적해서 저장
  let answer = ""; //사용자가 입력할 단어를 저장할 변수
  let timer; // 타이머 변수
  let gameStarted = false;
  let gameOver = false; // 게암 종료 여부
  let timeLeft = 100; // 남은 시간 60초
  let congratsMessage = "";
  let congratsImage = "src/assets/2.gif";
  let remainWords = 50; // 남은 단어의 개수를 초기화
  let countdown = 5;

  const getRandomWords = () => {
    const selectWords = new Set(); //Set : 같은 값을 두 번 추가할 수 없음, 랜덤으로 다 다른 단어를 가져올 수 있도록
    while (selectWords.size < 50) {
      const randomIndex = Math.floor(Math.random() * words.length);
      selectWords.add(words[randomIndex]);
    }
    randomWords = Array.from(selectWords);
  };

  const startCountdown = () => {
    const interval = setInterval(() => {
      countdown--;
      if (countdown <= 0) {
        clearInterval(interval); // 카운트다운 타이머 종료
        gameStarted = true; // 게임 시작
        startGame(); // 게임 시작 함수 호출
      }
    }, 1000);
  };
  const startGame = () => {
    startTimer();
  };

  const checkAnswer = () => {
    if (gameOver) return; // 게임이 종료된 경우, 더 이상 동작하지 않음

    if (randomWords.includes(answer)) {
      matchedWord.add(answer); // 맞춘 단어를 Set에 추가
      randomWords = randomWords.filter((word) => word !== answer); // 정답 단어를 배열에서 삭제
      remainWords = randomWords.length;
      answer = ""; // 입력란 초기화

      if (randomWords.length === 0) {
        congratsMessage = "Clear! Congratulation!";

        gameOver = true;
        clearInterval(timer);
      }
    }
  };

  const startTimer = () => {
    // startTimer : setInterval 을 사용해서 1초마다 timeLeft를 시킴
    timer = setInterval(() => {
      if (timeLeft > 0) {
        timeLeft--;
      } else {
        // 잔여 시간이 0 이면 타이머를 중지시키고 gameOver을 true로 설정하여 게임 종료를 알린다.
        clearInterval(timer);
        gameOver = true;
      }
    }, 1000);
  };

  onMount(() => {
    getRandomWords(); // 컴포넌트가 마운트될 때 랜덤 단어 선택
    startCountdown();
  });
</script>

<header>
  <div class="title">SCHNELL</div>
  <div class="timer">Time Left : {timeLeft} seconds</div>
  <div class="status-bar"><p>Remaining Word : {remainWords}</p></div>
</header>

<main>
  <div class="board-row row-0">
    {#each randomWords.slice(0, 10) as word, index}
      <!-- randomWords 배열에서 10개씩 잘라서 #each 를 통해 각 블록에 넣는다. -->
      {#if !matchedWord.has(word)}
        <div class="board-block" data-index={index}>
          {word}
        </div>
      {/if}
    {/each}
  </div>

  <div class="board-row row-1">
    {#each randomWords.slice(10, 20) as word, index}
      {#if !matchedWord.has(word)}
        <div class="board-block" data-index={index + 10}>
          {word}
        </div>
      {/if}
    {/each}
  </div>

  <div class="board-row row-2">
    {#each randomWords.slice(20, 30) as word, index}
      {#if !matchedWord.has(word)}
        <div class="board-block" data-index={index + 20}>
          {word}
        </div>
      {/if}
    {/each}
  </div>

  <div class="board-row row-3">
    {#each randomWords.slice(30, 40) as word, index}
      {#if !matchedWord.has(word)}
        <div class="board-block" data-index={index + 30}>
          {word}
        </div>
      {/if}
    {/each}
  </div>

  <div class="board-row row-4">
    {#each randomWords.slice(40, 50) as word, index}
      {#if !matchedWord.has(word)}
        <div class="board-block" data-index={index + 40}>
          {word}
        </div>
      {/if}
    {/each}
  </div>

  {#if gameOver}
    {#if congratsMessage}
      <div class="congrats">
        <p>{congratsMessage}</p>
        <img src={congratsImage} alt="Congratulations!" />
      </div>
    {:else}
      <div class="game-over">⏰ Game Over! Time's up! ⏰</div>
    {/if}
  {:else}
    <div>
      <input
        type="text"
        class="input-answer"
        bind:value={answer}
        on:keydown={(e) => e.key === "Enter" && checkAnswer()}
        placeholder="Please enter a word"
        disabled={gameOver}
      />
      <!-- bind:value={answer} : 입력 필드 값과 answer을 양방향으로 바인딩, 실시간으로 answer 변수에 업데이트 해준다. -->
      <!-- on:keydown : 키를 누를 때마다 이벤트를 발생시킨다. -->
      <!-- {(e) => e.key === "Enter" && checkAnswer()} : Enter 키를 눌렀을 때만 checkAnswer() 함수를 호출한다. -->
    </div>
  {/if}

  {#if !gameStarted && countdown > 0}
    <div class="countdown">{countdown}</div>
  {/if}
</main>

<style>
  :root {
    background-color: black;
    color: white;
    font-family: "Jersey 10", sans-serif;
    font-weight: 400;
    font-style: normal;
  }

  header {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 40px;
  }

  .title {
    color: plum;
    font-size: 50px;
  }

  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }

  .board-row {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }

  .board-block {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 120px;
    height: 50px;
    border: none;
    border-radius: 10px;
    font-weight: bold;
    font-size: 24px;
    color: black;
    background-color: #fef0fc;
  }

  .input-answer {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 10px;
    width: 800px;
    height: 70px;
    border: none;
    border-radius: 10px;
    background-color: #fbbbea;
    text-align: center;
    font-family: "Jersey 10", sans-serif;
    font-weight: 400;
    font-style: normal;
    font-size: 40px;
  }

  ::placeholder {
    color: whitesmoke;
    font-family: "Jersey 10", sans-serif;
  }

  .timer {
    background-color: none;
    font-size: 30px;
  }

  .game-over {
    color: red;
    font-weight: bold;
    font-size: 25px;
    margin-top: 10px;
    animation: shake 0.3s ease-in-out 3;
    /* 반복하고 싶은 횟수를 infinite 대신 넣어주면 됨 */
  }

  .status-bar {
    font-size: 20px;
    text-align: center; /* 중앙 정렬 */
  }

  .countdown {
    font-size: 50px;
    color: red;
  }

  .congrats {
    text-align: center; /* 중앙 정렬 */
  }

  .congrats img {
    max-width: 100%; /* 이미지의 최대 너비를 100%로 설정하여 반응형으로 만듭니다. */
    height: auto; /* 높이는 자동으로 설정 */
  }

  @keyframes shake {
    0% {
      transform: translateX(0);
    }
    25% {
      transform: translateX(-5px);
    }
    50% {
      transform: translateX(5px);
    }
    75% {
      transform: translateX(-5px);
    }
    100% {
      transform: translateX(0);
    }
  }
</style>
