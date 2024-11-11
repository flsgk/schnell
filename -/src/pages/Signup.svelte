<form id="signup-form" action="/signup" method="post">
  <!-- /signup 은 폼이 전송될 서버의 엔드포인트
    이 경로에 있는 서버가 폼 데이터를 처리하도록 설정하는 것 -->
  <div><h1>회원가입</h1></div>

  <div>
    <label for="id">아이디</label>
    <input type="text" name="id" id="id" required />
  </div>
  <div>
    <label for="password">비밀번호</label>
    <input type="password" name="password" id="password" required />
  </div>
  <div>
    <label for="password-check">비밀번호 확인</label>
    <input type="password" name="password-check" id="password-check" required />
  </div>
  <div>
    <label for="name">이름</label>
    <input type="text" name="name" id="name" required />
  </div>
  <div>
    <label for="email">이메일</label>
    <input type="email" name="email" id="email" required />
  </div>

  <div>
    <button type="submit">회원가입</button>
  </div>
</form>

<style>
  form {
    display: flex;
    flex-direction: column;
    text-align: left;
    gap: 10px;
  }

  label {
    font-size: 15px;
  }

  input[type="text"] {
    border-radius: 15px;
    width: 150px;
    height: 30px;
  }

  input[type="password"] {
    border-radius: 15px;
    width: 150px;
    height: 30px;
  }

  input[type="email"] {
    border-radius: 15px;
    width: 150px;
    height: 30px;
  }

  button {
    background-color: pink;
    border: none;
    border-radius: 15px;
    width: 100px;
    height: 40px;
    font-size: 18px;
    font-weight: bold;
  }
</style>
