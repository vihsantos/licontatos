<template>
  <view class="container">
    <text class="text-color-primary">Lista de Contatos</text>
    <button title="Acesse a Lista de Contatos" :on-press="getLocation"/>
    <flat-list
      :data="contact"
      :render-item="(item) => renderList(item)"
    />
  </view>
</template>

<script>
  import React from 'react';
  import { Text } from 'react-native'
  import * as Permissions from "expo-permissions";
  import * as Contacts from 'expo-contacts';
  export default {
    data() {
      return {
        message: "Hello World",
        errorMessage: ""
      };
    },
    methods: {
       getLocation: function() {
         Permissions.askAsync(Permissions.CONTACTS)
          .then(status => {
             if (!status.granted) {
               this.errorMessage = "Acesso Negado";
             } else if (status.granted) {
                 const contact = Contacts.getContactsAsync({
                   fields: [Contacts.PHONE_NUMBERS],
                   pageXOffset:0
                 });
                 if (contact.total > 0) {
                     contact: contact.data
                 }
             }
          })
       },
       renderList: function (item){
           return (<Text>{item.contact}</Text>)
       }
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
