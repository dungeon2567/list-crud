<template>
  <div style="display: grid; grid-template-rows: auto auto auto auto; grid-gap: 10px;">
    <slot name="header">
      <span>{{plural.charAt(0).toUpperCase() + plural.slice(1)}}</span>
    </slot>
    <div class="list-container">
      <select multiple v-model="selected">
        <option v-for="item in value"
                v-bind:key="item"
                v-bind:value="item">
          {{item}}
        </option>
      </select>
    </div>
    <div>
      <input style="width: 100%;" v-model="nome" />
    </div>
    <div class="button-group">
      <button v-on:click="add" v-bind:disabled="nome.length === 0">Adicionar {{desc}}</button>
      <button v-on:click="remove" v-bind:disabled="selected.length === 0">Remover {{selected.length > 1 ? plural : desc}}</button>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'ListCrud',
    props: {
      value: {
        type: Array,
      },
      desc: {
        type: String,
        required: true
      },
      plural: {
        type: String,
        required: true,
      }
    },
    data() {
      return {
        selected: [],
        //nome do item da ser adicionado.
        nome: "",
      }
    },
    methods: {
      remove() {
        console.log(this.plural);

        if (this.selected) {
          this.selected.forEach(item => {
            this.value.splice(this.value.indexOf(item), 1);
          });

          this.selected = [];
        }
      },
      add() {
        if (this.nome) {
          var value = this.value;

          if (value === null) {
            value = [];

            value.push(this.nome);

            this.$emit('input', value);
          }
          else if (this.value.indexOf(this.nome) != -1) {
            alert(`${this.desc} já cadastrado.`);
          }
          else {
            value.push(this.nome);
          }

          this.nome = '';
        }
      }
    }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .list-container > select {
    width: 100%;
  }

  .button-group {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;
  }
</style>
