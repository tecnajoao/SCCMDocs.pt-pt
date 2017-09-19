---
title: "Como criar itens de configuração para dispositivos Windows Phone geridos com o Intune | Microsoft Docs"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df10dc4d-c9ff-4574-bb33-8d30eb14cfe3
caps.latest.revision: "13"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 092bb15e6c1d5cdfb5b8670ad46028a6daa49b8b
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/14/2017
---
# <a name="how-to-create-configuration-items-for-windows-phone-devices-managed-without-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para dispositivos Windows Phone geridos sem o cliente do System Center Configuration Manager
Utilizar o System Center Configuration Manager**Windows Phone** item de configuração para gerir as definições para dispositivos Windows Phone que são inscritos pelo Configuration Manager no Microsoft Intune ou geridos no local.  
  
### <a name="to-create-a-windows-phone-configuration-item"></a>Para criar um item de configuração do Windows Phone  
  
1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade**.  
  
2.  Na área de trabalho **Ativos e Conformidade** , expanda **Definições de Conformidade**e, em seguida, clique em **Itens de Configuração**.  
  
3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4.  Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5.  Em **especificar o tipo de item de configuração que pretende criar**, selecione **Windows Phone**.  
  
6.  Clique em **categorias** se criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  
  
7.  No **plataformas suportadas** página do assistente, selecione as plataformas específicas do Windows Phone que irão avaliar o item de configuração.  
  
