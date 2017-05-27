---
title: "Capacidades na pré-visualização técnica 1601 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1601."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: ef0db5b11ae2be5edcb4db87400c5c273c89972e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1601-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1601 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1601. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.  

 **Problemas conhecidos para esta pré-visualização técnica:**  

-   Quando gerir **opções de atualização de cliente** para promover um cliente de pré-produção para produção, o texto para a caixa de verificação apresenta uma versão cliente do zero (0) em vez do número de compilação atual do cliente. A versão correta de cliente de pré-produção é apresentada na superfície acima esta opção e é a versão de cliente é promovida para produção quando selecionar esta opção.  

-   Quando a atualização para o técnico de pré-visualização de 1601 e escolhendo testar o cliente do Configuration Manager numa coleção de pré-produção, o pacote de cliente para a coleção não serão atualizados. Este problema é apenas para o técnico de pré-visualização de 1601.  

     A solução este problemas, efetue um da seguir:  

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

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="bkmk_hybrid1"></a>Melhoramentos para integração do Microsoft Intune  
O 1601 pré-visualização técnica, adicionámos suporte para as seguintes funcionalidades:  

### <a name="improvements-to-conditional-access"></a>Melhoramentos de acesso condicional  

-   **Suporte de acesso condicional para PCs que são geridos pelo System Center Configuration Manager**  

     Agora pode configurar políticas de acesso condicional para PCs geridos pelo System Center Configuration Manager, que irá necessitar que os PCs estar em conformidade com a política de conformidade para aceder aos serviços Exchange Online e no SharePoint Online.  Com esta nova funcionalidade, pode também registar PCs com o Azure AD através da política de conformidade e para monitorizar e comunicar no registo do Azure AD.  

    > [!NOTE]  
    >  Acesso condicional ainda não é suportado no Windows 10.  

    Seguem-se os pré-requisitos para utilizar esta funcionalidade:  

    -   Azure Active Directory Premium subscrição e a sincronização de ADFS.  

    -   Uma Subscrição do Microsoft Intune. Subscrição do Microsoft Intune devem ser configurada na consola do Configuration Manager.  

    -   [Pré-requisitos para o Azure AD auto-registo](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Para utilizar a opção, tem de criar uma política de conformidade no Configuration Manager com regras específicas, descritas abaixo e definir uma política de acesso condicional na consola do Intune.  Além disso, para se certificar de PCs apenas compatíveis são permissão de acesso, tem de definir o requisito de PC do Windows **dispositivos têm de ser compatíveis** opção. Seguem-se as regras de política de conformidade que são aplicáveis ao PCs geridos pelo System Center Configuration manager.  

    -   **Exigir registo no Azure ActiveDirectory:** Esta regra verifica se o dispositivo do utilizador é o local de trabalho associado para o Azure AD e se não estiver, o dispositivo está automaticamente registado no Azure AD. O registo automático é suportado apenas no Windows 8.1. Para PCs Windows 7, implemente um MSI para efetuar o registo automático. Para obter mais informações, consulte o artigo [aqui](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Todas as atualizações necessárias instaladas com um prazo mais antigo do que um determinado número de dias:** Esta regra verifica ver se o dispositivo do utilizador tem todas as atualizações necessárias (especificado no **necessárias atualizações automáticas** regra) dentro do prazo e período de tolerância especificada por si e automaticamente instalar qualquer pendentes atualizações necessárias.  

    -   **Exigir encriptação de unidade BitLocker:** Esta é uma verificação de para ver se a unidade principal (por exemplo, c:\\) no dispositivo é BitLocker encriptado. Se a encriptação Bitlocker não estiver ativada no dispositivo primário, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

    -   **Exigir proteção contra software maligno:** Esta é uma verificação de para ver se o software antimalware (System Center Endpoint Protection ou apenas o Windows Defender) está ativado e em execução.  
         Se não estiver ativado, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

    Os utilizadores finais que estão bloqueados devido a incompatibilidade irão ver informações de compatibilidade no Centro de Software do SCCM e serão iniciada uma avaliação das políticas do novo quando são remediados problemas de compatibilidade.  

-   **Acesso condicional com o serviço de integridade de atestado** agora pode restringir o acesso ao e-mail e 0365 serviços baseados o estado de funcionamento dos dispositivos, conforme comunicado pelo serviço de integridade de atestado.  Além disso, os dispositivos que são geridos pelo Intune são incluídos nos relatórios de estado de funcionamento do dispositivo.  

    Foi adicionada uma nova regra de compatibilidade para a consola do configuration manager que permite-lhe especificar se os dispositivos devem ser permitidos ou bloquear o acesso com base no respetivo estado de funcionamento.  Para criar esta regra, abra o **criar Assistente de política de conformidade**e adicionar uma nova regra.  Selecione o **comunicado como estado de funcionamento pelo serviço de integridade de atestado** para a condição e defina o valor como **verdadeiro**.  Isto irá Certifique-se de que apenas dispositivos que são considerados Saudável terão acesso aos recursos da empresa. Para obter detalhes sobre o serviço de integridade de atestado e como é reportado o estado de funcionamento dos dispositivos no Intune, consulte o artigo [atestado de estado de funcionamento do dispositivo](#bkmk_devicehealth).  

-   **Novas definições de política de conformidade:** As novas definições de política de conformidade ajudam a melhorar a segurança e proteção nos dispositivos que são utilizados para aceder ao e-mail da empresa e do SharePoint services:  

    -   **Requerer atualizações automáticas:** É possível requerer dispositivos com Windows 8.1 ou posterior para permitir a instalação automática das atualizações e especifique também a classe de atualizações que estão instalados.  Pode optar por optar por: instalar apenas atualizações marcadas como importantes ou instalar atualizações de todos os recomendado.  

         Para criar uma regra para as atualizações automáticas, abra o **criar Assistente de política de conformidade**e adicionar uma nova regra.  Selecione **classificação mínima de atualizações necessárias** como a condição e defina o valor para um dos valores disponíveis: **Nenhum**, **recomendado**, e **importante**.  

        -   **Nenhum:** As atualizações não são instaladas automaticamente.  

        -   **Recomendada:** Todas as atualizações recomendadas estão instaladas  

        -   **Importante:** Apenas as atualizações classificadas como importantes estão instaladas.  

    -   **Exigir uma palavra-passe para desbloquear os dispositivos móveis:** Quando esta definição está definida como **Sim**, utilizadores finais tem de introduzir uma palavra-passe antes de poderem aceder ao respetivo dispositivo.  

         Para criar uma regra para palavra-passe para desbloquear os dispositivos móveis, abra o **criar Assistente de política de conformidade**e adicionar uma nova regra. Selecione **exigir uma palavra-passe para desbloquear um dispositivo inativo** como a condição e defina o valor como **verdadeiro**.  

    -   **Minutos de inatividade antes da palavra-passe é exigida:**  Especifica o tempo inativo antes de o utilizador ter de reintroduzir a palavra-passe.  

         Para criar esta regra, abra o **criar Assistente de política de conformidade**e adicionar uma nova regra. **Selecione os minutos de inatividade antes da palavra-passe é exigida** como a condição e defina o valor para uma das opções disponíveis: 1 minuto, 5 minutos, 15 minutos, 30 minutos, posso hora.  

-   **Predefinição Ignorar regra - permitir sempre inscritos do Intune e dispositivos compatíveis aceder ao Exchange no local:**  

     Quando seleciona esta opção, os dispositivos inscritos no Intune e em conformidade com as políticas de conformidade estão autorizados a aceder ao Exchange no local. Esta regra substitui a regra predefinida, o que significa que mesmo que defina a regra predefinida para colocar em quarentena ou bloquear o acesso, inscritos e dispositivos compatíveis com continuará a poder aceder ao Exchange no local.  
     Utilize esta definição quando pretender inscritos e dispositivos compatíveis para têm sempre acesso ao correio eletrónico através do Exchange no local.  

     Isto é suportado nas seguintes plataformas:  Windows Phone 8 e posterior, iOS 6 e posterior. Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior.  

     Para utilizar esta opção, vá para o **geral** página do **configurar Assistente de política de acesso condicional** para Exchange no local.  

##  <a name="bkmk_clientStatus"></a>Estado do cliente online  
A partir da pré-visualização técnica 1601, pode identificar rapidamente se um cliente está online ou offline na consola do Configuration Manager. Com ícones atualizados e colunas nas listagens do dispositivo de consola, pode avaliar o estado dos clientes no seu ambiente para identificar áreas problemáticas e outros problemas que poderão ter a sua atenção.  

Um cliente está online, se está atualmente ligado a uma função de sistema de sites do ponto de gestão do Configuration Manager. Desde que o ponto de gestão está a receber mensagens de como o ping do cliente, o respetivo estado é online. Se a gestão não receber uma mensagem para 5 minutos ou -lo, o estado do cliente é alterado para offline.  

### <a name="icons-for-client-status"></a>Ícones de estado do cliente  

|||  
|-|-|  
|![ícone de estado online dos clientes](media/online-status-icon.png)|Cliente está online.|  
|![ícone de estado offline dos clientes](media/offline-status-icon.png)|Cliente estiver offline.|  
|![ícone de estado desconhecido dos clientes](media/unknown-status-icon.png)|Estado do cliente é desconhecido.|  

### <a name="prerequisites"></a>Pré-requisitos  
 Estado do cliente online não tem nenhum pré-requisito. Pode começar a utilizá-lo assim que o Configuration Manager pré-visualização técnica 1601 está instalado.  

### <a name="limitations"></a>Limitações  
 Estado do cliente online só está disponível para computadores com o Windows com o cliente do Configuration Manager instalado. Estado do cliente online não é suportado para computadores Mac, Linux ou UNIX computador ou dispositivos geridos no\-local gestão de dispositivos móveis.  

### <a name="to-view-client-online-status"></a>Para ver o estado do cliente online  

1.  Na consola do Configuration Manager, aceda a **ativos e compatibilidade > Descrição geral > dispositivos**.  

2.  Com o botão direito no cabeçalho da coluna e, em seguida, clique em um dos campos de estado online do cliente para adicioná-lo para a vista do dispositivo. Os campos são  

    -   **Estado Online do Dispositivo** indica se o cliente está atualmente online ou offline.  

    -   **Última hora Online** indica quando o estado do cliente online mudou de offline para online.  

    -   **Última hora Offline** indica quando o estado mudou de online para offline.  

 Para mostrar as alterações recentes estado do cliente, atualize a consola.  

##  <a name="bkmk_appmgmt1601"></a>Melhorias na gestão de aplicações  
 A pré-visualização técnica do 1601 adicionámos suporte para as seguintes funcionalidades:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerir aplicações compradas em grandes volumes para dispositivos iOS  
 Algumas lojas de aplicações dão-lhe a capacidade de comprar várias licenças para uma aplicação que pretende executar na sua empresa. Isto ajuda a reduzir a sobrecarga administrativa de controlar várias cópias adquiridas de aplicações.  

 Gestor de configuração agora ajuda-o a gerir aplicações comprado através de um programa ao importar as informações da licença da loja de aplicações e controlar o número das licenças que utilizou.  

 Para obter mais detalhes, consulte o artigo [gerir aplicações comprado através de um programa de compra do volume com o Configuration Manager](https://technet.microsoft.com/library/mt627954.aspx).  

### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS - configuração da aplicação para aplicações<br />Híbrido  
 Algumas aplicações iOS suportam a pré-configuração de definições, tais como um servidor ou base de dados a que a aplicação deve estabelecer ligação. O Configuration Manager suporta agora implementar aplicações políticas de configuração para o dispositivo que permitem ao utilizador para utilizar a aplicação imediatamente sem necessitar de conhecer estas informações. Os programadores tem de ativar esta funcionalidade nas suas aplicações.  

 Um número limitado de aplicações publicamente lançadas atualmente suporta a pré-configurar definições; poderá também tenha in-house programado linha de negócio que suportam estas.  

#### <a name="prerequisites-for-this-scenario"></a>Pré-requisitos para este cenário  

-   Deve ter adicionado uma subscrição do Microsoft Intune ao Configuration Manager.  

-   Tem de ter adicionado um certificado do Apple APNs válido à subscrição do Intune.  

-   Tem de estar implementada uma aplicação do iOS que suporta a configuração da aplicação.  

#### <a name="try-it-out"></a>Experimente!  
 Assim que são cumpridos os pré-requisitos acima, terá de criar uma aplicação do Configuration Manager que utiliza um tipo de implementação do iOS. A aplicação que utiliza tem de suportar configuração da aplicação. Consulte a documentação do fornecedor da aplicação para saber que itens específicos (pares nome/valor), pode configurar.  

 Em seguida, associar a política de configuração de aplicação com o tipo de implementação de iOS durante a implementação de aplicação. Também é possível implementar a política a partir de **políticas de configuração de aplicação** nó, direcionada para uma aplicação existente e a recolha.  

 Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de comentários perto da parte superior deste tópico para nos transmitir como trabalharam:  

-   Se tiver uma aplicação iOS que suporta a configuração da aplicação, consulte a aplicação documentação do fornecedor para descobrir os pares de nome e o valor que tem de especificar a configurar a aplicação.  

-   Iniciar o **criar política de configuração de aplicação** assistente. No **política para iOS** página do assistente, tente adicionar os pares de nome e valor encontrar a documentação do fornecedor de aplicação ou podem importar um ficheiro XML que contém os valores necessários.  

-   No **Implementar Software** assistente, no **política de configuração de aplicação** página, associar a política de configuração de aplicação que criou com um tipo compatível de implementação da aplicação.  

##  <a name="bkmk_compliance1601"></a>Foram introduzidos melhoramentos nas definições de compatibilidade  
 A pré-visualização técnica do 1601 adicionámos suporte para as seguintes funcionalidades:  

### <a name="microsoft-edge-browser-settings"></a>Definições do browser Microsoft Edge  
 Foram adicionadas novas definições do browser Microsoft Edge para o **Windows 8.1 e Windows 10** item de configuração (definições aplicam-se para apenas para dispositivos Windows 10).  

 Para ver as novas definições, selecione **Microsoft Edge** do item de configuração **definições do dispositivo** página do **Criar Item de configuração** assistente.  

 Para obter mais informações, consulte o artigo [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Definições de compatibilidade para dispositivos Windows 10 Team  
 Utilize estas novas definições de compatibilidade para configurar dispositivos que executam o Windows 10 equipa, tais como superfície Hub dispositivos.  

 Para ver as novas definições, selecione **Windows 10 Team** do item de configuração **definições do dispositivo** página do **Criar Item de configuração** assistente.  

 Para obter mais informações, consulte o artigo [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android - modo de local público para o Samsung KNOX Standard<br />Híbrido  
 Modo de local público permite-lhe bloquear um dispositivo para permitir apenas determinadas funcionalidades funcionem. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo ou para um dispositivo com a finalidade de desempenhar apenas uma função, como um dispositivo de ponto de venda. Estas definições não estão disponíveis para dispositivos Samsung KNOX Standard no **Windows 8.1 e Windows 10** item de configuração (definições aplicam-se para apenas para dispositivos Windows 10).  

 Para ver as novas definições, selecione **modo de local público - Samsung KNOX** do item de configuração **definições do dispositivo** página do **Criar Item de configuração** assistente.  

 Para obter mais informações, consulte o artigo [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

