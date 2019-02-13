---
title: Funcionalidades no Technical Preview 1601
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1601.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa96b497ce942430c5a8391eefd41e939c634ae3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56143678"
---
# <a name="capabilities-in-technical-preview-1601-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1601 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1601. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.  

 **Problemas conhecidos desta pré-visualização técnica:**  

-   Quando gere **opções de atualização de cliente** para promover um cliente de pré-produção para produção, o texto da caixa de verificação apresenta uma versão de cliente zero (0) em vez do número de compilação atual do cliente. A versão correta de cliente de pré-produção é apresentada na superfície acima desta opção e é a versão de cliente que é promovida para produção quando seleciona esta opção.  

-   Quando atualizar para a Technical Preview 1601 e escolhendo a testar o cliente do Configuration Manager numa coleção de pré-produção, o pacote de cliente para a coleção não será atualizado. Este problema é apenas na Technical Preview 1601.  

     Para resolver que estes problemas, efetue um dos seguintes:  

    -   Execute o seguinte script SQL na base de dados do site primário:  

        ```  
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Adicione uma nova função de sistema de sites do ponto de distribuição para o seu site de laboratório. O novo ponto de distribuição irá atualizar a coleção de pré-produção com o novo pacote de cliente.  

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

##  <a name="bkmk_hybrid1"></a> Melhoramentos à integração do Microsoft Intune  
No 1601 Technical Preview, foi adicionado suporte para as seguintes funcionalidades:  

### <a name="improvements-to-conditional-access"></a>Melhoramentos ao acesso condicional  

-   **Suporte de acesso condicional para PCs geridos pelo System Center Configuration Manager**  

     Agora pode definir políticas de acesso condicional para PCs geridos pelo System Center Configuration Manager, que irá exigir que os computadores estejam em conformidade com a política de conformidade para aceder aos serviços Exchange Online e SharePoint Online.  Com esta nova funcionalidade, também pode registar PCs com o Azure AD através da política de conformidade e para monitorizar e comunicar no registo do Azure AD.  

    > [!NOTE]  
    >  Acesso condicional ainda não é suportado no Windows 10.  

    Seguem-se os pré-requisitos para utilizar esta funcionalidade:  

    -   Subscrição do Active Directory Premium e ADFS Sync do Azure.  

    -   Uma Subscrição do Microsoft Intune. A subscrição do Microsoft Intune deve ser configurada na consola do Configuration Manager.  

    -   [Pré-requisitos para o registo automático do Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Para utilizar a opção, tem de criar uma política de conformidade no Configuration Manager com regras específicas, descritas abaixo e definir uma política de acesso condicional na consola do Intune.  Além disso, para se certificar-se de que apenas a computadores conformes têm permissão para aceder, tem de definir o requisito do Windows PC como **dispositivos têm de estar em conformidade** opção. Seguem-se as regras de política de conformidade que são aplicáveis a PCs geridos pelo System Center Configuration manager.  

    -   **Exigir registo no Azure Active Directory:** Esta regra verifica se o dispositivo do utilizador é o local de trabalho associado ao Azure AD e, se não estiver, o dispositivo é automaticamente registado no Azure AD. O registo automático é suportado apenas no Windows 8.1. Para PCs Windows 7, implemente um MSI para efetuar o registo automático. Para obter mais informações, consulte [aqui](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Todas as atualizações necessárias instaladas com um prazo mais antigo do que um determinado número de dias:** Esta regra verifica se o dispositivo do utilizador tem todas as atualizações necessárias (especificadas na **atualizações automáticas necessárias** regra) dentro do prazo e o período de tolerância especificada por si e automaticamente instalar quaisquer atualizações necessárias pendentes.  

    -   **Exigir encriptação de unidade de disco BitLocker:** Esta é uma verificação para ver se a unidade principal (por exemplo, c:\\) no dispositivo é encriptada por BitLocker. Se a encriptação Bitlocker não estiver ativada no dispositivo primário, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

    -   **Exigir Antimalware:** Esta é uma verificação para ver se o software antimalware (System Center Endpoint Protection ou apenas o Windows Defender) está ativado e em execução.  
         Se não estiver ativado, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

    Os utilizadores finais que estão bloqueados devido a não conformidade Verão informações de conformidade no Centro de Software do SCCM e iniciar uma nova avaliação de políticas quando os problemas de conformidade estiverem resolvidos.  

-   **Acesso condicional com o serviço de atestado de estado de funcionamento** agora pode restringir o acesso ao e-mail e aos 0365 serviços com base no estado de funcionamento dos dispositivos, conforme comunicado pelo serviço de atestado de estado de funcionamento.  Além disso, os dispositivos que são geridos pelo Intune são incluídos nos relatórios de estado de funcionamento do dispositivo.  

    Foi adicionada uma nova regra de conformidade à consola do configuration manager permite-lhe especificar se os dispositivos devem ser permitidos ou bloqueado o acesso com base no respetivo estado de funcionamento.  Para criar esta regra, abra a **criar Assistente de política de conformidade**e adicionar uma nova regra.  Selecione o **reportado como estado de funcionamento pelo serviço de atestado de estado de funcionamento** para a condição e defina o valor como **verdadeiro**.  Esta ação irá garantir que apenas os dispositivos que são considerados Saudável terão acesso aos recursos da empresa. Para obter detalhes sobre o serviço de atestado de estado de funcionamento e como o estado de funcionamento dos dispositivos é reportado no Intune, consulte [atestado de estado de funcionamento do dispositivo](#bkmk_devicehealth).  

-   **Novas definições de política de conformidade:** As novas definições de política de conformidade ajudam a melhorar a segurança e proteção em dispositivos que são utilizados para aceder ao e-mail da empresa e o SharePoint services:  

    -   **Exigir atualizações automáticas:** Pode exigir que os dispositivos com Windows 8.1 ou posterior para permitir a instalação automática de atualizações e também de especificar a classe de atualizações que estão instalados.  Pode optar por: instalar apenas as atualizações marcadas como importantes ou instalar todas as atualizações recomendadas.  

         Para criar uma regra para atualizações automáticas, abra a **criar Assistente de política de conformidade**e adicionar uma nova regra.  Selecione **classificação mínima de atualizações necessárias** como condição e defina o valor como um dos valores disponíveis: **NONE**, **recomendado**, e **importante**.  

        -   **Nenhum:** As atualizações não são instaladas automaticamente.  

        -   **Recomendado:** Todas as atualizações recomendadas são instaladas  

        -   **Importante:** Apenas as atualizações classificadas como importantes são instaladas.  

    -   **Exigir uma palavra-passe para desbloquear dispositivos móveis:** Quando esta definição está definida como **Sim**, os utilizadores finais tem de introduzir uma palavra-passe antes de poderem aceder ao respetivo dispositivo.  

         Para criar uma regra para palavra-passe desbloquear dispositivos móveis, abra a **criar Assistente de política de conformidade**e adicionar uma nova regra. Selecione **exigir uma palavra-passe para desbloquear um dispositivo inativo** como a condição e defina o valor como **verdadeiro**.  

    -   **Minutos de inatividade antes de palavra-passe é exigida:**  Especifica o tempo inativo antes de o utilizador ter de reintroduzir a palavra-passe.  

         Para criar esta regra, abra a **criar Assistente de política de conformidade**e adicionar uma nova regra. **Selecione os minutos de inatividade antes de palavra-passe é exigida** como condição e defina o valor como uma das opções disponíveis: 1 minuto, 5 minutos, 15 minutos, 30 minutos, eu hora.  

-   **Substituição da regra predefinida - permitir sempre aos dispositivos em conformidade e inscritos no Intune aceder ao Exchange no local:**  

     Quando seleciona esta opção, os dispositivos que estão inscritos no Intune e em conformidade com as políticas de conformidade têm permissão para aceder ao Exchange no local. Esta regra substitui a regra predefinida, que significa que mesmo que defina a regra predefinida para colocar em quarentena ou bloquear o acesso, inscritos e em conformidade com dispositivos ainda será possível aceder ao Exchange no local.  
     Utilize esta definição se pretender que inscritos e dispositivos em conformidade tenham sempre acesso ao e-mail através do Exchange no local.  

     Isto é suportado nas seguintes plataformas:  Windows Phone 8 e posterior, iOS 6 e posterior. Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior.  

     Para utilizar esta opção, vá para o **gerais** página do **configurar Assistente de política de acesso condicional** para o Exchange no local.  

##  <a name="bkmk_clientStatus"></a> Estado online do cliente  
A partir do technical preview 1601, pode identificar rapidamente se um cliente está online ou offline na consola do Configuration Manager. Com ícones atualizados e colunas nas listagens de dispositivo da consola, pode avaliar o estado de clientes no seu ambiente para identificar áreas problemáticas e outros problemas que poderão ter a sua atenção.  

Um cliente está online se estiver atualmente ligado a uma função de sistema de sites do ponto de gestão do Configuration Manager. Desde que o ponto de gestão está a receber mensagens do tipo ping do cliente, o respetivo estado é online. Se a gestão não receber uma mensagem para 5 minutos, o estado do cliente é alterado para offline.  

### <a name="icons-for-client-status"></a>Ícones de estado do cliente  

|||  
|-|-|  
|![ícone de estado online dos clientes](media/online-status-icon.png)|O cliente está online.|  
|![ícone de estado offline dos clientes](media/offline-status-icon.png)|O cliente está offline.|  
|![ícone de estado desconhecido dos clientes](media/unknown-status-icon.png)|Estado do cliente é desconhecido.|  

### <a name="prerequisites"></a>Pré-requisitos  
 Estado online do cliente não tem pré-requisitos. Pode começar a usá-lo assim que o Configuration Manager pré-visualização técnica 1601 está instalado.  

### <a name="limitations"></a>Limitações  
 Estado online do cliente só está disponível para computadores Windows com o cliente do Configuration Manager instalado. Estado online do cliente não é suportado para computadores Mac, Linux ou UNIX computador ou dispositivos geridos com no\-no local a gestão de dispositivos móveis.  

### <a name="to-view-client-online-status"></a>Para ver o estado online do cliente  

1. Na consola do Configuration Manager, aceda a **ativos e compatibilidade > Descrição geral > dispositivos**.  

2. Faça duplo clique no cabeçalho da coluna e, em seguida, clique em um dos campos de estado online do cliente para adicioná-lo à vista do dispositivo. Os campos são  

   -   **Estado Online do Dispositivo** indica se o cliente está atualmente online ou offline.  

   -   **Última vez Online** indica se o estado online do cliente mudou de offline para online.  

   -   **Última vez Offline** indica se o estado mudou de online para offline.  

   Para mostrar as alterações recentes ao estado do cliente, atualize a consola.  

##  <a name="bkmk_appmgmt1601"></a> Melhorias à gestão de aplicações  
 No 1601 Technical Preview foi adicionado suporte para as seguintes funcionalidades:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerir aplicações compradas em grandes volumes para dispositivos iOS  
 Algumas lojas de aplicações permitem comprar várias licenças para uma aplicação que pretende executar na sua empresa. Isto ajuda a reduzir a sobrecarga administrativa de controlar várias cópias adquiridas de aplicações.  

 Agora o Configuration Manager ajuda a gerir aplicações compradas através de um programa ao importar as informações da licença da loja de aplicações e ao controlar a quantidade de licenças utilizou.  

 Para obter detalhes, consulte [gerir aplicações compradas através de um programa de compra em volume com o Configuration Manager](https://technet.microsoft.com/library/mt627954.aspx).  

### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS - configuração de aplicação para aplicações<br />Híbrido  
 Algumas aplicações iOS suportam a pré-configuração de definições, tais como um servidor ou base de dados a que a aplicação deve estabelecer ligação. O Configuration Manager suporta agora implementar aplicações políticas de configuração para o dispositivo que permitem que o utilizador utilize a aplicação imediatamente sem necessitar de conhecer estas informações. Os desenvolvedores tem de ativar esta funcionalidade nas suas aplicações.  

 Um número limitado de aplicações lançadas ao público suporta atualmente a pré-configuração de definições; Pode também ter desenvolvidos internamente aplicações linha de negócio que suportá-las.  

#### <a name="prerequisites-for-this-scenario"></a>Pré-requisitos para este cenário  

-   Tem de ter adicionado uma subscrição do Microsoft Intune ao Configuration Manager.  

-   Tem de ter adicionado um certificado do Apple APNs válido à subscrição do Intune.  

-   Tem de estar implementada uma aplicação iOS que suporte a configuração de aplicação.  

#### <a name="try-it-out"></a>Experimente!  
 Assim que são cumpridos os pré-requisitos acima, tem de criar uma aplicação do Configuration Manager que utiliza um tipo de implementação iOS. A aplicação que utilizar tem de suportar a configuração de aplicação. Consulte a documentação do fornecedor da aplicação para saber que itens específicos (pares nome/valor), pode configurar.  

 Em seguida, associar a política de configuração de aplicação com o tipo de implementação iOS durante a implementação de aplicação. Também pode implementar a política a partir da **políticas de configuração de aplicação** nó, direcionado para uma aplicação existente e a coleção.  

 Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de feedback perto da parte superior deste tópico para nos informar como correu:  

-   Se tiver uma aplicação iOS que suporta a configuração de aplicações, consulte a documentação do fornecedor da aplicação para descobrir os pares de nome / valor que tem de especificar para configurar a aplicação.  

-   Iniciar o **criar política de configuração de aplicação** assistente. Sobre o **política para iOS** página do assistente, tente adicionar os pares de nome e valor que encontrou a documentação do fornecedor de aplicação, ou podem importar um ficheiro XML que contém os valores necessários.  

-   Na **implementação de Software** assistente, na **política de configuração de aplicação** página, associe a política de configuração de aplicação que criou com um tipo de implementação compatível da aplicação.  

##  <a name="bkmk_compliance1601"></a> Melhoramentos às definições de conformidade  
 No 1601 Technical Preview foi adicionado suporte para as seguintes funcionalidades:  

### <a name="microsoft-edge-browser-settings"></a>Definições do browser Microsoft Edge  
 Foram adicionadas novas definições para o browser Microsoft Edge para o **Windows 8.1 e Windows 10** item de configuração (definições aplicáveis apenas a dispositivos Windows 10).  

 Para ver as novas definições, escolha **Microsoft Edge** do item de configuração **definições do dispositivo** página do **criação de Item de configuração** assistente.  

 Para obter mais informações, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Definições de conformidade para dispositivos Windows 10 Team  
 Utilize estas novas definições de compatibilidade para configurar dispositivos que executam o Windows 10 team, tais como os dispositivos Surface Hub.  

 Para ver as novas definições, escolha **Windows 10 Team** do item de configuração **definições do dispositivo** página do **criação de Item de configuração** assistente.  

 Para obter mais informações, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android - modo de local público para Samsung KNOX Standard<br />Híbrido  
 Modo de local público permite-lhe bloquear um dispositivo para permitir que apenas determinadas funcionalidades funcionem. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo ou para um dispositivo com a finalidade de desempenhar apenas uma função, como um dispositivo de ponto de venda. Estas definições não estão disponíveis para dispositivos Samsung KNOX Standard no **Windows 8.1 e Windows 10** item de configuração (definições aplicáveis apenas a dispositivos Windows 10).  

 Para ver as novas definições, escolha **modo de local público - Samsung KNOX** do item de configuração **definições do dispositivo** página do **criação de Item de configuração** assistente.  

 Para obter mais informações, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
