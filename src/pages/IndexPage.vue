<template>
  <q-page class="">
    <div class="row" style="display: flex; justify-content: center; align-items: center; height: 50vh">
      <div class="text-h3">
        <q-icon name="school" size="70px" class="text-bold text-grey-9" />
        <span class="text-bold text-grey-9">Knowledge</span>
        <span class="text-bold text-blue-10">Base</span>
      </div>
    </div>
    <div class="row flex flex-center q-gutter-md">
      <q-input outlined dense v-model="userName" label="Utilizador" />
      <q-select outlined style="width: 200px;" map-options dense v-model="operationId" :options="arrayOfOperation"
        label="Operação" option-label="descricao" option-value="idOperacao" emit-value />
      <q-btn label="Reiniciar" icon="refresh" color="primary" @click="refresh()" />

    </div>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Smooch from 'smooch';

import { useQuasar } from "quasar";
defineOptions({
  name: "IndexPage",
});
const $q = useQuasar()
const userName = ref("assistente");
const operationId = ref(27);
const arrayOfOperation = [
  {
    idOperacao: 1,
    descricao: "TAAG",
    isActivo: true,
  },
  {
    idOperacao: 2,
    descricao: "Unitel",
    isActivo: true,
  },
  {
    idOperacao: 3,
    descricao: "Nossa Seguros",
    isActivo: true,
  },
  {
    idOperacao: 4,
    descricao: "BFA",
    isActivo: true,
  },
  {
    idOperacao: 5,
    descricao: "UmbiUmbi",
    isActivo: true,
  },
  {
    idOperacao: 8,
    descricao: "CFAO Mobility",
    isActivo: true,
  },
  {
    idOperacao: 9,
    descricao: "Pumangol",
    isActivo: true,
  },
  {
    idOperacao: 10,
    descricao: "Partilhados",
    isActivo: true,
  },
  {
    idOperacao: 11,
    descricao: "Academia BAI",
    isActivo: true,
  },
  {
    idOperacao: 12,
    descricao: "ENBI",
    isActivo: true,
  },
  {
    idOperacao: 13,
    descricao: "Mais Saúde",
    isActivo: true,
  },
  {
    idOperacao: 14,
    descricao: "Mais Saúde Talatona",
    isActivo: true,
  },
  {
    idOperacao: 15,
    descricao: "Uni1",
    isActivo: true,
  },
  {
    idOperacao: 16,
    descricao: "BIC",
    isActivo: true,
  },
  {
    idOperacao: 17,
    descricao: "BPC",
    isActivo: true,
  },
  {
    idOperacao: 18,
    descricao: "BIC Seguros",
    isActivo: true,
  },
  {
    idOperacao: 19,
    descricao: "Aliança Seguros",
    isActivo: true,
  },
  {
    idOperacao: 20,
    descricao: "BFA Capital Markets",
    isActivo: true,
  },
  {
    idOperacao: 21,
    descricao: "Áurea SDVM",
    isActivo: true,
  },
  {
    idOperacao: 22,
    descricao: "Taag Supervisão",
    isActivo: true,
  },
  {
    idOperacao: 23,
    descricao: "Aurea SDVM",
    isActivo: true,
  },
  {
    idOperacao: 24,
    descricao: "BFA - Capital Markets",
    isActivo: true,
  },
  {
    idOperacao: 25,
    descricao: "Duzinda Van-dunem",
    isActivo: true,
  },
  {
    idOperacao: 26,
    descricao: "ÁUREA",
    isActivo: true,
  },
  {
    idOperacao: 27,
    descricao: "Centro-Vita",
    isActivo: true,
  },
  {
    idOperacao: 28,
    descricao: "Sonangol",
    isActivo: true,
  },
];

const refresh = () => {

  // window.location.reload()
  localStorage.clear()
  sessionStorage.clear()
  indexedDB.deleteDatabase('smooch')
  Smooch.destroy();
  initSmooch(userName.value, operationId.value);
  $q.notify({
    message: 'Reiniciado com sucesso',
    color: 'positive',
    icon: 'check',
    position: 'top',
    timeout: 2000
  })


};
const initSmooch = (userName, operationId) => {
  const delegate = {
    beforeSend(message, data) {
      message.metadata = {
        ...message.metadata,
        userName,
        operationId,
      };
      return message;
    },
  };
  Smooch.init({
    delegate,
    integrationId: "67f68f0bbef82389185b4a27",
    menuItems: {
      imageUpload: false,
      fileUpload: false,
      shareLocation: false,
    },

    customText: {
      syncConversation: "Sincronizar conversa",
      linkChannelPageHeader: "Sincronizar sua conversa",
      connectNotificationText:
        "Sincronize sua conversa e continue a enviar-nos mensagens através do seu aplicativo favorito.",
      viberChannelDescription:
        "Conecte sua conta do Viber para ser notificado quando receber uma resposta e continue a conversa no Viber. Para começar, digitalize o código QR usando o aplicativo Viber.",
      telegramChannelDescription:
        "Conecte sua conta do Telegram para ser notificado quando receber uma resposta e continuar a conversa no Telegram",
      messengerChannelDescription:
        "Conecte sua conta do Facebook Messenger para ser notificado quando receber uma resposta e continue a conversa no Facebook Messenger.",
      smsSendText: "Send me a text",
      smsStartTexting: "Start Texting",
      //Labels da caixa de envio
      headerText: "Posso ajudar?",
      inputPlaceholder: "Digite a mensagem...",
      sendButtonText: "Enviar",
      //Labels de Tempo
      conversationListTimestampFormat: "D/MM/YYYY",
      conversationTimestampHeaderFormat: "D/MM/YYYY, HH:MM",
      conversationListHeaderText: "Minhas Conversas",
      conversationListRelativeTimeJustNow: "Agora Mesmo!",
      conversationListPreviewUserText: "Você",
      conversationListRelativeTimeMinute: "1 minutos atrás",
      conversationListRelativeTimeMinutes: "{value} minutos atrás",
      conversationListRelativeTimeHour: "1 hora atrás",
      conversationListRelativeTimeHours: "{value} horas atrás",
      conversationListRelativeTimeYesterday: "Ontem",
      messageIndicatorTitlePlural: "({count}) Novas mensagens",
      messageIndicatorTitleSingular: "({count}) Nova mensagem",
      messageRelativeTimeDay: "{value}d atrás",
      messageRelativeTimeHour: "{value}h atrás",
      messageRelativeTimeJustNow: "Agora Mesmo!",
      messageRelativeTimeMinute: "{value}m atrás",
      messageTimestampFormat: "HH:MM",
      messageDelivered: "Entregue",
      messageSeen: "Visto",
      messageSending: "Enviando ...",
      newConversationButtonText: "Nova Conversa",
    },
    /* customColors: {
        brandColor: '65758e',
        conversationColor: '65758e',
        actionColor: '65758e',
    }, */
  });
};
onMounted(() => {
  initSmooch(userName.value, operationId.value);
});
</script>
