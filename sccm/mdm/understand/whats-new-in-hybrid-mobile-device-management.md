---
title: "Novidades do MDM com o Configuration Manager híbrido | Microsoft Docs"
description: "Saiba mais sobre os novos recursos de gerenciamento de dispositivo móvel disponíveis para implantações híbridas com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6f9e6e93fce95666503907010a5c253158c5de7c
ms.openlocfilehash: b9777e8cfa63eda77512e4837de17b99c792a036
ms.contentlocale: pt-pt
ms.lasthandoff: 07/07/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Novidades no gerenciamento de dispositivo móvel híbrido com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Este artigo fornece detalhes sobre o novo dispositivo móvel, recursos de gerenciamento (MDM) disponíveis para implantações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada seção deste artigo lista os recursos de híbrida em 3 categorias diferentes. Use as diretrizes a seguir para determinar a compatibilidade dos recursos em cada categoria com versões diferentes do Configuration Manager:  

|Categorias de recursos|Descrição|
|-|-|
|**Novo no Microsoft Intune** | Em geral, todos os recursos listados nesta categoria devem funcionar com todas as versões do Configuration Manager, incluindo versões do System Center 2012 R2 Configuration Manager, pois esses recursos exigem o serviço Intune somente e não exigem a funcionalidade adicional no Configuration Manager.|
|**Novo no Configuration Manager Technical Preview**| Todos os recursos listados nesta categoria só funcionam com a versão de visualização técnica especificada. Para testar esses recursos, você deve instalar a versão de visualização técnica especificada na descrição do recurso. Para obter mais informações, consulte [visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Novo no Configuration Manager (ramificação atual)**| Todos os recursos listados nesta categoria só funcionam com a versão especificada do Configuration Manager (ramificação atual), como a versão 1511 ou 1602. Se você estiver usando uma versão mais antiga do Configuration Manager para sua implantação híbrida, você deve atualizar para a versão do Configuration Manager (ramificação atual) especificada na descrição do recurso. Para obter mais informações, consulte [atualizar para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|

## <a name="june-2017"></a>Junho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Alterar sua autoridade MDM**

  A partir do Configuration Manager versão 1610 e Microsoft Intune version 1705, você pode alterar sua autoridade MDM sem precisar entrar em contato com o Microsoft Support e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter detalhes, consulte [alterar sua autoridade MDM]( /sccm/mdm/deploy-use/change-mdm-authority).

- **Integração de proxy de navegador e o aplicativo gerenciada**

  O navegador gerenciado do Intune agora pode integrar com o serviço de Proxy de aplicativo do Azure AD para permitir que os usuários a acessar sites internos, mesmo quando estão trabalhando remotamente. Os usuários do navegador simplesmente digite a URL do site conforme eles normalmente e o navegador gerenciado roteia a solicitação através do gateway de web do proxy de aplicativo. Para obter mais informações, consulte [gerenciar acesso à Internet usando políticas de navegador gerenciado](/intune/app-configuration-managed-browser).

- **Aplicativo de Portal da empresa para Android agora tem uma nova experiência do usuário final para as políticas de proteção do aplicativo**

  Com base nos comentários dos clientes, modificou o aplicativo de Portal da empresa para Android mostrar um **acesso da empresa conteúdo** botão. A intenção é impedir que os usuários finais desnecessariamente passar pelo processo de registro quando eles só precisam acessar os aplicativos que dão suporte a políticas de proteção do aplicativo, um recurso de gerenciamento de aplicativos móveis do Intune. Você pode ver essas alterações no [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui) página.

- **Nova ação de menu remover facilmente o Portal da empresa**

  Com base nos comentários do usuário, o aplicativo de Portal da empresa para Android adicionou uma nova ação de menu para iniciar a remoção do Portal da empresa do seu dispositivo. Esta ação remove o dispositivo do gerenciamento do Intune para que o aplicativo pode ser removido do dispositivo pelo usuário. Você pode ver essas alterações no [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui) página e no [documentação do usuário final do Android](/intune-user-help/unenroll-your-device-from-intune-android).

- **Melhorias a sincronização de aplicativo com os criadores de atualização do Windows 10**

  O aplicativo de Portal da empresa para Windows 10 agora iniciará automaticamente uma sincronização para solicitações de instalação do aplicativo para dispositivos com Windows 10 criadores de atualização (versão 1703). Isso reduz o problema de instalações de aplicativos, atrasando durante o estado de "Sincronização pendente". Além disso, os usuários poderão iniciar manualmente uma sincronização de dentro do aplicativo. Você pode ver essas alterações no [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui) página.

- **Nova experiência guiada para o Portal de empresa do Windows 10**

  O aplicativo de Portal da empresa para Windows 10 incluirá uma experiência guiada de instruções passo a passo do Intune para dispositivos que não foram identificados ou registrado. A nova experiência fornece instruções passo a passo que o guiam o usuário pelo processo de registro no Active Directory do Azure (necessária para recursos de acesso condicional) e o registro do MDM (necessário para os recursos de gerenciamento de dispositivo). A experiência guiada estarão acessível na home page do Portal da empresa. Os usuários podem continuar a usar o aplicativo se não concluir o registro e registro, mas terá funcionalidade limitada.

  Esta atualização só é visível em dispositivos que executam o Windows 10 aniversário Update (build 1607) ou superior. Você pode ver essas alterações no [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui) página.

- **Aprimoramentos para os blocos de aplicativo no aplicativo do Portal da empresa para iOS**

  Atualizamos o design dos blocos de aplicativo na home page para refletir a cor de identidade visual que você definiu para o Portal da empresa. Para obter mais informações, consulte [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).

- **Seletor de conta já está disponível para o aplicativo de Portal da empresa para iOS**

  Usuários de dispositivos iOS podem ver nosso novo seletor de conta ao entrar no Portal da empresa se usar seu trabalho ou escola conta para entrar em outros aplicativos da Microsoft. Para obter mais informações, consulte [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novo no Configuration Manager Technical Preview 1706

- **Novas configurações de política de gerenciamento de aplicativos móveis**    

  As seguintes configurações de política de gerenciamento (MAM) do aplicativo móvel agora estão disponíveis:

  - **Bloquear captura de tela (somente para dispositivos Android):** Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.
  - **Desabilite sincronização do contato:** Impede que o aplicativo salvando dados para o aplicativo nativo de contatos no dispositivo.
  - **Desabilite a impressão:** Impede que o aplicativo de dados de escola ou trabalho de impressão.

  Consulte [proteger aplicativos usando políticas de proteção de aplicativos no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para testar as novas configurações de política de proteção do aplicativo.

- **Novas definições de item de configuração do Windows**  <!-- 1354715 -->    

  Novos itens de configuração do Windows estão disponíveis para as categorias de configuração de senha, o dispositivo, o armazenamento e o Microsoft Edge. Para obter mais informações, consulte [definições de item de configuração do novo Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).

- **Novas regras de política de conformidade do dispositivo**    

  Agora você pode configurar as novas opções de políticas de conformidade que anteriormente estavam disponíveis somente no Intune autônomo. Para obter detalhes, consulte [aprimoramentos de política de conformidade do dispositivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrições de registro do Android e iOS**<!-- 1290826 -->      

  Os administradores agora podem especificar que os usuários não podem registrar dispositivos Android ou iOS pessoais em seu ambiente híbrido. Isso permite que você limite registrado dispositivos declaradas previamente, dispositivos da empresa ou dispositivos iOS registrados somente com o programa de registro do dispositivo. Para obter detalhes, consulte [restrições de registro do Android e iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).

- **Suporte para autoridades de certificação Entrust**<!-- 1350740 -->     

  Agora, o Configuration Manager dá suporte a autoridades de certificação Entrust; Isso permite o fornecimento de certificado PFX para dispositivos registrados no Microsoft Intune.    

  Você pode configurar Entrust como a autoridade de certificação quando adicionar a função do ponto de registro de certificado no Configuration Manager. Ao adicionar um novo perfil de certificado que emite os certificados PFX, você pode selecionar um Microsoft ou Entrust autoridade de certificação.

  **Problema conhecido**: Na visualização técnica 1706, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Isso não afeta os certificados PFX importados ou perfis SCEP.

- **Suporte para perfis VPN macOS Cisco (IPsec)**  <!-- 1321367 -->    

  Você pode criar um macOS perfil VPN com a Cisco (IPsec) como o tipo de conexão. Para obter mais informações, consulte [criar perfis de VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="april-2017"></a>Abril de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **MyApps disponível para o navegador gerenciado**

  Microsoft MyApps agora têm suporte melhor dentro do navegador gerenciado. Os usuários gerenciados do navegador que não são direcionados para o gerenciamento serão levados diretamente ao serviço MyApps, onde eles podem acessar seus aplicativos SaaS provisionado pelo administrador. Os usuários que são direcionados para o gerenciamento de continuará poder acessar MyApps do indicador interno do Managed Browser.

- **Novos ícones para o navegador gerenciado e o Portal da empresa**

  O navegador gerenciado está recebendo ícones atualizados para o Android e iOS versões do aplicativo. O ícone da nova conterá a notificação do Intune atualizada para torná-lo mais consistente com outros aplicativos no Enterprise Mobility + Security (EM + S). Você pode ver o ícone novo para o Managed Browser no [Novidades na página de interface do usuário do aplicativo Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

  O Portal da empresa também está recebendo ícones atualizados para as versões do Windows, iOS e Android do aplicativo para melhorar a consistência com outros aplicativos em + S. Esses ícones serão liberadas gradualmente em plataformas de abril de maio tardia.

- **Indicador de progresso de entrar no Portal da empresa do Android**

  Uma atualização para o aplicativo de Portal da empresa Android mostra um indicador de progresso entrar quando o usuário inicia ou retoma o aplicativo. Avança o indicador por meio do novo status, começando com "Conectar …", e "Assinatura in..." e "Verificação de requisitos de segurança..." antes de permitir que o usuário para acessar o aplicativo. Você pode ver as novas telas para o aplicativo de Portal da empresa para Android no [Novidades na página de interface do usuário do aplicativo Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

- **Bloquear aplicativos acessem o SharePoint Online**

  Agora você pode criar uma política de acesso condicional com base no aplicativo para bloquear aplicativos que não tem políticas de proteção do aplicativo aplicadas a elas, acesse [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online). No cenário de acesso condicional com base em aplicativos, você pode especificar os aplicativos que você deseja ter acesso ao SharePoint Online usando o portal do Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novo no Configuration Manager Technical Preview 1704

- **Configurar aplicativos Android com as políticas de configuração de aplicativo**

  Você pode usar políticas de configuração de aplicativo no System Center Configuration Manager (Gerenciador de configuração) para distribuir as configurações previamente definidas quando um usuário executa um aplicativo no Android para dispositivos de trabalho. Políticas de configuração de aplicativo do Android estão disponíveis somente em dispositivos que executam o Android para o trabalho e se aplicam a aplicativos aprovados de reprodução para armazenamento de trabalho. Para obter informações sobre como testar esse recurso, consulte [Android configurar aplicativos com políticas de configuração de aplicativo](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).

## <a name="march-2017"></a>Março de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Nova experiência do usuário para o aplicativo de Portal da empresa para Android**

  O aplicativo de Portal da empresa para Android tem uma aparência moderna mais à sua interface do usuário. As atualizações importantes são:

  - Cores: Cabeçalhos de guia de Portal da empresa são coloridos em definido IT identidade visual.
  - Aplicativos: No **aplicativos** guia, o **aplicativos em destaque** e **todos os aplicativos** botões são atualizados.
  - Pesquisa: No **aplicativos** guia, o **pesquisa** botão é um botão de ação flutuante.
  - Navegando aplicativos: **Todos os aplicativos** exibição mostra uma exibição com guias de **em destaque**, **todos os**, e **categorias** para facilitar a navegação.
  - Suporte a: **Meus dispositivos** e **contato de TI** guias são atualizadas para melhorar a legibilidade.

  Para obter mais detalhes sobre essas alterações, consulte [atualizações de interface do usuário para aplicativos de usuário final do Intune](/intune/whats-new/whats-new-in-intune-app-ui).

- **Assinatura de Script para o Portal de empresa do Windows 10**

  Se você precisa baixar e carregar o aplicativo de Portal da empresa do Windows 10, agora você pode usar um script para simplificar e simplificar o processo de autenticação de aplicativos para sua organização.  Para baixar o script e as instruções para usá-lo, consulte [assinatura Script para Windows 10 da empresa Portal do Microsoft Intune](https://aka.ms/win10cpscript) na Galeria do TechNet. Para obter mais detalhes sobre este lançamento, consulte [atualizar seu aplicativo de Portal da empresa do Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) no Blog da equipe de suporte do Intune.

- **Suporte aprimorado para os usuários do Android com base na China**

  Devido à ausência da loja Google Play na China, dispositivos Android devem obter aplicativos de mercados chinês. O Portal da empresa oferecerá suporte a esse fluxo de trabalho redirecionando os usuários Android na China para baixar os aplicativos de Portal da empresa e o Outlook de lojas de aplicativos local. Isso melhora a experiência do usuário quando as políticas de acesso condicional são habilitadas para gerenciamento de dispositivo móvel e gerenciamento de aplicativos móveis. Os aplicativos de Portal da empresa e o Outlook para Android estão disponíveis nos seguintes armazenamentos de aplicativo chinês:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Verifique se que seus aplicativos de Portal da empresa estão atualizados**

  Em dezembro de 2016, lançamos uma atualização que habilitado imposição para autenticação multifator (MFA) em um grupo de usuários quando eles registram um iOS, Android, Windows 8.1 + ou dispositivo Windows Phone 8.1 e posteriores. Esse recurso não funciona sem determinadas versões de linha de base do aplicativo Portal da empresa para Android (v5.0.3419.0 +) e iOS (v2.1.17 +).

  Recursos de gerenciamento do Intune continuamente estão aumentando e muitas melhorias tem coordenada atualizações para os aplicativos de Portal da empresa em todas as plataformas com suporte. Como resultado, é recomendável que você mantenha as versões mais recentes dos aplicativos do Portal da empresa em instalado nos dispositivos para tirar proveito das melhorias no Intune e para a melhor experiência de usuário.

  >[!Tip]
  > Que os usuários para definir seus dispositivos para atualizar automaticamente os aplicativos da loja de aplicativos apropriado. Se você tiver feito o aplicativo de Portal da empresa Android disponível em um compartilhamento de rede, você pode baixar a versão mais recente do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams está habilitado para MAM no iOS e Android**

  Os aplicativos Microsoft Teams para iOS e Android agora são habilitados com recursos de gerenciamento (MAM) de aplicativo móvel do Intune, para que você pode capacitar as equipes para trabalhar livremente entre dispositivos, garantindo que as conversas e dados corporativos estejam protegidos em cada vez. Para obter mais detalhes, consulte [o lançamento do Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) no blog de segurança e mobilidade corporativa.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novo no Configuration Manager Technical Preview 1703

- **Suporte adicional para cenários do Apple Volume Purchase Program**

   A partir de 1703 de visualização técnica, agora você tem suporte para os seguintes cenários de programa de compra de Volume (VPP):

   - Licenciamento do dispositivo - aplicativos que dão suporte ao licenciamento de dispositivo e são implantados em coleções de dispositivos exigirá apenas uma licença para cada dispositivo.  Anteriormente, era necessário usar uma licença para cada usuário em um dispositivo. Para obter mais informações, consulte [implantar aplicativos iOS adquiridos por volume em coleções de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Uso de vários tokens VPP para um locatário único híbrida com ambos os tokens usados para o gerenciamento de aplicativos.
   - Uso de tokens de educação de VPP com a capacidade de diferenciar os tokens de treinamento e de negócios.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)

Os seguintes recursos que estavam anteriormente disponíveis em versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e Configuration Manager (ramificação atual) versão 1702.

- [Android para suporte de trabalho](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Configurações de conformidade de aplicativos não compatíveis](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Criação de certificado PFX e distribuição e suporte a S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Android e iOS versões não são mais targetable nos assistentes para criação de MDM híbrido](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Os seguintes recursos híbridos adicionais também estão incluídos na versão 1702 do Configuration Manager (ramificação atual):

- **Suporte aprimorado para Apple VPP Volume Purchase Program)**

  - Agora você pode implantar aplicativos licenciados para dispositivos, bem como os usuários. Dependendo da capacidade de aplicativos para dar suporte ao licenciamento de dispositivo, uma licença apropriada será ser solicitada ao implantá-lo, da seguinte maneira:

    | Versão do Configuration Manager | Aplicativo dá suporte ao licenciamento de dispositivo? | Tipo de coleção de implantação | Licença declarada |
    |-|-|-|-|
    |Anteriores 1702|Sim|Utilizador|Licença de usuário|
    |Anteriores 1702|Não|Utilizador|Licença de usuário|
    |Anteriores 1702|Sim|Dispositivo|Licença de usuário|
    |Anteriores 1702|Não|Dispositivo|Licença de usuário|
    |1702 e posterior|Sim|Utilizador|Licença de usuário|
    |1702 e posterior|Não|Utilizador|Licença de usuário|
    |1702 e posterior|Sim|Dispositivo|Licença do dispositivo|
    |1702 e posterior|Não|Dispositivo|Licença de usuário|

  - Você pode também implantar e rastrear aplicativos adquiridos de iOS Volume Purchase Program para treinamento.

  - Agora você pode associar vários tokens do Apple volume purchase program com o Configuration Manager.

  Para obter mais informações sobre aplicativos iOS adquiridos por volume, consulte [gerenciar aplicativos iOS adquiridos por volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Suporte para a linha de aplicativos de negócios da Windows Store para empresas**

  Agora você pode sincronizar personalizado aplicativos de linha de negócios da Windows Store para empresas.

- **Novo Mobile defesa contra ameaças ferramentas de monitoramento**

    Agora você tem novas maneiras de monitorar o status de conformidade com seu provedor de serviços de proteção contra ameaças de celular.

    Para obter mais informações, consulte [como monitorar a conformidade de defesa contra ameaças de Mobile](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Fevereiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **O site de Portal da empresa para modernizar**

  O site de Portal da empresa oferece suporte a aplicativos que são destinados a usuários que não tem dispositivos gerenciados. O site de acordo com outros produtos da Microsoft e serviços usando um novo esquema de cores contrastantes, ilustrações dinâmicas e um "menu de hambúrguer", que contém detalhes de contato de suporte técnico e obter informações sobre os dispositivos gerenciados existentes. A página inicial é reorganizada para enfatizar a aplicativos que estão disponíveis para usuários com carrosséis para aplicativos em destaque e atualizado recentemente. Você pode encontrar imagens antes e depois disponíveis no [atualizações de interface do usuário](/intune/whats-new/whats-new-in-intune-app-ui) página.

- **Novo endereço do servidor MDM para dispositivos Windows**

  O endereço do servidor MDM para o registro de dispositivos do Windows e Windows Phone foi alterado de manage.microsoft.com para enrollment.manage.microsoft.com. Notificar o usuário use enrollment.manage.microsoft.com como o endereço do servidor MDM se solicitado durante o registro do Windows ou dispositivo Windows Phone e. Essa atualização também requer que qualquer CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para manage.microsoft.com deve ser substituído por um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com. Para obter informações adicionais sobre essa alteração, visite http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novo no Configuration Manager Technical Preview 1702

- **Android para suporte de trabalho**

  Agora você pode gerenciar dispositivos Android usando o Android para o trabalho em ambientes de MDM híbrido com o Configuration Manager Technical Preview 1702. Dispositivos Android com suporte agora podem ser registrados como Android, para dispositivos de trabalho, que cria um perfil de trabalho no dispositivo para o qual aplicativos aprovados na execução do trabalho podem ser implantados. Você também pode configurar e implantar itens de configuração, as políticas de conformidade e perfis de acesso de recursos para esses dispositivos. Para obter mais informações, consulte [Android para suporte de trabalho](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Configurações de conformidade de aplicativos não compatíveis**

  Agora você pode criar regras de aplicativos não compatíveis para aplicativos do Android e iOS nas políticas de conformidade. Se dispositivos têm especificados aplicativos instalados, eles serão marcados "incompatível" e perderá o acesso aos recursos da empresa de acordo com as políticas de acesso condicional no local. Para obter mais informações [aprimoramentos de política de conformidade de dispositivo de acesso condicional](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Criação de certificado PFX e distribuição e suporte a S/MIME**

  Agora você pode criar e implantar os certificados PFX para usuários em um ambiente híbrido. Esses certificados, em seguida, podem ser usados para descriptografia e criptografia de email de S/MIME por dispositivos que o usuário registrado. Para obter mais informações, consulte [suportam a certificados de PFX criar com S MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Suporte para definições de configuração do iOS adicionais**
   
    Agora você tem 42 configurações do iOS adicionais que você pode configurar como parte de um item de configuração. A maioria das configurações (35 em todos os) foram adicionada para dispositivos iOS supervisionados. Para obter mais informações, consulte [novas configurações de conformidade para dispositivos iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Janeiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Suporte do Android 7.1.1**

  Intune agora totalmente suporta e gerencia 7.1.1 Android.

- **Resolver o problema em dispositivos iOS estão inativos ou o console do administrador não pode se comunicar com eles**

  Quando os dispositivos dos usuários perdem o contato com o Intune, você pode fornecer novas etapas de solução de problemas para ajudá-lo a recuperar o acesso aos recursos da empresa. Consulte [dispositivos estão inativos ou o console do administrador não pode se comunicar com eles](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novo no Configuration Manager Technical Preview 1701

- **Android e iOS versões não são mais targetable nos assistentes para criação de MDM híbrido**

  Partir 1701 de visualização técnica de gerenciamento de dispositivo móvel híbrido (MDM), você não precisa versões específicas do Android e iOS de destino ao criar novas políticas e perfis para dispositivos gerenciados pelo Intune. Com essa alteração, implantações híbridas podem fornecer suporte mais rapidamente para novas versões do Android e iOS sem a necessidade de uma nova versão do Configuration Manager ou a extensão. Para obter mais informações, consulte [Android e iOS versões não são mais targetable nos assistentes para criação](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Avisos

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>Configuração do System Center 2012 SP1 e System Center 2012 R2 Configuration Manager (RTM): Suporte para gerenciamento de dispositivo móvel híbrido terminando em 10 de abril de 2017

*11 de janeiro de 2017*

Suporte para o System Center 2012 Configuration Manager SP1 e System Center 2012 R2 Configuration Manager RTM terminou em 12 de julho de 2016. Subsequentemente, o suporte para essas versões conectando ao serviço para MDM híbrido termina em 10 de abril de 2017 o Microsoft Intune. Após essa data, MDM híbrido deixarão de funcionar com essas versões. Dispositivos gerenciados essencialmente tornarão não gerenciados, como o conector do Intune não se conectará ao serviço Intune. Dados do Configuration Manager (como políticas e aplicativos) não liberará até o Intune e dados de dispositivo gerenciado não passará para o Configuration Manager até que uma atualização ocorra.

Se você estiver executando uma implantação híbrida com o Configuration Manager 2012 SP1 ou R2 RTM, recomendamos que antes de 10 de abril de 2017 atualizar para o Configuration Manager (ramificação atual) ou o último service pack com suporte do Configuration Manager 2012 (R2 SP1 ou SP2) para evitar a interrupção do serviço.

Recursos adicionais:
-   [Atualizar para System Center Configuration Manager (ramificação atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planejando a atualização para o System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planejando a atualização para o System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Carregamento de Portal da empresa do Windows Phone 8 preterido
*25 de outubro de 2016*

A capacidade de carregar um aplicativo de Portal da empresa assinado foi removida do console do Configuration Manager, como o suporte do Intune está sendo substituído para Windows 8, Windows Phone 8 e Windows RT e suporte para o Portal da empresa do Windows Phone 8 está terminando em novembro.  Windows 8, Windows Phone 8 e Windows RT dispositivos já registrados continuarão a ter suporte, mas o registro de dispositivos adicionais com essas plataformas não terão suporte.


### <a name="see-also"></a>Consulte Também

- [Além de recursos MDM híbrida](whats-new-hybrid-archive.md)
- [Quais são as novidades do MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

