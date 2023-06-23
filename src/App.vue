<template>
  <div>
    <button @click="openPopup('caça-níquel')">Abrir Pop-up Caça-níquel</button>
    <button @click="openPopup('vídeo')">Abrir Pop-up de Vídeo</button>

    <div v-if="showPopup">
      <div class="popup">
        <h2>{{ popupData.title }}</h2>
        <h3>{{ popupData.subtitle }}</h3>

        <div v-if="popupType === 'caça-níquel'">
        <img src="@/assets/caca-niquel.png" width="300" height="200" alt="Descrição da imagem">

          <!-- Conteúdo do jogo caça-níquel -->
          <h2>{{ popupData.content}}</h2>
        </div>

        <div v-if="popupType === 'vídeo'">
          <!-- Reprodutor de vídeo -->
          <video :src="popupData.content" controls></video>
        </div>

        <form>
          <div v-for="(field, index) in popupData.formFields" :key="index">
            <label :for="field">{{ field }}</label>
            <input :type="field" :id="field" />
          </div>

          <div v-if="popupData.consentCheckbox">
            <label for="consentCheckbox">
              <input type="checkbox" id="consentCheckbox" />
              Consentimento para coleta de dados
            </label>
          </div>

          <button>Enviar</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import popupData from "./popupData.json";

export default {
  name: "App",
  data() {
    return {
      showPopup: false,
      popupType: "",
      popupData: {}
    };
  },
  methods: {
    openPopup(type) {
      this.showPopup = true;
      this.popupType = type;
      this.popupData = popupData[type];
    }
  }
};
</script>

<style scoped>
.popup {
  position:fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 400px;
  padding: 20px;
  background-color: #ffff;
  border: 2px solid #000000;
}




</style>

