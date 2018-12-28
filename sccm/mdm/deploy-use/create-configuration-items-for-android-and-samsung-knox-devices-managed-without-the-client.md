---
title: Criar itens de configuração para dispositivos Android e Samsung KNOX Standard geridos com o Intune
titleSuffix: Configuration Manager
description: Utilize o item de configuração do System Center Configuration Manager Android e Samsung KNOX Standard para gerir as definições dos dispositivos.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a1759013902a75c26ec5004b932a81b536e303e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417001"
---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para os dispositivos Android e Samsung KNOX geridos sem o cliente System Center Configuration Manager

Utilizar o System Center Configuration Manager **Android e Samsung KNOX** item de configuração para gerir as definições para dispositivos Android e Samsung KNOX inscritos no Microsoft Intune ou geridos no local pelo Configuration Manager .  

#### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>Para criar um item de configuração do Android e Samsung KNOX  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2. Na **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e, em seguida, escolha **itens de configuração**.  

3. Sobre o **home page** separador a **criar** de grupo, escolha **Criar Item de configuração**.  

4. Sobre o **gerais** página do Assistente de Item de configuração criar, especifique um nome e uma descrição opcional para o item de configuração.  

5. Sob **especifique o tipo de item de configuração que pretende criar**, escolha **Android e Samsung KNOX**.  

6. Escolher **categorias** se criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  

7. Sobre o **plataformas suportadas** página do assistente, selecione as plataformas específicas do Android ou Samsung KNOX que irão avaliar o item de configuração.  

