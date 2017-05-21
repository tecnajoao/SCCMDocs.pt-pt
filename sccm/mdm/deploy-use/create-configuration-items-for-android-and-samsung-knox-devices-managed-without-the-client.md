---
title: "Criar itens de configuração para Android e Samsung KNOX Standard dispositivos geridos com o Intune | Documentos do Microsoft"
description: "Utilize o item de configuração do System Center Configuration Manager Android e Samsung KNOX Standard para gerir as definições dos dispositivos."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 4b9261db93c9bf72c492e3c9be5b30f81835134a
ms.openlocfilehash: c9961c2e9866199571a1b39a7b185cb6bb96f998
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para os dispositivos Android e Samsung KNOX geridos sem o cliente System Center Configuration Manager

Utilizar o System Center Configuration Manager **Android e Samsung KNOX** item de configuração para gerir as definições para dispositivos Android e Samsung KNOX que são inscritos pelo Configuration Manager no Microsoft Intune ou gerido no local.  

#### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>Para criar um item de configuração do Android e Samsung KNOX  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2. No **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e, em seguida, escolha **itens de configuração**.  

3. No **base** separador o **criar** grupo, selecione **Criar Item de configuração**.  

4. No **geral** página do Assistente de Item de configuração criar, especifique um nome e uma descrição opcional para o item de configuração.  

5. Em **especifique o tipo de item de configuração que pretende criar**, escolha **Android e Samsung KNOX**.  

6. Escolher **categorias** se pode criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  

7. No **plataformas suportadas** página do assistente, selecione as plataformas Android ou Samsung KNOX específicas que irão avaliar o item de configuração.  

