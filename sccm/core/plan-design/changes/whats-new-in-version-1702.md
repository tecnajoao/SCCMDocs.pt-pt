---
title: Nova versão 1702
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1702 do System Center Configuration Manager.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2cc827b782f6776978c1a2361f1ed8d1659f23a3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128471"
---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>O que&#39;s novo na versão 1702 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para o ramo atual do System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1602, 1606 ou 1610 de atualização 1702. Também está disponível como uma versão de linha de base que pode utilizar ao instalar uma nova implementação.

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalar atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre alterações e novas funcionalidades introduzidas na versão 1702 do Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Funcionalidades preteridas e sistemas operativos
Saiba mais sobre as alterações de suporte antes de eles são implementados no [removidas e preteridas itens](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Quedas de versão 1702 suportam para os seguintes produtos:
- **SQL Server 2008 R2**, para servidores de base de dados do site. Descontinuação de suporte foi [anunciada pela primeira vez](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database) 10 de Julho de 2015. Esta versão do SQL Server continua a ser suportada quando utiliza uma versão do Configuration Manager antes da versão 1702.
- **Windows Server 2008 R2**, para servidores do sistema de sites e a maioria das funções de sistema de sites. Descontinuação de suporte foi [anunciada pela primeira vez](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) 10 de Julho de 2015. Esta versão do Windows continua a ser suportado quando utiliza uma versão do Configuration Manager antes da versão 1702.  
- **Windows Server 2008**, para servidores do sistema de sites e a maioria das funções de sistema de sites. Descontinuação de suporte foi [anunciada pela primeira vez](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) 10 de Julho de 2015.
- **Windows XP Embedded**, como um sistema operativo cliente. Preterição foi [anunciada pela primeira vez](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems) 10 de Julho de 2015. Esta versão do Windows continua a ser suportado quando utiliza uma versão do Configuration Manager antes da versão 1702.




## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="improvements-for-in-console-search"></a>Aprimoramentos de pesquisa na consola
Seguem-se melhoramentos para utilizar a pesquisa na consola do Configuration Manager:
 - **Caminho do objeto:**  
  Muitos objetos suportam agora uma coluna chamada **caminho do objeto**.  Ao pesquisar e inclua esta coluna nos resultados de sua apresentação, pode ver o caminho para cada objeto. Por exemplo, se executar uma pesquisa para as aplicações no nó Applications e também é pesquisar sub-nós, o *caminho do objeto* coluna no painel de resultados mostram-lhe o caminho para cada objeto que é devolvido.   

- **Preservação do texto de pesquisa:**  
  Quando inserir texto na caixa de texto de pesquisa e, em seguida, alternar entre pesquisando um nó secundário e o nó atual, o texto digitado será manter e permanecem disponível para uma nova pesquisa sem ter de reintroduzir a ele.

- **Preservação da sua decisão de pesquisar sub-nós:**  
 A opção que escolher para pesquisar os *nó atual* ou *todos os nós secundários* agora persistir quando altera o nó que está a trabalhar. Esse novo comportamento significa que não é necessário repor constantemente essa decisão, como mover a consola. Por predefinição, quando abrir a consola a opção é pesquisar apenas o nó atual.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentários a partir da consola do Configuration Manager

 Pode utilizar as opções de comentários na consola para enviar comentários diretamente para a equipe de desenvolvimento.

 Pode encontrar os **comentários** opção:
- No Friso, na extremidade esquerda do separador base de cada nó.  
  ![Faixa de opções](./media/feedback-home.png)

- Quando com o botão direito em qualquer objeto na consola do.   
   ![Opção de clique Righ](./media/feedback-option.png)   

  Escolher **comentários** abre-se o browser para o [Web site de comentários do UserVoice do Configuration Manager](https://go.microsoft.com/fwlink/?linkid=617029).


###  <a name="changes-for-updates-and-servicing"></a>Alterações para atualizações e manutenção
Seguem-se as alterações para atualizações e manutenção:

- **Localização do nó**   
  Depois de instalar a versão 1702, o **atualizações e manutenção** nó aparece como um nó de nível superior sob **administração**. Já não é um nó filho abaixo **serviços Cloud**.

- **Novos Estados de atualização**  
  Ao visualizar as atualizações disponíveis na consola, existem dois novos Estados:  
  - **Disponível para instalação** -esta é uma atualização que foi transferido e pronto para instalar.
  - **Pronto para transferência** -esta atualização está disponível, mas não foi transferida. Pode optar por transferir esta atualização, mas foi substituída por uma atualização mais recente.


- **Opções de atualização mais simples**  
  Da próxima vez que sua infraestrutura é elegível para dois ou mais atualizações, apenas a atualização mais recente é transferida. Por exemplo, se a sua versão atual do site é dois ou mais anterior à versão mais recente disponível, apenas nessa versão de atualização mais recente é transferida automaticamente.  

  Pode optar por transferir e instalar as outras atualizações disponíveis, mesmo quando não estão a versão mais atual. Se baixar uma atualização mais antiga, receberá um aviso de que a atualização foi substituída por uma mais recente. Para transferir uma atualização que está *disponível para Download*, selecione a atualização na consola e, em seguida, clique em **transferir**.

- **Melhorada a limpeza das atualizações mais antigas**   
  Adicionámos uma função de limpeza automática, que elimina transferências desnecessárias da pasta "EasySetupPayload" no servidor de site. Porque isso é introduzido com a versão 1702, limpeza começa a funcionar depois de instalar uma atualização subsequente como um pacote cumulativo de atualizações ou a versão de atualização futura.  


### <a name="data-warehouse-service-point"></a>Ponto de serviço do armazém de dados
 Utilize o ponto de serviço do armazém de dados para armazenar e gerar relatórios sobre dados históricos de longo prazo para a sua implementação do Configuration Manager.

 O armazém de dados suporta até 2 TB de dados, carimbos de data de registo de alterações. Armazenamento de dados é realizado pela sincronizações automáticas da base de dados do site do Configuration Manager para a base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do seu ponto de Reporting Services.

 Para obter mais informações, consulte [ponto de serviço do armazém de dados a](/sccm/core/servers/manage/data-warehouse).


### <a name="peer-cache-improvements"></a>Melhorias da Cache ponto a ponto
 A partir da versão 1702, um computador de origem de cache ponto a ponto irão rejeitar um pedido para o conteúdo quando o computador de origem de cache ponto a ponto cumpre qualquer um dos seguintes condições:  
  -  Está no modo de pouca bateria.
  -  Carga da CPU excede 80%, no momento que o conteúdo é solicitado.
  -  E/s de disco tem um *AvgDiskQueueLength* que excede a 10.
  -  Não existem ligações não é mais disponíveis para o computador.   
Para obter mais informações, consulte **acesso a uma origem de cache ponto a ponto limitado** na [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).   

Além disso, três novos relatórios são adicionados ao seu ponto de geração de relatórios. Pode utilizar estes relatórios para obter mais detalhes sobre pedidos rejeitados de conteúdo, incluindo o limite de grupo, o computador e o conteúdo foi envolvido de compreender. Ver [monitorização](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring) no tópico de cache ponto a ponto.

### <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos
 Utilize o [ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo dos pontos de distribuição quando esse conteúdo não se encontra associado a uma aplicação.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Utilizar o conector do OMS com a cloud do Azure Government
Pode utilizar o conector do OMS para ligar ao OMS Log Analytics na cloud do Microsoft Azure Government. Isso exige que modifique um ficheiro de configuração antes de instalar o conector do OMS, para que o conector pode trabalhar com a cloud do Governo. Para obter mais informações, consulte [utilizar o conector do OMS com a cloud do Azure Government](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Pontos de atualização de software são adicionados a grupos de limites
A partir da versão 1702, os clientes utilizam grupos de limites para encontrar um novo ponto de atualização de software e de contingência e localização de uma nova atualização de software ponto, se seus um atual já não está acessível. Pode adicionar pontos de atualização de software individuais aos grupos de limites diferentes para controlar quais os servidores em que um cliente pode encontrar. Para obter mais informações, consulte [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) no [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) tópico.


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="new-compliance-settings-for-ios"></a>Novas definições de conformidade para iOS

Adicionámos muitas definições novas para dispositivos iOS de acordo com as que estão disponíveis com o Microsoft Intune.
Para obter uma lista de todas as definições disponíveis, consulte [criar itens de configuração para iOS e dispositivos Mac OS X geridos com o Intune](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).


## <a name="application-management"></a>Gestão de Aplicações

### <a name="improved-support-for-windows-store-for-business-apps"></a>Suporte aprimorado à Windows Store para aplicações empresariais

Pode implementar aplicações licenciadas online a partir da Windows Store para empresas para PCs com Windows 10 que gere com o cliente do Configuration Manager.
Para obter mais informações, consulte [gerir aplicações a partir da Windows Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Verifique a existência de executar ficheiros executáveis antes de instalar uma aplicação

Na **propriedades** , na caixa de diálogo de uma implementação escreva a **comportamento instalar** separador, pode agora especificar uma das mais ficheiros executáveis que, se executar, irão bloquear a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução (ou pode ser fechado automaticamente para implementações com um objetivo necessário) antes da implantação tipo pode ser instalado.

Se a aplicação foi implementada como **disponível**e um utilizador final tenta instalar uma aplicação, será solicitado a eles para fechar a quaisquer especificou antes que eles podem continuar a instalação de executáveis em execução.

Se a aplicação foi implementada como **necessários**e a opção **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação** é selecionado, verá uma caixa de diálogo que informa de que os executáveis que especificou serão fechados automaticamente quando é atingido o prazo de instalação do aplicativo.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Melhorias de gestão de aplicações para MDM híbrida

- [Implementar aplicações iOS compradas em volume para coleções de dispositivos](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Suporte para iOS Volume Purchase Program for Education](#support-for-ios-volume-purchase-program-for-education)
- [Suporte para vários tokens do programa de compra em volume](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="expire-stand-alone-media"></a>Expirar dados autónomos
Quando criar suportes de dados autónomo, existem novas opções para definir as datas de início e de expiração opcionais no suporte de dados. Estas definições estão desativadas por predefinição. As datas são em comparação com a hora do sistema no computador antes do suporte de dados autónomo é executado. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, o suporte de dados autónomo não está iniciado. Estas opções também estão disponíveis ao utilizar o cmdlet New-CMStandaloneMedia PowerShell. Para obter detalhes, consulte [criar suporte de dados autónomo](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="package-id-displayed-in-task-sequence-steps"></a>ID do pacote apresentado nos passos de sequência de tarefas
Qualquer passo de sequência de tarefas que faça referência a um pacote, o pacote de controladores, a imagem do sistema operativo, a imagem de arranque ou o pacote de atualização do sistema operativo agora irá apresentar o ID do pacote do objeto referenciado. Quando um passo de sequência de tarefas faz referência um aplicativo, ele irá apresentar o ID de objeto.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Suporte para conteúdo adicional no suporte de dados autónomo
Conteúdo adicional é agora suportado no suporte de dados autónomo. Pode selecionar pacotes adicionais, pacotes de controladores e aplicações para ser preparado no suporte de dados, juntamente com os outros conteúdos referenciados na sequência de tarefas. Anteriormente, apenas os conteúdos referenciados na sequência de tarefas foi testado no suporte de dados autónomo. Para obter detalhes, consulte [criar suporte de dados autónomo](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações de UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para ajudar a determinar se um computador é iniciado no modo UEFI. Quando um computador é iniciado no modo UEFI, o **UEFI** estiver definida como **verdadeiro**. Esta opção estiver ativada no inventário de hardware por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Melhoramentos para mensagens de aviso do Centro de Software para sequências de tarefas de alto impacto
Esta versão inclui as seguintes melhorias às mensagens de aviso do Centro de Software para sequências de tarefas de implementação de alto impacto:

- Nas propriedades da sequência de tarefas, agora, pode configurar qualquer sequência de tarefas, incluindo sequências de tarefas de sistema não operacionais, como uma implementação de alto risco. Qualquer sequência de tarefas que cumpre determinadas condições automaticamente é definida como alto impacto. Para obter detalhes, consulte [gerir implementações de alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Nas propriedades da sequência de tarefas, pode optar por utilizar a mensagem de notificação predefinidas ou criar sua própria mensagem de notificação personalizada para implementações de alto impacto.
- Nas propriedades da sequência de tarefas, pode configurar o Centro de Software propriedades, que incluem fazer um reinício necessário, o tamanho de download da sequência de tarefas, e o estimado tempo de execução.
- A mensagem de implementação de alto impacto predefinida para in-loco atualiza agora os Estados que aplicações, dados e definições são migradas automaticamente. Anteriormente, a mensagem predefinida para qualquer instalação do sistema operativo indicado que todas as aplicações, dados e definições seriam perdidas, que não era válido para uma atualização no local.

Para obter detalhes, consulte [configurar as definições de sequência de tarefas de impacto elevado](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior quando ocorre uma falha de uma sequência de tarefas
Agora pode retornar a uma página anterior quando executa uma sequência de tarefas e de falha. Antes desta versão, tinha que reinicie a sequência de tarefas quando ocorreu uma falha. Por exemplo, pode utilizar o **Previous** botão nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar-se antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas é apresentada uma mensagem que não há nenhum sequências de tarefas disponíveis. Agora, pode clicar **Previous** para procurar novamente sequências de tarefas disponíveis. Pode repetir esse processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdo dependentes ainda não estão disponíveis em pontos de distribuição, a sequência de tarefas falhará. Pode agora distribuir o conteúdo em falta (se não foi distribuída ainda) ou aguardar que o conteúdo fique disponível nos pontos de distribuição e, em seguida, clique em **Previous** para que a pesquisa de sequência de tarefas novamente para o conteúdo.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Pré-armazenar conteúdo em cache para as implementações disponíveis e sequências de tarefas
Partir da versão 1702, para as implementações de sequências de tarefas disponíveis, pode optar por utilizar pré-armazenar conteúdo em cache. Pré-armazenar conteúdo em cache lhe dá a opção para permitir que o cliente transferir apenas o conteúdo aplicável assim que receber a implementação. Por conseguinte, quando o usuário clica **instalar** no Centro de Software, os conteúdos estiverem prontos e a instalação inicia rapidamente porque o conteúdo está no disco rígido local. Para obter detalhes, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização no local
Windows 10 Creators Update introduz uma ferramenta de conversão simples que automatiza o processo para criar novas partições de disco rígido para o hardware preparado para UEFI e integra-se a ferramenta de conversão para o 7 do Windows para o processo de atualização do Windows 10 no local. Ao combiná-essa ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta de OEM que converte o firmware de BIOS para UEFI, pode converter seus computadores de BIOS para UEFI durante uma atualização no local para a atualização para criativos do Windows 10. Para obter detalhes, consulte [passos para gerir o BIOS para conversão de UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Passo de melhorias à sequência de tarefas instalar aplicações
Esta versão introduziu os seguintes melhoramentos:
- Aumentar o número máximo de aplicações que pode instalar a 99 no **instalar aplicações** passo de sequência de tarefas. O número máximo anterior era 9 aplicativos.
- Ao adicionar aplicações para o **instalar aplicativos** passo de sequência de tarefas no editor de sequência de tarefas, agora, pode selecionar vários aplicativos sejam os **selecione a aplicação a instalar** painel.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Melhoramentos à sequência de tarefas aplicar controladores automaticamente
Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite no passo de sequência de tarefas aplicar controladores automaticamente quando são efetuados pedidos do catálogo HTTP. Estão disponíveis as seguintes variáveis e valores predefinidos (em segundos):
   - SMSTSDriverRequestResolveTimeOut  
     predefinição: 60
   - SMSTSDriverRequestConnectTimeOut  
     predefinição: 60
   - SMSTSDriverRequestSendTimeOut  
     predefinição: 60
   - SMSTSDriverRequestReceiveTimeOut  
     predefinição: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK controlados por versão de compilação
O Windows 10 ADK agora é controlado pela versão de compilação para garantir uma experiência mais suporte ao personalizar imagens de arranque do Windows 10. Por exemplo, se o site utiliza o Windows ADK para Windows 10, versão 1607, apenas as imagens de arranque com a versão 10.0.14393 podem ser personalizadas na consola do. Para obter detalhes sobre como personalizar as versões do WinPE, consulte [personalizar imagens de arranque](/sccm/osd/get-started/customize-boot-images).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Já não pode ser alterado o caminho de origem de imagem de arranque predefinido
Imagens de arranque predefinidas são geridas pelo Configuration Manager e o caminho de origem de imagem de arranque predefinido já não pode ser alterado na consola do Configuration Manager ou com o SDK do Configuration Manager. Pode continuar a configurar um caminho de origem de dados personalizada para imagens de arranque personalizadas.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Imagens de arranque predefinidas são gerados novamente após a atualização do Configuration Manager para uma nova versão
A partir desta versão, quando atualizar a versão do Windows ADK e, em seguida, utilizar as atualizações e manutenção para instalar a versão mais recente do Configuration Manager, Configuration Manager gera novamente a imagens de arranque predefinidas. Isto inclui a nova versão de janela PE a partir do ADK atualizado do Windows, a nova versão do cliente do Configuration Manager, controladores, personalizações, etc. Imagens de arranque personalizadas não são modificadas. Para obter detalhes, consulte [gerir imagens de arranque](/sccm/osd/get-started/manage-boot-images#BKMK_BootImageDefault).

## <a name="software-updates"></a>Atualizações de software

### <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicações do Office 365 em clientes
A partir da versão 1702, a partir do dashboard de gestão de clientes do Office 365, pode iniciar o instalador do Office 365 que lhe permite configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdos (CDNs) do Office e implementar os ficheiros como um aplicações no Configuration Manager. Para obter detalhes, consulte [atualizações de gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).

> [!IMPORTANT]
> A aplicação do Office 365 que criar e implementar com o Assistente de aplicativo do Office 365 no Configuration Manager não é automaticamente gerenciada pelo Configuration Manager até que tenha ativado a **ativar a gestão do Office 365 Client novamente**definição de agente de cliente de atualizações de software. Para obter detalhes, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir Ficheiros de instalação rápida para as atualizações do Windows 10
Partir da versão 1702, o Configuration Manager suporta ficheiros de instalação rápida para atualizações do Windows 10. Quando utiliza uma versão suportada do Windows 10, pode utilizar as definições do Gestor de configuração para transferir apenas as alterações entre Windows 10 Cumulative Update o mês atual e atualização deste mês anterior. Sem ficheiros de instalação rápida, o Configuration Manager transfere o completo Windows 10 Cumulative Update (incluindo todas as atualizações dos meses anteriores) por mês. A utilização de ficheiros de instalação rápida fornece para transferências mais pequenas e tempos de instalação mais rápidos nos clientes. Para obter detalhes, consulte [gerir ficheiros de instalação rápida para atualizações do Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Versões do Android e iOS já não são targetable nos assistentes de criação para MDM híbrida

Partir da versão 1702 para gestão de dispositivos móveis híbridos (MDM), já não precisar de atingir versões específicas do Android e iOS durante a criação de novas políticas e perfis de dispositivos geridos pelo Intune. Em vez disso, escolha um dos seguintes tipos de dispositivos:

- Android
- Samsung KNOX Standard 4.0 e superior
- iPhone
- iPad

Esta alteração afeta os assistentes para criar os seguintes itens:

- Itens de configuração
- Políticas de conformidade
- Perfis de certificados
- Perfis de e-mail
- Perfis VPN
- Perfis de Wi-Fi

Com esta alteração, implementações híbridas podem fornecer suporte mais rapidamente para novas versões do Android e iOS sem a necessidade de uma nova versão do Configuration Manager ou a extensão. Depois de uma nova versão é suportada no Intune autónomo, os utilizadores poderão atualizar os dispositivos móveis para essa versão.

Para evitar problemas durante a atualização de versões anteriores do Configuration Manager, versões de sistema operativo móvel ainda estão disponíveis nas páginas de propriedades para esses itens. Se ainda precisar de uma versão específica de destino, pode criar o novo item e, em seguida, especifique a versão de destino na página de propriedades do item criado recentemente. 

> [!NOTE]
> A última versão de sistema operativo móvel disponível nas páginas de propriedades aplica-se de que a versão e todas as versões subsequentes. Páginas de propriedades fornecem as seguintes opções para o direcionamento posterior ao Android 7 e iOS 10 os sistemas operativos: 
> - **Android 7 ou superior**
> - **Todos os 10 dispositivos iOS e superiores iPhone ou iPod touch**
> - **Todos os 10 dispositivos iOS e superiores iPad**

### <a name="android-for-work-support"></a>Android para o suporte de trabalho
A partir do 1702, gestão de dispositivos móveis híbrida com o Microsoft Intune agora suporta Android para gestão e inscrição de dispositivos de trabalho. Android gerido para documentação de orientação de dispositivos de trabalho:

- [Inscrever dispositivos Android para dispositivos de trabalho](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)
- [Aprovar e implementar o Android for Work](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração para Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-for-work-configuration-items)
- [Eliminação seletiva em dispositivos Android para dispositivos de trabalho](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)
- [Perfis de e-mail do Android for Work](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Políticas de conformidade para Android for Work](/sccm/mdm/deploy-use/create-compliance-policy)


### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementar aplicações iOS compradas em volume para coleções de dispositivos

Pode agora implementar aplicações licenciadas para dispositivos, bem como os utilizadores. Consoante a capacidade de aplicações para suportar de licenciamento de dispositivos, uma licença adequada irá ser solicitada ao implantá-lo, da seguinte forma:

|||||
|-|-|-|-|
|Versão do Configuration Manager|Aplicação suporta o licenciamento de dispositivos?|Tipo de coleção de implementação|Licença solicitada|
|Anterior ao 1702|Sim|Utilizador|Licença de utilizador|
|Anterior ao 1702|Não|Utilizador|Licença de utilizador|
|Anterior ao 1702|Sim|Dispositivo|Licença de utilizador|
|Anterior ao 1702|Não|Dispositivo|Licença de utilizador|
|1702 e posterior|Sim|Utilizador|Licença de utilizador|
|1702 e posterior|Não|Utilizador|Licença de utilizador|
|1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|1702 e posterior|Não|Dispositivo|Licença de utilizador|

Para obter mais informações sobre aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Suporte para iOS Volume Purchase Program for Education

Agora também pode implementar e controlar aplicações compradas a partir do iOS Volume Purchase Program for Education.
Para obter mais informações sobre aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Suporte para vários tokens do programa de compra em volume

Agora pode associar vários tokens do programa de compra em volume da Apple com o Configuration Manager.
Para obter mais informações sobre aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Suporte para aplicações linha de negócio na Windows Store para empresas

Agora pode sincronizar personalizada aplicações de linha de negócio da Windows Store para empresas.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Melhorias de política de conformidade de dispositivo de acesso condicional

Uma nova regra de política de conformidade do dispositivo está disponível para o ajudar a bloquear o acesso a recursos da empresa que suportam o acesso condicional, quando os utilizadores estão a utilizar aplicações que fazem parte de uma lista de em não conformidades de aplicações. A lista de em não conformidades de aplicações pode ser definida pelo administrador, ao adicionar a nova regra de conformidade **aplicações que não não possível instalar**. Esta regra requer que o administrador para introduzir os **nome da aplicação**, o **ID de aplicação**e o **publicador da aplicação** (opcional) ao adicionar uma aplicação à lista de não conformidade. Esta definição aplica-se apenas a dispositivos iOS e Android.

Além disso, esta definição ajuda as organizações a reduzir a fuga de dados através de aplicações não protegidas e a impedir o consumo excessivo de dados através de determinadas aplicações.

- Saiba mais [como funcionam as políticas de conformidade do dispositivo](/sccm/mdm/deploy-use/device-compliance-policies).
- Saiba mais [como criar políticas de conformidade de dispositivos](/sccm/mdm/deploy-use/create-compliance-policy).

### <a name="new-mobile-threat-defense-monitoring-tools"></a>Novo Mobile Threat Defense ferramentas de monitorização

Partir da versão 1702, terá de novas formas de monitorizar o estado de conformidade com o seu fornecedor de serviços de defesa contra ameaças móveis.

- Saiba mais [como monitorizar a conformidade de Mobile Threat Defense](https://docs.microsoft.com/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="detect-outdated-antimalware-client-versions"></a>Detetar versões de cliente de antimalware desatualizados
A partir da versão 1702, pode configurar um alerta para garantir que os clientes do Endpoint Protection não estão desatualizados. Para obter mais informações, consulte [alerta para o cliente de software maligno Desatualizadas](/sccm/protect/deploy-use/endpoint-configure-alerts#detect-outdated-antimalware-client-versions).

### <a name="device-health-attestation-updates"></a>Atualizações de atestado de estado de funcionamento do dispositivo
Serviço de atestado de estado de funcionamento de dispositivos para locais clientes agora podem ser configurados e geridos a partir do ponto de gestão. Para obter mais informações, consulte [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Perfis de certificado para Windows Hello para empresas

Se pretende armazenar os perfis de certificado do Windows Hello para o contentor de chaves de negócios e o perfil de certificado utiliza a EKU de início de sessão de Smart Card, tem de configurar permissões para o registo de chave garantir que o certificado é validado corretamente.
Para obter mais informações, consulte [Windows Hello para empresas](/sccm/protect/deploy-use/windows-hello-for-business-settings).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Novo Windows Hello para notificação de negócios para os utilizadores finais
Uma nova notificação do Windows 10 informa os utilizadores finais que têm de realizar ações adicionais para concluir Windows Hello para a configuração de negócio (por exemplo, configuração de um PIN).
