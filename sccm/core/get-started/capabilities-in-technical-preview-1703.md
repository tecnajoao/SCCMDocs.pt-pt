---
title: Funcionalidades no Technical Preview 1703
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1703.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6d427571db52f19e9d1e45648bdf2cc66b6c6d9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141277"
---
# <a name="capabilities-in-technical-preview-1703-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1703 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1703. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementar aplicações iOS compradas em volume para coleções de dispositivos

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

## <a name="direct-links-to-applications-in-software-center"></a>Ligações diretas para aplicações no Centro de Software

Agora pode fornecer aos utilizadores finais com uma ligação direta a uma aplicação no Centro de Software. Isso significa que eles já não tem de abrir o Centro de Software e procurar uma aplicação antes de poder instalá-lo. Trata-se disponível apenas para o Configuration Manager aplicativos, não pacotes e programas ou sequências de tarefas.

### <a name="try-it-out"></a>Experimentar                 

Utilize o seguinte formato de URL para abrir o Centro de Software a uma determinada aplicação:

**Softwarecenter:SoftwareId=_Application Identifier_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Como obter o identificador da aplicação de um aplicativo.

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2.  Na área de trabalho biblioteca de Software, expanda **gestão de aplicações**e, em seguida, clique em **aplicativos**.
3.  Na **aplicativos** ver, faça duplo clique de um dos cabeçalhos de coluna e, em seguida, na lista, selecione **ID de CI exclusivo**. Verá que o ID exclusivo de cada aplicativo é agora apresentado na lista.
4.  Tenha em atenção a **ID de CI exclusivo** da aplicação que pretende disponibilizar uma ligação para, por exemplo: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5.  Em seguida, remova qualquer texto seguindo o aplicativo GUID, neste caso **/2**. Isso permite que tenha o identificador da aplicação.
6.  Por fim, para concluir a construir o link, coloque-o com **Softwarecenter:SoftwareID =**. Com o exemplo acima, irá ler a ligação final: **Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Ao utilizar esta ligação, os utilizadores finais podem abrir o Centro de Software diretamente para a aplicação que especificou.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certificados PFX para computadores de cliente do Windows do Configuration Manager

Agora, pode implementar perfis de certificado PFX importadas para computadores de cliente do Configuration Manager com o Windows 10.

### <a name="try-it-out"></a>Experimentar

Utilize as instruções em [como criar perfis de certificado PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) para importar um perfil PFX, implemente o perfil e, em seguida, verifique se o certificado foi instalado para o utilizador de destino.



## <a name="configure-azure-services-wizard"></a>Configurar o Assistente de serviços do Azure
Technical preview 1703 apresenta os **configurar os serviços do Azure** assistente. Este assistente fornece uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os serviços de cloud que utiliza com o Configuration Manager. Isso é feito usando uma **aplicação web do Azure** para fornecer os detalhes de subscrição e a configuração que caso contrário, introduzir sempre que configurou um novo componente do Configuration Manager ou o serviço com o Azure.

Com o technical preview 1703, apenas a Windows Store para empresas (WSfB) é configurada ao utilizar este assistente.  Outros serviços em nuvem são configurados utilizando os seus fluxos de trabalho separados.

