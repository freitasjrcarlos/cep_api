<template>
  <div class="main">
    <form>
      <label for="cep"><span>Cep</span></label>
      <input id="cep" name="cep" type="text" v-model="cep" @keyup="fillCep" />
    </form>
    <div class="items" v-if="rua">
      <p><span>Rua:</span> {{ this.rua }}</p>
      <p><span>Bairro:</span> {{ this.bairro }}</p>
      <p><span>Cidade:</span> {{ this.cidade }}</p>
      <p><span>Estado:</span> {{ this.estado }}</p>
    </div>
  </div>
</template>

<script>
import { getCep } from "@/services.js";

export default {
  data() {
    return {
      cep: "",
      rua: "",
      bairro: "",
      cidade: "",
      estado: "",
    };
  },
  methods: {
    fillCep() {
      const cep = this.cep.replace(/\D/g, "");
      if (cep.length === 8) {
        getCep(cep).then((response) => {
          this.rua = response.data.logradouro;
          this.bairro = response.data.bairro;
          this.estado = response.data.uf;
          this.cidade = response.data.localidade;
        });
      }
    },
  },
};
</script>

<style scoped>
.main {
  width: 300px;
  border-radius: 5%;
  padding: 20px;
  margin: 0 auto;
  box-shadow: 0px 0px 32px 5px rgba(0, 0, 0, 0.75);
}
form {
  display: flex;
  justify-content: center;
  align-items: center;
}
label {
  padding: 10px;
}
input {
  padding: 10px;
  width: 60px;
}
span {
  font-weight: bold;
}
</style>
