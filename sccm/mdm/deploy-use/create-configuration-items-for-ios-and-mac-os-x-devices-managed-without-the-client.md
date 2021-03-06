---
title: Criar itens de configuração para dispositivos iOS e Mac OS X geridos com o Intune
titleSuffix: Configuration Manager
description: Utilize o item de configuração de Mac OS X e iOS do System Center Configuration Manager para gerir as definições dos dispositivos iOS e Mac OS X.
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 613a48ac-c55d-4c4a-94ea-d3747a1b10cb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 690aefeac875e3c3f39d5801bdb33d69ccecb45e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135825"
---
# <a name="how-to-create-configuration-items-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Como criar itens de configuração para dispositivos iOS e Mac OS X geridos com o Intune
Utilizar o System Center Configuration Manager **iOS e Mac OS X** item de configuração para gerir as definições para dispositivos iOS e Mac OS X que são inscritos pelo Configuration Manager no Microsoft Intune ou geridos no local.  
  
### <a name="to-create-an-ios-and-mac-os-x-configuration-item"></a>Para criar um item de configuração do iOS e Mac OS X  
  
1. Na consola do Configuration Manager, clique em **ativos e compatibilidade**.  
  
2. Na área de trabalho **Ativos e Conformidade** , expanda **Definições de Conformidade**e, em seguida, clique em **Itens de Configuração**.  
  
3. No separador **Home Page** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4. Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5. Em **Especifique o tipo de item de configuração que pretende criar**, selecione **iOS e Mac OS X**.  
  
6. Clique em **categorias** se criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  
  
7. Na página **Plataformas Suportadas** do assistente, selecione as plataformas específicas do iOS ou do Mac OS X que irão avaliar o item de configuração.  
  
