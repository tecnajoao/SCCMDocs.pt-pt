---
title: "Como criar itens de configuração para Android para trabalho dispositivos geridos com o Intune"
ms.custom: na
ms.date: 2017-03-28
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: e6170339b8f3354c549579f127a5c3c618833943
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>Como criar itens de configuração para Android para trabalho dispositivos geridos com o Intune
  
 Utilizar o System Center Configuration Manager **Android para trabalhar** item de configuração para gerir as definições para Android para dispositivos de trabalho que são inscritos pelo Configuration Manager no Microsoft Intune ou gerido no local.  
  
### <a name="to-create-an-android-for-work-configuration-item"></a>Para criar o Android de item de configuração de trabalho  
  
1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade**.  
  
2.  Na área de trabalho **Ativos e Conformidade** , expanda **Definições de Conformidade**e, em seguida, clique em **Itens de Configuração**.  
  
3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4.  Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5.  Em **especifique o tipo de item de configuração que pretende criar**, selecione **Android para trabalhar**.  
  
6.  Clique em **categorias** se pode criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  
  
7.  Na página **Definições do Dispositivo** do assistente, selecione o grupo de definições que pretende configurar. veja **Referência de definições do item de configuração do Android e Samsung KNOX** neste tópico para detalhes e, em seguida, clique em **Seguinte**.  
  
    > [!TIP]  
    >  Se a definição pretendida não estiver listada, selecione a caixa de verificação **Configurar definições adicionais que não estejam incluídas nos grupos de predefinições**.  
  
9. Em cada página de definições, configure as definições de que necessita e se pretende resolvê-las quando não forem compatíveis com dispositivos (quando esta opção é suportada).  
  
10. Para cada grupo de definições, também pode configurar a gravidade que será comunicada quando um item de configuração não for compatível:  
  
    -   **Nenhum** -dispositivos que não obedeçam a esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  
  
    -   **Informações** -dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.  
  
    -   **Aviso** -dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.  
  
    -   **Crítico** -dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager.  
  
    -   **Crítico com evento** -dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos da aplicação.  
  
11. Na página **Aplicabilidade da Plataforma** do assistente, reveja as definições que não são compatíveis com as plataformas suportadas que selecionou anteriormente. Pode voltar atrás e remover estas definições ou pode continuar.  
  
    > [!TIP]  
    >  As definições não suportadas não são avaliadas em termos de compatibilidade.  
  
12. Conclua o assistente.  
  
 Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade** .  
  
##  <a name="android-for-work-configuration-item-settings-reference"></a>Android para referência de definições de item de configuração de trabalho  
  
### <a name="password"></a>Palavra-passe  
   
|Definição|Detalhes|  
|-------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos**|Exigir uma palavra-passe em dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|O comprimento mínimo da palavra-passe.|  
|**Expiração da palavra-passe em dias**|O número de dias antes de uma palavra-passe tem de ser alterado.|  
|**Número de palavras-passe memorizadas**|Impede a reutilização de palavras-passe.|  
|**Número de tentativas de início de sessão falhadas antes de o dispositivo ser apagado**|Apaga o dispositivo em caso de falha deste número de tentativas de início de sessão.|  
|**Tempo de inatividade antes do dispositivo está bloqueado**|Selecione o período de tempo até o dispositivo ser bloqueado quando este não está a ser utilizado.|
|**Qualidade da palavra-passe**|Selecionar o nível de complexidade da palavra-passe exigido e se podem ser utilizados dispositivos biométricos.|  
|**Permitir o bloqueio de smart card e outros agentes de fidedignidade**|Vamos controlar a funcionalidade Smart Lock em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como agentes de confiança, permite desativar ou ignorar a palavra-passe de bloqueio do ecrã do dispositivo se o dispositivo estiver numa localização fidedigna, como quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores finais configurem o Smart Lock.|
|**Impressão digital para desbloquear**||
  
###  <a name="work-profile"></a>Perfil de trabalho  
 Estas definições aplicam-se apenas a dispositivos Samsung KNOX.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Permitir que os dados entre o trabalho e perfis pessoais de partilha**|Escolha entre:<br>- **Não configurado**<br>- **Impedir a qualquer partilha através de limites**<br>- **As aplicações no perfil de trabalho podem processar o pedido a partir do perfil pessoal**<br>- **Sem restrições sobre como partilhar**<br>|  
|**Ocultar as notificações de perfil de trabalho quando o dispositivo está bloqueado (Android 6.0 +)**||
|**Definir a política de permissão de aplicação predefinida (Android 6.0 +)**|Escolha entre:<br>- **Não configurado**<br>- **Pedir sempre**<br>- **Conceder automática**<br>- **Negar automática**|
  
 
## <a name="see-also"></a>Consulte Também  
 [Itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
