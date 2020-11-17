<template>
  <view class="header">
    <text class="texto"> Lista de Contatos</text>
    <button color="#841584" title="Acessar os contatos!!" :on-press="getContatos"></button>
    <text>{{errorMessage}}</text>
  </view>

</template>

<script>
  import React, {useState} from 'react';
  import * as Contacts from 'expo-contacts';
  import * as Permissions from "expo-permissions";
  export default{
    data(){
      return{
        errorMessage: "",
          contact: []
      }  
    },
    methods: {
      getContatos(){
      Permissions.askAsync(Permissions.CONTACTS)
        .then(status => {
          if (!status.granted) {
            this.errorMessage = "Acesso Negado";
          } else if (status.granted) {
              this.errorMessage = "FUNCIONOOOOU!!!";
              const { data } = Contacts.getContactsAsync({
                  fields: [Contacts.Fields.Emails],
              });

              if (data.length > 0) {
                  const contact = data[0];
                  console.log(contact);
              }
          }
        })
      }
    }
  }
</script>

<style>
  .header{
    background-color:#D8BFD8;
    align-items: center;
    flex: 1;
    justify-content: center;
  }
  .texto{
    color: black;
    font-size: 40px;
  }
  .contatos{
    background-color: #FFF0F5;
    flex-direction:column;
  }
</style>