8. Na página **Definições do Dispositivo** do assistente, selecione o grupo de definições que pretende configurar. Veja [Referência das definições do item de configuração do iOS e Mac OS X](#BKMK_Setref) neste tópico para obter detalhes e clique em **Seguinte**.  
  
   > [!TIP]  
   >  Se a definição pretendida não estiver listada, selecione a caixa de verificação **Configurar definições adicionais que não estejam incluídas nos grupos de predefinições**.  
  
9. Em cada página de definições, configure as definições de que necessita e se pretende resolvê-las quando não forem compatíveis com dispositivos (quando esta opção é suportada).  
  
10. Para cada grupo de definições, também pode configurar a gravidade que será comunicada quando um item de configuração não for compatível:  
  
    -   **Nenhum** -dispositivos que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  
  
    -   **Informações** -os dispositivos que não obedeçam a esta regra de compatibilidade comunicam uma gravidade de falha **informações** para relatórios do Configuration Manager.  
  
    -   **Aviso** -os dispositivos que não obedeçam a esta regra de compatibilidade comunicam uma gravidade de falha **aviso** para relatórios do Configuration Manager.  
  
    -   **Crítico** -os dispositivos que não obedeçam a esta regra de compatibilidade comunicam uma gravidade de falha **críticos** para relatórios do Configuration Manager.  
  
    -   **Crítico com evento** -os dispositivos que não obedeçam a esta regra de compatibilidade comunicam uma gravidade de falha **críticos** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos da aplicação.  
  
11. Na página **Aplicabilidade da Plataforma** do assistente, reveja as definições que não são compatíveis com as plataformas suportadas que selecionou anteriormente. Pode voltar atrás e remover estas definições ou pode continuar.  
  
    > [!TIP]  
    >  As definições não suportadas não são avaliadas em termos de compatibilidade.  
  
12. Conclua o assistente.  
  
    Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade**.  
  
##  <a name="ios-and-mac-os-x-configuration-item-settings-reference"></a>Referência das definições do item de configuração do iOS e Mac OS X  
  
###  <a name="password"></a>Palavra-passe  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos móveis**|Exigir uma palavra-passe em dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|O comprimento mínimo da palavra-passe.|  
|**Expiração da palavra-passe em dias**|O número de dias antes de uma palavra-passe tem de ser alterado.|  
|**Número de palavras-passe memorizadas**|Impede a reutilização de palavras-passe.|  
|**Número de tentativas de início de sessão falhadas antes de o dispositivo ser apagado**|Apaga o dispositivo em caso de falha deste número de tentativas de início de sessão.<br /><br /> (Apenas no iOS)|  
|**Complexidade de palavra-passe**|Escolher se pretende especificar um PIN como "1234" ou se tem de fornecer uma palavra-passe segura.| 
|**Permitir palavras-passe simples**|Permitir palavras-passe simples, como **0000** e **1234**.|
|**Impressão digital de desbloqueio**|Permitir a utilização de uma impressão digital para desbloquear o dispositivo.|
|**Modificação do código de acesso** (apenas supervisionado)|Permitir que a palavra-passe do dispositivo ser adicionado, alteradas ou removidas.|
  
###  <a name="device"></a>Dispositivo  
 Estas definições aplicam-se a dispositivos iOS e Mac OS X.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Adicionar amigos do game center**|Permite-lhe adicionar amigos na aplicação do centro de jogos.|
|**Marcação por voz**|Permite a utilização da funcionalidade de marcação por voz no dispositivo.|  
|**Assistente de voz**|Permite a utilização de uma aplicação de assistente de voz como o Siri.|  
|**Assistente de voz quando bloqueado**|Permite a utilização de uma aplicação de assistente de voz como o Siri quando o dispositivo está bloqueado.|  
|**Captura de ecrã**|Permite-lhe tirar uma captura de ecrã do ecrã do dispositivo.|  
|**Cliente de chat por vídeo**|Permite a utilização de aplicações de chat de vídeo como o Facetime.|  
|**Jogos de vários jogadores**|Permite-lhe jogar jogos com outros jogadores na Internet.|  
|**Software de carteira pessoal quando bloqueado**|Permite a utilização de software de carteira pessoal como o Passbook.|  
|**Submissão de dados de diagnóstico**|Permitir a submissão de ficheiros de registo de aplicações.|  
|**Notificações do Centro de ação**|Permitir que o utilizador aceda à vista de notificações sem desbloquear o dispositivo.|
|**Apple Music** (apenas supervisionado)|Permita a utilização da aplicação Apple Music.|
|**Podcasts** (apenas supervisionado)|Permita a utilização da aplicação Podcasts.|
|**Aplicação mensagens** (apenas supervisionado)|Permita a utilização da aplicação mensagens para enviar mensagens de texto.|
|**Modificação da imagem de fundo** (apenas supervisionado)|Permitir ao utilizador alterar a imagem de fundo do dispositivo.|
|**Pesquisa de definição de palavras** (apenas supervisionado)|Permita a funcionalidade do iOS que permite realçar uma palavra e procurar a respetiva definição.|
|**Deteção de pulso para Apple Watches emparelhados**|Quando ativada, o Apple Watch não apresenta notificações quando não estiver a ser utilizado.|
|**Filtro de palavras ofensivas da Siri** (apenas supervisionado)|Impede que a Siri Dite ou fale com linguagem profana.|
|**Modificação do nome do dispositivo** (apenas supervisionado)|Permitir ao utilizador alterar o nome do dispositivo.|
|**Modificação de definições de submissão de diagnósticos** (apenas supervisionado)|Permitir ou bloquear o dispositivo de submeter dados de diagnóstico à Apple.|
|**Centro de jogos** (apenas supervisionado)|Permita a utilização da aplicação Game Center.|
|**iTunes Radio** (apenas supervisionado)|Permita a utilização da aplicação iTunes Radio.|
|**Apple News** (apenas supervisionado)|Permita a utilização da aplicação Apple News.|
|**O emparelhamento do Apple Watch** (apenas supervisionado)|Permitir que o dispositivo se emparelhe com um Apple Watch.|
|**Correção automática** (apenas supervisionado)|Permite que o dispositivo corrija automaticamente palavras com erros ortográficos.|
|**Modificação de Bluetooth** (apenas supervisionado)|Permite que o utilizador altere as definições de Bluetooth no dispositivo.|
|**Alterações às definições de utilização de dados via rede móvel de aplicação** (apenas supervisionado)|Permitir que o utilizador controle que aplicações estão autorizadas a utilizar dados via rede móvel.|
|**Atalhos de teclado** (apenas supervisionado)|Permite a utilização de atalhos de teclado.|
|**Teclados preditivos** (apenas supervisionado)|Permita a utilização de teclados preditivos que sugerem palavras que o utilizador poderá querer.|
|**Verificação ortográfica do teclado** (apenas supervisionado)|Permite que o verificador ortográfico do dispositivo.|
|**Modificação das definições de notificação** (apenas supervisionado)|Permitir que o utilizador altere as definições de notificação do dispositivo.|
|**Devolver resultados da Internet na pesquisa Spotlight** (apenas supervisionado)|Permitir que a ligação à Internet para fornecer mais resultados da pesquisa Spotlight.|
|**Utilizar a Siri para consultar conteúdos gerados pelo utilizador da Internet** (apenas supervisionado)|Permitir a Siri aceda a sites para responder a perguntas.|

  
###  <a name="store"></a>Arquivo  
 Estas definições aplicam-se apenas a dispositivos iOS.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Loja de aplicações**|Permite o acesso à loja de aplicações no dispositivo.|  
|**Introduzir uma palavra-passe para aceder à loja de aplicações**|Os utilizadores têm de introduzir uma palavra-passe para aceder à loja de aplicações.|  
|**Compras via aplicação**|Permite que os utilizadores façam compras via aplicação.|
|**Instalar aplicações com o Apple Configurator e o iTunes apenas** (apenas supervisionado)|Ativa ou desativa o Store de aplicação a partir do ecrã principal do dispositivo. Os utilizadores podem ainda utilizar o iTunes ou a ferramenta Apple Configurator para instalar e atualizar aplicações.|
|**Acesso à iBooks store** (apenas supervisionado)|Permitir que o utilizador procure e compre livros da loja iBooks.|
|**Transferências automáticas de aplicações** (apenas supervisionado)|Permitir que aplicações compradas noutros dispositivos sejam automaticamente transferidas para este dispositivo. Esta definição não afeta as atualizações de aplicações.|

  
###  <a name="browser"></a>Browser  
 Estas definições aplicam-se apenas a dispositivos iOS.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Browser predefinido**|O utilizador pode alterar o browser de Internet predefinido.|  
|**Preenchimento automático**|O utilizador pode alterar as definições de conclusão automática no browser.|  
|**Scripting ativo**|O browser pode executar scripts, como scripts do Active X.|  
|**Bloqueador de janelas pop-up**|Ativa ou desativa o bloqueador de janelas pop-up do browser.|  
|**Cookies**|Permitir que os cookies sejam guardados no dispositivo.|  
|**Aviso de fraude**|Ativar ou desativar avisos de sites potencialmente fraudulentos.|  
  
###  <a name="content-rating"></a>Classificação de conteúdo  
 Estas definições aplicam-se apenas a dispositivos iOS.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Conteúdo explícito no arquivo de multimédia**|Especificar se pretende permitir o acesso a conteúdo para adultos a partir da App Store.|  
|**Região das classificações**|Especifica o país/região ao qual quer aplicar restrições de classificações.|  
|**Classificação do filme**|Especifica a classificação máxima de conteúdos de filmes que pretende permitir.|  
|**Classificação de TV**|Especifica a classificação máxima de conteúdos de programa de TV que pretende permitir.|  
|**Classificação da aplicação**|Especifica a classificação máxima de conteúdos da aplicação que pretende permitir.| 
|**Conteúdos da Ibooks store sinalizada como "Erótico"** (apenas supervisionado)|Permitir ao utilizador transferir livros da categoria "Erótico".| 
  
> [!NOTE]  
>  As classificações que pode selecionar irão variar dependendo da **Região das classificações** que selecionou.  
  
###  <a name="cloud"></a>Nuvem  
 Estas definições aplicam-se apenas a dispositivos iOS.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Cópia de segurança da cloud**|Permitir a cópia de segurança para um serviço em nuvem como o iCloud.|  
|**Cópia de segurança encriptada**|Permitir que a cópia de segurança para um serviço em nuvem seja encriptada.|  
|**Sincronização de documentos**|Permitir a sincronização de documentos com um serviço em nuvem.|  
|**Sincronização de fotografias**|Permitir a sincronização de fotografias com um serviço em nuvem.| 
|**Fototeca em iCloud**|Se definido como **não**, desativa a utilização da biblioteca de fotografias do iCloud que permite aos utilizadores armazenar fotografias e vídeos na cloud. Qualquer fotos não sido completamente transferidas da Fototeca em iCloud para o dispositivo serão removidas do dispositivo se isto estiver definido como **não**.|
|**Partilha de fotografias em iCloud**|Defina como **não** para desativar a partilha de fotografias em iCloud no dispositivo.|
|**Handoff continue as atividades noutro dispositivo**|Permita ao utilizador continuar o trabalho que iniciou num dispositivo iOS no iOS outro ou dispositivo Mac OS X.|
|**Dados de sincronização de aplicações geridas para o iCloud**|Permita aplicações que gere com o Intune sincronizem dados para a conta de utilizador iCloud.|

  
###  <a name="security"></a>Segurança  
 Estas definições aplicam-se apenas a dispositivos iOS.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Câmara**|Permitir a utilização da câmara do dispositivo.| 
|**Confiar em novos autores de aplicações empresariais**|Permite que o utilizador opte por confiar em aplicações que não foram transferidas a partir da app store.| 
  
###  <a name="roaming"></a>Roaming  
 Estas definições aplicam-se apenas a dispositivos iOS.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Chamadas em roaming**|Permite chamadas quando está em roaming.|  
|**Sincronização automática em roaming**|Permite a sincronização automática do dispositivo quando está em roaming.|  
|**Roaming de dados**|Permitir roaming entre redes ao aceder a dados.|  
  
###  <a name="system-security"></a>Segurança do sistema  
 Estas definições aplicam-se apenas a dispositivos iOS.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Utilizador para aceitar certificado TLS não fidedigno**|Se **Permitido**, permite ao utilizador aceitar estes certificados. Se **Proibido**, rejeita automaticamente certificados não fidedignos.|
|**Permitir bloqueio de ativação (modo supervisionado apenas)**|Utilize esta definição para ativar o Bloqueio de Ativação do iOS nos dispositivos iOS **supervisionados** que gere. Para obter mais informações sobre o Bloqueio de Ativação, veja [Gerir o Bloqueio de Ativação do iOS com o System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md).
|**Centro de controlo do ecrã de bloqueio**|Controla se a aplicação do centro de controlo pode ser acedida quando o dispositivo está bloqueado.|  
|**Vista de notificação do ecrã de bloqueio**|Controla se as notificações podem ser visualizadas quando o dispositivo está bloqueado.|  
|**Vista atual do ecrã de bloqueio**|Controla se a vista Hoje pode ser visualizada quando o dispositivo está bloqueado.|  
|**Modificar as definições de conta** (apenas supervisionado)|Permitir ao utilizador alterar as definições de conta, tais como configurações de e-mail.|
|**Efetuar alterações às definições da aplicação Find My Friends** (apenas supervisionado)|Permitir que o utilizador altere as definições da aplicação Find My Friends.|
|**Utilize emparelhamento de anfitriões para controlar os dispositivos com um dispositivo iOS pode emparelhar** (apenas supervisionado)|Permitir emparelhamento de anfitriões para permitir que o administrador o controlo sobre que dispositivos um dispositivo iOS pode emparelhar.|
|**Apagar todo o conteúdo e definições** (apenas supervisionado)|Permitir que o utilizador utilize a opção de apagar todos os conteúdos e definições no dispositivo.|
|**Configurar restrições no dispositivo** (apenas supervisionado)|Permitir ao utilizador configurar as restrições de dispositivo (restrições de acesso) no dispositivo.|
|**Instalar certificados e perfis de configuração** (apenas supervisionado)|Permitir que o utilizador instale perfis de configuração e certificados.|
|**Palavra-passe para AirPlay a enviar pedidos**|Exigir uma palavra-passe de emparelhamento quando o utilizador utiliza AirPlay transmitir conteúdos para outros dispositivos da Apple.|
  
###  <a name="data-protection"></a>Proteção de dados  
 Estas definições aplicam-se apenas a dispositivos iOS.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Abrir documentos em aplicações geridas noutras aplicações não geridas**|Para utilização com aplicações geridas por políticas de gestão de aplicações do Configuration Manager.|  
|**Abrir documentos em aplicações não geridas noutras aplicações geridas**|Para utilização com aplicações geridas por políticas de gestão de aplicações do Configuration Manager.| 
|**Tratar o AirDrop como um destino não gerido** (apenas supervisionado)|Paragens de aplicações geridas possam enviar dados por meio de. Airdrop.|
|**AirDrop** (apenas supervisionado)|Permita a utilização da funcionalidade AirDrop para trocar conteúdos com dispositivos próximos.|
  
###  <a name="compliant-and-noncompliant-apps-ios"></a>Aplicações compatíveis e incompatíveis (iOS)  
 Permite-lhe especificar uma lista de aplicações iOS que são compatíveis ou incompatíveis com a sua empresa. Pode utilizar relatórios para apresentar dispositivos que tenham aplicações incompatíveis instaladas e o utilizador associado.  
  
 Não é possível especificar aplicações compatíveis e incompatíveis no mesmo item de configuração.  
  
#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Especificar a lista de aplicações em conformidade ou não conformes  
  
1. Na página **Aplicações Compatíveis e Incompatíveis (iOS)**, especifique as seguintes informações:  
  
   -   **Lista de aplicações incompatíveis** - Selecione esta opção se pretende especificar uma lista de aplicações que serão comunicadas como incompatíveis se forem instaladas por utilizadores.  
  
   -   **Lista de aplicações compatíveis** - Selecione esta opção se pretender especificar uma lista de aplicações que os utilizadores podem instalar. Quaisquer outras aplicações instaladas serão comunicadas como incompatíveis.  
  
   -   **Adicionar** - Adiciona uma aplicação à lista selecionada. Especifique um nome à sua escolha, o fabricante da aplicação (opcional) e o URL para a aplicação na loja de aplicações.  
  
        Para especificar o URL, a partir da App Store do iTunes, procure a aplicação que pretende utilizar.  
  
        Abra a página da aplicação e copie o URL para a área de transferência. Agora pode utilizar este URL na lista de aplicações em conformidade ou na lista de aplicações não conformes.  
  
        **Example:** Procure na loja a **Microsoft Word para iPad** aplicação. O URL que irá utilizar será **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  
  
   -   **Editar** - Permite-lhe editar o nome, o fabricante e o URL da aplicação selecionada.  
  
   -   **Remover** - Elimina a aplicação selecionada da lista.  
  
   -   **Importar** - Importa uma lista de aplicações especificadas num ficheiro de valores separados por vírgulas. Utilize o formato, o nome da aplicação, o fabricante e o URL da aplicação no ficheiro.  
  
2. Quando tiver terminado, clique em **Seguinte**.  
  
   Pode utilizar um dos seguintes relatórios para monitorizar aplicações compatíveis e não compatíveis:  
  
- **Lista de Aplicações e Dispositivos incompatíveis para um utilizador especificado** - apresenta informações sobre utilizadores e dispositivos que têm instaladas aplicações que não são compatíveis com uma política especificada por si.  
  
- **Resumo de Utilizadores com Aplicações Não Conformes** - Apresenta informações sobre utilizadores que têm instaladas aplicações que não são compatíveis com uma política especificada por si.  
  
  Para obter informações sobre como utilizar relatórios, veja [Relatórios do System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
###  <a name="compliant-and-noncompliant-apps-mac-os-x"></a>Aplicações compatíveis e incompatíveis (Mac OS X)  
 Permite-lhe especificar uma lista de aplicações Mac OS X que são compatíveis ou incompatíveis na sua empresa. Pode utilizar relatórios para apresentar dispositivos que tenham aplicações incompatíveis instaladas e o utilizador associado.  
  
 Não é possível especificar aplicações compatíveis e incompatíveis no mesmo item de configuração.  
  
#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Especificar a lista de aplicações compatíveis ou incompatíveis  
  
1. Na página **Aplicações Compatíveis e Não Compatíveis (Mac OS X)**, especifique as seguintes informações:  
  
   - **Lista de aplicações incompatíveis** - Selecione esta opção se pretende especificar uma lista de aplicações que serão comunicadas como incompatíveis se forem instaladas por utilizadores.  
  
   - **Lista de aplicações compatíveis** - Selecione esta opção se pretender especificar uma lista de aplicações que os utilizadores podem instalar. Quaisquer outras aplicações instaladas serão comunicadas como incompatíveis.  
  
   - **Adicionar** - Adiciona uma aplicação à lista selecionada. Especifique um nome à sua escolha, o publicador da aplicação (opcional) e o ID do pacote da aplicação.  
  
     > [!TIP]
     >  Para localizar o ID do pacote de uma aplicação, utilize os passos seguintes num computador Mac que tenha a aplicação instalada:  
     > 
     > 1. Abra a pasta na qual a aplicação está instalada (por exemplo, **/Applications**)  
     >    2.  Selecione o grupo _<App Name\>_**.app** e escolha **Mostrar Conteúdo do Pacote**  
     >    3.  Abra o ficheiro **Info.plist**  
     >    4.  Verifique o valor associado à chave **CFBundleIdentifier**  
     > 
     >    O formato do ID do pacote é **com.contoso.appname**  
  
   - **Editar** - Permite-lhe editar o nome, o publicador e o ID do pacote da aplicação selecionada.  
  
   - **Remover** - Elimina a aplicação selecionada da lista.  
  
   - **Importar** - Importa uma lista de aplicações especificadas num ficheiro de valores separados por vírgulas. Utilize o formato, o nome da aplicação, o publicador e o ID do pacote de aplicações no ficheiro.  
  
2. Quando tiver terminado, clique em **Seguinte**.  
  
   Pode utilizar um dos seguintes relatórios para monitorizar aplicações compatíveis e não compatíveis:  
  
- **Lista de Aplicações e Dispositivos incompatíveis para um utilizador especificado** - apresenta informações sobre utilizadores e dispositivos que têm instaladas aplicações que não são compatíveis com uma política especificada por si.  
  
- **Resumo de Utilizadores com Aplicações Não Conformes** - Apresenta informações sobre utilizadores que têm instaladas aplicações que não são compatíveis com uma política especificada por si.  
  
  Para obter informações sobre como utilizar relatórios, veja [Relatórios do System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
### <a name="ios-and-mac-os-x-custom-profile-settings"></a>Definições do perfil personalizado do iOS e do Mac OS X  
 Utilize **Perfis Personalizados do iOS e do Mac OS X** para implementar as definições criadas com a [Ferramenta Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) em dispositivos iOS e Mac OS X. Esta ferramenta permite criar muitas definições que controlam o funcionamento destes dispositivos e exportá-las para um perfil de configuração. Em seguida, pode importar este perfil de configuração para um perfil personalizado do iOS e do Mac OS X e implementar as definições em utilizadores e dispositivos na sua organização.  
  
> [!NOTE]  
>  Certifique-se de que as definições que exportar a partir da ferramenta Apple Configurator são compatíveis com a versão do iOS ou do Mac OS X nos dispositivos nos quais implementar o perfil. Para obter informações sobre como são resolvidas as definições incompatíveis, pesquise Configuration Profile Reference (Referência de Perfil de Configuração) e Mobile Device Management Protocol Reference (Referência do Protocolo de Gestão de Dispositivos Móveis) no site [Apple Developer](https://developer.apple.com/).  
  
#### <a name="to-create-an-ios-and-mac-os-x-custom-profile"></a>Criar um perfil personalizado do iOS e do Mac OS X  
  
1.  Na página **Configurar definições de perfil personalizado do iOS e do Mac OS X** do **Assistente de Criação de Item de Configuração**, especifique as seguintes informações:  
  
    -   **Nome do perfil de configuração personalizada (apresentado aos utilizadores)** -indique um nome para a política será apresentado no dispositivo e na configuração do Gestor de relatórios.  
  
    -   **Importar** - Escolha um ficheiro que tenha exportado a partir da ferramenta Apple Configurator.  
  
    -   **Detalhes do perfil de configuração** - Apresenta o ficheiro que importou.  
  
    -   **Remediar definições incompatíveis** -  
  
         Selecione se pretende resolver definições de configuração incompatíveis (quando suportadas).  
  
    -   **Gravidade de não conformidade para relatórios** - Especifica o nível de gravidade comunicado se esta política de conformidade for avaliada como não conforme. Os níveis de gravidade disponíveis são os seguintes:  
  
        > [!NOTE]  
        >  Quando um dispositivo Mac OS X está no modo de Suspensão, não é possível entregar ou inventariar políticas e perfis. Como resultado, consola do Configuration Manager poderá apresentar temporariamente o estado de definições de política em erro até a próxima vez que o dispositivo sair do modo de suspensão.  
  
        -   **Nenhum** dispositivos que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  
  
        -   **Informações** dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **informações** para relatórios do Configuration Manager.  
  
        -   **Aviso** dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **aviso** para relatórios do Configuration Manager.  
  
        -   **Crítico** dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **críticos** para relatórios do Configuration Manager.  
  
        -   **Crítico com evento** dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **críticos** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos da aplicação.  
  
#### <a name="how-to-create-a-configuration-profile-file"></a>Como criar um ficheiro de perfil de configuração  
 Pode criar o ficheiro de perfil de configuração utilizado pela política personalizada de duas formas:  
  
-   Exporte o ficheiro (com a extensão **.mobileconfig**) a partir da ferramenta Apple Configurator.  
  
-   Crie o ficheiro com o esquema adequado a partir da página [Apple Configuration Profile Key Reference (Referência de Chaves de Perfis de Configuração da Apple)](https://developer.apple.com/library/ios/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html).  
  
###  <a name="kiosk-mode-ios"></a>Modo de Local Público (iOS)  
 O modo Kiosk permite-lhe bloquear um dispositivo e permitir que apenas determinadas funcionalidades funcionem. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo ou para um dispositivo com a finalidade de desempenhar apenas uma função, como um dispositivo de ponto de venda.  
  
#### <a name="to-configure-kiosk-mode-for-ios-devices"></a>Configurar o modo de local público para dispositivos iOS  
  
1. Na página **Configurar Definições do Modo de Local Público para Dispositivos iOS** do **Assistente de Criação de Item de Configuração**, especifique as seguintes informações:  
  
   - **Selecionar Aplicação** - Selecione a aplicação que terá permissão para ser executada quando o dispositivo estiver no modo de local público. Não será permitida a execução de outras aplicações no dispositivo. Escolha entre:  
  
     - **Aplicação Gerida** – Clique em Procurar e, em seguida, selecione uma aplicação gerida.  
  
     - **Aplicação da Loja** – Especifique o URL de uma aplicação na loja de aplicações e, em seguida, clique em **Obter ID da Aplicação** para preencher o campo **ID da Aplicação**.  
  
       Para encontrar o URL da aplicação:  
  
     - Através de um motor de pesquisa, localize a aplicação que pretende utilizar na App Store do iTunes e abra a página da aplicação.  
  
     - Copie o URL da página e utilize-o como URL para especificar a aplicação que pretende executar no modo de local público.  
  
     - **Example:** Procure **Microsoft Word para iPad**. O URL que irá utilizar será **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  
  
   - **Toque** - Ativa ou desativa o ecrã tátil do dispositivo.  
  
   - **Rotação do ecrã** - Ativa ou desativa a mudança da orientação do ecrã ao rodar o dispositivo.  
  
   - **Botões de volume** - Ativa ou desativa a utilização dos botões de volume no dispositivo.  
  
   - **Comutador do toque** - Ativa ou desativa a alteração do toque (desativar som) no dispositivo.  
  
   - **Suspensão de ecrã e botão de reativação** - Ativa ou desativa o botão suspender/reativar ecrã do dispositivo.  
  
   - **Bloqueio automático** - Ativa ou desativa o bloqueio automático do dispositivo.  
  
   - **Áudio mono** - Ativa ou desativa a definição de acessibilidade **Áudio mono**.  
  
   - **Voice over** - Ativa ou desativa a definição de acessibilidade **VoiceOver** que lê em voz alta o texto no ecrã do dispositivo.  
  
   - **Ajustes do voice over** - Ativa ou desativa os ajustes do VoiceOver, o que lhe permite ajustar a função VoiceOver (por exemplo, a rapidez de leitura em voz alta do texto no ecrã).  
  
   - **Zoom** - Ativa ou desativa a definição de acessibilidade **Zoom**, o que lhe permite utilizar o toque para aplicar zoom no ecrã do dispositivo.  
  
   - **Ajustes de zoom** - Ativa ou desativa os ajustes de Zoom, o que lhe permite ajustar a função Zoom.  
  
   - **Inverter cores** - Ativa ou desativa a definição de acessibilidade **Inverter Cores** que ajusta o ecrã para ajudar utilizadores com deficiências visuais.  
  
   - **Inverter ajustes de cores** - Ativa ou desativa os ajustes da funcionalidade Inverter Cores, o que lhe permite ajustar a função Inverter Cores.  
  
   - **Toque de apoio** - Ativa ou desativa a definição de acessibilidade **Toque de apoio** que ajuda os utilizadores a executar gestos no ecrã que lhes poderão ser difíceis.  
  
   - **Ajustes do toque de apoio** - Ativa ou desativa os ajustes de toque de apoio, o que lhe permite ajustar a função de Toque de apoio.  
  
   - **Seleção de voz** - Ativa ou desativa a definição de acessibilidade **Enunciar Seleção** que lê em voz alta o texto que selecionou.  
  
   - **Remediar definições incompatíveis** - Selecione se pretende resolver definições de configuração incompatíveis (quando suportadas).  
  
   - **Gravidade de não conformidade para relatórios** - Especifica o nível de gravidade comunicado se esta política de conformidade for avaliada como não conforme. Os níveis de gravidade disponíveis são:  
  
     -   **Nenhum** dispositivos que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  
  
     -   **Informações** dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **informações** para relatórios do Configuration Manager.  
  
     -   **Aviso** dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **aviso** para relatórios do Configuration Manager.  
  
     -   **Crítico** dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **críticos** para relatórios do Configuration Manager.  
  
     -   **Crítico com evento** dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **críticos** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos da aplicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
