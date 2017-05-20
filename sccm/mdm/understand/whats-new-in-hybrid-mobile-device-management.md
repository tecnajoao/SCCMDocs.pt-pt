---
title: "O que há de novo no híbrida MDM com o Configuration Manager | Documentos do Microsoft"
description: "Saiba mais sobre as novas funcionalidades de gestão do dispositivo móvel disponíveis para implementações híbridas com o Configuration Manager e do Intune."
ms.custom: na
ms.date: 04/21/2017
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
ms.sourcegitcommit: ae008c91a7387ba76f2bfac13f8feb489a0cc558
ms.openlocfilehash: 0af5ae68353fcf1db846e2e27f3391fe87dcfc42
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>O que há de novo na gestão de dispositivos móveis híbrida com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre o dispositivo móvel novas funcionalidades de gestão (MDM) disponíveis para implementações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada secção deste artigo apresenta uma lista de funcionalidades de híbrida em 3 categorias diferentes. Utilize as orientações seguintes para determinar a compatibilidade das funcionalidades em cada categoria com diferentes versões do Configuration Manager:  

|Categorias de funcionalidade|Descrição|
|-|-|
|**Novidades no Microsoft Intune** | Em geral, todas as funcionalidades listadas sob esta categoria deverá trabalhar com todas as versões do Configuration Manager incluindo versões do System Center 2012 R2 Configuration Manager, uma vez que estas funcionalidades requerem o serviço Intune apenas e não necessitam de funcionalidades adicionais no Configuration Manager.|
|**Novidades do Configuration Manager Technical Preview**| Todas as funcionalidades listadas sob esta categoria só funcionam com a versão de pré-visualização técnica especificada. Para experimentar estas funcionalidades, tem de instalar a versão de pré-visualização técnica especificada na descrição da funcionalidade. Para obter mais informações, consulte o artigo [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Novo no Configuration Manager (ramo atual)**| Todas as funcionalidades listadas sob esta categoria só funcionam com a versão especificada do Configuration Manager (ramo atual), tal como versão 1511 ou 1602. Se estiver a utilizar uma versão mais antiga do Configuration Manager para a sua implementação híbrida, tem de atualizar para a versão do Configuration Manager (ramo atual) especificada na descrição da funcionalidade. Para obter mais informações, consulte o artigo [atualizar para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|

## <a name="april-2017"></a>De 2017 Abril

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

- **MyApps disponíveis para o Browser gerido**

  Microsoft MyApps agora tem um melhor suporte de Browser gerido. Utilizadores de Browser geridos não direcionados para a gestão são encaminhados diretamente para o serviço de MyApps, onde pode aceder às suas aplicações de SaaS aprovisionado pelo administrador. Os utilizadores que são direcionados para a gestão Intune irão continuar a ser capazes de aceder MyApps do marcador de Browser gerido incorporado.

- **Ícones de novo para o Browser gerido e o Portal da empresa**

  O Browser gerido está a receber ícones atualizados para o Android e iOS versões da aplicação. No ícone novo irá conter o distintivo Intune atualizado para o tornar mais consistente com outras aplicações na Enterprise Mobility + segurança (EM + S). Pode ver no ícone novo para o Browser gerido do [quais são as novidades na página de IU do Intune aplicação](/intune/whats-new/whats-new-in-intune-app-ui.md).

  O Portal da empresa também está a receber ícones atualizadas para as versões do Android, iOS e Windows da aplicação para melhorar a consistência com outras aplicações em + S. Estes ícones são lançadas gradualmente através de plataformas do Abril para Maio atrasada.

- **Indicador de progresso de início de sessão no Portal da empresa Android**

  Uma atualização para a aplicação de Portal da empresa Android mostra um início de sessão do indicador quando o utilizador inicia ou retoma a aplicação. A continuará indicador através de Estados novos, começar com "Ligar...", em seguida, "Assinatura in. …", em seguida, "A verificar os requisitos de segurança..." antes de permitir que o utilizador para aceder à aplicação. Pode ver ecrãs de novo para a aplicação de Portal da empresa para Android o [quais são as novidades na página de IU do Intune aplicação](/intune/whats-new/whats-new-in-intune-app-ui.md).

- **Impedir que as aplicações acedam ao SharePoint Online**

  Agora pode criar uma política de acesso condicional com base na aplicação para bloquear aplicações, que não têm políticas de proteção de aplicações aplicadas às mesmas, de aceder ao [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online). No cenário acesso condicional baseado em aplicações, pode especificar as aplicações que pretende que tenham acesso ao SharePoint Online através do portal do Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novidades do Configuration Manager Technical Preview 1704

- **Configurar as aplicações Android com as políticas de configuração de aplicação**

  Pode utilizar as políticas de configuração da aplicação no System Center Configuration Manager (Configuration Manager) para distribuir as definições de pré-configuradas quando um utilizador executa uma aplicação no Android para dispositivos de trabalho. Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos que executam o Android para trabalhar e aplicam a aplicações aprovadas da Play para o arquivo de trabalho. Para obter informações sobre como experimentar esta funcionalidade, consulte o artigo [configurar Android aplicações com políticas de configuração de aplicação](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).

## <a name="march-2017"></a>De 2017 Março

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

- **Nova experiência de utilizador para a aplicação de Portal da empresa para Android**

  A aplicação de Portal da empresa para Android tem um aspeto e funcionamento mais recente de interface de utilizador. As atualizações dignas de nota são:

  - Cores: Cabeçalhos de separador de Portal da empresa são cor na definidos IT de imagem corporativa.
  - Aplicações: No **aplicações** separador, o **aplicações em destaque** e **todas as aplicações** botões são atualizados.
  - Pesquisa em: No **aplicações** separador, o **pesquisa** botão é um botão de ação de vírgula flutuante.
  - Navegar em aplicações: **Todas as aplicações** vista mostra uma vista com separadores de **em destaque**, **todos os**, e **categorias** para uma navegação mais fácil.
  - Suporte: **Os dispositivos** e **contactar TI** separadores são atualizados para melhorar a legibilidade.

  Para obter mais detalhes sobre estas alterações, consulte o artigo [atualizações de IU para aplicações de utilizador final do Intune](/intune/whats-new/whats-new-in-intune-app-ui).

- **Assinatura de Script para o Portal da empresa do Windows 10**

  Se precisar de transferir e sideload da aplicação do Portal da empresa do Windows 10, agora, pode utilizar um script para simplificar e simplificar o processo de assinatura de aplicações para a sua organização.  Para transferir o script e as instruções para utilizá-lo, consulte o artigo [Microsoft Intune assinatura Script do Windows 10 Portal da empresa](https://aka.ms/win10cpscript) na galeria do TechNet. Para obter mais detalhes sobre este anúncio, consulte o artigo [a atualizar a aplicação de Portal da empresa do Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) no blogue de equipa de suporte do Intune.

- **Suporte melhorado para os utilizadores do Android com base na China**

  Devido a ausência do Google Play Store na China, dispositivos Android tem de obter aplicações a partir de chinês marketplaces. O Portal da empresa irá suportar este fluxo de trabalho por redirecionar os utilizadores do Android na China transferir as aplicações do Portal da empresa e o Outlook a partir de lojas de aplicações locais. Isto irá melhorar a experiência do utilizador quando as políticas de acesso condicional são ativadas, para gestão de dispositivos móveis e gestão de aplicações móveis. As aplicações de Portal da empresa e o Outlook para Android estão disponíveis nas lojas de aplicações chinês seguintes:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Certifique-se as suas aplicações de Portal da empresa estão atualizadas**

  No de 2016 de Dezembro, lançada uma atualização que permitia a imposição de autenticação multifator (MFA) num grupo de utilizadores quando inscrevam uma iOS, Android, Windows 8.1 + ou dispositivo Windows Phone 8.1 +. Esta funcionalidade não é possível trabalhar sem determinadas versões do plano base da aplicação Portal da empresa para Android (v5.0.3419.0 +) e iOS (v2.1.17 +).

  Funcionalidades de gestão do Intune continuamente são melhorar e vários melhoramentos a tem coordenados atualizações para as aplicações de Portal da empresa em todas as plataformas suportadas. Consequentemente, recomendamos que mantenha as versões mais recentes das aplicações de Portal da empresa instalado nos dispositivos para tirar partido dos melhoramentos no Intune e para a melhor experiência de utilizador.

  >[!Tip]
  > Que os seus utilizadores a configurar os seus dispositivos para atualizar automaticamente as aplicações da loja de aplicações adequada. Se efetuar a aplicação de Portal da empresa Android disponível numa partilha de rede, pode transferir a versão mais recente a partir de [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140).

- **Teams da Microsoft está agora ativada para MAM no iOS e Android**

  As aplicações de Teams da Microsoft para iOS e Android agora estão ativadas com capacidades de gestão (MAM) de aplicação móvel do Intune, pelo que pode aumentar a produtividade das suas equipas para o seu trabalho livremente em vários dispositivos, enquanto se certificar de que as conversações e dados empresariais estão protegidos em cada vez. Para obter mais detalhes, consulte o artigo [anúncio Teams da Microsoft](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) no blogue do Enterprise Mobility e segurança.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novo no Configuration Manager Technical Preview 1703

- **Suporte adicional para cenários de programa de compra da Apple Volume**

   A partir 1703 de pré-visualização técnica, agora tem suporte para os seguintes cenários de programa de compra de Volume (VPP):

   - Licenciamento do dispositivo - aplicações que suportam licenciamento do dispositivo e forem implementadas em coleções de dispositivos apenas necessitarão de uma licença por dispositivo.  Anteriormente, tinha de utilizar uma licença para cada utilizador num dispositivo. Para obter mais informações, consulte o artigo [implementar aplicações iOS adquiridos de volume em coleções de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Utilização de vários tokens VPP para um inquilino híbrido único com ambos os tokens utilizados para gerir VPP aplicações.
   - Utilização de tokens de educação VPP com a capacidade de distinguir entre os tokens de negócio e para educação.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que se encontravam anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com Intune e Configuration Manager (ramo atual) 1702 de versão.

- [Android para o suporte de trabalho](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Definições de compatibilidade de aplicações não compatíveis](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [A criação de certificado do PFX e a distribuição e suporte S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Versões do Android e iOS já não são targetable nos assistentes de criação para uma implementação híbrida MDM](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

As seguintes funcionalidades adicionais híbrida também estão incluídas na versão 1702 do Configuration Manager (ramo atual):

- **Suporte melhorado para o programa de compra de Volume do Apple (VPP)**

  - Pode agora implementar aplicações licenciadas dispositivos, bem como os utilizadores. Dependendo da capacidade de aplicações para suportar o dispositivo de licenciamento, uma licença adequada irá ser reclamada quando implementá-la, da seguinte forma:

    | Versão do Configuration Manager | A aplicação suporta licenciamento do dispositivo? | Tipo de coleção de implementação | Licença alegada |
    |-|-|-|-|
    |Anteriores ao 1702|Sim|Utilizador|Licença de utilizador|
    |Anteriores ao 1702|Não|Utilizador|Licença de utilizador|
    |Anteriores ao 1702|Sim|Dispositivo|Licença de utilizador|
    |Anteriores ao 1702|Não|Dispositivo|Licença de utilizador|
    |1702 e posterior|Sim|Utilizador|Licença de utilizador|
    |1702 e posterior|Não|Utilizador|Licença de utilizador|
    |1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
    |1702 e posterior|Não|Dispositivo|Licença de utilizador|

  - Pode também implementar e monitorizar aplicações comprou a partir do iOS do programa de compra de Volume para a educação.

  - Agora pode associar vários tokens de programa de compra de volume Apple com o Configuration Manager.

  Para mais informações sobre as aplicações iOS adquiridos de volume, consulte o artigo [gerir aplicações iOS adquiridos volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Suporte para a linha de negócio na loja Windows para empresas**

  Agora pode sincronizar personalizada aplicações de linha de negócio a partir da loja Windows para empresas.

- **Novo Mobile ameaça defesa ferramentas de monitorização**

    Tem de ter agora novas formas de monitorizar o estado de compatibilidade com o seu fornecedor de serviços móveis ameaça defesa.

    Para obter mais informações, consulte o artigo [como monitorizar a compatibilidade de Mobile ameaça defesa](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>De 2017 Fevereiro

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

- **Modernizing o site do Portal da empresa**

  O site do Portal da empresa suporta as aplicações que são direcionadas para os utilizadores que não disponham de dispositivos geridos. Alinha o Web site com outros produtos e serviços Microsoft, utilizando um novo esquema de cores contraste, ilustrações dinâmicas e um "menu hamburger," o que contém os detalhes de contacto de suporte técnico e as informações nos dispositivos geridos existentes. A página de destino é modificada para realçar as aplicações que estão disponíveis para os utilizadores com carousels para aplicações em destaque e actualizado recentemente. Pode encontrar antes-e-depois de imagens disponíveis a [IU atualizações](/intune/whats-new/whats-new-in-intune-app-ui) página.

- **Novo endereço do servidor MDM para dispositivos Windows**

  O endereço do servidor MDM para inscrição de dispositivos Windows e Windows Phone tem alterado de manage.microsoft.com para enrollment.manage.microsoft.com. Notificar o utilizador para utilizar enrollment.manage.microsoft.com como o endereço do servidor MDM se lhe for solicitado para a mesma durante a inscrição do Windows ou e dispositivo Windows Phone. Esta atualização também necessita de qualquer CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para manage.microsoft.com ser substituídos por um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment s.manage.microsoft.com. Para obter informações adicionais sobre esta alteração, visite http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novidades do Configuration Manager Technical Preview 1702

- **Android para o suporte de trabalho**

  Já pode gerir dispositivos Android com o Android para trabalhar em ambientes de MDM híbridos através do 1702 de pré-visualização técnica do Configuration Manager. Dispositivos Android suportados agora podem ser inscritos como Android para dispositivos de trabalho, que cria um perfil de trabalho no dispositivo para os quais as aplicações aprovadas no Play para o trabalho podem ser implementadas. Também pode configurar e implementar itens de configuração, as políticas de conformidade e perfis de acesso a recursos para estes dispositivos. Para obter mais informações, consulte o artigo [Android para o suporte de trabalho](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Definições de compatibilidade de aplicações não compatíveis**

  Agora, pode criar regras de aplicações não conformes para aplicações Android e iOS nas políticas de conformidade. Se os dispositivos têm aplicações especificadas instaladas, estes serão marcadas como "não conformes" e irão perder acesso aos recursos da empresa, de acordo com as políticas de acesso condicional no local. Para obter mais informações [melhoramentos de política de conformidade de dispositivos de acesso condicional](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **A criação de certificado do PFX e a distribuição e suporte S/MIME**

  Agora pode criar e implementar os certificados PFX para os utilizadores num ambiente híbrido. Estes certificados, em seguida, podem ser utilizados para encriptação de correio eletrónico de S/MIME e a desencriptação pelos dispositivos que o utilizador tem inscritos. Para obter mais informações, consulte o artigo [certificados PFX criar com S MIME suportam](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Suporte para as definições de configuração iOS adicionais**
   
    Tem agora 42 definições do iOS adicionais que pode configurar como parte de um item de configuração. Foram adicionada a maioria das definições (35 em todos os) para dispositivos iOS supervisionado. Para obter mais informações, consulte o artigo [novas definições de compatibilidade para dispositivos iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>De 2017 Janeiro

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

- **Suporte Android 7.1.1**

  Intune agora totalmente suporta e gere Android 7.1.1.

- **Resolver o problema onde dispositivos iOS estão inativos ou a consola de administração não é possível comunicar com eles**

  Quando os dispositivos dos utilizadores perdem entre em contacto com o Intune, pode dar-lhes novos passos de resolução de problemas para ajudar a recuperar o acesso aos recursos da empresa. Consulte o artigo [dispositivos estão inativos ou a consola de administração não é possível comunicar com eles](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novo no Configuration Manager Technical Preview 1701

- **Versões do Android e iOS já não são targetable nos assistentes de criação para uma implementação híbrida MDM**

  A partir no 1701 de pré-visualização técnica híbrida gestão de dispositivos móveis (MDM), já não tem de versões específicas do Android e iOS de destino quando criar novas políticas e perfis de dispositivos geridos pelo Intune. Com esta alteração, implementações híbridas podem fornecer suporte mais rapidamente para novas versões do Android e iOS sem necessitar de uma nova versão do Configuration Manager ou a extensão. Para obter mais informações, consulte o artigo [versões do Android e iOS já não são targetable nos assistentes de criação](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="december-2016"></a>Dezembro de 2016

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

- **A autenticação Multifator (MFA) na inscrição é mover para o portal do Azure**

  Anteriormente, poderá aceder a consola do Intune ou a consola do Configuration Manager para configurar a MFA para inscrições através do Intune. Com esta funcionalidade atualizada, agora início de sessão para [portal do Microsoft Azure] (https://manage.windowsazure.com) a utilizar o Intune as credenciais e configurar definições de MFA através do Azure AD. Para obter mais informações, consulte o artigo [multi-factor authentication do Microsoft Intune] (https://aka.ms/mfa_ad).

- **Aplicação de Portal da empresa para Android, agora disponível na China**

  A aplicação de Portal da empresa para Android está agora disponível na China. Devido a ausência do Google Play Store na China, dispositivos Android tem de obter aplicações da marketplaces app chinês. A aplicação de Portal da empresa para Android está disponível para transferência na arquivos do seguinte:

  -    [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  -    [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  -    [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  -    [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  -    [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  A aplicação de Portal da empresa para Android utiliza reproduzir os serviços do Google para comunicar com o serviço Microsoft Intune. Uma vez que os serviços do Google reproduzir ainda não estão disponíveis na China, efetuar qualquer uma das seguintes tarefas pode demorar até 8 horas a concluir.

  | Consola de administração do Configuration Manager | Aplicação do Portal da empresa do Intune para Android | Site de Portal da empresa do Intune |
  |----|----|----|        
  | Extinguir/apagar (remover todos os dados)    | Remover um dispositivo remoto | Remover dispositivo (local e remoto) |
  | Extinguir/apagar (remove os dados da empresa)    | Repor o dispositivo | Repor o dispositivo|
  | Implementações das aplicações novas ou atualizadas | Instalar aplicações de linha de negócio disponíveis | Reposição do código de acesso de dispositivo|
  | Bloqueio remoto    | | |
  | Repor código de acesso | | |        


## <a name="november-2016"></a>Novembro de 2016

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

- **Portal da empresa do Intune Microsoft novos disponível para dispositivos Windows 10**

  Microsoft foi lançado um novo [aplicação Portal da empresa para dispositivos Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Esta aplicação, que utiliza o novo formato do Windows 10 Universal, fornece uma experiência de utilizador atualizado é idêntica em todos os dispositivos Windows 10, o PC e o Mobile igual, permitindo ainda todos da mesma funcionalidade fornecida pela anterior aplicações de Portal da empresa.

  A nova aplicação tira partido de funcionalidades de plataforma, como de sessão único (SSO) e a autenticação baseada em certificados em dispositivos Windows 10. A aplicação está disponível como uma atualização para o Portal de empresa de existente do Windows 8.1 e instala o Portal da empresa do Windows Phone 8.1 na loja Windows. Para obter mais detalhes, consulte o artigo o [blogue da equipa de suporte do Intune](http://aka.ms/intunecp_universalapp).

  A nova aplicação do Portal da empresa também apresenta qualquer loja Windows para as aplicações empresariais marcadas **disponível** na consola do Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que se encontravam anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com Intune e Configuration Manager (ramo atual) versão 1610.

* [Definições adicionais e experiência melhorada para itens de configuração](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Definições adicionais para perfis DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Paga aplicações na loja Windows para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipos de ligação nativo para perfis VPN do Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Gráficos de conformidade do Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [A sincronização de política de pedido a partir da consola](/sccm/mdm/deploy-use/sync-intune-device)
* [Definições de configuração do Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

As seguintes funcionalidades de híbrida adicionais também estão incluídas na versão 1610 do Configuration Manager (ramo atual):

- **Aumento do número de dispositivos inscritos**

  Agora pode permitir que os utilizadores inscrevam dispositivos até 15. O limite anterior era de 5 dispositivos por utilizador.


- **Suporte de segurança Addtional**

  Para além de administrador global, as seguintes funções de segurança incorporadas têm agora acesso total a itens no nó de todos os dispositivos de empresa, incluindo dispositivos Predeclared, perfis de inscrição do iOS e perfis de inscrição do Windows:

    - Gestor do Asset Intelligence
    - Gestor de acesso a recursos da empresa

  Acesso só de leitura a estas áreas da consola do Configuration Manager ainda é concedido à função do analista só de leitura.

- **Acesso VPN de acionamento automático a partir das aplicações de proteção de informações do Windows**

  Pode adicionar um domínio principal da proteção de informações do Windows para perfis VPN do Windows 10 que faz com que todas as aplicações associadas a acionar automaticamente uma ligação VPN quando são executados no dispositivo. Esta opção só está disponível quando escolher um tipo de ligação nativo.

- **Acesso condicional para perfis VPN do Windows 10**

    Agora pode exigir o Windows 10 dispositivos inscritos no Azure Active Directory para estar em conformidade para ter acesso VPN através de perfis VPN do Windows 10 criados na consola do Configuration Manager. Isto é possível através da nova **ativar o acesso condicional para esta ligação VPN** caixa de verificação na página do método de autenticação no Assistente do perfil VPN e propriedades de perfil da VPN para perfis VPN do Windows 10. Esta opção só está disponível quando escolher um tipo de ligação nativo.

    Também pode especificar um certificado separado para autenticação de início de sessão único se permitir o acesso condicional para o perfil.


## <a name="notices"></a>Avisos

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): Suporte para gestão de dispositivos móveis híbrida termina a 10 de Abril de 2017

*11 de Janeiro de 2017*

Suporte para o System Center 2012 Configuration Manager SP1 e System Center 2012 R2 Configuration Manager RTM terminou no 12 de Julho de 2016. Posteriormente, suporte para estas versões ligar ao serviço para uma implementação híbrida MDM termina a 10 de Abril de 2017 o Microsoft Intune. Após esta data, híbrida MDM deixarão de funcionar com estas versões. Essencialmente se tornarem não geridos dispositivos geridos como o conector do Intune já não irá ligar para o serviço Intune. Dados do Configuration Manager (por exemplo, políticas e aplicações) não irão fluir até do Intune e dados de dispositivo gerido não irão fluir por defeito para o Configuration Manager até que uma atualização é aplicada.

Se estiver a executar uma implementação híbrida com o Configuration Manager 2012 SP1 ou R2 RTM, recomendamos que 10 de Abril de 2017 antes de atualizar para o Configuration Manager (ramo atual) ou o suportados service pack mais recente do Configuration Manager 2012 (R2 SP1 ou SP2) para evitar uma interrupção do serviço.

Recursos adicionais:
-    [Atualizar o System Center Configuration Manager (ramo atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-    [Planeamento atualizar para o System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-    [Planeamento atualizar para o System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Carregamento do Portal da empresa do Windows Phone 8 preterido
*25 de Outubro de 2016*

A capacidade de carregar uma aplicação assinada do Portal da empresa foi removida a partir da consola do Configuration Manager, tal como está a ser preterido suporte do Intune para Windows 8, Windows Phone 8, e Windows RT e o suporte para o Portal da empresa do Windows Phone 8 está a terminar em Novembro.  Windows 8, Windows Phone 8 e Windows RT dispositivos já inscritos irão continuar a ser suportada, mas a inscrição de dispositivos adicionais com estes plataformas não será suportada.


### <a name="see-also"></a>Consulte Também

- [Decorridos desde funcionalidades MDM híbrida](whats-new-hybrid-archive.md)
- [Quais são as novidades para MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

