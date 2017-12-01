---
title: Funcionalidades no Technical Preview 1703
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1703."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
caps.latest.revision: "5"
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: a44d6a0c9b02a529fe8776033e58e971af37e332
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1703-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1703 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1703. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementar aplicações iOS compradas em volume para coleções de dispositivos

Pode agora implementar aplicações licenciadas para dispositivos, bem como os utilizadores. Consoante a capacidade de aplicações para suportar o dispositivo de licenciamento, uma licença adequada irá ser reclamada quando a implementá-la, da seguinte forma:

|||||
|-|-|-|-|
|Versão do Configuration Manager|Aplicação suporta o licenciamento do dispositivo?|Tipo de coleção de implementação|Licença pedida|
|Anteriores ao 1702|Sim|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Não|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Sim|Dispositivo|Licença de utilizador|
|Anteriores ao 1702|Não|Dispositivo|Licença de utilizador|
|1702 e posterior|Sim|Utilizador|Licença de utilizador|
|1702 e posterior|Não|Utilizador|Licença de utilizador|
|1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|1702 e posterior|Não|Dispositivo|Licença de utilizador|

Para mais informações sobre as aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

## <a name="direct-links-to-applications-in-software-center"></a>Ligações diretas para aplicações no Centro de Software

Agora pode fornecer aos utilizadores finais com uma ligação direta para uma aplicação no Centro de Software. Isto significa que já não tem de abrir o Centro de Software e procure uma aplicação antes de poderem instalar. Isto só está disponível para o Configuration Manager aplicações, não pacotes e programas ou sequências de tarefas.

### <a name="try-it-out"></a>Experimente                 

Utilize o seguinte formato de URL para abrir o Centro de Software a uma determinada aplicação:

**Softwarecenter:SoftwareId =*identificador da aplicação***

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Como obter o identificador da aplicação de uma aplicação.

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2.  Na área de trabalho biblioteca de Software, expanda **gestão de aplicações**e, em seguida, clique em **aplicações**.
3.  No **aplicações** ver, faça duplo clique de um dos cabeçalhos de coluna e, em seguida, na lista, selecione **ID exclusivo de CI**. Verá que o ID exclusivo de cada aplicação agora é apresentado na lista.
4.  Tenha em atenção o **ID exclusivo de CI** da aplicação que pretende disponibilizar uma ligação para, por exemplo: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5.  Em seguida, remova qualquer texto após a aplicação GUID, neste caso **/2**. Isso deixa o identificador da aplicação.
6.  Por fim, para concluir a construir a ligação, coloque-o com **Softwarecenter:SoftwareID =**. A ligação final utilizando o exemplo acima, serão lidos: **Softwarecenter:SoftwareId = ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Ao utilizar esta ligação, os utilizadores finais podem abrir o Centro de Software diretamente para a aplicação que especificou.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certificados PFX para computadores de cliente do Windows do Configuration Manager

Agora pode implementar perfis de certificado PFX importado para computadores de cliente do Configuration Manager com o Windows 10.

### <a name="try-it-out"></a>Experimente

Utilize as instruções no [como criar perfis de certificado PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) para importar um perfil PFX, implemente o perfil e, em seguida, verifique se o certificado foi instalado para o utilizador de destino.



## <a name="configure-azure-services-wizard"></a>Configurar o Assistente de serviços do Azure
Pré-visualização técnica 1703 introduz o **configurar os serviços do Azure** assistente. Este assistente fornece uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os serviços em nuvem que utiliza com o Configuration Manager. Isto é feito utilizando um **aplicação web do Azure** para fornecer os detalhes da subscrição e a configuração que introduziu, caso contrário, sempre que configurou um novo componente do Configuration Manager ou o serviço com o Azure.

Com a pré-visualização técnica 1703, está configurada apenas loja Windows para empresas (WSfB) ao utilizar este assistente.  Outros serviços em nuvem estão configurados utilizando os seus fluxos de trabalho separados.

