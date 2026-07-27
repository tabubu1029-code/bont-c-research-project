---
title: "AI 研究助理 (BoNT/C Skill)"
permalink: /ai-assistant/
---

歡迎來到 BoNT/C AI 研究助理專區！請在右下角的對話框輸入你想分析的口袋編號，或進行抗體篩選。

<script src="https://sf-cdn.coze.com/obj/unpkg-va/flow-platform/chat-app-sdk/1.2.0-beta.6/libs/oversea/index.js"></script>
<script>
  new CozeWebSDK.WebChatClient({
    config: {
      bot_id: '7667081245704880133',
    },
    componentProps: {
      title: 'Coze',
    },
    auth: {
      type: 'token',
      token: 'pat_********',
      onRefreshToken: function () {
        return 'pat_********'
      }
    }
  });
</script>
