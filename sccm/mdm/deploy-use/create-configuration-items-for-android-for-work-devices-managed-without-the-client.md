---
title: Como criar itens de configuração para Android para dispositivos de trabalho geridos com o Intune
titleSuffix: Configuration Manager
ms.date: 2017-07-31
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
author: aczechowski
ms.author: aaroncz
ms.openlocfilehash: ba70e4d3a87f2a305312449907730174c62c4775
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>Como criar itens de configuração para Android para dispositivos de trabalho geridos com o Intune

 Utilizar o System Center Configuration Manager **Android para trabalho** item de configuração para gerir as definições para Android para dispositivos de trabalho que são inscritos pelo Configuration Manager no Microsoft Intune ou geridos no local.  

### <a name="to-create-an-android-for-work-configuration-item"></a>Para criar um Android para o item de configuração de trabalho  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade**.  

2.  Na área de trabalho **Ativos e Conformidade** , expanda **Definições de Conformidade**e, em seguida, clique em **Itens de Configuração**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

5.  Em **especificar o tipo de item de configuração que pretende criar**, selecione **Android para trabalho**.  

6.  Escolha **categorias** se criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  

  Clique em **Seguinte**.

7.  No **definições do dispositivo** página do assistente, selecione os grupos de definições que pretende configurar. Consulte [Android para definições de item de configuração de trabalho](#android-for-work-configuration-item-settings-reference) para obter detalhes e, em seguida, clique em **seguinte**.  

  > [!TIP]  
  >  Se a definição pretendida não estiver listada, selecione a caixa de verificação **Configurar definições adicionais que não estejam incluídas nos grupos de predefinições**.  

9. Em cada página de definições, configure as definições de que necessita e se pretende resolvê-las quando não forem compatíveis com dispositivos (quando esta opção é suportada).  

10. Para cada grupo de definições, também pode configurar a gravidade que será comunicada quando um item de configuração não for compatível:  

    -   **Nenhum** -dispositivos que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  

    -   **Informações** -dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.  

    -   **Aviso** -dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.  

    -   **Crítico** -dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos** para relatórios do Configuration Manager.  

    -   **Crítico com evento** -dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos da aplicação.  

11. Na página **Aplicabilidade da Plataforma** do assistente, reveja as definições que não são compatíveis com as plataformas suportadas que selecionou anteriormente. Pode voltar atrás e remover estas definições ou pode continuar.  

    > [!TIP]  
    >  As definições não suportadas não são avaliadas em termos de compatibilidade.  

12. Conclua o assistente.  

 Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade** .  

##  <a name="android-for-work-configuration-item-settings-reference"></a>Android para a referência de definições de item de configuração de trabalho  

### <a name="password"></a>Palavra-passe  

|Definição|Detalhes|  
|-------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos**|Exigir uma palavra-passe em dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|O comprimento mínimo da palavra-passe.|  
|**Expiração da palavra-passe em dias**|O número de dias antes de uma palavra-passe tem de ser alterado.|  
|**Número de palavras-passe memorizadas**|Impede a reutilização de palavras-passe utilizadas recentes.|  
|**Número de tentativas de início de sessão falhadas antes de o dispositivo ser apagado**|Apaga o dispositivo em caso de falha deste número de tentativas de início de sessão.|  
|**Tempo de inatividade antes do dispositivo está bloqueado**|Selecione a quantidade de tempo que não é utilizado o dispositivo antes de esta bloqueia.|
|**Qualidade da palavra-passe**|Selecionar o nível de complexidade da palavra-passe exigido e se podem ser utilizados dispositivos biométricos.|  
|**Permitir Smart Lock e outros agentes de confiança**|Vamos controlar a funcionalidade Smart Lock em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como agentes de confiança, permite desativar ou ignorar a palavra-passe da ecrã de bloqueio do dispositivo se o dispositivo estiver numa localização fidedigna, como quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores finais configurem o Smart Lock.|
|**Impressão digital para desbloquear**|&nbsp;|

###  <a name="work-profile"></a>Perfil de trabalho  
 Estas definições aplicam-se apenas a dispositivos Samsung KNOX.  

|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Permitir partilha de dados entre perfis pessoais e de trabalho**|Escolha entre:<br>- **Não configurado**<br>- **Predefinição restrições de partilha**<br>- **As aplicações no perfil de trabalho podem processar o pedido do perfil pessoal**<br>- **Aplicações pessoais perfil podem processar o pedido do perfil de trabalho**<br><br>(Consulte também [definições copiar-colar](#copy-paste-configuration-item-settings) com o URI personalizado)|  
|**Ocultar as notificações de perfil de trabalho quando o dispositivo está bloqueado (Android 6.0 +)**||
|**Definir a política de permissão de aplicação predefinido (Android 6.0 +)**|Escolha entre:<br>- **Não configurado**<br>- **Sempre apresentado um aviso**<br>- **Automática conceder**<br>- **Negar automática**|

### <a name="copy-paste-configuration-item-settings"></a>Definições do item de configuração de copiar-colar
Nenhuma do **permitir partilha de dados entre a vida profissional e a pessoais perfis** opções evitar o comportamento de copiar-colar. Utilize uma definição personalizada que pode ser configurada para impedir a copiar-colar. Isto pode ser definido através de URI personalizada.

- OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Tipo de valor: Booleano

Definição DisallowCrossProfileCopyPaste para verdadeiro impede o comportamento de copiar-colar entre Android para trabalho pessoal e perfis de trabalho.

## <a name="see-also"></a>Consulte Também  
 [Itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
