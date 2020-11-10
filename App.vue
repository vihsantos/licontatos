<template>
  <view class="container">
    <text class="text-color-primary">Lista de Contatos</text>
    <button title="Acesse a Lista de Contatos" :on-press="getContatos"/>
    <text>{{this.contact}}</text> 
    <text class="text-error">{{ errorMessage }}</text>
  </view>
</template>

<script>
  import React from 'react';
  import { Text } from 'react-native'
  import * as Permissions from "expo-permissions";
  import * as Contacts from 'expo-contacts';
  export default {
    state(){
       
    },
    data() {
      return {
        message: "Hello World",
        errorMessage: "",
        contact: {}
      };
    },
    methods: {
       getContatos: function() {
         Permissions.askAsync(Permissions.CONTACTS)
          .then(status => {
             if (!status.granted) {
               this.errorMessage = "Acesso Negado";
             } else if (status.granted) {
                 const { data } = Contacts.getContactsAsync({
                     fields: [Contacts.Fields.FirstName],
                 });
                 this.contact = data;
                 this.errorMessage = "Funcionou!!";
             }
          })
       },
    }
  };
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
  font-size: 30px;
}
</style>