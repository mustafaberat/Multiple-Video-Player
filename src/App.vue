<template>
  <div id="app">
    <div class="login" v-if="!input.logedIn">
      <h1>Bilgiler:</h1>
      <input
        type="text"
        name="username"
        v-model="input.usernameIn"
        placeholder="Kullanici Adi"
      />
      <input type="password" name="password" v-model="input.passwordIn" />
      <button class="loginbtn" type="button" v-on:click="check()">
        Giris Yap
      </button>
    </div>

    <div class="videoYeri" v-if="input.logedIn">
      <h1>Yayin Gösterme Sayfası</h1>

      <div class="eklemeyeri">
        <input
          type="text"
          name="link"
          v-model="input.tempLink"
          placeholder="Yayin Linki"
        />
        <button v-on:click="ekle()">Ekle</button>
      </div>

      <div v-for="yayin in input.yayinlar" :key="yayin.link">
        <Video />
        <button v-on:click="sil()" class="kapatbtn">Kapat</button>
      </div>
    </div>
  </div>
</template>

<script>
import Video from "./components/Video.vue";

export default {
  name: "app",
  components: {
    Video,
  },
  data() {
    return {
      input: {
        logedIn: false,
        username: "admin",
        usernameIn: "",
        password: "admin",
        passwordIn: "",
        tempLink: "",
        yayinlarLimit: 4,
        yayinlar: [
          {
            video: "",
            link: "",
          },
        ],
      },
    };
  },
  methods: {
    check() {
      if (
        this.input.username == this.input.usernameIn &&
        this.input.password == this.input.passwordIn
      ) {
        this.input.logedIn = true;
      } else {
        alert("A username and password must be present");
      }
    },

    ekle() {
      if (this.input.yayinlar.length < this.input.yayinlarLimit) {
        this.input.yayinlar.push({
          video: this.input.tempLink,
          link: this.input.tempLink,
        });
      } else {
        alert("MAX LIMIT");
      }
    },

    sil() {
      if (this.input.yayinlar.length > 0) {
        this.input.yayinlar.shift();
      } else {
        alert("Silinecek video yok");
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.login {
  width: 500px;
  border: 1px solid #cccccc;
  background-color: #ffffff;
  margin: auto;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  align-items: center;
}

input,
button {
  margin: 5px;
  font-size: 22px;
  width: 80%;
  display: block;
  padding: 5px 10px;
  background: none;
  background-image: none;
  border: 1px solid #eee;
  color: #333;
  border-radius: 0;
  transition: border-color 0.25s ease, box-shadow 0.25s ease;
}
input:focus {
  outline: 0;
  border-color: #333;
}

button {
  background-color: #333;
  color: #fff;
  cursor: pointer;
}

.kapatbtn {
  margin-bottom: 40px;
  width: 100%;
}

.eklemeyeri {
  width: 80%;
  display: flex;
  text-align: center;
  align-items: center;
  justify-content: center;
  flex-direction: row;
}

.eklemeyeri button {
  width: 20%;
}
</style>