-   Utilize as informações neste tópico de pré-visualização para substituir os passos de configuração encontradas no [configurar loja Windows para a sincronização de negócio](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization) secção do tópico Current Branch [gerir aplicações da loja Windows para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

-   Para mais informações sobre as aplicações web, consulte [autenticação e autorização no serviço de aplicações do Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview), e [descrição geral das aplicações Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Pré-requisitos e planear
Quando configurar uma ligação entre o Configuration Manager e na loja Windows para empresas, tem de fornecer uma pasta em que será mantido sincronizado a partir da loja de conteúdo de aplicação. Para se certificar de que esta pasta está protegida e que o respetivo conteúdo pode ser implementado em dispositivos, certifique-se que as seguintes permissões são cumpridos:
-   O computador no qual instala a função de sistema de sites de ponto de ligação serviço (site de nível superior na hierarquia) tem de ter de leitura e permissões de escrita para a pasta que especificou quando utilizar o **computador$** conta.  

-   O autor da aplicação tem de ter permissões de leitura para a pasta que especificou.  

-   O **computador$** conta de cada computador que aloja uma instância do fornecedor de SMS tem de ser capaz de utilizar a pasta que especificou.

No Azure Active Directory, registe o Configuration Manager como uma aplicação web ou a ferramenta de gestão de Web API. Esta ação cria o ID de cliente que irá precisar mais tarde.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Utilize o Assistente para configurar o serviço de nuvem WSfB

1. Na consola, aceda a **administração** > **descrição geral** > **gestão de serviços em nuvem** > **Azure** > **serviços do Azure**e, em seguida, escolha **configurar os serviços do Azure** para iniciar o **Assistente de serviços do Azure**.

2. No **serviços do Azure** página, selecione o serviço que pretende configurar e, em seguida, clique em **seguinte**. Com esta pré-visualização, WSfB só pode ser configurado.

3. No **geral** , indique um nome amigável para o **nome do serviço do Azure** e uma descrição opcional e, em seguida, clique em **seguinte**.

4. No **aplicação** página, especifique o seu ambiente do Azure e, em seguida, clique em **procurar** para abrir a janela de aplicação de servidor.

5. No **aplicação Server** janela, selecione a aplicação de servidor que pretende utilizar e, em seguida, clique em **OK**.
Aplicações de servidor são as aplicações web do Azure que contêm as configurações para a sua conta do Azure, incluindo o ID de inquilino, ID de cliente e uma chave secreta para clientes. Se não tiver uma aplicação de servidor disponível, utilize um dos seguintes:
  - **Criar**: Para criar uma nova aplicação de servidor, clique em **criar**. Forneça um nome amigável para a aplicação e de inquilino. Em seguida, depois, inicie sessão no Azure, o Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode ver estes do portal do Azure.
  - **Importar**: Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e de inquilino e, em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação web do Azure que pretende utilizar o Configuration Manager. Depois de **verifique** informações, clique em **OK** para continuar.  </br></br>

6. Reveja o **informações** página e conclua quaisquer passos adicionais e configurações, conforme indicado. Estas configurações são necessárias para utilizar o serviço com o Configuration Manager.
Por exemplo, para configurar WSfB:

  1. No Azure tem de registar o Configuration Manager como uma aplicação web ou a Web API e registar o ID de cliente. Também especificar uma chave de cliente para utilização pela ferramenta de gestão (que é o Configuration Manager).

  2.    Na consola do WSfB tem de configurar o Configuration Manager como a ferramenta de gestão de armazenamento, ativar o suporte para aplicações licenciadas offline e, em seguida, comprar, pelo menos, uma aplicação.   </br>

  Clique em **seguinte** quando estiver pronto para continuar.

7. No **configurações aplicação** página, conclua as configurações de idioma e o catálogo de aplicações para este serviço e, em seguida, clique em **seguinte**.
8. Depois de concluir o assistente, a consola do Configuration Manager mostra que configurou **loja Windows para empresas** como um **o tipo de serviço de nuvem**.

Agora, pode utilizar o resto do [conteúdo Current Branch](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) para gestão de aplicações do WSfB sincronizar, criar e implementar e monitorizar a loja Windows para as aplicações da empresa.

### <a name="modify-a-cloud-service-configuration"></a>Modificar a configuração do serviço de nuvem
Pode ver e editar as propriedades de um serviço em nuvem para modificar a configuração.

Na consola, aceda a **administração** > **descrição geral** > **gestão de serviços em nuvem** > **Azure** > **serviços do Azure**e, em seguida, escolha **configurar os serviços do Azure**, selecione um serviço em nuvem e, em seguida, escolha **propriedades**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>A conversão de BIOS em UEFI durante uma atualização no local
Atualização do Windows 10 criadores introduz uma ferramenta de conversão simples que automatiza o processo para reparticionar o disco rígido para hardware ativado para UEFI e integra-se a ferramenta de conversão para o Windows 7 para o processo de atualização do Windows 10 no local. Ao combinar esta ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta do OEM que converte o firmware de BIOS para UEFI, pode converter os seus computadores de BIOS para UEFI durante uma atualização no local para o Windows 10 criadores Update. Para obter mais informações, consulte [para gerir o BIOS para conversão de UEFI, os passos de sequência de tarefas](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

## <a name="collapsible-task-sequence-groups"></a>Grupos de sequências de tarefas expansível
Esta versão apresenta a capacidade para expandir e fechar a grupos de sequências de tarefas. Pode expandir ou fechar grupos individuais ou expandir ou fechar todos os grupos em simultâneo.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Definições de cliente para configurar a análise do Windows para a preparação da atualização
Começando com esta versão, pode utilizar as definições de cliente do dispositivo para simplificar a configuração de telemetria do Windows necessária utilizar [Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) soluções como [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) com o Configuration Manager. O Configuration Manager pode obter dados de análise do Windows que podem fornecer informações valiosas para o estado atual do seu ambiente com base nos dados de telemetria do Windows relatados pelos seus computadores de cliente. Os dados telemétricos do Windows são reportados pelos computadores cliente para o serviço de telemetria do Windows e, em seguida, os dados relevantes, subsequentemente, são transferidos para soluções de análise do Windows que estão alojadas das áreas de trabalho OMS da sua organização. Preparação de atualização é uma solução de análise do Windows que pode ajudar a atribuir prioridades a tomar decisões sobre a atualizações do Windows para os seus dispositivos geridos.

Para obter informações sobre definições de telemetria do Windows, consulte [telemetria de configurar o Windows na sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).

### <a name="prerequisites"></a>Pré-requisitos
- Tem de ter configurado o site para utilizar o serviço de nuvem de preparação de atualização. Para obter mais informações consulte [preparação de atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics)

### <a name="configure-windows-analytics-client-settings"></a>Configurar definições de cliente Windows Analytics
Para configurar a análise do Windows, na consola do Configuration Manager vá para **administração** > **as definições de cliente**, faça duplo clique em **criar definições personalizadas do dispositivo cliente** e, em seguida, verifique **Windows Analytics**.  

Em seguida, configure o seguinte após ao navegar para o **Windows Analytics** separador definições:
- **ID comercial**  
A chave de ID comercial mapeia informações dos dispositivos que gere para a área de trabalho do OMS que aloja os dados de análise do Windows da sua organização. Se já tiver configurado uma chave de ID comercial para utilização com a preparação de atualização, utilize esse ID. Se ainda não tiver uma chave de ID comercial, consulte [gerar a chave de ID comercial]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

- Definir um **nível de telemetria para dispositivos Windows 10**   
Para obter informações sobre o que é recolhido por cada nível de telemetria do Windows 10, consulte [telemetria de configurar o Windows na sua organização]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

- Optar por **optar ativamente por participar na recolha de dados comerciais em dispositivos Windows 7, 8 e 8.1**   
Para informações sobre os dados recolhidos a partir destes sistemas operativos quando que optar ativamente por participar sessão, consulte Transferir o [eventos de telemetria appraiser Windows 7, Windows 8 e Windows 8.1 e campos](https://go.microsoft.com/fwlink/?LinkID=822965) ficheiro pdf da Microsoft.

- **Configurar a recolha de dados de Internet explorar** em dispositivos Windows 8.1 ou anterior em execução, recolha de dados do Internet Explorer pode permitir que a preparação de atualização detetar incompatibilidades de aplicação web que podem impedir uma atualização sem problemas para o Windows 10. Recolha de dados do Internet Explorer, pode ser ativada num por base de zona de internet. Para obter mais informações sobre as zonas de internet, consulte [sobre zonas de segurança do URL](https://msdn.microsoft.com/en-us/library/ms537183(v=vs.85).aspx).