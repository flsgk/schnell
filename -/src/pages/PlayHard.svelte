<script>
  import { onMount } from "svelte";
  import { words } from "../word.js";

  let randomWords = Array(50).fill(""); //50개의 빈 문자열로 초기화
  let matchedWord = new Set(); // 맞춘 단어를 누적해서 저장
  let answer = ""; //사용자가 입력할 단어를 저장할 변수

  const getRandomWords = () => {
    const selectWords = new Set(); //Set : 같은 값을 두 번 추가할 수 없음, 랜덤으로 다 다른 단어를 가져올 수 있도록
    while (selectWords.size < 50) {
      const randomIndex = Math.floor(Math.random() * words.length);
      selectWords.add(words[randomIndex]);
    }
    randomWords = Array.from(selectWords);
  };

  const checkAnswer = () => {
    if (randomWords.includes(answer)) {
      matchedWord.add(answer); // 맞춘 단어를 Set에 추가
      randomWords = randomWords.filter((word) => word !== answer); // 정답 단어를 배열에서 삭제
      answer = ""; // 입력란 초기화
    }
  };

  onMount(() => {
    getRandomWords(); // 컴포넌트가 마운트될 때 랜덤 단어 선택
  });
</script>

<header>
  <div><h2>SCHNELL</h2></div>
  <div>Timer</div>
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

  <div>
    <input
      type="text"
      class="input-answer"
      bind:value={answer}
      on:keydown={(e) => e.key === "Enter" && checkAnswer()}
      placeholder="단어를 입력하세요."
    />
    <!-- bind:value={answer} : 입력 필드 값과 answer을 양방향으로 바인딩, 실시간으로 answer 변수에 업데이트 해준다. -->
    <!-- on:keydown : 키를 누를 때마다 이벤트를 발생시킨다. -->
    <!-- {(e) => e.key === "Enter" && checkAnswer()} : Enter 키를 눌렀을 때만 checkAnswer() 함수를 호출한다. -->
  </div>
</main>

<style>
  :root {
    background-color: black;
    color: white;
  }

  header {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
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
    width: 100px;
    height: 50px;
    border: none;
    border-radius: 10px;
    font-weight: bold;
    color: black;
    background-color: #fef0fc;
  }

  .input-answer {
    margin-top: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 800px;
    height: 70px;
    border: none;
    border-radius: 10px;
    font-weight: bold;
    background-color: #fbbbea;
    text-align: center;
    font-size: 20px;
  }

  ::placeholder {
    color: whitesmoke;
    font-style: italic;
    font-size: 20px;
  }
</style>