8. No **definições do dispositivo** página do assistente, selecione o grupo de definições que pretende configurar. Consulte o artigo [Android e Samsung KNOX referência de definições de item de configuração](#BKMK_setref) neste tópico para obter detalhes e, em seguida, escolha **seguinte**.  

    > [!TIP]  
    >  Se a definição que pretende não estiver listada, verifique o **configurar definições adicionais que não estejam em grupos de predefinições** caixa.  

9. Em cada página de definições, configure as definições que sejam necessárias. Além disso, escolha se pretende resolvê-los quando estes não são compatíveis em dispositivos (quando esta opção é suportada).  

10. Para cada grupo de definição, também pode configurar a gravidade que será reportada quando um item de configuração é encontrado for compatível:  

    - **Nenhum**. Dispositivos que não obedeçam a esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  

    - **Informações**. Dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.  

    - **Aviso**. Dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.  

    - **Crítico**. Dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager.  

    - **Crítico com evento**. Dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  

11. No **plataforma aplicabilidade** página do assistente, reveja as definições que não são compatíveis com as plataformas suportadas escolhidos anteriormente. Pode voltar atrás e remover estas definições ou pode continuar.  

    > [!TIP]  
    >  As definições não suportadas não são avaliadas em termos de compatibilidade.  

12. Conclua o assistente.  

 Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade** .  

## <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Referência de definições do item configuração do Android e Samsung KNOX  

### <a name="password"></a>Palavra-passe  
Estas definições aplicam-se a dispositivos Android e Samsung KNOX.  

|Definição|Detalhes|  
|-------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos**|Requer uma palavra-passe em dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|Especifica o comprimento mínimo da palavra-passe.|  
|**Expiração da palavra-passe em dias**|Especifica o número de dias antes de uma palavra-passe tem de ser alterada.|  
|**Número de palavras-passe memorizadas**|Impede o reutilizar palavras-passe utilizadas anteriormente.|  
|**Número de tentativas de início de sessão falhadas antes de o dispositivo ser apagado**|Se este número de início de sessão tenta falhar, apaga o dispositivo.|  
|**Tempo de inatividade antes do dispositivo está bloqueado**|Especifica a quantidade de tempo antes do dispositivo será bloqueado se não está a ser utilizado.|
|**Qualidade da palavra-passe**|Especifica a complexidade de palavra-passe nível necessário e se biométrica dispositivos podem ser utilizados.|  
|**Permitir o bloqueio de smart card e outros agentes de fidedignidade**|Permite-lhe controlar a funcionalidade de bloqueio de smart card em dispositivos Android compatíveis. Esta capacidade de telefone permite-lhe desativar ou ignorar a palavra-passe do dispositivo bloqueio ecrã se o dispositivo estiver numa localização fidedigna, como quando esta está ligada para um dispositivo Bluetooth específico ou quando for próximo uma etiqueta de NFC. Pode utilizar esta definição para impedir que os utilizadores a partir da configuração de bloqueio de smart card.|
|**Impressão digital para desbloquear (KNOX 5.0 +)**|Esta definição permite a utilização de uma identificação digital para desbloquear os dispositivos compatíveis.|

### <a name="device"></a>Dispositivo   

|Definição|Detalhes|  
|------------------|-------------|  
|**Marcação por voz**|Ativa ou desativa a funcionalidade de marcação de voz no dispositivo.|
|**Assistente de voz**|Esta definição permite a utilização do software do Assistente de voz no dispositivo.|
|**Captura de ecrã**|Permite ao utilizador capturar os conteúdos de ecrã como uma imagem.|
|**Submissão de dados de diagnóstico**|Permite que o dispositivo enviar informações de diagnóstico para a Google.|
|**Geolocalização**|Permite que o dispositivo utilize informações de localização.|
|**Copiar e Colar**|Permite que as funções de copiar e colar no dispositivo.|
|**Reposição de fábrica**|Permite ao utilizador efetuar uma reposição de fábrica num dispositivo.|  |
|**Partilha da área de transferência entre aplicações**|Permite ao utilizador utilizar a área de transferência para copiar e colar entre aplicações.|  |
|**Bluetooth**|Esta definição permite a utilização de Bluetooth no dispositivo.|

### <a name="store"></a>Arquivo

|Definição|Detalhes|  
|------------------|-------------|  
|**Loja de aplicações**|Permite ao utilizador aceder ao Google Play store no dispositivo.|

### <a name="browser"></a>Browser

|Definição|Detalhes|  
|------------------|-------------|  
|**Permitir browser**|Permite que browser predefinido o dispositivo para ser utilizado.|
|**Preenchimento automático**|Permite que a função de preenchimento automático de browser para ser utilizado.|
|**Scripting ativo**|Esta definição permite aos browser da web do dispositivo utilizar scripting ativo.|
|**Bloqueador de janelas pop-up**|Esta definição permite a utilização do Bloqueador de janelas pop-up no browser.|
|**Cookies**|Esta definição permite aos browser da web do dispositivo utilizar cookies.|

### <a name="cloud"></a>Nuvem  

|Definição|Detalhes|  
|-------------|-------------|  
|**Cópia de segurança do Google**|Esta definição permite a utilização da cópia de segurança do Google.|  
|**Sincronização automática da conta Google**|Permite que as definições da conta Google sejam sincronizadas automaticamente.|  

### <a name="security"></a>Segurança  

|Definição|Detalhes|  
|-------------|-------------|  
|**Mensagens de SMS e MMS**|Esta definição permite a utilização de SMS e MMS mensagens no dispositivo.|
|**Armazenamento amovível**|Permite que o dispositivo utilize armazenamento amovível, como um cartão SD.|
|**Câmara**|Permite a utilização da câmara do dispositivo.<br /><br /> Aplicável a dispositivos Android e Samsung KNOX.|
|**Comunicação de proximidade (NFC)**|Permite que as tarefas que utilizam comunicação de proximidade se o dispositivo suporta.|
|**No YouTube**|Esta definição permite a utilização da aplicação do YouTube no dispositivo.<br /><br /> Aplicável apenas a dispositivos Samsung KNOX.|  
|**Desligar**|Permite que o dispositivo seja desligado.<br /><br /> Aplicável apenas a dispositivos Samsung KNOX.|  

### <a name="roaming"></a>Roaming

|Definição|Detalhes|  
|-------------|-------------|  
|Roaming de voz|Permite chamadas em roaming quando o dispositivo estiver numa rede móvel.|
|Roaming de dados|Permite que dados roaming quando o dispositivo estiver numa rede móvel.|


### <a name="encryption"></a>Encriptação  
 Estas definições aplicam-se a dispositivos Android e Samsung KNOX.  

|Definição|Detalhes|  
|-------------|-------------|  
|**Encriptação do cartão de armazenamento**|Requer que o cartão de armazenamento do dispositivo é encriptado.|
|**Encriptação de ficheiros no dispositivo**|Necessita que os ficheiros no dispositivo móvel sejam encriptados.|  

### <a name="wireless-communications"></a>Comunicações sem fios

|Definição|Detalhes|  
|-------------|-------------|  
|**Ligação de rede sem fios**|Esta definição permite a utilização das capacidades de Wi-Fi do dispositivo.|
|**Tethering Wi-Fi**|Esta definição permite a utilização de partilha de Wi-Fi no dispositivo.|


### <a name="compliant-and-noncompliant-apps-android"></a>Aplicações compatíveis e incompatíveis (Android)  
Pode especificar uma lista de aplicações Android que são compatíveis ou não compatíveis na sua empresa. Em seguida, pode utilizar relatórios para dispositivos que têm instaladas aplicações não compatíveis de mostrar e o utilizador associado.  

Não é possível especificar aplicações em conformidade e não conformes no mesmo item de configuração.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Especificar a lista de aplicações compatíveis ou incompatíveis  

Na página **Aplicações Compatíveis e Incompatíveis (Android)**, especifique as seguintes informações:  

|Definição|Mais informações|  
|-------------|----------------------|  
|**Lista de aplicações não compatíveis**|Especifica uma lista de aplicações que serão reportadas como não conforme se instaladas pelos utilizadores.|  
|**Lista de aplicações compatíveis**|Especifica uma lista de aplicações que os utilizadores estão autorizados a instalar. Quaisquer outras aplicações instaladas serão comunicadas como incompatíveis.|  
|**Adicionar**|Adiciona uma aplicação à lista selecionada. Especifique um nome à sua escolha, o fabricante da aplicação (opcional) e o URL para a aplicação na loja de aplicações.<br /><br /> Para especificar o URL, a partir de [secção aplicações do Google Play](https://play.google.com/store/apps), procure a aplicação que pretende utilizar.<br /><br /> Abra a página da aplicação e copie o URL para a área de transferência. Agora pode utilizar este URL na lista de aplicações em conformidade ou na lista de aplicações não conformes.<br /><br /> **Exemplo:** Procure no Google Play para **do Microsoft Office Mobile**. O URL que utiliza será **https://Play.google.com/Store/Apps/details?ID=com.microsoft.Office.officehub&hl=PT**.|  
|**Editarar**|Permite-lhe editar o nome, o publisher e o URL da aplicação selecionada.|  
|**Remove**|Elimina a aplicação selecionada da lista.|  
|**Importarar**|Importa uma lista de aplicações que tenha especificado um ficheiro de valores separados por vírgulas. Utilize o nome de aplicação do formato, publicador, URL da aplicação no ficheiro.|  

## <a name="android-for-work-configuration-items"></a>Android para itens de configuração de trabalho
Android para trabalhar tem dois grupos de definição para itens de configuração:

- **Palavra-passe**. Idêntico às definições para Android "clássica."

- **O seu trabalho perfil**. Ativa o Android seguinte para definições de trabalho:
  -    **Permitir que os dados entre o trabalho e perfis pessoais de partilha**
  - **Ocultar as notificações de perfil de trabalho quando o dispositivo está bloqueado** (Android 6.0 +)
  -    **Configurar a política de permissão de aplicação predefinida** (Android 6.0 +)

Para criar um item de configuração no perfil de trabalho Android, escolha **Android para trabalhar** no **geral** página e configure as definições para cada um dos grupos de definição. Adicionar o item de configuração para um plano base e implementar como habitualmente. Estas definições serão aplicadas apenas para dispositivos inscritos como Android para trabalhar e não a dispositivos inscritos como Android.

### <a name="kiosk-mode-samsung-knox-only"></a>Modo de local público (apenas Samsung KNOX)  
Pode utilizar o modo de local público para bloquear um dispositivo para permitir que apenas determinadas funcionalidades para o seu trabalho. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo. Ou pode ser utilizados para um dispositivo com a finalidade de desempenhar apenas uma função, como um dispositivo de ponto de venda.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Configurar o modo de local público para um dispositivo Samsung KNOX  

1. No **configurar definições do modo de local público para dispositivos do Samsung KNOX** página do Assistente de Item de configuração criar, especifique as seguintes informações:  

   |Definição|Mais informações|  
   |-------------|----------------------|  
   |**Selecione a aplicação**|Escolher **procurar** para selecionar uma aplicação Android do Configuration Manager (com a extensão **. apk**) que terá permissão para ser executada quando o dispositivo estiver em modo de local público. Não será permitida a execução de outras aplicações no dispositivo.|  
   |**Botões de volume**|Ativa ou desativa a utilização dos botões de volume no dispositivo.|  
   |**Suspensão de ecrã e botão de reativação**|Ativa ou desativa o botão suspender/reativar ecrã do dispositivo.|  

2. Quando tiver terminado, selecione **seguinte**.  

## <a name="reports-for-monitoring"></a>Relatórios de monitorização
Pode utilizar um dos seguintes relatórios para monitorizar aplicações compatíveis e incompatíveis:  

- **Lista de aplicações e dispositivos para um utilizador especificado não compatíveis**. Mostra informações sobre utilizadores e dispositivos que têm instaladas aplicações que não são compatíveis com uma política que especificou.  

- **Resumo dos utilizadores que têm aplicações não compatíveis**. Mostra informações sobre os utilizadores que têm instaladas aplicações que não são compatíveis com uma política que especificou.  

Para obter informações sobre como utilizar relatórios, veja [Relatórios do System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="see-also"></a>Consulte também  
[Itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)

