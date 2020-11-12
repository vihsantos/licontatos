<template>
  <view class="header">
    <text class="texto">Lista de Contatos</text>
    <button title="Acesse a Lista de Contatos" :on-press="getContatos" />

    <text class="text-error">{{ errorMessage }}</text>
  </view>
</template>

<script>
  import React, { useState } from 'react';
  import { View, Text} from 'react-native'
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
        const [contacts] = useState([]);
        const status = await Permissions.getAsync(Permissions.CONTACTS)
        if (!status.granted){
            this.errorMessage="Acesso Negado"
        } else if (status.granted) {
            const { data } = await Contacts.getContactsAsync({
                fields: [Contact.Fields.FirstName],
            });
            if (data.length > 0) {
                contacts(data)
            }
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

</style>