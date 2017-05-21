---
title: "Criar itens de configuração para Windows 8.1 e Windows 10 dispositivos geridos com o Intune | Documentos do Microsoft"
description: "Utilize o item de configuração do System Center Configuration Manager Windows 10 para gerir as definições para computadores Windows 10."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
caps.latest.revision: 20
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: f75bac7887772119f30654fe15c16a8f993cad75
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-configuration-items-for-windows-81-and-windows-10-devices-managed-without-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para os dispositivos Windows 8.1 e Windows 10 geridos sem o cliente System Center Configuration Manager
||  
|-|  
|Este artigo contém informações sobre [nova funcionalidade introduzida na versão 1602](https://technet.microsoft.com/library/mt622084.aspx) do System Center Configuration Manager \(ramo atual\). Para utilizar a nova funcionalidade, terá de [instalar a atualização 1602](https://technet.microsoft.com/library/mt607046.aspx). Se não terem sido atualizados para a versão mais recente do Configuration Manager, pode [transferir a documentação da versão utilizar](https://gallery.technet.microsoft.com/Documentation-for-System-ea90eaf1) na galeria do TechNet.|  
  
 Utilizar o System Center Configuration Manager**Windows 8.1 e Windows 10** item de configuração para gerir as definições para o Windows 8.1 e dispositivos Windows 10 inscritos no Microsoft Intune ou no local gerido pelo Configuration Manager.  
  
### <a name="to-create-a-windows-81-and-windows-10-configuration-item"></a>Criar um item de configuração do Windows 8.1 e do Windows 10  
  
1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade**.  
  
2.  Na área de trabalho **Ativos e Conformidade** , expanda **Definições de Conformidade**e, em seguida, clique em **Itens de Configuração**.  
  
3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4.  Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5.  Em **Especifique o tipo de item de configuração que pretende criar**, selecione **Windows 8.1 e Windows 10**.  
  
6.  Clique em **categorias** se pode criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  
  
7.  Na página **Plataformas Suportadas** do assistente, selecione as plataformas específicas do Windows que irão avaliar o item de configuração.  
  
8.  Na página **Definições do Dispositivo** do assistente, selecione o grupo de definições que pretende configurar. Veja [Referência de definições do item de configuração Windows 8.1 e Windows 10](#BKMK_Setref) deste tópico para obter detalhes e, em seguida, clique em **Seguinte**.  
  
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
  
 Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade**.  
  
##  <a name="windows-81-and-windows-10-configuration-item-settings-reference"></a>Referência de definições do item de configuração do Windows 8.1 e do Windows 10  
  
### <a name="password"></a>Palavra-passe  
 Estas definições destinam-se apenas a dispositivos com o Windows 10 e posterior.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos**|Exigir uma palavra-passe em dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|O comprimento mínimo da palavra-passe.|  
|**Expiração da palavra-passe em dias**|O número de dias antes de uma palavra-passe tem de ser alterado.|  
|**Número de palavras-passe memorizadas**|Impede a reutilização de palavras-passe.|  
|**Número de tentativas de início de sessão falhadas antes de o dispositivo ser apagado**|Apaga o dispositivo em caso de falha deste número de tentativas de início de sessão.|  
|**Tempo de inatividade antes do dispositivo está bloqueado**|Especifique o período que um dispositivo pode ficar inativo (sem intervenção do utilizador) antes de ser bloqueado.|  
|**Complexidade de palavra-passe**|Escolher se pretende especificar um PIN como "1234" ou se tem de fornecer uma palavra-passe segura.|  
|**Qualidade da palavra-passe**|Selecionar o nível de complexidade da palavra-passe exigido e se podem ser utilizados dispositivos biométricos.|  
|**Enviar PIN de recuperação da palavra-passe para o Exchange Server**||  
  
###  <a name="device"></a>Dispositivo  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Captura de ecrã**|Permite-lhe tirar uma captura de ecrã do ecrã do dispositivo.<br /><br /> (Apenas no Windows 10)|  
|**Submissão de dados de diagnóstico**|Permitir a submissão de ficheiros de registo de aplicações.<br /><br /> (Apenas no Windows 8.1)|  
|**Submissão de dados de diagnóstico (Windows 10)**|Permitir a submissão de ficheiros de registo de aplicações.<br /><br /> (Apenas no Windows 10)|  
|**Geolocalização**|Permitir que o dispositivo utilize informações dos serviços de localização.<br /><br /> (Apenas no Windows 10)|  
|**Copiar e Colar**|Utilizar a ação copiar e colar para transferir dados entre aplicações.<br /><br /> (Apenas no Windows 10)|
|**Reposição de fábrica**|Permite ao utilizador final repor o dispositivo para as respetivas definições iniciais.<br /><br /> (Apenas no Windows 10)|  
|**Bluetooth**|Permitir a utilização de dispositivos com funcionalidades Bluetooth.|  
|**Modo detetável Bluetooth**|Permitir que o dispositivo seja detetados por outros dispositivos Bluetooth.<br /><br /> (Apenas no Windows 10)|  
|**Publicidade Bluetooth**|Permita a utilização de publicidade do Bluetooth.<br /><br /> (Apenas no Windows 10)|  
|**Gravação de voz**|Permita a utilização de funcionalidades de gravação de voz do dispositivo.<br /><br /> (Apenas no Windows 10)|
|**Cortana**|Permita a utilização do Assistente de voz Cortana.<br /><br /> (Apenas no Windows 10)|
|**Notificações de centro de ação**|Ativar ou desativar o painel de notificação no Windows 10. <br /><br /> (Apenas no Windows 10)|
  
### <a name="email-management"></a>Gestão de e-mail  
 Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**E-mail POP e IMAP**|Permite a ligação a contas de e-mail que utilizam as normas POP e IMAP.|  
|**Tempo máximo para guardar e-mail**|Durante quanto tempo guardar o e-mail antes de este ser eliminado do servidor.|  
|**Formatos de mensagem permitidos**|Especificar se os e-mails dos utilizadores podem ser HTML ou apenas em texto simples.|  
|**Tamanho máximo de correio eletrónico com texto simples (transferido automaticamente)**|Controla o tamanho máximo de e-mail com texto simples quando transferidos automaticamente.|  
|**Tamanho máximo de e-mail HTML (transferido automaticamente)**|Controla o tamanho máximo de e-mails HTML quando transferidos automaticamente.|  
|**Tamanho máximo de um anexo (transferido automaticamente)**|Configura o tamanho máximo de e-mail que será transferido automaticamente.|  
|**Sincronização de calendário**|Permite a sincronização de calendários no dispositivo.|  
|**Conta de e-mail personalizada**|Permitir a utilização de uma conta não Microsoft no dispositivo.|  
|**Tornar a Conta Microsoft opcional na aplicação Windows Mail**|Permite configurar esta opção para remover o requisito de uma conta Microsoft no Windows Mail.|  
  
### <a name="store"></a>Arquivo  
 Estas definições destinam-se apenas a dispositivos com o Windows 10 e posterior.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Loja de aplicações**|Permite o acesso à loja de aplicações no dispositivo.|  
|**Introduzir uma palavra-passe para aceder à loja de aplicações**|Os utilizadores têm de introduzir uma palavra-passe para aceder à loja de aplicações.|  
|**Compras via aplicação**|Permite que os utilizadores façam compras via aplicação.|  
  
### <a name="browser"></a>Browser  
 Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Permitir browser**|Permite a utilização do browser no dispositivo.|  
|**Preenchimento automático**|O utilizador pode alterar as definições de conclusão automática no browser.|  
|**Scripting ativo**|O browser pode executar scripts, como scripts do Active X.|  
|**Plug-ins**|O utilizador pode adicionar plug-ins ao Internet Explorer.|  
|**Bloqueador de janelas pop-up**|Ativa ou desativa o bloqueador de janelas pop-up do browser.|  
|**Cookies**|Permitir que os cookies sejam guardados no dispositivo.|  
|**Aviso de fraude**|Ativar ou desativar avisos de sites potencialmente fraudulentos.|  
  
###  <a name="internet-explorer"></a>Internet Explorer  
 Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Enviar sempre cabeçalho Não Controlar**|Impede que as informações de navegação sejam enviadas para sites de terceiros.|  
|**Zona de segurança da intranet**|Permite atribuir um nível de segurança para a zona de segurança da Intranet.|  
|**Lever de segurança da zona de Internet**|Configurar o nível de segurança da zona de Internet.|  
|**Nível de segurança da zona de intranet**|Configurar o nível de segurança da zona de intranet.|  
|**Nível de segurança da zona de sites fidedignos**|Configurar o nível de segurança da zona de sites fidedignos.|  
|**Nível de segurança da zona de sites restritos**|Configurar o nível de segurança da zona de sites restritos.|  
|**Espaços de nomes da zona de intranet**|Permite configurar Websites que irão ser adicionados ou removidos da zona da intranet.|  
|**Ir para o site da intranet para introdução de uma única palavra**|Ativa ou desativa a definição que permite ao Internet Explorer aceder automaticamente a um site de intranet se for introduzido um nome de site válido sem HTTP: precedente|  
|**Opção de menu modo empresarial**|Permitir que os utilizadores ativem e desativem o Modo de Empresa a partir do menu **Ferramentas** do Internet Explorer.|  
|**Localização do relatório de registo (URL)**|Especificar um URL onde os sites visitados serão registados quando o Modo de Empresa estiver ativo.|  
|**Localização (URL) da lista de sites do Modo de Empresa**|Especificar a localização da lista de sites que utilizarão o Modo de Empresa quando este está ativo.|  
  
###  <a name="cloud"></a>Nuvem  
 Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.  
  
|Nome da definição|Detalhes|Windows 8,1|Windows 10|  
|------------------|-------------|-----------------|----------------|  
|**Sincronização de definições**|Permite a sincronização de definições entre dispositivos.|Sim|Sim|  
|**Sincronização de credenciais**|Permite a sincronização de credenciais entre dispositivos.|Sim|Sim|  
|**Conta Microsoft**|Permitir a utilização de uma conta Microsoft no dispositivo.|Sim|Sim|  
|**Sincronização de definições através de ligações com tráfego limitado**|Permitir a sincronização de definições quando a ligação à Internet tem tráfego limitado.|Sim|Sim|  
  
###  <a name="security"></a>Segurança  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Instalação de ficheiros não atribuídos**|Permite o carregamento de ficheiros não atribuídos.<br /><br /> (Apenas no Windows 10)|  
|**Aplicações não atribuídas**|Permite o carregamento de aplicações não atribuídas.<br /><br /> (Apenas no Windows 10)|  
|**Mensagens de SMS e MMS**|Permitir o envio de mensagens SMS e MMS a partir do dispositivo.<br /><br /> (Apenas no Windows 10)|  
|**Armazenamento amovível**|Permitir a utilização de armazenamento amovível, como um cartão SD, no dispositivo.<br /><br /> (Apenas no Windows 10)|  
|**Câmara**|Permitir a utilização da câmara do dispositivo.<br /><br /> (Apenas no Windows 10)|  
|**Comunicação de proximidade (NFC)**|Permitir a comunicação através de NFC no dispositivo.<br /><br /> (Apenas no Windows 10)|  
|**Modo antiTheft**|Controla se o modo Anti-roubo do Windows 10 está ativado.<br /><br /> (Apenas no Windows 10)|  
|**Permitir ligação USB**|Esta definição permite aos dispositivos que ligar neste dispositivo com uma ligação de USB.<br /><br /> (Apenas no Windows 10)|
|**Ficheiro de perfil**|Aprovisiona um perfil VPN para dispositivos Windows RT.<br /><br /> (Apenas no Windows 8.1)|  
|**Nome do perfil**|Aprovisiona um perfil VPN para dispositivos Windows RT.<br /><br /> (Apenas no Windows 8.1)|  
|**Perfil para todos os utilizadores**|Aprovisiona um perfil VPN para dispositivos Windows RT.<br /><br /> (Apenas no Windows 8.1)|  
  
###  <a name="peak-synchronization"></a>Sincronização de pico  
 Estas definições destinam-se apenas a dispositivos com o Windows 10 e posterior.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Especificar a hora de ponta**|Permite configurar a hora de pico de sincronização do dispositivo móvel.|  
|**Frequência de sincronização dentro do período de ponta**|Configura a frequência de sincronização durante as horas de pico que configurou.|  
|**Frequência de sincronização fora do período de ponta**|Permite configurar a frequência de sincronização fora das horas de pico que configurou.|  
  
###  <a name="roaming"></a>Roaming  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Gestão de dispositivos no modo de roaming**|Permite que o dispositivo para serem geridos pelo Configuration Manager quando este estiver em roaming.<br /><br /> (Apenas no Windows 10)|  
|**Transferência de software em roaming**|Permite a transferência de aplicações e de software quando está em roaming.<br /><br /> (Apenas no Windows 10)|  
|**Transferência de e-mail em roaming**|Permite as transferências de e-mail quando está em roaming.<br /><br /> (Apenas no Windows 10)|  
|**Roaming de dados**|Permitir roaming entre redes ao aceder a dados.| 
|**VPN por rede móvel**|Permite que as ligações do dispositivo acesso VPN quando ligado a uma rede celular.<br /><br /> (Apenas no Windows 10)|
|**VPN roaming por rede móvel**|Esta definição permite ligações de VPN de acesso de dispositivo em roaming numa rede celular.<br /><br /> (Apenas no Windows 10)| 
  
###  <a name="encryption"></a>Encriptação  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Encriptação do cartão de armazenamento**|Exigir a encriptação de cartões de armazenamento utilizados com o dispositivo.<br /><br /> (Apenas no Windows 10)|  
|**Encriptação de ficheiros no dispositivo**|Requer que os ficheiros no dispositivo estejam encriptados.|  
|**Exigir assinatura de e-mail**|Requer que os e-mails sejam assinados antes de serem enviados.|  
|**Algoritmo de assinatura**|Selecione o algoritmo de assinatura para assinar mensagens de correio eletrónico.|  
|**Exigir encriptação de correio eletrónico**|Requer que os e-mails sejam encriptados antes de serem enviados.|  
|**Algoritmo de encriptação**|Selecione o algoritmo de encriptação de mensagens de correio eletrónico.|  
  
###  <a name="wireless-communications"></a>Comunicações sem fios  
 Estas definições destinam-se apenas a dispositivos com o Windows 10 e posterior.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Ligação de rede sem fios**|Ativar ou desativar a funcionalidade Wi-Fi dos dispositivos.|  
|**Tethering Wi-Fi**|Permite que os utilizadores utilizem o dispositivo como um hotspot móvel.|  
|**Descarregar dados para Wi-Fi quando possível**|Configure esta opção para utilizar a ligação Wi-Fi no dispositivo sempre que possível.|  
|**Relatórios de hotspots de Wi-Fi**||  
|**Configuração de Wi-Fi manual**||  
  
#### <a name="to-configure-a-wireless-network-connection"></a>Para configurar uma ligação de rede sem fios  
  
1.  Na página **Configurar definições da comunicação sem fios do dispositivo móvel**, clique em **Adicionar**.  
  
2.  Na caixa de diálogo **Ligação de Rede sem Fios**, especifique as seguintes informações acerca da ligação sem fios que será aprovisionada em dispositivos móveis:  
  
|Definição|Mais informações|  
|-------------|----------------------|  
|**Nome da rede (SSID)**|Permite introduzir o nome da rede Wi-Fi.|  
|**Ligação de rede**|Escolha entre **Internet** ou **Trabalho**.|  
|**Autenticação**|Para o método de autenticação para a ligação sem fios escolha entre:<br /><br /> - **Abrir**<br /><br /> - **Partilhado**<br /><br /> - **WPA**<br /><br /> - **WPA PSK**<br /><br /> - **WPA2**<br /><br /> - **WPA2 PSK**|  
|**Encriptação de dados**|Escolha o método de encriptação utilizado por esta ligação. Os valores que pode selecionar serão diferentes consoante o método de **Autenticação** que selecionou:<br /><br /> - **Desativado**<br /><br /> - **WEP**<br /><br /> - **TKIP**<br /><br /> - **AES**|  
|**Índice de chaves**|Selecione um índice de chaves de **1** a **4** , que será utilizado com uma definição de **Encriptação de dados** de **WEP**.|  
|**Esta rede liga-se à Internet**|Selecione esta opção se quiser fornecer definições proxy que permitam que dispositivos móveis numa ligação sem fios se liguem à Internet.|  
|**Definições do servidor proxy**|Especificar conforme necessário as definições **Servidor** e **Porta** para **HTTP**, **WAP** e **Sockets**.|  
|**Ativar o acesso à rede 802.1X**|Selecionar esta opção se pretender assegurar a ligação ao especificar um tipo EAP.|  
|**Tipo EAP**|Escolher o tipo EAP a utilizar entre:<br /><br /> - **PEAP**<br> - **Smart card ou certificado**|  
  
  
  
### <a name="certificates"></a>Certificados  
 Permite-lhe importar certificados para instalar em dispositivos móveis.  
  
 Clique em **Importar** e, em seguida, especifique os seguintes valores:  
  
-   **Ficheiro de certificado** – Clique em Procurar e, em seguida, selecione o ficheiro de certificado com a extensão **.cer** que pretende importar.  
  
-   **Arquivo de destino** – selecione um ou mais arquivos de destino onde o certificado importado será adicionado no dispositivo móvel de entre:  
  
    -   **Raiz**  
  
    -   **AC**  
  
    -   **Normal**  
  
    -   **Com privilégios**  
  
    -   **SPC**  
  
    -   **Ponto a ponto**  
  
-   **Função** – se **SPC** (Software Publisher Certificate) estiver selecionado como arquivo de destino, escolha a função que será associada ao certificado de entre:  
  
    -   **Operadora de rede**  
  
    -   **Gestor de**  
  
    -   **Utilizador autenticado**  
  
    -   **Administrador de TI**  
  
    -   **Utilizador não autenticado**  
  
    -   **Aprovisionamento de servidor fidedigno**  
  
### <a name="system-security"></a>Segurança do sistema  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Controlo de Conta de Utilizador**|Ativa ou desativa o Controlo de Conta de Utilizador do Windows no dispositivo.|  
|**Firewall da rede**|Ativa ou desativa a Firewall do Windows.<br /><br /> (Apenas no Windows 8.1)|  
|**Atualizações (Windows 8.1 e anterior)**|Escolha como as atualizações de software do Windows serão transferidas para os computadores. Por exemplo, pode transferir as atualizações automaticamente mas permitir que o utilizador decida quando as instalar.|  
|**Classificação mínima de atualizações**|Escolha a classificação mínima de atualizações que será transferida para computadores Windows: **Nenhuma**, **Importante**ou **Recomendadas**.|  
|**Atualizações (Windows 10)**|Escolha como as atualizações de software do Windows serão transferidas para os computadores. Por exemplo, pode transferir as atualizações automaticamente mas permitir que o utilizador decida quando as instalar.<br /><br /> (Apenas no Windows 10)|  
|**Instalar o dia**|Escolha o dia em que as atualizações serão instaladas.<br /><br /> (Apenas no Windows 10)|  
|**Hora de instalação**|Escolha o hora em que as atualizações serão instaladas.<br /><br /> (Apenas no Windows 10)|  
|**SmartScreen**|Ativar ou desativar o Windows Smart Screen.|  
|**Proteção contra vírus**|Selecione para se certificar de que o software antivírus está instalado no dispositivo.|  
|**As assinaturas da proteção contra vírus estão atualizadas**|Selecione esta opção para garantir que os ficheiros de assinatura antivírus estão atualizados.|  
|**Funcionalidades da versão de pré-lançamento**|Permite à Microsoft implementar funcionalidades e definições de pré-lançamento no dispositivo.<br /><br /> (Apenas no Windows 10)|  
|**Instalação do certificado de raiz manual**|(Apenas no Windows 10)| 
|**Permitir manual unenrollment**|Permite que o utilizador anular a inscrição próprios da gestão por uma solução MDM.| 
  
###  <a name="windows-server-work-folders"></a>Pastas de Trabalho do Windows Server  
 Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**URL das Pastas de Trabalho**|Configura a localização de uma pasta de trabalho do Windows Server a que os utilizadores podem ligar a partir do respetivo dispositivo.|  
  
### <a name="allowed-and-blocked-apps-windows-phone-only"></a>Aplicações permitidas e bloqueadas (apenas no Windows Phone)  
 Permite-lhe especificar uma lista de aplicações geridas pelo Intune que são compatíveis ou incompatíveis com a sua empresa. O Windows Phone pode permitir ou bloquear a instalação destas aplicações.  
  
 Não é possível especificar aplicações compatíveis e incompatíveis no mesmo item de configuração.  
  
#### <a name="to-specify-apps-that-will-be-allowed-or-blocked"></a>Especificar aplicações que serão permitidas ou bloqueadas  
  
1.  Na página **Lista de Aplicações Permitidas e Bloqueadas**, especifique as seguintes informações:  
  
    |Definição|Mais informações|  
    |-------------|----------------------|  
    |**Lista de aplicações bloqueadas**|Selecione esta opção se pretende especificar uma lista de aplicações que os utilizadores não podem instalar.|  
    |**Lista de aplicações permitidas**|Selecione esta opção se pretender especificar uma lista de aplicações que os utilizadores podem instalar. Todas as outras aplicações serão impedidas de instalação.|  
    |**Adicionar**|Adiciona uma aplicação à lista selecionada. Especifique um nome à sua escolha, o fabricante da aplicação (opcional) e o URL para a aplicação na loja de aplicações.<br /><br /> Para especificar o URL, a partir da Loja Windows, procure a aplicação que pretende utilizar.<br /><br /> Abra a página da aplicação e copie o URL para a área de transferência. Agora, pode utilizar este URL na lista de aplicações permitidas ou bloqueadas.<br /><br /> **Exemplo:** Procure na loja a **Skype** aplicação. O URL a utilizar será o seguinte **http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**.|  
    |**Editarar**|Permite-lhe editar o nome, o fabricante e o URL da aplicação selecionada.|  
    |**Remove**|Elimina a aplicação selecionada da lista.|  
    |**Importarar**|Importa uma lista de aplicações especificadas num ficheiro de valores separados por vírgulas. Utilize o formato, o nome da aplicação, o fabricante e o URL da aplicação no ficheiro.|  
  
### <a name="windows-10-team"></a>Windows 10 Team  
 Estas definições destinam-se apenas a dispositivos com o Windows 10 Team.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Permitir o ecrã para reativação automaticamente quando sensores que Deteta uma pessoa na sala**|Permite ao dispositivo ser reativado automaticamente quando o respetivo sensor deteta alguém na sala.|  
|**PIN necessária para a projecção sem fios**|Especifica se deve introduzir um PIN antes de poder utilizar as capacidades de projeção sem fios do dispositivo.|  
|**Janela de manutenção**|Configura a janela quando podem ocorrer atualizações ao dispositivo. Pode configurar a hora de início da janela e a duração (de 1 a 5 horas).|
|**Informações operacionais do Azure**|Azure Operational Insights, parte do Microsoft Operations Manager recolhe o conjunto de aplicações, armazena e analisa os dados de ficheiro de registo a partir de dispositivos Windows 10 Team.<br>Para ligar às informações operacionais do Azure, tem de especificar um ID da área de trabalho e uma chave de área de trabalho.| 
|**Projecção de Miracast sem fios**|Ative esta opção se pretender permitir que o dispositivo de Windows 10 Team utiliza dispositivos Miracast ativada para o project.<br>Se ativar esta opção, a partir do **escolher Miracast canal** selecione o canal de Miracast utilizado para conteúdo de projeto.|
|**Informações de reunião apresentadas no ecrã de boas-vindas**|Se ativar esta opção, pode escolher as informações que serão apresentadas no **reuniões** mosaico do **bem-vindo** ecrã. É possível:<br><br>- **Mostrar organizador e só de tempo**<br>- **Mostrar o organizador, hora e no assunto (assunto ocultado para reuniões privadas)**|
|**URL da imagem de fundo Lockscreen**|Utilize esta definição para apresentar um fundo personalizado a **bem-vindo** ecrã de dispositivos Windows 10 Team a partir do URL que especifica.<br>A imagem tem de estar no formato PNG e o URL tem de começar por **https://**.| 
  
### <a name="windows-information-protection"></a>Proteção de informações do Windows  

Com o aumento dos dispositivos pertencentes a funcionários na empresa, existe também um risco crescente de fugas de dados acidentais através de aplicações e serviços, como o e-mail, redes sociais e a nuvem pública, que fogem ao controlo da empresa. Por exemplo, quando um empregado envia as imagens de engenharia mais recentes a partir da respetiva conta de e-mail pessoal, copia e cola informações sobre produtos num tweet ou guarda um relatório de vendas em curso no respetivo armazenamento de nuvem pública.

Proteção de informações do Windows (WIP) ajuda a proteger contra esta potenciais fuga de dados sem caso contrário a interferir com a experiência de funcionário. WIP também ajuda a proteger aplicações da empresa e os dados contra dados acidentais leaks em dispositivos pessoais que os funcionários trazer para trabalhar sem necessidade de alterações no seu ambiente ou outras aplicações e dispositivos pertencentes à empresa.

 Definições de item de configuração do Configuration Manager WIP gerir a lista de aplicações protegidas por EDP, localizações de rede da empresa, nível de proteção e definições de encriptação.

Para obter informações sobre como configurar a proteção de dados de empresa com o Configuration Manager, consulte o artigo [proteger os dados de empresa através da proteção de informações do Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).


### <a name="microsoft-edge"></a>Microsoft Edge  
Estas definições destinam-se a dispositivos com o Windows 10 e posterior.  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Permitir sugestões de pesquisa na barra de endereço**|Esta definição permite ao seu motor de busca sugerir sites à medida que escreve frases de pesquisa.|  
|**Permitir o envio de tráfego de intranet para o Internet Explorer**||  
|**Permitir not track**|Não monitoriza os Websites que não pretende que monitorizem a sua visita a um site.|  
|**Ativar SmartScreen**|Utilize o SmartScreen para verificar se os ficheiros transferidos pelos seus utilizadores não contêm código malicioso.|  
|**Permitir pop-ups**|Permite ou desativa os pop-ups do browser.|  
|**Permitir cookies**|Permite ou desativa os cookies.|  
|**Permitir Preenchimento automático**|Permite a utilização da funcionalidade Preenchimento Automático do browser Edge.|  
|**Permitir que o Gestor de palavra-passe**|Permite a utilização da funcionalidade do gestor de palavras-passe do browser Edge.|  
|**Localização de lista de sites do modo de empresa**|Especifica onde encontrar a lista de Web sites que serão abertos no modo Empresarial. Os utilizadores não podem editar esta lista.|  


### <a name="windows-defender"></a>O Windows Defender
Estas definições destinam-se a dispositivos com o Windows 10 e posterior.
 
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Permitir a monitorização em tempo real**|Permite a análise em tempo real para software maligno, spyware e outro software indesejável.|
|**Permitir a monitorização de comportamento**|Esta definição permite aos Defender procurar determinados conhecidos padrões específicos de atividades suspeitas em dispositivos.|
|**Ativar o sistema de inspeção de rede**|O sistema de inspeção de rede (NIS) ajuda a proteger os dispositivos contra exploits baseados em rede, utilizando as assinaturas de vulnerabilidades conhecidas a partir do Microsoft Endpoint Protection Center para o ajudar a detetar e a bloquear tráfego malicioso.|
|**Analisar todas as transferências**|Controla se Defender analisa todos os ficheiros que são transferidos a partir da Internet.|
|**Permitir a análise de scripts**|Esta definição permite aos Defender analisar os scripts que são utilizados no Internet Explorer.|
|**Monitorizar a atividade de programas e ficheiros**|Esta definição permite aos Defender monitorizar programas e ficheiros a atividade em dispositivos.
|**Dias para controlar software maligno resolvido**|Esta definição permite aos Defender continuar a controlar software maligno resolvido para o número de dias que especificar para que possa manualmente verificação anteriormente afetados dispositivos. Se definir o número de dias como 0, o software maligno permanece na pasta de quarentena e não é removido automaticamente.|
|**Permitir acesso à IU de cliente**|Controla se a interface de utilizador do Windows Defender é ocultada dos utilizadores.<br>Quando esta definição é alterada, ela tem efeito assim da próxima vez que PC o utilizador for reiniciado.|
|**Agendar uma análise do sistema**|Permite-lhe agendar uma análise de sistema completo ou rápida ocorre regularmente o dia e a hora em que selecionar.|
|**Agendar uma análise rápida diária**|Permite-lhe agendar uma análise rápida, que ocorre diariamente o momento que selecionar
|**Limitar a utilização da CPU durante uma análise**|Permite-lhe limitar a quantidade de CPU que análises estão autorizados a utilizar (de 1 a 100).|
|**Analisar ficheiros de arquivo**|Permite Defender analisar ficheiros arquivados como. zip ou. cab ficheiros.|
|**Analisar mensagens de e-mail**|Permite Defender analisar mensagens de e-mail chegam como no dispositivo.|
|**Analisar unidades amovíveis**|Esta definição permite aos Defender analisar unidades amovíveis, como USB USB.|
|**Analisar unidades mapeadas**|Esta definição permite aos Defender analisar ficheiros em unidades de rede mapeadas.<br>Se os ficheiros na unidade são só de leitura, Defender será não é possível remover qualquer software maligno encontrado nas mesmas.|
|**Analisar ficheiros abertos a partir de pastas partilhadas na rede**|Esta definição permite aos Defender analisar ficheiros em unidades de rede partilhada (por exemplo, os acedido a partir de um caminho UNC)<br>Se os ficheiros na unidade são só de leitura, Defender será não é possível remover qualquer software maligno encontrado nas mesmas.|
|**Intervalo de atualização de assinatura**|Especifica o intervalo no quais verificações Defender para novos ficheiros de assinatura.
|**Permitir proteção da nuvem**|Permite ou bloqueia o serviço de proteção ativa Microsoft a partir do recetor informações sobre a atividade de software maligno a partir dos dispositivos que gere. Estas informações são utilizadas para melhorar o serviço no futuro.|
|**Utilizadores de linha de comandos para submissão de exemplos**|Controla se os ficheiros que podem exigir adicional análise pela Microsoft para determinar se são maliciosos são automaticamente enviados à Microsoft.|
|**Deteção de aplicação potencialmente indesejável**|Protege os dispositivos Windows inscritos ambiente de trabalho em relação a executar o software que é classificada pela Windows Defender como potencialmente indesejável. Pode proteger contra estas aplicações em execução ou utilizar o modo de auditoria ao relatório quando é instalada uma aplicação potencialmente indesejável.|
|**Exclusões de ficheiros e pastas**|Adiciona um ou mais ficheiros e pastas, como C:\Path ou %ProgramFiles%\Path\filename.exe à lista de exclusões. Estes ficheiros e pastas não são incluídas no quaisquer análises em tempo real ou agendadas.|
|**Exclusões de extensão de ficheiro**|Adicione uma ou mais extensões de ficheiro como formato jpg ou txt à lista de exclusões. Todos os ficheiros com estas extensões não estão incluídos no quaisquer análises em tempo real ou agendadas.|
|**Processo exclusões**|Adiciona um ou mais processos do tipo .exe,. com ou. scr à lista de exclusões. Estes processos não estão incluídos no quaisquer análises em tempo real ou agendadas.|

  
## <a name="see-also"></a>Consulte Também  
 [Itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
