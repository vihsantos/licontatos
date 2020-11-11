<template>
  <view class="header">
    <text class="texto">Lista de Contatos</text>
    <button title="Acesse a Lista de Contatos" :on-press="getContatos" />
    <text class="lista" v-for="contacts in contact" :key="Contacts.Fields.FirstName">
        {{ Contacts.Fields.FirstName }}
    </text>
    <text class="text-error">{{ errorMessage }}</text>
  </view>
</template>

<script>
  import React from 'react';
  import { Text } from 'react-native'
  import * as Permissions from "expo-permissions";
  import * as Contacts from 'expo-contacts';
  export default {
    data: function () {
      return {
         message: "Hello World",
         errorMessage: "",
          contact: {}
      }
    },
    methods: {
      getContatos: async function () { 
        const status = await Permissions.getAsync(Permissions.CONTACTS)
        if (!status.granted){
            this.errorMessage="Acesso Negado"
        } else if (status.granted){
            const { data } = await Contacts.getContactsAsync({
            fields: [Contacts.Fields.FirstName],
            pageSize: 15
            });
            if (data.length > 0) {
                this.contact = data[0];
            }
        }
      }
    }
</script>

<style>
.header {
  background-color: #FFEFD5;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.texto {
  color: #B0E0E6;
  font-size: 35px;
}
.lista{
    color:aquamarine;
    padding: 2px;
}
</style>