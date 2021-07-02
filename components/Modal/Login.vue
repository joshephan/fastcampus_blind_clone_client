<template>
  <div v-if="modal.login.show" class="modal-outside">
    <div id="login-modal">
      <div class="head">
        <h5>{{modal.login.directLogin ? "로그인": "블라인드 OTP 안전 인증"}}</h5>
        <a @click.prevent="$store.commit('modal/SET_LOGIN_MODAL_CLOSE')" class="close-btn">
          <img src="/icon/close.png" alt="닫기" />
        </a>
      </div>
      <div v-if="!modal.login.directLogin" class="body">
        <p>블라인드 앱의 마이페이지 > 블라인드 웹 로그인 메뉴에서 아래 생성된 일회용 인증코드 8자리를 입력하시면 웹에서도 모든 기능을 이용할 수 있습니다.</p>
        <div class="info">블라인드 OTP</div>
        <button class="otp-btn">U - 460 - 6051</button>
        <div class="left-time">남은 시간: {{displayTime}}</div>
      </div>
      <div v-else class="body">
        <div class="row">
          <label for="user-email">이메일</label>
          <input id="user-email" type="email" v-model="email" />
        </div>
        <div class="row">
          <label for="user-password">비밀번호</label>
          <input id="user-password" type="password" v-model="password" />
        </div>
        <button class="login-btn" @click="loginWithEmail">이메일로 로그인</button>
      </div>
      <div v-if="!modal.login.directLogin" class="foot">
        <a @click.prevent="$store.commit('modal/SET_LOGIN_MODAL_DIRECT_LOGIN')">블라인드에 처음이신가요?</a>
      </div>
    </div>
  </div>
</template>
<script>
import { mapState } from "vuex";
export default {
  computed: { ...mapState(["modal"]) },
  data() {
    return {
      leftTime: 180,
      displayTime: "3분",
      email: null,
      password: null
    };
  },
  watch: {
    "modal.login.show": function(to, from) {
      if (to !== from && to) {
        this.leftTime = 180;
        setInterval(() => {
          this.timeModifier();
        }, 1000);
      }
    }
  },
  methods: {
    async loginWithEmail() {
      const data = await this.$axios.$post(`http://localhost:3000/user/login`, {
        email: this.email,
        password: this.password
      });

      // 로그인 에러 캐칭
      if (data.error) {
        return;
      }

      this.$store.commit("user/SET_USER", {
        email: data.email,
        nickname: data.nickname,
        token: data.token
      });

      this.$store.commit("modal/SET_LOGIN_MODAL_CLOSE");
    },
    timeModifier() {
      this.leftTime -= 1;
      if (this.leftTime <= 0) {
        this.leftTime = 180;
        this.displayTime = `3분`;
      } else if (this.leftTime >= 120) {
        this.displayTime = `2분 ${this.leftTime - 120}초`;
      } else if (this.leftTime >= 60) {
        this.displayTime = `1분 ${this.leftTime - 60}초`;
      } else {
        this.displayTime = `${this.leftTime}초`;
      }
    }
  }
};
</script>
<style lang="scss" scoped>
#login-modal {
  background: white;
  width: 520px;
  .body {
    font-size: 16px;
    padding: 0 30px;
    line-height: 24px;
    p {
      padding: 20px 0;
      margin: 0;
    }
    .info {
      color: rgb(148, 150, 155);
      font-size: 14px;
      letter-spacing: -0.1px;
      margin: 20px 0 30px;
      line-height: 21px;
    }
    .row {
      margin: 20px 0;
      label {
        display: block;
      }
      input {
        width: 100%;
        box-sizing: border-box;
        padding: 12px;
      }
    }
    .otp-btn {
      display: flex;
      justify-content: center;
      align-items: center;
      background: rgb(55, 172, 201);
      border: none;
      color: white;
      font-size: 40px;
      font-weight: 400;
      width: 100%;
      height: 82px;
    }
    .login-btn {
      display: flex;
      justify-content: center;
      align-items: center;
      background: rgb(55, 172, 201);
      border: none;
      color: white;
      font-size: 24px;
      font-weight: 400;
      width: 100%;
      height: 64px;
      margin-bottom: 30px;
    }
    .left-time {
      text-align: center;
      color: rgb(55, 172, 201);
      font-size: 14px;
      font-weight: 700;
      margin-top: 16px;
    }
  }
  .foot {
    color: rgb(160, 160, 174);
    font-size: 14px;
    line-height: 17.5px;
    text-align: center;
    text-decoration: underline;
    padding: 30px;
  }
}
</style>