-   Utilize as informações neste tópico de pré-visualização para substituir os passos de configuração encontradas no [configurar a Windows Store para sincronização de negócios](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization) secção do tópico Current Branch [gerir aplicações a partir do Store do Windows para Empresa-com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

-   Para obter mais informações sobre as aplicações web, consulte [autenticação e autorização no serviço de aplicações do Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview), e [descrição geral das aplicações Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Pré-requisitos e planeamento
Quando configurar uma ligação entre o Configuration Manager e a Windows Store para empresas, tem de fornecer uma pasta onde será mantido sincronizado a partir da loja de conteúdo da aplicação. Para garantir que esta pasta é segura e que seu conteúdo pode ser implementado em dispositivos, certificar-se de que as seguintes permissões são cumpridos:
-   O computador no qual instala a função de sistema do site de ponto de ligação serviço (site de nível superior na hierarquia) tem de ter de leitura e permissões de escrita para a pasta que especificou ao utilizar o **computador$** conta.  

-   O autor da aplicação tem de ter permissões de leitura para a pasta que especificou.  

-   O **computador$** conta de cada computador que aloja uma instância do fornecedor de SMS tem de ser capaz de usar a pasta que especificou.

No Azure Active Directory, registe o Configuration Manager como uma aplicação web ou a ferramenta de gestão de Web API. Esta ação cria o ID de cliente que irá precisar mais tarde.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Utilize o Assistente para configurar o serviço de nuvem WSfB

1. Na consola, aceda a **Administration** > **descrição geral** > **gestão de serviços na Cloud** > **Azure**   >  **Dos serviços do azure**e, em seguida, escolha **configurar os serviços do Azure** para iniciar o **o Assistente de serviços do Azure**.

2. Sobre o **dos serviços do Azure** página, selecione o serviço que pretende configurar e, em seguida, clique em **próxima**. Com esta pré-visualização, pode ser configurada apenas WSfB.

3. Na **gerais** , indique um nome amigável para o **nome do serviço do Azure** e uma descrição opcional e, em seguida, clique em **seguinte**.

4. Sobre o **App** página, especifique o seu ambiente do Azure e, em seguida, clique em **procurar** para abrir a janela de aplicação de servidor.

5. Na **aplicação de servidor** janela, selecione a aplicação de servidor que pretende utilizar e clique em **OK**.
   As aplicações de servidor são as aplicações web do Azure que contêm as configurações para a sua conta do Azure, incluindo o ID de inquilino, ID de cliente e uma chave secreta para clientes. Se não tiver uma aplicação de servidor disponíveis, utilize um dos seguintes:
   - **Criar**: Para criar uma nova aplicação de servidor, clique em **criar**. Forneça um nome amigável para a aplicação e o inquilino. Em seguida, depois que iniciar sessão para o Azure, o Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode visualizá-las no portal do Azure.
   - **Importar**: Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e o inquilino e, em seguida, especifique o ID de inquilino, ID de cliente e a chave secreta da aplicação web do Azure que pretende que o Configuration Manager para utilizar. Depois de **Verifique se** as informações, clique em **OK** para continuar.  </br></br>

6. Reveja os **informações** página e conclua quaisquer passos adicionais e configurações, conforme indicado. Estas configurações são necessárias para utilizar o serviço com o Configuration Manager.
   Por exemplo, para configurar WSfB:

   1. No Azure tem de registar o Configuration Manager como uma aplicação web ou a Web API e registe o ID de cliente. Também pode especificar uma chave de cliente para utilização pela ferramenta de gestão (que é o Configuration Manager).

   2.    Na consola do WSfB tem de configurar o Configuration Manager como a ferramenta de gestão de armazenamento, ativar o suporte para aplicações licenciadas offline e, em seguida, comprar, pelo menos, uma aplicação.   </br>

   Clique em **seguinte** quando estiver pronto para continuar.

7. Sobre o **as configurações de aplicações** página, conclua as configurações de catálogo e o idioma de aplicação para este serviço e, em seguida, clique em **próxima**.
8. Depois de concluir o assistente, a consola do Configuration Manager mostra que configurou **Windows Store para empresas** como um **tipo de serviço de nuvem**.

Agora, pode utilizar o restante dos [conteúdo de Current Branch](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) para gerir aplicações do WSfB para sincronizar, criar e implementar e monitorizar a Windows Store para aplicações de negócio.

### <a name="modify-a-cloud-service-configuration"></a>Modificar uma configuração de serviço cloud
Pode ver e editar as propriedades de um serviço em nuvem para modificar a configuração.

Na consola, aceda a **Administration** > **descrição geral** > **gestão de serviços na Cloud** > **Azure**   >  **Dos serviços do azure**e, em seguida, escolha **configurar os serviços do Azure**, selecione um serviço em nuvem e, em seguida, escolha **propriedades**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização no local
Windows 10 Creators Update introduz uma ferramenta de conversão simples que automatiza o processo para criar novas partições de disco rígido para o hardware preparado para UEFI e integra-se a ferramenta de conversão para o 7 do Windows para o processo de atualização do Windows 10 no local. Ao combiná-essa ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta de OEM que converte o firmware de BIOS para UEFI, pode converter seus computadores de BIOS para UEFI durante uma atualização no local para a atualização para criativos do Windows 10. Para obter detalhes, consulte [passos para gerir o BIOS para conversão de UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

## <a name="collapsible-task-sequence-groups"></a>Grupos de sequências de tarefas minimizáveis
Esta versão apresenta a capacidade para expandir e recolher grupos de sequências de tarefas. Pode expandir ou fechar grupos individuais ou expandir ou fechar todos os grupos de uma só vez.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Definições de cliente para configurar o Windows Analytics para preparação de atualizações
A partir desta versão, pode utilizar as definições de cliente do dispositivo para simplificar a configuração de telemetria Windows necessária para utilizar [Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) soluções como [preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) com Gestor de configuração. O Configuration Manager pode obter dados de análise do Windows que podem fornecer informações valiosas sobre o estado atual do seu ambiente com base nos dados de telemetria Windows enviados pelos computadores cliente. Dados de telemetria do Windows são enviados pelos computadores cliente para o serviço de telemetria do Windows e, em seguida, os dados relevantes, em seguida, são transferidos para soluções de análise de Windows que estão alojadas em uma das áreas de trabalho do OMS da sua organização. Preparação da atualização é uma solução de análise do Windows que pode ajudar a priorizar as decisões sobre as atualizações do Windows para os seus dispositivos geridos.

Para obter informações sobre as definições de telemetria do Windows, consulte [telemetria de configurar o Windows na sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).

### <a name="prerequisites"></a>Pré-requisitos
- Tem de ter configurado seu site para utilizar o serviço de nuvem de preparação de atualizações. Para obter mais informações consulte [preparação de atualizações](/sccm/core/clients/manage/upgrade/upgrade-analytics)

### <a name="configure-windows-analytics-client-settings"></a>Configurar definições de cliente do Windows Analytics
Para configurar a análise do Windows, na consola do Configuration Manager aceda a **Administration** > **definições de cliente**, faça duplo clique em **criar definições personalizadas do dispositivo cliente**  e, em seguida, marque **Windows Analytics**.  

Em seguida, configure o seguinte depois de navegar para o **Windows Analytics** separador definições:
- **ID comercial**  
A chave ID comercial mapeia informações dos dispositivos que gere para a área de trabalho do OMS que aloja os dados de análise do Windows da sua organização. Se já tiver configurado uma chave de ID comercial para utilização com a preparação, use esse ID. Se ainda não tiver uma chave de ID comercial, consulte [gerar a chave de ID comercial]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

- Definir um **nível de telemetria para dispositivos Windows 10**   
Para obter informações sobre o que é recolhido por cada nível de telemetria do Windows 10, consulte [telemetria de configurar o Windows na sua organização]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

- Optar por **optar ativamente por participar na recolha de dados comerciais em dispositivos Windows 7, 8 e 8.1**   
Para informações sobre os dados recolhidos a partir desses sistemas operacionais quando participar, consulte transfira o [eventos de telemetria de appraiser do Windows 7, Windows 8 e Windows 8.1 e campos](https://go.microsoft.com/fwlink/?LinkID=822965) ficheiro pdf da Microsoft.

- **Configurar a recolha de dados do Internet Explore** em dispositivos com o Windows 8.1 ou anterior, a recolha de dados do Internet Explorer pode permitir que a preparação de atualizações detetar incompatibilidades de aplicação web que poderiam impedir uma atualização suave para o Windows 10. Recolha de dados do Internet Explorer pode ser ativada num por base de zona de internet. Para obter mais informações sobre as zonas de internet, consulte [sobre zonas de segurança do URL](https://msdn.microsoft.com/en-us/library/ms537183(v=vs.85).aspx).
