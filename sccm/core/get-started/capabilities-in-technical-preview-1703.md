---
title: "Capacidades na pré-visualização técnica 1703 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1703."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4cb711f369698fe8e045f8c83dd96ec6fb29d70
ms.openlocfilehash: bb1b96a56db68dcea22270855b899ba3a90afd0d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1703-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1703 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1703. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementar aplicações iOS adquiridos de volume em coleções de dispositivos

Pode agora implementar aplicações licenciadas dispositivos, bem como os utilizadores. Dependendo da capacidade de aplicações para suportar o dispositivo de licenciamento, uma licença adequada irá ser reclamada quando implementá-la, da seguinte forma:

|||||
|-|-|-|-|
|Versão do Configuration Manager|A aplicação suporta licenciamento do dispositivo?|Tipo de coleção de implementação|Licença alegada|
|Anteriores ao 1702|Sim|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Não|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Sim|Dispositivo|Licença de utilizador|
|Anteriores ao 1702|Não|Dispositivo|Licença de utilizador|
|1702 e posterior|Sim|Utilizador|Licença de utilizador|
|1702 e posterior|Não|Utilizador|Licença de utilizador|
|1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|1702 e posterior|Não|Dispositivo|Licença de utilizador|

Para mais informações sobre as aplicações iOS adquiridos de volume, consulte o artigo [gerir aplicações iOS adquiridos volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

## <a name="direct-links-to-applications-in-software-center"></a>Ligações diretas para aplicações no Centro de Software

Agora pode fornecer aos utilizadores finais com uma ligação direta a uma aplicação no Centro de Software. Isto significa que já não tem de abrir o Centro de Software e a pesquisa para uma aplicação antes de poderem instalar. Isto só está disponível para o Configuration Manager aplicações, não pacotes e programas ou sequências de tarefas.

### <a name="try-it-out"></a>Experimente                 

Utilize o seguinte formato de URL para abrir o Centro de Software para uma determinada aplicação:

**Softwarecenter:SoftwareId =*identificador da aplicação***

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Como obter o identificador da aplicação de uma aplicação.

1.    Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2.    Na área de trabalho biblioteca de Software, expanda **gestão de aplicações**e, em seguida, clique em **aplicações**.
3.    No **aplicações** ver, faça duplo clique dos cabeçalhos de coluna e, em seguida, na lista, selecione **ID único do IC**. Verá que o ID exclusivo de cada aplicação é agora apresentado na lista.
4.    Tenha em atenção o **ID único do IC** da aplicação que pretende fornecer uma ligação para, por exemplo: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5.    Em seguida, remover qualquer texto a seguir a aplicação GUID, neste caso **/2**. Isso deixa o identificador da aplicação.
6.    Por fim, para concluir a construir a ligação, preceda-o com **Softwarecenter:SoftwareID =**. Utilizando o exemplo acima, irá ler a ligação final: **Softwarecenter:SoftwareId = ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Ao utilizar esta ligação, os utilizadores finais podem abrir o Centro de Software diretamente para a aplicação que especificou.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certificados PFX para computadores cliente do Windows do Configuration Manager

Agora pode implementar perfis de certificado PFX importadas para computadores de cliente do Configuration Manager com o Windows 10.

### <a name="try-it-out"></a>Experimente

Utilize as instruções no [como criar perfis de certificado PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) para importar um perfil PFX, implemente o perfil e, em seguida, verifique se o certificado foi instalado para o utilizador de destino.



## <a name="configure-azure-services-wizard"></a>Configurar o Assistente de serviços do Azure
Pré-visualização técnica 1703 introduz o **configurar serviços do Azure** assistente. Este assistente fornece-lhe uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os serviços em nuvem que utiliza com o Configuration Manager. Isto é feito através da utilização de um **Azure web app** para fornecer os detalhes de configuração e de subscrição que caso contrário, introduzir sempre que configura um novo componente do Configuration Manager ou o serviço com o Azure.

Com a pré-visualização técnica 1703, apenas da loja Windows para empresas (WSfB) é configurada ao utilizar este assistente.  Outros serviços em nuvem são configurados utilizando os seus fluxos de trabalho separados.

-    Utilize as informações neste tópico de pré-visualização para substituir os passos de configuração encontradas no [configurar da loja Windows para a sincronização de empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization) secção do ramo atual tópico [gerir aplicações na loja Windows para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

-    Para obter mais informações sobre o web apps, consulte o artigo [autenticação e autorização no serviço de aplicação do Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview), e [descrição geral de aplicações Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Pré-requisitos e planeamento
Ao configurar uma ligação entre o Configuration Manager e a loja Windows para empresas, tem de fornecer uma pasta onde o conteúdo de aplicação sincronizado a partir do arquivo de será mantido. Para se certificar de que esta pasta é segura e que o respetivo conteúdo pode ser implementado nos dispositivos, certifique-se as seguintes permissões no local:
-    O computador no qual instala a função de sistema de sites de ponto de ligação service (site de nível superior na hierarquia) tem de ter para ler e escrever as permissões na pasta que especificou ao utilizar o **computador$** conta.  

-    O autor da aplicação tem de ter permissões de leitura para a pasta que especificou.  

-    O **computador$** conta de cada computador que aloja uma instância do fornecedor de SMS tem de ser possível utilizar a pasta que especificou.

No Azure Active Directory, registe o Configuration Manager como uma aplicação web ou a ferramenta de gestão de Web API. Esta ação cria o ID de cliente que irá precisar mais tarde.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Utilize o Assistente para configurar o serviço de nuvem WSfB

1. Na consola, vá para **administração** > **descrição geral** > **gestão de serviços de nuvem** > **Azure** > **serviços do Azure**e, em seguida, escolha **configurar serviços do Azure** para iniciar o **Assistente de serviços do Azure**.

2. No **serviços do Azure** página, selecione o serviço que pretende configurar e, em seguida, clique em **seguinte**. Com esta pré-visualização, WSfB só pode ser configurado.

3. No **geral** página, forneça um nome amigável para a **nome do serviço Azure** e uma descrição opcional e, em seguida, clique em **seguinte**.

4. No **App** página, especifique o seu ambiente do Azure e, em seguida, clique em **procurar** para abrir a janela de aplicação de servidor.

5. No **aplicação Server** janela, selecione a aplicação de servidor que pretende utilizar e, em seguida, clique em **OK**.
Aplicações de servidor são as aplicações Azure web que contêm as configurações para a sua conta Azure, incluindo o seu ID de inquilino, ID de cliente e uma chave secreta para clientes. Se não tiver uma aplicação de servidor disponíveis, utilize um dos seguintes procedimentos:
  -    **Criar**: Para criar uma nova aplicação de servidor, clique em **criar**. Forneça um nome amigável para a aplicação e o inquilino. Em seguida, depois de a início de sessão para o Azure, Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode ver estas partir do portal do Azure.
  -    **Importar**: Para utilizar uma aplicação web que já exista na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e o inquilino e, em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação Azure web que pretende utilizar o Configuration Manager. Após **verificar** as informações, clique em **OK** para continuar.  </br></br>

6. Rever o **informações** página e conclua os passos adicionais e configurações conforme indicado. Estas configurações são necessárias para utilizar o serviço com o Configuration Manager.
Por exemplo, para configurar WSfB:

  1. No Azure tem de registar o Configuration Manager como uma aplicação web ou de uma Web API e gravar o ID de cliente. Pode também especificar uma chave de cliente para utilização pela ferramenta de gestão (que é o Configuration Manager).

  2.    Na consola do WSfB tem de configurar do Configuration Manager como a ferramenta de gestão de arquivo, ativar o suporte para aplicações licenciadas offline e, em seguida, comprar pelo menos uma aplicação.   </br>

  Clique em **seguinte** quando estiver pronto para continuar.

7. No **App configurações** página, conclua as configurações de idioma e o catálogo de aplicações para este serviço e, em seguida, clique em **seguinte**.
8. Depois de concluído o assistente, a consola do Configuration Manager mostra que foram configurados **da loja Windows para empresas** como um **tipo de serviço de nuvem**.

Agora pode utilizar o resto do [conteúdo ramo atual](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) para gerir aplicações a partir de WSfB para sincronizar, criar e implementar e monitorizar as aplicações da empresa da loja Windows.

### <a name="modify-a-cloud-service-configuration"></a>Modificar uma configuração de serviço de nuvem
Pode ver e editar as propriedades de um serviço em nuvem para modificar a configuração.

Na consola de ir para **administração** > **descrição geral** > **gestão de serviços de nuvem** > **Azure** > **serviços do Azure**e, em seguida, escolha **configurar serviços do Azure**, selecione um serviço em nuvem e, em seguida, selecione **propriedades**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização no local
Atualização do Windows 10 criadores apresenta uma ferramenta de conversão simples que automatiza o processo para criar partições do disco rígido para o hardware preparados para UEFI e integra-se a ferramenta de conversão para o Windows 7 para o processo de atualização de no local do Windows 10. Esta ferramenta se as combinar com a sequência de tarefas de atualização do sistema operativo e a ferramenta do OEM que converte o firmware de BIOS UEFI, pode converter os computadores de BIOS para UEFI durante uma atualização no local para a atualização de criadores do Windows 10. Para obter mais detalhes, consulte o artigo [tarefas passos de sequência para gerir BIOS para conversão de UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

## <a name="collapsible-task-sequence-groups"></a>Grupos de sequências de tarefas expansíveis
Esta versão introduzirá a capacidade de expandir e fechar grupos de sequências de tarefas. Pode expandir ou fechar grupos individuais ou expandir ou fechar todos os grupos em simultâneo.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Definições de cliente para configurar o Windows Analytics para a preparação da atualização
Iniciar com esta versão, pode utilizar as definições de cliente de dispositivo para simplificar a configuração da telemetria do Windows necessária para utilizar [Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) soluções como [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) com o Configuration Manager. O Configuration Manager pode obter dados a partir do Windows Analytics que podem fornecer informações valiosas para o estado atual do seu ambiente baseada nos dados de telemetria de Windows enviados pelos computadores cliente. Dados de telemetria do Windows são enviados pelos computadores cliente ao serviço de telemetria do Windows e, em seguida, os dados relevantes subsequentemente for transferidos para soluções de análise do Windows que estão alojadas dos OMS as áreas de trabalho da sua organização. Preparação para atualização é uma solução de análise do Windows que pode ajudar a atribuir prioridades a tomar decisões sobre a atualização do Windows para os seus dispositivos geridos.

Para obter informações sobre definições de telemetria do Windows, consulte o artigo [telemetria configurar janelas na sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).

### <a name="prerequisites"></a>Pré-requisitos
- Tem de ter configurado o site para utilizar o serviço de nuvem de preparação para atualização. Para mais informações consulte [preparação para atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics)

### <a name="configure-windows-analytics-client-settings"></a>Configurar definições de cliente Windows Analytics
Para configurar o Windows Analytics, na consola do Configuration Manager vá para **administração** > **definições de cliente**, faça duplo clique **criar definições personalizadas do dispositivo cliente** e, em seguida, verifique **Windows Analytics**.  

Em seguida, configure o seguinte procedimento depois de navegar para o **Windows Analytics** separador definições:
- **ID comercial**  
A chave de ID comercial maps informações a partir dos dispositivos geridos por si a área de trabalho do OMS que aloja os dados de análise do Windows da sua organização. Se já tiver configurado uma chave de ID comercial para utilização com preparação para atualização, utilize esse ID. Se ainda não tem uma chave de ID comercial, consulte o artigo [gerar a chave de ID comercial]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

- Definir um **nível de telemetria para dispositivos Windows 10**   
Para obter informações sobre o que é recolhido por cada nível de telemetria do Windows 10, consulte o artigo [telemetria configurar janelas na sua organização]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

- Optar por **a possibilidade da recolha de dados comercial em dispositivos Windows 7, 8 e 8.1**   
Para informações sobre dados recolhidos a partir desses sistemas operativos quando é a possibilidade de, consulte o artigo transferir o [eventos de telemetria appraiser Windows 7, Windows 8 e Windows 8.1 e campos](https://go.microsoft.com/fwlink/?LinkID=822965) ficheiro pdf a partir de Microsoft.

- **Configurar a recolha de dados Internet explorar** em dispositivos com Windows 8.1 ou anterior, recolha de dados do Internet Explorer pode permitir que a atualização preparação detetar incompatibilidades da aplicação web que foi impedem uma atualização suave para Windows 10. Recolha de dados do Internet Explorer pode ser ativada num por base de zona de internet. Para mais informações sobre as zonas de internet, consulte o artigo [sobre das zonas de segurança URL](https://msdn.microsoft.com/en-us/library/ms537183(v=vs.85).aspx).
