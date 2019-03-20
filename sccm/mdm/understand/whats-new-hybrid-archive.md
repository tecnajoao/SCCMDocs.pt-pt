---
title: Arquivo morto do que é a MDM híbrida de novo
titleSuffix: Configuration Manager
description: Arquivo das últimas funcionalidades de gestão de dispositivos móveis disponíveis para implementações híbridas com o System Center Configuration Manager e o Intune.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 73eda37c9432750d94ef0b770348fc3d3250800c
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/19/2019
ms.locfileid: "58197083"
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Nos últimos híbrida apresenta com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre o dispositivo móvel nos últimos recursos de gerenciamento (MDM) disponíveis para implementações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada secção deste artigo apresenta uma lista de funcionalidades híbridas em 3 diferentes categorias. Utilize as seguintes orientações para determinar a compatibilidade dos recursos em cada categoria com diferentes versões do Configuration Manager:  

|Categorias de funcionalidade|
|-|  
|**Novo no Microsoft Intune** - em geral, todos os recursos listados nesta categoria deve solicitar a trabalhar com todas as versões do Configuration Manager incluindo versões do System Center 2012 R2 Configuration Manager, uma vez que estas funcionalidades apenas o Intune serviço e não necessitam de funcionalidades adicionais no Configuration Manager.<br /><br /> **Novo no Configuration Manager Technical Preview** -todos os recursos listados nesta categoria funcionam apenas com a versão de pré-visualização técnica especificada. Para experimentar estas funcionalidades, tem de instalar a versão de pré-visualização técnica especificada na descrição do recurso. Para obter mais informações, consulte [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Novo no Configuration Manager (ramo atual)** -todos os recursos listados nesse trabalho único de categoria com a versão especificada do Configuration Manager (ramo atual), por exemplo, a versão 1511 ou 1602. Se estiver a utilizar uma versão mais antiga do Configuration Manager para a sua implementação híbrida, tem de atualizar para a versão do Configuration Manager (ramo atual) especificada na descrição do recurso. Para obter mais informações, consulte [atualizar para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  



## <a name="april-2017"></a>Abril de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **My Apps disponível para o Managed Browser**  
  O Microsoft My Apps agora tem melhor suporte no Managed Browser. Utilizadores de Browser geridos que não são visados para a gestão são colocados diretamente para o serviço MyApps, onde eles podem aceder a aplicações SaaS aprovisionadas pelo administrador. Os utilizadores que são visados para a gestão do Intune continuam a aceder My Apps a partir do indicador de Managed Browser incorporado.

- **Ícones de novo para o Managed Browser e o Portal da empresa**  
  O Managed Browser receberá ícones atualizados nas versões para Android e iOS da aplicação. O novo ícone contém o destaque do Intune atualizado para que seja mais consistente com outros aplicativos no Enterprise Mobility + Security (EM + S). Pode ver o novo ícone do Managed Browser na [página Novidades na IU da aplicação Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  O Portal da Empresa também receberá ícones atualizados para as versões para Android, iOS e Windows da aplicação para melhorar a consistência com as outras aplicações no EM+S. Estes ícones são lançados gradualmente nas plataformas a partir de Abril até finais de Maio.

- **Indicador de progresso de início de sessão no Portal da empresa para Android**  
  Uma atualização à aplicação Portal da Empresa para Android mostra um indicador de progresso de início de sessão quando o utilizador inicia ou retoma a aplicação. O indicador mostra novos estados de progresso, a começar com “A ligar...”, “A iniciar sessão...” e “A verificar os requisitos de segurança...” antes de o utilizador poder aceder à aplicação. Pode ver os novos ecrãs da aplicação Portal da Empresa para Android na [página Novidades na IU da aplicação Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Impedir que as aplicações acedam ao SharePoint Online**  
  Agora, pode criar uma política de acesso condicional com base na aplicação para impedir que as aplicações que não têm políticas de proteção aplicadas acedam ao [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). No cenário de acesso condicional baseado em aplicações, pode especificar as aplicações que pretende que tenham acesso ao SharePoint Online através do portal do Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novo no Configuration Manager Technical Preview 1704

- **Configurar aplicações Android com políticas de configuração de aplicação**  
  Quando um utilizador executa uma aplicação no Android para dispositivos de trabalho, utilize as políticas de configuração de aplicações no Configuration Manager para distribuir pré-configurações. Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos Android for Work. Aplicam estas políticas para aplicações aprovadas a partir da Play for Work store. Para obter mais informações, consulte [aplicações de configurar o Android com políticas de configuração de aplicação](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).



## <a name="march-2017"></a>Março de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Nova experiência de utilizador para a aplicação Portal da empresa para Android**  
  A aplicação Portal da empresa para Android tem uma aspeto e funcionalidade mais modernos de sua interface do usuário. As atualizações relevantes são:

  - Cores: Cabeçalhos de separador do Portal da empresa são coloridos na imagem corporativa definida de IT.
  - Aplicações: Na **aplicações** separador, o **aplicações em destaque** e **todas as aplicações** botões são atualizados.
  - Pesquisa: Na **aplicações** separador, o **pesquisa** botão é um botão de ação flutuante.
  - Navegar em aplicações: **Todas as aplicações** vista mostra uma vista com os separadores **em destaque**, **todos**, e **categorias** para uma navegação mais fácil.
  - Suporte: **Os meus dispositivos** e **contactar TI** separadores são atualizados para melhorar a legibilidade.

  Para obter mais informações sobre estas alterações, consulte [atualização da IU para aplicações de utilizadores finais do Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Script de assinatura para o Portal da empresa do Windows 10**  
  Se precisar de transferir e de carregar em sideload a aplicação Portal da Empresa do Windows 10, poderá agora utilizar um script para simplificar e otimizar o processo de assinatura de aplicações para a sua organização. Para transferir o script e as instruções para o utilizar, veja [Microsoft Intune Signing Script for Windows 10 Company Portal (Script de Assinatura do Microsoft Intune para o Portal da Empresa do Windows 10)](https://aka.ms/win10cpscript) na Galeria do TechNet. Para obter mais informações sobre este anúncio, veja [a atualizar a sua aplicação do Portal da empresa do Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) no blogue de equipa de suporte do Intune.

- **Suporte aprimorado para os utilizadores do Android sediados na China**  
  Devido à ausência da Google Play Store na China, os dispositivos Android têm de obter aplicações a partir de mercados chineses. O Portal da empresa oferece suporte a esse fluxo de trabalho. Ele redireciona os utilizadores do Android na China para transferir as aplicações Portal da empresa e Outlook a partir de lojas de aplicações locais. Este comportamento melhora a experiência do usuário quando as políticas de acesso condicional estão ativadas, para gestão de dispositivos móveis e gestão de aplicações móveis. As aplicações Portal da Empresa e Outlook para Android estão disponíveis nas seguintes lojas de aplicações chinesas:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Certifique-se de que as suas aplicações do Portal da empresa estão atualizadas**  
  Em dezembro de 2016, lançamos uma atualização que permitia a imposição da autenticação multifator (MFA) num grupo de utilizadores no momento da inscrição de um dispositivo iOS, Android, Windows 8.1 e superior ou Windows Phone 8.1 e superior. Esta funcionalidade não pode funcionar sem determinadas versões de linha de base da aplicação Portal da empresa para Android (V5.0.3419.0+) e iOS (v2.1.17+).

  Continuamente a melhorar as capacidades de gestão do Intune. Muitos aprimoramentos tem coordenada atualizações para as aplicações Portal da empresa em todas as plataformas suportadas. Recomendamos que mantenha as versões mais recentes das aplicações Portal da empresa em instaladas em dispositivos. Esta prática tira partido das melhorias no Intune e para a melhor experiência de utilizador.

  >[!Tip]
  > Solicite aos seus utilizadores que configurem os dispositivos para atualizarem automaticamente as aplicações da loja de aplicações adequada. Se tiver disponibilizado a aplicação Portal da Empresa do Android numa partilha de rede, poderá transferir a versão mais recente a partir do [Centro de Transferências da Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams está agora ativada para MAM em iOS e Android**  
  As aplicações do Microsoft Teams para iOS e Android estão agora ativadas com capacidades de gestão (MAM) de aplicações móveis do Intune. Capacite as suas equipas trabalhem livremente em vários dispositivos, garantindo que as conversações e os dados empresariais estão protegidos. Para obter mais informações, consulte [o anúncio do Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) no blogue do Enterprise Mobility + Security.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novo no Configuration Manager Technical Preview 1703

- **Suporte adicional para cenários de Apple Volume Purchase Program**  
   A partir 1703 de pré-visualização técnica, agora tem suporte para os seguintes cenários de Volume Purchase Program (VPP):

   - Licenciamento de dispositivos - as aplicações que suportam o licenciamento de dispositivos e são implementadas em coleções de dispositivos agora exigir apenas uma licença por dispositivo. Anteriormente, tinha de utilizar uma licença para cada utilizador num dispositivo. Para obter mais informações, consulte [implementar aplicações iOS compradas em volume para coleções de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Utilização de múltiplos tokens VPP para um inquilino híbrido único com ambos os tokens utilizados para gerir aplicações VPP.
   - Utilização de tokens VPP do ensino com a capacidade de distinguir entre os tokens de negócios e treinamento.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades foram anteriormente disponíveis em versões do Configuration Manager Technical Preview. Estas funcionalidades estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1702.

- [Android for Work suporte](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Definições de compatibilidade de aplicações não conformes](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Criação do certificado PFX e a distribuição e suporte de S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Versões do Android e iOS já não são targetable nos assistentes de criação para MDM híbrida](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

As seguintes funcionalidades de híbrida adicionais também estão incluídas na versão 1702 do Configuration Manager (ramo atual):

- **Suporte aprimorado para o Apple Volume Purchase Program (VPP)**  
  - Pode agora implementar aplicações licenciadas para dispositivos, bem como os utilizadores. Consoante a capacidade de aplicações para suportar de licenciamento de dispositivos, uma licença adequada seja solicitada quando implantá-lo, da seguinte forma:

    | Versão do Configuration Manager | Aplicação suporta o licenciamento de dispositivos? | Tipo de coleção de implementação | Licença solicitada |
    |-|-|-|-|
    |Anterior ao 1702|Sim|Utilizador|Licença de utilizador|
    |Anterior ao 1702|Não|Utilizador|Licença de utilizador|
    |Anterior ao 1702|Sim|Dispositivo|Licença de utilizador|
    |Anterior ao 1702|Não|Dispositivo|Licença de utilizador|
    |1702 e posterior|Sim|Utilizador|Licença de utilizador|
    |1702 e posterior|Não|Utilizador|Licença de utilizador|
    |1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
    |1702 e posterior|Não|Dispositivo|Licença de utilizador|

  - Agora também pode implementar e controlar aplicações compradas a partir do iOS Volume Purchase Program for Education.

  - Agora pode associar vários tokens do programa de compra em volume da Apple com o Configuration Manager.

  Para obter mais informações sobre aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Suporte para aplicações de linha de negócios na Microsoft Store para empresas**  
  Agora pode sincronizar aplicações de linha de negócio personalizadas da Microsoft Store para empresas.

- **Novo Mobile Threat Defense ferramentas de monitorização**  
    Tem agora novas formas de monitorizar o estado de conformidade com o seu fornecedor de serviços de defesa contra ameaças móveis.

    Para obter mais informações, consulte [como monitorizar a conformidade de Mobile Threat Defense](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).





## <a name="february-2017"></a>Fevereiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Modernizar o site do Portal da empresa**

  O site do Portal da empresa suporta aplicações visadas para utilizadores que não têm dispositivos geridos. O Web site está alinhado com outros produtos e serviços Microsoft através da utilização de um novo esquema de cores contrastante, ilustrações dinâmicas e um "menu de opções," que contém os detalhes de contacto de suporte técnico e obter informações sobre dispositivos geridos existentes. A página de destino é reorganizada de forma a realçar as aplicações que estão disponíveis para utilizadores, com carrosséis para aplicações em destaque e recentemente atualizadas. Pode encontrar antes e depois imagens disponíveis no [atualizações da interface do Usuário](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Novo endereço do servidor MDM para dispositivos Windows**

  O endereço do servidor MDM para a inscrição de dispositivos Windows e Windows Phone foi alterado de manage.microsoft.com para enrollment.manage.microsoft.com. Notificar o utilizador para utilizar enrollment.manage.microsoft.com como o endereço do servidor MDM, se solicitado durante a inscrição de um Windows ou e o dispositivo Windows Phone. Esta atualização também requer que qualquer CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para manage.microsoft.com ser substituído por um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para enterpriseenrollment-s.Manage.microsoft.com. Para obter mais informações sobre esta alteração, visite http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novo no Configuration Manager Technical Preview 1702

- **Android for Work suporte**

  Agora pode gerir dispositivos Android com o Android for Work em ambientes de MDM híbrida com 1702 de pré-visualização técnica do Configuration Manager. Agora podem ser inscritos dispositivos Android suportados como Android para dispositivos de trabalho, que cria um perfil de trabalho no dispositivo a que aplicações aprovadas na Play for Work podem ser implementadas. Também pode configurar e implementar itens de configuração, as políticas de conformidade e perfis de acesso a recursos para estes dispositivos. Para obter mais informações, consulte [Android para o suporte de trabalho](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Definições de compatibilidade de aplicações não conformes**

  Agora, pode criar regras de aplicações não conformes para aplicações Android e iOS nas políticas de conformidade. Se os dispositivos têm aplicações especificadas instaladas, eles são marcadas como "não conforme" e perdem o acesso aos recursos da empresa, de acordo com as políticas de acesso condicional no local. Para obter mais informações, consulte [melhorias de política de conformidade de dispositivo de acesso condicional](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Criação do certificado PFX e a distribuição e suporte de S/MIME**

  Agora pode criar e implementar certificados PFX para utilizadores num ambiente híbrido. Estes certificados, em seguida, podem ser utilizados para encriptação de correio eletrónico de S/MIME e desencriptação pelos dispositivos que o utilizador tiver inscrito. Para obter mais informações, consulte [suportam certificados PFX criar com S MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Suporte para as definições de configuração do iOS adicionais**
   
    Tem agora 42 definições do iOS adicionais que pode configurar como parte de um item de configuração. A maioria das definições (35 em todos) foram adicionada para dispositivos iOS supervisionados. Para obter mais informações, consulte [novas definições de conformidade para dispositivos iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).



## <a name="january-2017"></a>Janeiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Suporte para Android 7.1.1**

  Agora, o Intune suporta e gere totalmente o Android 7.1.1.

- **Resolver o problema em que dispositivos iOS estão inativos ou a consola de administração não consegue comunicar com os mesmos**

  Quando os dispositivos dos utilizadores perdem o contacto com o Intune, pode dar-lhes novos passos de resolução de problemas que os ajudem a recuperar o acesso aos recursos da empresa. Veja [Os dispositivos estão inativos ou a consola de administração não consegue comunicar com os mesmos](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novo no Configuration Manager Technical Preview versão 1701

- **Versões do Android e iOS já não são targetable nos assistentes de criação para MDM híbrida**

  A partir na versão 1701 de pré-visualização técnica para gestão de dispositivos móveis híbridos (MDM), já não precisar de atingir versões específicas do Android e iOS durante a criação de novas políticas e perfis de dispositivos geridos pelo Intune. Com esta alteração, implementações híbridas podem fornecer suporte mais rapidamente para novas versões do Android e iOS sem a necessidade de uma nova versão do Configuration Manager ou a extensão. Para obter mais informações, consulte [versões do Android e iOS já não são targetable nos assistentes de criação](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).



## <a name="december-2016"></a>Dezembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Multi-factor authentication (MFA) na inscrição está a mudar para o portal do Azure**

  Anteriormente, utilizariam a consola do Intune ou a consola do Configuration Manager para configurar a MFA para inscrições no Intune. Com esta funcionalidade atualizada, que agora iniciar sessão para o [portal do Microsoft Azure](https://manage.windowsazure.com) com as suas credenciais do Intune e configurar as definições da MFA através do Azure AD. Para obter mais informações, consulte [multi-factor authentication do Microsoft Intune](https://aka.ms/mfa_ad).

- **Aplicação Portal da empresa para Android, agora disponível na China**

  A aplicação Portal da empresa para Android está agora disponível na China. Devido à ausência da Google Play Store na China, os dispositivos Android têm de obter aplicações a partir de mercados de aplicações chineses. A aplicação Portal da empresa para Android está disponível para download nos seguintes lojas:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  A aplicação Portal da Empresa para Android utiliza os Serviços do Google Play para comunicar com o serviço Microsoft Intune. Uma vez que os Serviços do Google Play ainda não estão disponíveis na China, pode demorar até 8 horas a concluir a realização de qualquer uma das seguintes tarefas.

  | Consola de administração do Configuration Manager | Aplicação Portal da Empresa do Intune para Android | Site do Portal da Empresa do Intune |
  |----|----|----|
  | Extinguir/limpar (remover todos os dados)| Remover um dispositivo remoto | Remover dispositivo (local e remoto) |
  | Extinguir/limpar (remoção de dados da empresa)| Repor dispositivo | Repor dispositivo|
  | Implementações de aplicações novas ou atualizadas | Instalar aplicações de linha de negócio disponíveis | Repor código de acesso do dispositivo|
  | Bloqueio remoto| | |
  | Repor código de acesso | | |


## <a name="november-2016"></a>Novembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Portal de novo da empresa do Microsoft Intune disponível para dispositivos Windows 10**

  A Microsoft lançou uma nova [aplicação do Portal da empresa para dispositivos Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Esta aplicação, que tira partido do novo formato Windows 10 Universal, fornece uma experiência atualizada que é idêntica em todos os dispositivos Windows 10, o PC e dispositivos móveis semelhantes, enquanto ainda permite que todos os mesmos funcionalidade fornecida pelo anteriores aplicações do Portal da empresa.

  A nova aplicação tira partido de funcionalidades de plataforma, como o início de sessão único (SSO) e a autenticação baseada em certificados em dispositivos Windows 10. A aplicação está disponível como uma atualização para o Portal da empresa Windows 8.1 existente e instala o Portal da empresa do Windows Phone 8.1 a partir da Windows Store. Para obter mais detalhes, vá para o [blogue da equipa do Intune suporte](http://aka.ms/intunecp_universalapp).

  A nova aplicação do Portal da empresa também apresenta quaisquer Store do Windows para aplicativos de negócios marcados **disponível** na consola do Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que eram anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1610.

* [Definições adicionais e experiência aprimorada para itens de configuração](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Definições adicionais para perfis DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Pago aplicativos na Windows Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipos de ligação nativos para perfis de VPN do Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Gráficos de conformidade do Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Pedir a sincronização de política da consola](/sccm/mdm/deploy-use/sync-intune-device)
* [Definições de configuração do Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

As seguintes funcionalidades de híbrida adicionais também estão incluídas na versão 1610 do Configuration Manager (ramo atual):

- **Aumento do número de dispositivos inscritos**

  Agora pode permitir aos utilizadores inscrever até 15 dispositivos. O limite anterior era 5 dispositivos por utilizador.


- **Suporte de segurança adicionais**

  Além de administrador completo, as seguintes funções de segurança incorporadas têm agora acesso total aos itens no nó de todos os dispositivos da empresa, incluindo dispositivos pré-declarados, perfis de inscrição de iOS e perfis de inscrição do Windows:

    - Gestor do Asset Intelligence
    - Gestor de acesso de recursos da empresa

  Acesso só de leitura para essas áreas da consola do Configuration Manager ainda é concedido a função de analista só de leitura.

- **Acesso VPN de acionamento automático de aplicações do Windows Information Protection**

  Pode adicionar um domínio primário de Windows Information Protection para perfis de VPN do Windows 10 que faz com que todas as aplicações associadas acionar automaticamente uma ligação VPN quando são executados no dispositivo. Esta opção só está disponível ao escolher um tipo de ligação nativos.

- **Acesso condicional para perfis de VPN do Windows 10**

    Agora pode exigir a Windows 10 inscritos no Azure Active Directory para estar em conformidade, para ter acesso VPN através de perfis de VPN do Windows 10 criadas na consola do Configuration Manager. Isso é possível por meio do novo **ativar o acesso condicional para esta ligação VPN** caixa de verificação na página do método de autenticação no Assistente de perfil VPN e propriedades de perfil VPN para perfis de VPN do Windows 10. Esta opção só está disponível ao escolher um tipo de ligação nativos.

    Também pode especificar um certificado diferente para autenticação de início de sessão único se ativar o acesso condicional para o perfil.

## <a name="october-2016"></a>Outubro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas em Outubro de 2016 funcionam em implementações híbridas.

- **Acesso condicional para gestão de aplicações móveis**

  Pode restringir o acesso ao Exchange Online, para que o acesso é fornecido apenas a partir de aplicações que suportam políticas de gestão de aplicações móveis do Intune, como o Outlook. [Esta nova funcionalidade](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) totalmente compatível com políticas de gestão (MAM) de aplicações móveis do Intune que pode bloquear o acesso para clientes de e-mail incorporados ou a outras aplicações que não tenham sido configuradas com as políticas de MAM do Intune. Isto garante que os utilizadores acedem aos dados da sua organização com as aplicações que podem ser protegidos com a MAM do Intune. Pode começar a utilizar na gestão de aplicações móveis do Intune através do portal do Azure. Procure a nova secção acesso condicional no painel "Definições".

- **Ferramenta de encapsulamento de aplicações do Intune para Android**

  Pode ativar as suas aplicações utilizar políticas de gestão (MAM) de aplicações móveis do Intune com a ferramenta de encapsulamento de aplicações do Intune.

- **Compatibilidade do Android Samsung KNOX Standard com o Intune**

  Determinados modelos do telemóvel Samsung Galaxy ACE não podem ser geridos pelo Intune como dispositivos Samsung KNOX Standard. Ao inscrever estes dispositivos com o Intune, eles serão geridos como dispositivos Android padrão.

  Os números dos modelos afetados são:

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  E seus usuários finais não tem de tomar nenhuma ação adicional. Para obter mais informações, visite o site do Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Novo no Configuration Manager Technical Preview versão 1610

Foram introduzidas as seguintes novas funcionalidades de híbrida em Outubro de 2016 para 1610 de pré-visualização técnica do Configuration Manager.

- **Pedir uma sincronização de política a partir da consola de administração**

  Pode pedir uma sincronização de política num dispositivo móvel inscrito na consola do Configuration Manager, em vez de terem de pedir a sincronização na aplicação Portal da empresa no próprio dispositivo. Esta é uma nova ação chamada **enviar pedido de sincronização** no menu ações do dispositivo remoto, que aparece na faixa de opções quando um dispositivo móvel é selecionado no nó dispositivos.

- **Definições de configuração do Windows Defender**

  Agora, pode configurar definições de cliente do Windows Defender em computadores Windows 10 inscritos no Intune com itens de configuração na consola do Configuration Manager. Existe um novo grupo de definição denominado **o Windows Defender** no Assistente de Item de configuração. Tenha em atenção que isto é suportado apenas no Windows 10 versão 1511 e superior.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

Não existem novas funcionalidades híbridas foram introduzidas em Agosto de 2016 para o Configuration Manager (ramo atual).

## <a name="september-2016"></a>Setembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas em Setembro de 2016 funcionam em implementações híbridas.

- **Inclusão de "Notificações" no portal da empresa para Android**

  Foi adicionado um novo ícone de notificações no portal da empresa para Android na home page. Tocar neste ícone permite acede à página de notificações, que mostra os utilizadores finais todos os itens que necessitam de atenção na aplicação Portal da empresa, como não conformidade do dispositivo, atualizações de inscrições e ativação da inscrição. A aplicação Portal da empresa iOS já tem esta experiência de notificações. Ter a nova página de notificações permite que o utilizador não verá a página de configuração de acesso da empresa sempre que iniciar ou retomar o Portal da empresa, desde que o dispositivo já está inscrito. Se criar suas próprias orientações do utilizador final, pode querer atualizar a sua documentação para refletir esta alteração. Encontrar capturas de ecrã atualizadas [aqui](https://aka.ms/androidcpupdate).

- **Alterações ao suporte para a aplicação Portal da empresa do iOS**

  Todos os utilizadores da aplicação Portal da empresa do Microsoft Intune para iOS agora são necessários para utilizar a versão mais recente. Novos utilizadores podem transferir apenas a versão mais recente, e que os utilizadores atuais são necessárias para atualizar a ele. A versão mais recente requer o iOS 8.0 ou posterior, para que os dispositivos que executam versões mais antigas do iOS não é possível utilizar o Portal da empresa nem inscrever enquanto os atualizarem para o iOS 8.0 ou posterior e atualizarem a aplicação Portal da empresa para a versão mais recente. Dispositivos inscritos que executem versões anteriores ao iOS 8.0 continuarão a ser geridos e listados na consola de administração do Intune.

- **Botão de feedback adicionado à aplicação Portal da empresa do Windows Phone 8.1**

  A aplicação de Portal da empresa do Windows Phone 8.1 permite que os utilizadores finais enviar comentários sobre a aplicação com um novo botão "Enviar feedback". Para localizar o botão, os utilizadores toque no menu de "três pontos" na parte inferior direita do ecrã da aplicação Portal da empresa em, em seguida, toque em **enviar comentários**. Os comentários recolhidos, anónimos ajudará a Microsoft a melhorar a experiência da aplicação Portal da empresa para os utilizadores.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Novo no Configuration Manager Technical Preview versão 1609

Foram introduzidas as seguintes novas funcionalidades de híbrida em Setembro de 2016 para versão de 1609 das pré-visualização técnica do Configuration Manager.

- **Definições adicionais e experiência aprimorada para definições de Item de configuração**

  Foram adicionadas novas definições para Android, iOS e Windows, e apenas as definições que se aplicam às plataformas que selecionar na página de plataformas suportadas são apresentadas no assistente. Para obter mais informações, consulte [novas definições de conformidade para itens de configuração na versão 1609 de TP](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Definições adicionais para perfis DEP**

  TouchID, ApplePay e Zoom foram adicionados como definições configuráveis nos perfis DEP para dispositivos iOS.

- **Pago aplicativos na Windows Store para empresas**

  Agora pode adicionar aplicativos pagos e gratuitos para a Windows Store para empresas e implementá-las aos utilizadores na sua organização. Para obter mais informações, consulte [aprimoramentos na Windows Store para empresas na versão 1609 de TP](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Tipos de ligação nativos para perfis de VPN do Windows 10**

  Agora pode criar perfis de VPN do Windows 10 para MDM com tipos de ligação Microsoft Automatic, IKEv2 e PPTP na consola do Configuration Manager sem utilizar OMA-URI.

- **Gráficos de conformidade do Intune**

  Pode obter uma vista rápida do dispositivo global a motivos de conformidade e de cima para não-conformidade através de novos gráficos na área de trabalho monitorização. Para obter mais informações, consulte [gráficos de conformidade do Intune na versão 1609 de TP](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

A seguinte nova funcionalidade introduzida em Setembro de 2016 está disponível para implementações híbridas com o Microsoft Intune e Configuration Manager versão 1606 (ramo atual).

- **suporte do iOS 10**

  Se tiver perfis ou itens de configuração direcionadas para todas as plataformas iOS, estes também são enviados para o iOS 10. Também lançámos uma atualização do Configuration Manager versão 1606, que permite aos perfis de destino e itens de configuração para as plataformas iOS individuais, incluindo iOS 10. Pode instalar a atualização com a consola de administração do Configuration Manager no **administração > Descrição geral > Serviços Cloud > atualizações e manutenção**. Pode encontrar mais informações sobre a atualização na [ http://support.microsoft.com/kb/3192616 ](http://support.microsoft.com/kb/3192616).

## <a name="august-2016"></a>Agosto de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas em Agosto de 2016 funcionam em implementações híbridas.

- **Android, suportam 7 na aplicação Portal da empresa**

  A aplicação Portal da empresa do Intune para Android fornece suporte de "dia 0" para o futuro sistema de operativo Android 7.0 para dispositivos móveis.

- **Funcionalidade em dispositivos Android 7.0 de reposição de remoção de Google do código de acesso remoto**

  Google irá remover a capacidade dos administradores de TI e utilizadores finais poderem repor remotamente o código de acesso de dispositivos Android 7.0. Anteriormente, os administradores de TI podiam repor remotamente o código de acesso de um utilizador e os utilizadores finais podiam repor os seus códigos de acesso a partir do site do Portal da empresa.

- **Política de aplicações permitidas e bloqueadas para dispositivos Samsung KNOX Standard**

  Agora pode configurar uma política personalizada para dispositivos Samsung KNOX Standard que lhe permite criar um dos seguintes:

  - Uma lista de aplicações que estão impedidas de executar no dispositivo. Mesmo que se instalada, uma aplicação definida na lista de bloqueadas não pode ser ativada no dispositivo.
  - Uma lista de aplicações que os utilizadores do dispositivo estão autorizados a instalar a partir da Google Play store. Nenhuma outra aplicação pode ser instalada a partir da loja.

  Estas definições só podem ser utilizadas pelos dispositivos que executem o Samsung KNOX Standard. Para obter detalhes, consulte [utilizar políticas personalizadas para permitir e bloquear aplicações para dispositivos Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Ligação de comentários do Portal da empresa para a Microsoft**

   O site do Portal da empresa permite que os utilizadores finais toquem numa nova ligação de "Comentários", na parte inferior da página, para enviar comentários à Microsoft sobre as suas experiências com o site. Os comentários recolhidos, anónimos ajudará a Microsoft a melhorar a experiência de Web site do Portal da empresa para utilizadores.

- **Versão mínima do iOS Managed Browser atualizada para 8.0**

  A aplicação de Browser gerido do Microsoft Intune para iOS foi atualizada para suportar dispositivos com iOS 8.0 ou posterior. Enquanto os dispositivos iOS 7.1 podem ainda utilizar a aplicação Managed Browser atual, Incentive os seus utilizadores para atualizarem para o iOS 8.0 ou posterior para aceder e tirar partido das novas funcionalidades do Managed Browser.

### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview

Não existem novas funcionalidades híbridas foram introduzidas em Agosto de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

Não existem novas funcionalidades híbridas foram introduzidas em Agosto de 2016 para o Configuration Manager (ramo atual).

## <a name="july-2016"></a>Julho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas em Julho de 2016 funcionam em implementações híbridas.

- **SDK Xamarin para aplicações do Intune está disponível**

  O componente Xamarin do SDK da aplicação Intune permite-lhe ativar as funcionalidades de gestão de aplicações móveis do Intune no seu móveis aplicações iOS e Android compiladas com o Xamarin. Pode encontrar o componente no [arquivo Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) ou no [página do Microsoft Intune Github](https://github.com/msintuneappsdk).

- **Experiência do utilizador melhorada na inscrição de dispositivos do Windows**

  Quando estiver a utilizar o acesso condicional, os passos de inscrição para Windows 8.1, Windows 10 Desktop e Windows 10 Mobile foram clarificados no Web site do Portal da empresa. Os utilizadores irão ver agora separadas **inscrição de dispositivos** e **Workplace Join** passos, tornando mais fácil para os mesmos, para ver o estado dos respetivos dispositivos e concluir o processo se se deparar com um Workplace Join (WPJ) Falha. Os passos separados também espera para simplificar o processo de resolução de problemas para os administradores de TI. Anteriormente, quando os utilizadores finais tentavam inscrever e todos os passos de inscrição foi concluída com êxito, menos a WPJ, o dispositivo inscrito não aparecia na lista de dispositivos para os utilizadores identificarem, confundindo-os utilizadores.

  - **Eliminação completa já está disponível para dispositivos Windows 10**

    10 PCs e portáteis Windows inscritos como dispositivos móveis podem ser apagados para repor o dispositivo para as definições de fábrica. Para obter mais informações, consulte [como proteger os seus dispositivos com a eliminação remota](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Alterações às gestores de inscrição de dispositivos contas na aplicação do Portal da empresa do iOS**

  Para melhorar o desempenho e dimensionamento, o Intune já não apresenta todos os dispositivos de gestores de inscrição de dispositivos (DEM) no painel meus dispositivos da aplicação Portal da empresa iOS. Apenas o dispositivo local que executa a aplicação é apresentados e apenas se estiver inscrito através da aplicação Portal da empresa.

  O utilizador DEM pode executar ações no dispositivo local, mas a gestão remota de outros dispositivos inscritos só pode ser executada a partir da consola de administração do Intune. Além disso, Intune está a descontinuar a utilização de contas DEM com o programa de inscrição de dispositivos da Apple ou da ferramenta Apple Configurator. Estes métodos de inscrição já suportam a inscrição sem utilizador para dispositivos iOS partilhados.

  Utilize apenas contas DEM quando a inscrição sem utilizador para dispositivos partilhados não está disponível. Para obter mais informações, consulte [inscrever dispositivos pertencentes à empresa com o Gestor de inscrição do dispositivo no Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Alterações para a aplicação do Portal da empresa para Android**

  Se os utilizadores finais vir uma mensagem de erro que diz o dispositivo está em falta um certificado necessário, podem tocar num botão de "Como resolver este problema" para obter os passos para instalar o certificado em falta. Se os utilizadores de concluir os passos, mas veja um adicional "certificado em falta" mensagem de erro, é-lhes pedido para contactar o administrador de TI e fornecer esta ligação, que contém passos que os administradores de TI podem utilizar para corrigir o problema do certificado.

- **Restringir instalações de aplicações sideload em dispositivos Android inscritos**

  Dispositivos Android já não podem instalar aplicações através do site do Portal da empresa, a menos que os dispositivos foram inscritos no Intune ao utilizar a aplicação Portal da empresa do Intune para Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview

Não existem novas funcionalidades híbridas foram introduzidas em Julho de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que eram anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1606.

* Localizar, gerir e distribuir a Windows Store para aplicações de negócio para dispositivos Windows 10 na consola do Configuration Manager ([1604](#new-in-1604-technical-preview))
*   Definição de SmartLock para dispositivos Android ([1604](#new-in-1604-technical-preview))
*   Acionada por aplicação VPN para dispositivos Windows 10 ([1605](#new-in-1605-technical-preview))
*   Nova experiência para ações remotas de dispositivos ([1605](#new-in-1605-technical-preview))
*   Windows Store para aplicações empresariais ([1605](#new-in-1605-technical-preview))
*   Melhoramentos gerais para aplicações compradas em volume ([1605](#new-in-1605-technical-preview))
*   Windows Information Protection (WIP) ([1605](#new-in-1605-technical-preview))
*   Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS ([1605](#new-in-1605-technical-preview))
*   Categorizar automaticamente os dispositivos em coleções ([1606](#new-in-1606-technical-preview))

Para obter informações sobre a nova funcionalidade, consulte a documentação para a versão de pré-visualização técnica especificada.

## <a name="june-2016"></a>Junho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune
As seguintes funcionalidades do Intune introduzidas em Junho de 2016 funcionam em implementações híbridas.

- **Estado de funcionamento do serviço Intune** informações de estado de funcionamento do serviço do Intune foi movidas para uma localização central com outros serviços Microsoft. Agora, pode encontrar estas informações no Centro de administração do Microsoft 365 em estado de funcionamento do serviço. Para obter mais informações, consulte esta [mensagem de blogue](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Experiência melhorada configuração de política de dados do Windows 10 enterprise**

  O Intune tem agora uma experiência aprimorada para configurar a política de proteção de informações do Windows 10. As melhorias incluem melhores maneiras de criar regras de aplicação, especifique a definição de limite de rede e outras definições do Windows Information Protection. Para obter mais informações, consulte [criar uma política Windows Information Protection (WIP) com o Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Política de controlo do acesso do Cisco ISE rede para o Intune**

  Os clientes que utilizam o Cisco Identity serviço Engine (ISE) 2.1 e utilizam o Microsoft Intune também podem definir uma política de controlo de acesso de rede no ISE. Utilizar esta política, os dispositivos que precisam de ligar à rede através de Wi-Fi ou VPN tem de cumprir as seguintes condições antes de lhes ser concedido acesso:

  - Tem de ser gerido pelo Intune
  - Tem de estar em conformidade com todas políticas de conformidade do Intune implementadas

  Os utilizadores finais de dispositivos não conformes serão solicitados para inscrever e retificar quaisquer problemas de compatibilidade para obter acesso.

- **Acesso condicional para browser**

  Pode definir uma política de acesso condicional para Exchange Online e SharePoint Online, para que apenas podem ser acedidos a partir de browsers suportados em dispositivos geridos e em conformidade iOS e Android. Os utilizadores finais que tentarem iniciar sessão Outlook Web Access (OWA) e o SharePoint sites com dispositivos iOS e Android serão pedidos para inscrever o dispositivo no Intune, bem como que corrijam quaisquer problemas de não conformidade, para que poderem concluir o início de sessão. Para obter mais informações, veja

  * [Restringir o acesso ao e-mail no Exchange Online e no novo Exchange Online dedicado com o Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restringir o acesso ao SharePoint Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online suporta o acesso condicional**

  Pode definir uma política de acesso condicional para o Dynamics CRM Online, para que só possa ser acedida por dispositivos geridos e em conformidade iOS e Android. Os utilizadores finais que tentarem iniciar sessão na aplicação móvel Dynamics CRM em iOS e Android serão pedidos para se inscrever no Intune e que corrijam quaisquer problemas de não conformidade para concluir o início de sessão. Para obter mais informações, consulte [restringir o acesso ao Dynamics CRM Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Atualizações da aplicação Portal da empresa para Android**

  O Intune tem agora as seguintes novas políticas que irão afetar os utilizadores do Portal da empresa para Android:   

  Política  |Efeito nos utilizadores  
  ---------|---------
  Exigir que dispositivos não permitam a instalação de aplicações de origens desconhecidas (Android 4.0 +)     |  Os utilizadores finais com Android 4.0 ou dispositivos posteriores irão ver a mensagem, "Instalação de origens desconhecidas tem de ser desativada." Os utilizadores terão de ir para o **definições > segurança** nos seus dispositivos e desative **origens desconhecidas**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obterem mais informações sobre a mensagem e por que motivo é necessário desativar a definição.
  Exigir que dispositivos não permitam a instalação de aplicações de origens desconhecidas (Android 4.0 +)  |    Os utilizadores finais com Android 4.0 ou dispositivos posteriores irão ver a mensagem "Analisar se o dispositivo apresenta ameaças de segurança." Os utilizadores terão de ir para o **definições > Google > segurança** nos seus dispositivos e ative **análise de dispositivos de ameaças de segurança**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obterem mais informações sobre a mensagem e por que motivo é necessário para ativar a definição.     
  Exigir que a depuração USB esteja desativada (Android 4.2 e posterior)  | Os utilizadores finais com Android 4.2 ou dispositivos posteriores irão ver a mensagem, "a depuração de USB deve ser desativada." Os utilizadores terão de ir para o **definições > Opções de programador** nos seus dispositivos e desative **depuração de USB**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obterem mais informações sobre a mensagem e por que motivo é necessário desativar a definição.
  Nível de patch de segurança mínima para Android (Android 6.0 +)  | Os utilizadores finais com Android 6.0 ou dispositivos posteriores irão ver a mensagem, "este dispositivo não cumpre o nível de patch de segurança mínima para Android." Os utilizadores terão de instalar o patch de segurança necessário. Uma ligação na mensagem de compatibilidade permite aos utilizadores obter informações sobre como instalar o patch de segurança necessárias e para ver que patch de segurança que está atualmente instalado.

- **Atualizações da aplicação Portal da empresa do iOS**

  * Quando os utilizadores finais estiverem a instalar aplicações de linha de negócio, irão ver agora uma experiência de instalação de aplicações melhorada. Se a instalação da aplicação está a demorar muito tempo, os utilizadores podem sincronizar manualmente o respetivo dispositivo para forçar o continuação do processo de sincronização. Para consultar as instruções de utilizador final, consulte a sincronizar o dispositivo iOS manualmente.
  * A aplicação Portal da empresa do Microsoft Intune para iOS foi atualizada para suportar a versão do iOS 8.0 e posterior. Esta atualização significa que os utilizadores finais podem instalar a aplicação Portal da empresa e inscrever novos dispositivos no Intune, apenas se o dispositivo está a executar o iOS versão 8.0 ou posterior. Os utilizadores que já inscreveram dispositivos que executem uma versão não suportada do iOS podem continuar a utilizar a aplicação Portal da empresa que se encontra no respetivo dispositivo.


### <a name="new-in-1606-technical-preview"></a>No Technical Preview da versão 1606
Os seguintes novos recursos introduzidos em Junho de 2016 estão disponíveis em implementações híbridas com o Intune e Configuration Manager Technical Preview 1606.

- **Categorizar automaticamente os dispositivos em coleções**

  Pode criar categorias de dispositivos, que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando estiver a utilizar o Configuration Manager com o Intune. Em seguida, os utilizadores têm de escolher uma categoria de dispositivo quando estes inscrevem um dispositivo no Intune. Além disso, é possível alterar a categoria de um dispositivo da consola do Configuration Manager. Para obter mais informações, consulte [automaticamente categorizar dispositivos em coleções](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) na [capacidades 1606 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > Esse recurso funciona com a versão de Junho de 2016 do Microsoft Intune. Certifique-se de que tiver sido atualizado para esta versão antes de experimentar estes procedimentos.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)
Não existem novas funcionalidades híbridas foram introduzidas em Junho de 2016 para o Configuration Manager (ramo atual).

##  <a name="may-2016"></a>Maio de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas em Maio de 2016 funcionam em implementações híbridas.

- **SDK DE MAM: Configuração do comprimento do PIN suporte**

  Agora pode especificar o comprimento do PIN para aplicações MAM, semelhantes a um PIN do dispositivo. Isto requer que os utilizadores finais estão em conformidade com as novas restrições que definiu. O ecrã de PIN é ligeiramente modificado para a conta para a entrada mais longa. Para obter detalhes, consulte [definições de política MAM para Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings), e [definições de política MAM para iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype para empresas para iOS e Android**

  Agora pode visar o Skype para empresas com o [MAM sem políticas de inscrição](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Depois dos utilizadores iniciam sessão, as políticas MAM serão aplicadas.  

- **Novas aplicações disponíveis para gestão com políticas MAM**

  As aplicações do Microsoft Word, Excel e PowerPoint para Android podem agora ser associadas a políticas MAM em dispositivos que não estão inscritos no Intune. Para obter uma lista completa de aplicações suportadas, aceda à Galeria de aplicações móveis do Microsoft Intune na [parceiros de aplicações do Microsoft Intune](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) página.  

- **Aplicação do portal da empresa para Android: Notificações de alerta do utilizador final**

  Notificações de alerta a partir da aplicação Portal da empresa para Android são apresentadas quando os utilizadores finais inscrever ou remover os dispositivos do Portal da empresa.  

- **Site do Portal da empresa: Faixa de identificação do dispositivo irá fornecer mais informações aos utilizadores finais**

  Os utilizadores finais podem agora identificar mais facilmente o dispositivo que selecionaram quando estão a utilizar o site do Portal da empresa. Se for selecionado o dispositivo incorreto, podem selecionar o dispositivo correto ao tocar o **toque aqui** ligação na faixa da página inicial.  


### <a name="new-in-1605-technical-preview"></a>No Technical Preview da versão 1605  
 Os seguintes novos recursos introduzidos em Maio de 2016 estão disponíveis em implementações híbridas com o Intune e Configuration Manager Technical Preview 1605. Estas funcionalidades necessitam que utilize a consola do Configuration Manager para configurar e geri-los.  

- **Acionada por aplicação VPN para dispositivos Windows 10**

  Para dispositivos do Windows 10 geridos com o Configuration Manager com o Intune, pode adicionar uma lista de aplicações que abra automaticamente uma ligação de VPN que tiver configurado através da consola de administração do Configuration Manager. Para obter mais informações, consulte [acionada por aplicação VPN para dispositivos Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1605) no [funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nova experiência para ações remotas de dispositivos**

  Foi melhorada a experiência para executar ações remotas de dispositivos a partir da consola do Configuration Manager.

  Ações comuns, como **extinguir/limpar**, **repor código de acesso**, **bloqueio remoto**, e **ignorar bloqueio de ativação** agora podem ser encontradas no  **Ações do dispositivo remoto** menu acedido a partir de **ativos e compatibilidade** área de trabalho

  Para obter mais informações, consulte [nova experiência para ações do dispositivo remoto](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) na [funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Aplicações da Loja Windows para Empresas**

  O [Windows Store para empresas](https://www.microsoft.com/en-us/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja para o Configuration Manager, pode gerir aplicações compradas em volume a partir da consola do Configuration Manager. Para obter mais informações, consulte [Windows Store para aplicações de negócio](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) na [funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Melhoramentos gerais para aplicações compradas em volume**

  Aplicações compradas em volume a partir da Windows Store para empresas e a iOS app store foram consolidadas para a mesma exibição **informações de licença para aplicações Store**. Além disso, a maneira pela qual criar aplicações compradas em volume para iOS foi melhorada. Para obter mais informações, consulte[melhoramentos gerais para aplicações compradas em volume](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) na [funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS**

  Agora é possível identificar os dispositivos pertencentes ao importar os números de identidade (IMEI) de equipamento móvel internacional. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI de dispositivos ou pode introduzir manualmente as informações do dispositivo.  Também pode importar números de série para dispositivos iOS.  Para obter mais informações, consulte [pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) na [funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Information Protection (WIP)**

  Pode criar itens de configuração que permitem-lhe implementar as políticas de Windows Information Protection (WIP), incluindo permitindo que escolha as suas aplicações protegidas, seu nível de proteção do WIP e como encontrar os dados empresariais na rede. Para obter mais informações sobre WIP, consulte os seguintes tópicos:  

  -   [Proteger os dados empresariais com o Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Criar e implementar uma política Windows Information Protection (WIP) com o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 Não existem novas funcionalidades híbridas foram introduzidas em Maio de 2016 para o Configuration Manager (ramo atual).  

##  <a name="april-2016"></a>Abril de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas em Abril de 2016 funcionam em implementações híbridas.  

- **Conformidade de utilizadores MAM**

  Agora, pode ver o estado das suas políticas de gestão de aplicações para qualquer utilizador no seu inquilino do Azure Active Directory (AAD).  Para obter mais informações, consulte [monitorizar políticas de gestão de aplicações móveis com o Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Controlos de MAM para impedir a sincronização de contactos do Outlook (Android)**

  Uma nova definição está disponível que permite-lhe impedir que uma aplicação sincronize contactos no livro de endereços nativo em dispositivos Android. Esta nova definição é suportada inicialmente pela aplicação Outlook em dispositivos Android. Para obter mais informações, consulte [criar e implementar políticas de gestão de aplicações móveis com o Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Melhorias para o site do Portal da empresa**

  Quando os utilizadores do Windows 10 Mobile e Windows Phone 8.1 estiverem a instalar aplicações de linha de negócio, irão ver agora os seguintes Estados novos, que fornecem mais detalhes sobre o estado da instalação:  

  -   **A aguardar sincronização do dispositivo** – o utilizador tocou em "Instalar" e o dispositivo tenta agora sincronizar com a infraestrutura do Intune. A sincronização é necessária para concluir a instalação. A mensagem "A aguardar sincronização do dispositivo" também é uma ligação que os utilizadores podem tocar para ver instruções sobre como sincronizar manualmente o respetivo dispositivo no Intune se o processo de sincronização está a demorar muito tempo ou ficar parado.  

  -   **Baixar o** – o pedido de transferência do utilizador está a ser processado e que o dispositivo está a transferir e instalar a aplicação.  

- **Melhorias para a aplicação do portal da empresa para Android**

  Os utilizadores que não inscreveram o seu dispositivo no Intune e que não tenham o certificado correto instalado não será possível iniciar sessão na aplicação Portal da empresa para Android e verão a mensagem, "não pode iniciar sessão porque o dispositivo está em falta um certificado necessário." A mensagem inclui uma ligação de "Como resolver este problema", que os utilizadores podem tocar para ver instruções para instalar o certificado. Para ver os passos que os utilizadores finais seguem para resolver o problema, consulte [o dispositivo está em falta um certificado necessário](/intune/enduser/using-your-android-device-with-intune) na biblioteca do Intune.  

- **Melhorias para a aplicação Portal da empresa para iOS**

  Foi adicionado suporte para a ação de solicitação para a atualização atualizar o conteúdo do ecrã principal, que inclui as aplicações listadas, os dispositivos listados e contacto de TI informações. A ação de solicitação para a atualização não verifica se existem informações de conformidade ou políticas, que podem ser efetuadas ao selecionar o mosaico para o seu dispositivo atual e ao tocar o **sincronização** botão.  

- **Melhorias na aplicação do Portal do Windows 10 Mobile e da empresa do Windows Phone 8.1**

  Quando os utilizadores finais estiverem a instalar aplicações de linha de negócio, irão ver agora uma experiência de instalação de aplicações melhorada. Se a instalação da aplicação está a demorar muito tempo, os utilizadores podem sincronizar manualmente o respetivo dispositivo para forçar o continuação do processo de sincronização. Para rever as instruções de utilizador final, consulte [sincronizar o seu dispositivo manualmente para acelerar a instalação de aplicações](/intune/enduser/using-your-windows-device-with-intune) na biblioteca do Intune.  

###  <a name="new-in-1604-technical-preview"></a>Novo no 1604 Technical Preview
 Os seguintes novos recursos introduzidos em Abril de 2016 estão disponíveis em implementações híbridas com o Intune e Configuration Manager Technical Preview 1604. Estas funcionalidades necessitam que utilize a consola do Configuration Manager para configurar e geri-los.  

- **Localizar, gerir e distribuir a Windows Store para aplicações de negócio para dispositivos Windows 10 na consola do Configuration Manager**


  Suporte para Windows Store para empresas está disponível na configuração Manager Technical Preview 1604 para o ajudar a localizar, gerir e distribuir aplicações para os dispositivos Windows 10 que estiver a gerir. Para obter detalhes, consulte [gerir aplicações compradas em volume a partir da Windows Store para empresas](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) na [funcionalidades no Technical Preview 1604 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Definição de SmartLock para dispositivos Android**

  Foi adicionada uma nova definição para o item de configuração de Android e Samsung KNOX Standard que lhe permita controlar a funcionalidade de SmartLock em dispositivos Android compatíveis.  Pode utilizar esta definição para impedir que os utilizadores finais configurem o SmartLock. Ver [definição de SmartLock para dispositivos Android](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) na [funcionalidades no Technical Preview 1604 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 Não existem novas funcionalidades híbridas foram introduzidas em Abril de 2016 para o Configuration Manager (ramo atual).  

##  <a name="march-2016"></a>Março de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas em Março de 2016 funcionam em implementações híbridas.  

- **Controlos de MAM para impedir a sincronização de contactos do Outlook (iOS)**

  Uma nova definição está disponível que permite-lhe impedir que uma aplicação sincronize contactos no livro de endereços nativo em dispositivos iOS. Esta nova definição é suportada pela aplicação Outlook em dispositivos iOS. Para obter mais detalhes sobre esta e outras definições, consulte [criar e implementar políticas de MAM](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Skype para empresas Online suporta o acesso condicional**

  Pode definir uma política de acesso condicional para o Skype para empresas Online, para que só possa ser acedida por dispositivos geridos e em conformidade iOS e Android.  Para obter detalhes, consulte [gerir o acesso ao Skype para empresas Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) na biblioteca do Intune.  

- **Suporte para iOS 9.3**

  Na segunda-feira, 21 de Março, a Apple anunciou a disponibilidade do iOS 9.3. Todas as funcionalidades existentes do Intune atualmente disponíveis para gerir dispositivos iOS irão continuar a trabalhar de forma totalmente integrada quando os utilizadores atualizarem os seus dispositivos para iOS 9.3.  

- **Pacotes de aplicações do Windows disponíveis diretamente a partir do site do Portal da empresa**

  Os utilizadores de PCs com Windows RT, Windows 8.1 e Windows 8 podem agora instalar pacotes de aplicações do Windows (com a extensão. AppX) diretamente a partir do site do Portal da empresa. Anteriormente, era necessário implementar ou os utilizadores tinham de instalar a aplicação Portal da empresa nos respetivos dispositivos para instalar aplicações.  

- **Os utilizadores podem bloquear remotamente o seu dispositivo a partir do site do Portal da empresa**

  Foi adicionada uma nova opção de bloqueio remoto para o site do Portal da empresa para permitir que os utilizadores bloqueiem remotamente o seu dispositivo a partir do Portal se o dispositivo é perdido ou roubado.  

- **Tire partido do iOS "Open-in" gestão de dispositivos que estão inscritos numa solução de MDM de terceiros**

  Pode utilizar o seu fornecedor de gestão (MDM) de dispositivos móveis de terceiros para tirar partido do iOS gestão "Open-In". Pode configurar as restrições na configuração de definições de perfil e implementar a aplicação utilizando o software MDM. Quando o utilizador instala a aplicação gerida, são aplicadas as restrições. Leia os detalhes: [Políticas de gestão de aplicações móveis do Microsoft Intune e iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) na biblioteca do Intune.  

- **Aplicações da Microsoft que suportam MAM**

  A lista de aplicações da Microsoft que pode utilizar com políticas de gestão de aplicações móveis do Intune foi atualizada para incluir as aplicações mais recentes (para dispositivos inscritos com o Intune apenas).  

- **Implementar o Adobe Reader para Microsoft Intune para dispositivos iOS geridos pelo Intune na sua empresa**

  A aplicação Adobe Reader para iOS pode agora ser gerida em dispositivos inscritos com a política de gestão de aplicações móveis do Intune.  

- A aplicação de partilha Rights Management é suportada para Android

  Os administradores de TI podem implementar políticas de gestão de aplicações móveis, para que os utilizadores finais podem ver imagens, AV e PDF de forma mais segura, os ficheiros ou não IT utiliza o Intune para gerir os dispositivos.  

- **Melhorias para a aplicação Portal da empresa iOS e Android**

  -   Quando os seus utilizadores iniciarem uma aplicação que é gerida pela gestão de aplicações móveis (MAM), verão uma mensagem a indicar que a aplicação é gerida pela sua empresa. Os utilizadores podem agora tocar numa ligação "Mais informações" para obter mais informações aqui sobre o que significa "aplicações geridas". Eles também podem tocar "Não mostrar novamente" para que a mensagem deixa de aparecer quando iniciarem a aplicação.  

  -   Foram adicionados novos ecrãs para orientar os usuários por meio do processo de inscrição e fornecer mais informações sobre por que motivo devem inscrever os utilizadores e o que os administradores de TI podem e não podem ver nos seus dispositivos inscritos.  

  -   Mensagens de erro de inscrição são agora apresentadas na aplicação Portal da empresa.  

### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview  
 Não existem novas funcionalidades híbridas foram introduzidas no Março de 2016 para o Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 Os seguintes novos recursos introduzidos em Março de 2016 estão disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1602. Estas funcionalidades necessitam que utilize a consola do Configuration Manager para configurar e geri-los.  

- **Políticas de configuração de aplicações iOS**

  Na versão 1602 do Configuration Manager (ramo atual) pode utilizar políticas de configuração de aplicação para disponibilizar definições que poderão ser necessárias quando o utilizador executa uma aplicação iOS. Para obter detalhes, consulte [configurar aplicações iOS com políticas de configuração de aplicações no System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Gerir aplicações iOS compradas em volume**

  Na versão 1602 do Configuration Manager (ramo atual), pode implementar e gerir aplicações compradas em volume do Apple Volume Purchase Program (VPP) ao importar as informações de licença da loja de aplicações e ao controlar a quantidade de licenças utilizou. Para obter detalhes, consulte [gerir aplicações de iOS compradas em volume com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Criação automática de aplicações móveis do Office**

  As Microsoft Office seguintes aplicações móveis para Android e iOS partir da versão 1602 do Configuration Manager (ramo atual), são criadas durante a atualização da versão 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (apenas iOS)  
  -   Microsoft Outlook  

  Irá encontrar estas aplicações no nó Applications da consola do Configuration Manager. Para obter mais informações sobre a implementação de aplicações, consulte [como implementar aplicações com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Definições do modo de local público para dispositivos Android Samsung KNOX Standard**

  O modo Kiosk permite-lhe bloquear um dispositivo e permitir que apenas determinadas funcionalidades funcionem.  Partir da versão 1602 do Configuration Manager (ramo atual), pode agora especificar definições do modo de local público para dispositivos Samsung KNOX Standard. Para obter detalhes, consulte [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerido sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Bloqueio de ativação do iOS**

  Partir da versão 1602 do Configuration Manager (ramo atual), pode gerir o bloqueio de ativação do iOS, uma funcionalidade da aplicação encontrar o meu iPhone para iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo.  Para obter detalhes, consulte [ignorar o bloqueio de ativação de iOS de gerir para o System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  



## <a name="notices"></a>Avisos

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): Suporte para gestão de dispositivos móveis híbrida que termina em 10 de Abril de 2017
*11 de Janeiro de 2017*

Suporte para o System Center 2012 Configuration Manager SP1 e System Center 2012 R2 Configuration Manager RTM terminou em 12 de Julho de 2016. Posteriormente, suporte para essas versões ligar ao serviço para MDM híbrida termina a 10 de Abril de 2017 do Microsoft Intune. Após esta data, MDM híbrida deixará de funcionar com essas versões. Dispositivos geridos essencialmente se tornarem não geridos que o conector do Intune já não irá estabelecer ligação ao serviço do Intune. Dados do Configuration Manager (por exemplo, políticas e aplicações) não irão fluir até o Intune e os dados de dispositivo gerido não irão fluir para o Configuration Manager até que uma atualização ocorre.

Se estiver a executar uma implementação híbrida com o Configuration Manager 2012 SP1 ou R2 RTM, recomendamos que antes de 10 de Abril de 2017 Atualize para o Configuration Manager (ramo atual) ou o pacote de serviço mais recente suportado para o Configuration Manager 2012 (qualquer um dos R2 SP1 ou SP2) para evitar a interrupção do serviço.

Recursos adicionais:
-   [Atualizar para o System Center Configuration Manager (ramo atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planear a atualização para o System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planear a atualização para o System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Carregamento do Portal da empresa do Windows Phone 8 preterido
*25 de Outubro de 2016*

A capacidade de carregar uma aplicação assinada do Portal da empresa foi removida da consola do Configuration Manager, como suporte do Intune está sendo excluído do Windows 8, Windows Phone 8, e Windows RT e o suporte para o Portal da empresa do Windows Phone 8 termina em Novembro.  Dispositivos Windows 8, Windows Phone 8 e Windows RT, que já tenham sido inscritos continuarão a ser suportada, mas a inscrição de dispositivos adicionais com estas plataformas não será suportada.