8.  Na página **Definições do Dispositivo** do assistente, selecione o grupo de definições que pretende configurar. Veja [Referência das definições do item de configuração do Windows Phone](#BKMK_Setref) neste tópico para obter detalhes e clique em **Seguinte**.  
  
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
  
##  <a name="windows-phone-configuration-item-settings-reference"></a>Referência das definições do item de configuração do Windows Phone  
  
### <a name="password"></a>Palavra-passe  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos**|Exigir uma palavra-passe em dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|O comprimento mínimo da palavra-passe.|  
|**Expiração da palavra-passe em dias**|O número de dias antes de uma palavra-passe tem de ser alterado.|  
|**Número de palavras-passe memorizadas**|Impede a reutilização de palavras-passe.|  
|**Número de tentativas de início de sessão falhadas antes de o dispositivo ser apagado**|Apaga o dispositivo em caso de falha deste número de tentativas de início de sessão.|  
|**Complexidade de palavra-passe**|Escolher se pretende especificar um PIN como "1234" ou se tem de fornecer uma palavra-passe segura.|  
|**Enviar PIN de recuperação da palavra-passe para o Exchange Server**||  
  
### <a name="device"></a>Dispositivo  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Captura de ecrã**|Permitir que o utilizador tirar uma captura de ecrã do ecrã do dispositivo.<br /><br /> (Apenas Windows Phone 8.1)|  
|**Submissão de dados de diagnóstico**|Permitir a submissão de ficheiros de registo de aplicações.|  
|**Geolocalização**|Permitir que o dispositivo utilize informações dos serviços de localização.<br /><br /> (Apenas Windows Phone 8.1)|  
|**Copiar e Colar**|Utilizar a ação copiar e colar para transferir dados entre aplicações.<br /><br /> (Apenas Windows Phone 8.1)|  
|**Bluetooth**|Permite a utilização da funcionalidade Bluetooth do dispositivo.|  
  
### <a name="email-management"></a>Gestão de e-mail  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**E-mail POP e IMAP**|Permite a ligação a contas de e-mail que utilizam as normas POP e IMAP.|  
|**Tempo máximo para guardar e-mail**|Durante quanto tempo guardar o e-mail antes de este ser eliminado do servidor.|  
|**Formatos de mensagem permitidos**|Especificar se os e-mails dos utilizadores podem ser HTML ou apenas em texto simples.|  
|**Tamanho máximo de correio eletrónico com texto simples (transferido automaticamente)**|Controla o tamanho máximo de e-mail com texto simples quando transferidos automaticamente.|  
|**Tamanho máximo de e-mail HTML (transferido automaticamente)**|Controla o tamanho máximo de e-mails HTML quando transferidos automaticamente.|  
|**Tamanho máximo de um anexo (transferido automaticamente)**|Configura o tamanho máximo de e-mail que será transferido automaticamente.|  
|**Sincronização de calendário**||  
|**Conta de e-mail personalizada**|Permitir a utilização de uma conta não Microsoft no dispositivo.|  
|**Tornar a Conta Microsoft opcional na aplicação Windows Mail**|Não necessitam de utilização de uma conta Microsoft para iniciar sessão no Windows Mail.|  
  
### <a name="store"></a>Arquivo  
 Estas definições aplicam-se apenas a dispositivos Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Loja de aplicações**|Permite o acesso à loja de aplicações no dispositivo.|  
  
### <a name="browser"></a>Browser  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Permitir browser**|Ativar ou desativar o browser de Internet predefinido.|  
|**Preenchimento automático**|O utilizador pode alterar as definições de conclusão automática no browser.|  
|**Scripting ativo**|O browser pode executar scripts, como scripts do Active X.|  
|**Plug-ins**|O utilizador pode adicionar plug-ins ao Internet Explorer.|  
|**Bloqueador de janelas pop-up**|Ativa ou desativa o bloqueador de janelas pop-up do browser.|  
|**Aviso de fraude**|Ativar ou desativar avisos de sites potencialmente fraudulentos.|  
  
### <a name="internet-explorer"></a>Internet Explorer  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Enviar sempre cabeçalho Não Controlar**|Impede que as informações de navegação sejam enviadas para sites de terceiros.|  
|**Zona de segurança da intranet**||  
|**Nível de segurança da zona de Internet**|Configurar o nível de segurança da zona de Internet.|  
|**Nível de segurança da zona de intranet**|Configurar o nível de segurança da zona de intranet.|  
|**Nível de segurança da zona de sites fidedignos**|Configurar o nível de segurança da zona de sites fidedignos.|  
|**Nível de segurança da zona de sites restritos**|Configurar o nível de segurança da zona de sites restritos.|  
|**Espaços de nomes da zona de intranet**||  
|**Ir para o site da intranet para introdução de uma única palavra**|Ativa ou desativa a definição que permite ao Internet Explorer aceder automaticamente a um site de intranet se for introduzido um nome de site válido sem HTTP: precedente|  
|**Opção de menu do modo de empresa**|Permitir que os utilizadores ativem e desativem o Modo de Empresa a partir do menu **Ferramentas** do Internet Explorer.|  
|**Localização do relatório de registo (URL)**|Especificar um URL onde os sites visitados serão registados quando o Modo de Empresa estiver ativo.|  
|**Localização (URL) da lista de sites do Modo de Empresa**|Especificar a localização da lista de sites que utilizarão o Modo de Empresa quando este está ativo.|  
  
### <a name="cloud"></a>Nuvem  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Sincronização de definições**|Permite a sincronização de definições entre dispositivos.|  
|**Sincronização de credenciais**|Permite a sincronização de credenciais entre dispositivos.|  
|**Conta Microsoft**|Permitir a utilização de uma conta Microsoft no dispositivo.<br /><br /> (Apenas Windows Phone 8.1)|  
|**Sincronização de definições através de ligações com tráfego limitado**|Permitir a sincronização de definições quando a ligação à Internet tem tráfego limitado.|  
  
### <a name="security"></a>Segurança  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Instalação de ficheiros não atribuídos**|Permite o carregamento de ficheiros não atribuídos.|  
|**Aplicações não atribuídas**|Permite o carregamento de aplicações não atribuídas.|  
|**Mensagens de SMS e MMS**|Permitir o envio de mensagens SMS e MMS a partir do dispositivo.|  
|**Armazenamento amovível**|Permitir a utilização de armazenamento amovível, como um cartão SD, no dispositivo.|  
|**Câmara**|Permitir a utilização da câmara do dispositivo.|  
|**Comunicação de proximidade (NFC)**|Permitir a comunicação através de NFC no dispositivo.<br /><br /> (Apenas Windows Phone 8.1)|  
|**Permitir ligação USB**|Permita periféricos ligar a este dispositivo através de USB.|
  
### <a name="peak-synchronization"></a>Sincronização de pico  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Especificar a hora de ponta**|Especifique uma janela de tempo que será utilizado por duas definições seguintes.|  
|**Frequência de sincronização dentro do período de ponta**|Escolha com que frequência o dispositivo irá sincronizar durante o período de pico que especificou.|  
|**Frequência de sincronização fora do período de ponta**|Escolha com que frequência o dispositivo irá sincronizar fora da hora de pico que especificou.|  
  
### <a name="roaming"></a>Roaming  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Gestão de dispositivos no modo de roaming**|Permite que o dispositivo seja gerido pelo Configuration Manager quando estiver em roaming.|  
|**Transferência de software em roaming**|Permite a transferência de aplicações e de software quando está em roaming.|  
|**Transferência de e-mail em roaming**|Permite as transferências de e-mail quando está em roaming.|  
|**Roaming de dados**|Permitir roaming entre redes ao aceder a dados.|  
  
### <a name="encryption"></a>Encriptação  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Encriptação do cartão de armazenamento**|Exigir a encriptação de cartões de armazenamento utilizados com o dispositivo.|  
|**Encriptação de ficheiros no dispositivo**|Necessita que os ficheiros no dispositivo móvel sejam encriptados.|  
|**Exigir assinatura de e-mail**|Requer que os e-mails sejam assinados antes de serem enviados.|  
|**Algoritmo de assinatura**|Selecione o algoritmo utilizado para assinar e-mails.|  
|**Exigir encriptação de correio eletrónico**|Requer que os e-mails sejam encriptados antes de serem enviados.|  
|**Algoritmo de encriptação**|Selecione o algoritmo utilizado para encriptar e-mails.|  
  
###  <a name="wireless-communications"></a>Comunicações sem fios  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Ligação de rede sem fios**|Ativar ou desativar a funcionalidade Wi-Fi dos dispositivos.|  
|**Tethering Wi-Fi**|Permite que os utilizadores utilizem o dispositivo como um hotspot móvel.|  
|**Descarregar dados para Wi-Fi quando possível**||  
|**Relatórios de hotspots de Wi-Fi**||  
  
##### <a name="to-configure-a-wireless-network-connection"></a>Para configurar uma ligação de rede sem fios  
  
1.  Na página **Configurar definições da comunicação sem fios do dispositivo móvel**, clique em **Adicionar**.  
  
2.  Na caixa de diálogo **Ligação de Rede sem Fios**, especifique as seguintes informações acerca da ligação sem fios que será aprovisionada em dispositivos móveis:  
  
|Definição|Mais informações|  
|-------------|----------------------|  
|**Nome da rede (SSID)**||  
|**Ligação de rede**|Escolha entre **Internet** ou **Trabalho**.|  
|**Autenticação**|Para o método de autenticação para a ligação sem fios escolha entre:<br><br> - **Abrir**<br> - **Partilhado**<br> - **WPA**<br> - **WPA-PSK**<br> - **WPA2**<br> - **WPA2 PSK**|  
|**Encriptação de dados**|Escolha o método de encriptação utilizado por esta ligação. Os valores que pode selecionar serão diferentes consoante o método de **Autenticação** que selecionou:<br><br> - **Desativado**<br> - **WEP**<br> - **TKIP**<br> - **AES**|  
|**Índice de chaves**|Selecione um índice de chaves de **1** a **4** , que será utilizado com uma definição de **Encriptação de dados** de **WEP**.|  
|**Esta rede liga-se à Internet**|Selecione esta opção se quiser fornecer definições proxy que permitam que dispositivos móveis numa ligação sem fios se liguem à Internet.|  
|**Definições do servidor proxy**|Especificar conforme necessário as definições **Servidor** e **Porta** para **HTTP**, **WAP** e **Sockets**.|  
|**Ativar o acesso à rede 802.1X**|Selecionar esta opção se pretender assegurar a ligação ao especificar um tipo EAP.|  
|**Tipo EAP**|Escolher o tipo EAP a utilizar entre:<br><br> - **PEAP**<br> - **Smart card ou certificado**|  
    
  
###  <a name="certificates"></a>Certificados  
 Permite-lhe importar certificados para instalar em dispositivos móveis.  
  
 Clique em **Importar** e, em seguida, especifique os seguintes valores:  
  
-   **Ficheiro de certificado** – clique em **procurar** e, em seguida, selecione o ficheiro de certificado com a extensão **. cer** que pretende importar.  
  
-   **Arquivo de destino** – selecione um ou mais arquivos de destino onde o certificado importado será adicionado no dispositivo móvel de entre:  
  
    -   **Raiz**  
  
    -   **AC**  
  
    -   **Normal**  
  
    -   **Com privilégios**  
  
    -   **SPC**  
  
    -   **Ponto a ponto**  
  
-   **Função** – se **SPC** (Software Publisher Certificate) estiver selecionado como arquivo de destino, escolha a função que será associada ao certificado de entre:  
  
    -   **Operadora de rede móvel**  
  
    -   **Gestor**  
  
    -   **Utilizador autenticado**  
  
    -   **Administrador de TI**  
  
    -   **Utilizador não autenticado**  
  
    -   **Servidor de aprovisionamento fidedigno**  
  
### <a name="system-security"></a>Segurança do sistema  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Controlo de Conta de Utilizador**|Ativa ou desativa o Controlo de Conta de Utilizador do Windows no dispositivo.|  
|**Firewall da rede**|Ativa ou desativa a Firewall do Windows.|  
|**Atualizações**|Escolha como as atualizações de software do Windows serão transferidas para os computadores. Por exemplo, pode transferir as atualizações automaticamente mas permitir que o utilizador decida quando as instalar.|  
|**Classificação mínima de atualizações**|Escolha a classificação mínima de atualizações que será transferida para computadores Windows: **Nenhuma**, **Importante**ou **Recomendadas**.|  
|**SmartScreen**|Ativar ou desativar o Windows Smart Screen.|  
|**Proteção contra vírus**|Certifique-se de que o dispositivo está protegido por software antivírus|  
|**As assinaturas da proteção contra vírus estão atualizadas**|Certifique-se de que as assinaturas de software antivírus estão atualizadas.|
|**Permitir anular inscrições**|Vamos o utilizador de remover o dispositivo de MDM.|  
  
### <a name="windows-server-work-folders"></a>Pastas de Trabalho do Windows Server  
 Estas definições se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**URL das Pastas de Trabalho**|Configura a localização de uma pasta de trabalho do Windows Server a que os utilizadores podem ligar a partir do respetivo dispositivo.|  
  
### <a name="allowed-and-blocked-apps-list-windows-phone-81-only"></a>Lista de aplicações permitidas e bloqueadas (apenas Windows Phone 8.1)  
 Permite-lhe especificar uma lista de aplicações Windows Phone que estão em conformidade ou não conformes com a sua empresa. As aplicações que especifica como bloqueadas não podem ser instaladas pelos utilizadores. Se especificar uma lista de aplicações permitidas, os utilizadores só podem instalar as aplicações na lista.  
  
 Não é possível especificar ambas aplicações permitidas e bloqueadas no mesmo item de configuração.  
  
> [!IMPORTANT]  
>  Se especificar uma lista de aplicações permitidas, tem de garantir que a aplicação do portal da empresa e quaisquer aplicações implementadas em dispositivos Windows Phone 8.1 estão no **permitidos** lista de aplicações.  
  
##### <a name="to-specify-an-allowed-or-blocked-apps-list"></a>Para especificar uma lista de aplicações permitidas ou bloqueadas  
  
1.  No **lista de aplicações permitidas e bloqueadas (Windows Phone 8.1)** página, especifique as seguintes informações:  
  
|||  
|-|-|  
|Definição|Mais informações|  
|**Lista de aplicações bloqueadas**|Selecione esta opção se pretender especificar uma lista de aplicações que os utilizadores não poderão instalar.|  
|**Lista de aplicações permitidas**|Selecione esta opção se pretender especificar uma lista de aplicações que os utilizadores podem instalar.|  
|**Adicionar**|Adiciona uma aplicação à lista selecionada. Especifique um nome à sua escolha, o fabricante da aplicação (opcional) e o URL para a aplicação na loja de aplicações.<br /><br /> Para especificar o URL, na página da Loja do Windows Phone, procure a aplicação que pretende utilizar.<br /><br /> **Exemplo:** Procure na loja a **Skype** aplicação. O URL a utilizar será: http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51.<br /><br /> Para a aplicação portal da empresa ou linha de negócio, não é necessário especificar um URL completo, apenas o GUID da aplicação.|  
|**Editarar**|Permite-lhe editar o nome, o fabricante e o URL da aplicação selecionada.|  
|**Remove**|Elimina a aplicação selecionada da lista.|  
|**Importarar**|Importa uma lista de aplicações especificadas num ficheiro de valores separados por vírgulas. Utilize o formato, o nome da aplicação, o fabricante e o URL da aplicação no ficheiro.|  
  
## <a name="see-also"></a>Consulte Também  
 [Itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)