8. Sobre o **definições do dispositivo** página do assistente, selecione o grupo de definições que pretende configurar. Ver [Android e Samsung KNOX referência de definições de item de configuração](#BKMK_setref) neste tópico para obter detalhes e, em seguida, escolha **próxima**.  

    > [!TIP]  
    >  Verifique se a definição pretendida não estiver listada, o **configurar definições adicionais que não estão em grupos de predefinições** caixa.  

9. Em cada página de definições, configure as definições que necessita. Além disso, escolha se pretende resolvê-las quando não estiverem em conformidade com dispositivos (quando esta opção é suportada).  

10. Para cada grupo de definição, também pode configurar a gravidade que será comunicada quando um item de configuração encontra-se não for compatível:  

    - **Nenhum**. Dispositivos que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  

    - **Informações**. Dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **informações** para relatórios do Configuration Manager.  

    - **Aviso**. Dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **aviso** para relatórios do Configuration Manager.  

    - **Crítico**. Dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **crítico** para relatórios do Configuration Manager.  

    - **Crítico com evento**. Dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **crítico** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  

11. Sobre o **aplicabilidade da plataforma** página do assistente, reveja as definições que não são compatíveis com as plataformas suportadas que selecionou anteriormente. Pode voltar atrás e remover estas definições ou pode continuar.  

    > [!TIP]  
    >  As definições não suportadas não são avaliadas em termos de compatibilidade.  

12. Conclua o assistente.  

    Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade** .  

## <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Referência de definições do item configuração do Android e Samsung KNOX  

### <a name="password"></a>Palavra-passe  
Estas definições aplicam-se a dispositivos Android e Samsung KNOX.  

|Definição|Detalhes|  
|-------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos**|Requer uma palavra-passe nos dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|Especifica o comprimento mínimo da palavra-passe.|  
|**Expiração da palavra-passe em dias**|Especifica o número de dias antes de uma palavra-passe tem de ser alterada.|  
|**Número de palavras-passe memorizadas**|Impede a reutilização de palavras-passe utilizadas anteriormente.|  
|**Número de tentativas de início de sessão falhadas antes de o dispositivo ser apagado**|Apaga o dispositivo se este número de início de sessão tenta falhar.|  
|**Tempo de inatividade antes do dispositivo está bloqueado**|Especifica o período de tempo antes do dispositivo ser bloqueado quando não está a ser utilizado.|
|**Qualidade da palavra-passe**|Especifica a complexidade de palavra-passe obrigatório nível e se podem ser utilizados dispositivos biométricos.|  
|**Permitir Smart Lock e outros agentes de fidedignidade**|Permite-lhe controlar a funcionalidade Smart Lock em dispositivos Android compatíveis. Esta capacidade de telefone permite-lhe desativar ou ignorar a palavra-passe de ecrã do bloqueio de dispositivo se o dispositivo estiver numa localização fidedigna, como quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores configurem o Smart Lock.|
|**Impressão digital para desbloquear (KNOX 5.0 +)**|Permite a utilização de uma impressão digital para desbloquear dispositivos compatíveis.|

### <a name="device"></a>Dispositivo   

|                 Definição                  |                             Detalhes                             |
|------------------------------------------|-----------------------------------------------------------------|
|            **Marcação por voz**             |  Ativa ou desativa a funcionalidade de marcação por voz no dispositivo.   |
|           **Assistente de voz**            |    Permite a utilização do software de Assistente de voz no dispositivo.    |
|            **Captura de ecrã**            |     Permite ao utilizador capturar o conteúdo do ecrã como uma imagem.      |
|      **Submissão de dados de diagnóstico**      |    Permite que o dispositivo enviar informações de diagnóstico para a Google.     |
|             **Geolocalização**              |            Permite ao dispositivo utilizar informações de localização.            |
|            **Copiar e Colar**            |         Permite as funções de copiar e colar no dispositivo.          |
|            **Reposição de fábrica**             |      Permite ao utilizador efetuar uma reposição de fábrica no dispositivo.       |
| **Partilha da área de transferência entre aplicações** | Permite que o utilizador utilize a área de transferência para copiar e colar entre aplicações. |
|              **Bluetooth**               |           Permite a utilização de Bluetooth no dispositivo.            |

### <a name="store"></a>Arquivo

|Definição|Detalhes|  
|------------------|-------------|  
|**Loja de aplicações**|Permite ao utilizador aceder à loja do Google Play no dispositivo.|

### <a name="browser"></a>Browser

|Definição|Detalhes|  
|------------------|-------------|  
|**Permitir browser**|Permite que o navegador da web padrão do dispositivo a ser utilizado.|
|**Preenchimento automático**|Permite que a função de preenchimento automático do browser para ser utilizado.|
|**Scripting ativo**|Permite que o navegador da web do dispositivo utilizar o scripting ativo.|
|**Bloqueador de janelas pop-up**|Permite a utilização do Bloqueador de pop-up no browser.|
|**Cookies**|Permite que o navegador da web do dispositivo utilizar cookies.|

### <a name="cloud"></a>Nuvem  

|Definição|Detalhes|  
|-------------|-------------|  
|**Cópia de segurança do Google**|Permite a utilização da cópia de segurança do Google.|  
|**Sincronização automática da conta Google**|Permite que as definições da conta Google sejam sincronizadas automaticamente.|  

### <a name="security"></a>Segurança  

|Definição|Detalhes|  
|-------------|-------------|  
|**Mensagens de SMS e MMS**|Permite a utilização de SMS e MMS no dispositivo de mensagens.|
|**Armazenamento amovível**|Permite que o dispositivo utilizar armazenamento amovível, como um cartão SD.|
|**Câmara**|Permite a utilização da câmara do dispositivo.<br /><br /> Aplicável a dispositivos Android e Samsung KNOX.|
|**Comunicação de proximidade (NFC)**|Permite que as tarefas que utilizam comunicação de proximidade se o dispositivo a suportar.|
|**YouTube**|Permite a utilização da aplicação YouTube no dispositivo.<br /><br /> Aplicável apenas a dispositivos Samsung KNOX.|  
|**Desligar**|Permite que o dispositivo seja desligado.<br /><br /> Aplicável apenas a dispositivos Samsung KNOX.|  

### <a name="roaming"></a>Roaming

|Definição|Detalhes|  
|-------------|-------------|  
|Roaming de voz|Permite chamadas em roaming quando o dispositivo estiver numa rede celular.|
|Roaming de dados|Permite dados em roaming quando o dispositivo estiver numa rede celular.|


### <a name="encryption"></a>Encriptação  
 Estas definições aplicam-se a dispositivos Android e Samsung KNOX.  

|Definição|Detalhes|  
|-------------|-------------|  
|**Encriptação do cartão de armazenamento**|Requer que o cartão de armazenamento do dispositivo é encriptado.|
|**Encriptação de ficheiros no dispositivo**|Necessita que os ficheiros no dispositivo móvel sejam encriptados.|  

### <a name="wireless-communications"></a>Comunicações sem fios

|Definição|Detalhes|  
|-------------|-------------|  
|**Ligação de rede sem fios**|Permite a utilização das capacidades Wi-Fi do dispositivo.|
|**Tethering Wi-Fi**|Permite a utilização de tethering Wi-Fi no dispositivo.|


### <a name="compliant-and-noncompliant-apps-android"></a>Aplicações compatíveis e incompatíveis (Android)  
Pode especificar uma lista de aplicações Android que estão em conformidade ou não conformes na sua empresa. Em seguida, pode utilizar relatórios para mostrar os dispositivos que tenham aplicações incompatíveis instaladas e o utilizador associado.  

Não é possível especificar aplicações em conformidade e não conformes no mesmo item de configuração.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Especificar a lista de aplicações em conformidade ou não conformes  

Na página **Aplicações Compatíveis e Incompatíveis (Android)**, especifique as seguintes informações:  


|          Definição           |                                                                                                                                                                                                                                                                                                                 Mais informações                                                                                                                                                                                                                                                                                                                  |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Lista de aplicações não conformes** |                                                                                                                                                                                                                                                                               Especifica uma lista de aplicações que serão comunicadas como incompatíveis se forem instaladas por utilizadores.                                                                                                                                                                                                                                                                               |
|  **Lista de aplicações compatíveis**   |                                                                                                                                                                                                                                                              Especifica uma lista de aplicações que os utilizadores podem instalar. Quaisquer outras aplicações instaladas serão comunicadas como incompatíveis.                                                                                                                                                                                                                                                               |
|          **Adicionar**           | Adiciona uma aplicação à lista selecionada. Especifique um nome à sua escolha, o fabricante da aplicação (opcional) e o URL para a aplicação na loja de aplicações.<br /><br /> Para especificar o URL, a partir da [secção aplicações do Google Play](https://play.google.com/store/apps), procure a aplicação que pretende utilizar.<br /><br /> Abra a página da aplicação e copie o URL para a área de transferência. Agora pode utilizar este URL na lista de aplicações em conformidade ou na lista de aplicações não conformes.<br /><br /> **Example:** Procure Google Play **Microsoft Office Mobile**. O URL que utilizar será **<https://play.google.com/store/apps/details?id=com.microsoft.office.officehub>**. |
|          **Editarar**          |                                                                                                                                                                                                                                                                                          Permite-lhe editar o nome, fabricante e URL da aplicação selecionada.                                                                                                                                                                                                                                                                                          |
|         **Remove**         |                                                                                                                                                                                                                                                                                                      Elimina a aplicação selecionada da lista.                                                                                                                                                                                                                                                                                                      |
|         **Importarar**         |                                                                                                                                                                                                                                                 Importa uma lista de aplicações que especificou num ficheiro de valores separados por vírgulas. Utilize o nome da aplicação de formato, publicador, URL da aplicação no ficheiro.                                                                                                                                                                                                                                                 |

## <a name="android-for-work-configuration-items"></a>Android para itens de configuração de trabalho
O Android for Work tem dois grupos de definições para itens de configuração:

- **Palavra-passe**. Idênticas às definições do Android "clássico".

- **Perfil de trabalho**. Permite que as seguintes definições do Android for Work:
  - **Permitir partilha de dados entre perfis pessoais e de trabalho**
  - **Ocultar notificações do perfil de trabalho quando o dispositivo está bloqueado** (Android 6.0 +)
  - **Configurar a política de permissão de aplicação do padrão** (Android 6.0 +)

Para criar um item de configuração no perfil de trabalho Android, escolha **Android for Work** sobre o **geral** página e configurar as definições para cada um dos grupos de. Adicione o item de configuração para uma linha de base e implementar como de costume. Estas definições serão aplicadas apenas a dispositivos inscritos como Android for Work e não a dispositivos inscritos como Android.

### <a name="kiosk-mode-samsung-knox-only"></a>Modo de local público (apenas Samsung KNOX)  
Pode utilizar o modo de local público para bloquear um dispositivo para permitir que apenas determinadas funcionalidades funcionem. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo. Ou pode ser utilizados para um dispositivo de desempenhar apenas uma função, como um dispositivo de ponto de venda.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Configurar o modo de local público para um dispositivo Samsung KNOX  

1. Sobre o **configurar definições do modo de local público para dispositivos Samsung KNOX** página do Assistente de Item de configuração criar, especifique as seguintes informações:  

   |Definição|Mais informações|  
   |-------------|----------------------|  
   |**Selecionar aplicação**|Escolher **navegue** para selecionar uma aplicação Android do Configuration Manager (com a extensão **. apk**) que terá permissão para ser executada quando o dispositivo estiver no modo de local público. Não será permitida a execução de outras aplicações no dispositivo.|  
   |**Botões de volume**|Ativa ou desativa a utilização dos botões de volume no dispositivo.|  
   |**Suspensão de ecrã e botão de reativação**|Ativa ou desativa o botão suspender/reativar ecrã do dispositivo.|  

2. Quando tiver terminado, escolha **seguinte**.  

## <a name="reports-for-monitoring"></a>Relatórios para monitorização
Pode utilizar um dos seguintes relatórios para monitorizar aplicações compatíveis e incompatíveis:  

- **Lista de aplicações e dispositivos para um utilizador especificado incompatíveis**. Mostra informações sobre utilizadores e dispositivos que têm instaladas aplicações que não estão em conformidade com uma política especificada por si.  

- **Resumo de utilizadores que têm aplicações não conformes**. Mostra informações sobre os utilizadores que têm instaladas aplicações que não estão em conformidade com uma política especificada por si.  

Para obter informações sobre como utilizar relatórios, veja [Relatórios do System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="see-also"></a>Consulte também  
[Itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
