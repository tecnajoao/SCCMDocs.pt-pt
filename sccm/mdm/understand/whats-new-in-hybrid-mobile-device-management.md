---
title: "Novidades da MDM híbrido"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as novas funcionalidades de gestão do dispositivo móvel disponíveis para implementações híbridas com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 10/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 74b7578610f60bc9d5692f90227aa11da592efcf
ms.sourcegitcommit: b9c1c9ca5aaf806e8beee2709ed15392ee3e19fe
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Novidades na gestão de dispositivos móveis híbrida com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre o dispositivo móvel novo funcionalidades de gestão (MDM) disponíveis para implementações híbridas com o System Center Configuration Manager e o Microsoft Intune.     

> [!Note]    
> Intune no Azure é a solução de MDM recomendada da Microsoft.     
> - Para obter mais informações sobre novas funcionalidades e atualizações no Intune autónomo, consulte [Novidades do Intune](https://docs.microsoft.com/intune/whats-new).    
> - Para obter mais informações sobre como migrar para o Intune autónomo, consulte [migrar utilizadores MDM híbrida e dispositivos ao Intune autónomo](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).
> - Para obter detalhes sobre atualizações de IU para o Intune e o MDM híbrido, consulte [atualizações de IU para aplicações de utilizador final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  
Cada secção deste artigo apresenta uma lista de funcionalidades híbridas em três categorias diferentes. Utilize as seguintes orientações para determinar a compatibilidade das funcionalidades em cada categoria com diferentes versões do Configuration Manager:  

|Categorias de funcionalidade|Descrição|
|-|-|
|**Novo no Microsoft Intune** | Em geral, todas as funcionalidades listadas nesta categoria devem funcionar com todas as versões do Configuration Manager. Versões este incluindo System Center 2012 R2 Configuration Manager, uma vez que estas funcionalidades apenas requerem o serviço do Intune e não necessitam de funcionalidades adicionais no Configuration Manager.|
|**Novo no Configuration Manager Technical Preview**| Todas as funcionalidades listadas na categoria deste só funcionam com a versão de pré-visualização técnica especificada. Para experimentar estas funcionalidades, tem de instalar a versão de pré-visualização técnica especificada na descrição da funcionalidade. Para obter mais informações, consulte [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Novo no Configuration Manager (ramo atual)**| Todas as funcionalidades listadas na categoria deste funcionam apenas com a versão especificada do Configuration Manager (ramo atual), como versão 1511 ou 1602. Se estiver a utilizar uma versão mais antiga do Configuration Manager para a implementação híbrida, tem de atualizar para a versão do Configuration Manager (ramo atual) especificada na descrição da funcionalidade. Para obter mais informações, consulte [atualizar para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|


## <a name="october-2017"></a>Outubro de 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Novo no Configuration Manager Technical Preview 1709

- **Experiência de perfil da VPN na consola do Configuration Manager melhorada**<!-- 1313282 -->     
    Definições do perfil VPN agora são filtradas de acordo com a plataforma. Quando criar novos perfis VPN, cada plataforma suportada contém apenas as definições adequadas para a plataforma. Perfis VPN existentes não são afetados. Pode ler mais sobre esta alteração [aqui](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).


### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  

- **Melhoramentos ao dispositivo configurar fluxo de trabalho no Portal da empresa**<!--1490692-->    
  Iremos tiver melhorado o fluxo de trabalho do programa de configuração do dispositivo na aplicação Portal da empresa para Android. O idioma mais amigável de utilizador e específica da sua empresa e tenha combinado ecrãs sempre que possível. Pode vê-los no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017) página.

- **Melhorado orientações sobre o pedido de acesso para contactos em dispositivos Android**<!--1484985-->    
  A aplicação Portal da empresa para Android requer, muitas vezes, o utilizador final aceitar a permissão de contactos. Se um utilizador final recusar este acesso, irão ver agora uma notificação na aplicação que alertas-los para conceder acesso condicional. 

- **Proteger a remediação de arranque para Android**<!--1490712-->    
  Os utilizadores finais com dispositivos Android será possível toque o motivo de não conformidade na aplicação Portal da empresa. Sempre que possível, isto é reencaminhado diretamente para a localização correta na aplicação definições para corrigir o problema. 

- **Notificações de push adicionais para os utilizadores finais na aplicação Portal da empresa para Android Oreo**<!--1475932 -->    
  Os utilizadores finais irão ver notificações adicionais para indicar-lhes quando a aplicação Portal da empresa para Android Oreo está a efetuar tarefas em segundo plano, tais como obtenção de políticas do serviço do Intune. As notificações aumentam transparência para os utilizadores finais sobre quando o Portal da empresa está a realizar tarefas administrativas no respetivo dispositivo. Esta é a parte do global [Otimização da IU de Portal da empresa](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para a aplicação do Portal da empresa para Android Oreo. 

- **Novo comportamentos para a aplicação Portal da empresa para Android com perfis de trabalho**<!--1485783-->    
  Quando inscreve um Android para dispositivos de trabalho com um perfil de trabalho, é a aplicação Portal da empresa no perfil de trabalho que executa tarefas de gestão no dispositivo. 

  Se estiver a utilizar uma aplicação ativada para MAM no perfil de pessoal, a aplicação Portal da empresa para Android já não serve qualquer utilização. Para melhorar a experiência de perfil de trabalho, o Intune será automaticamente ocultar pessoal aplicação Portal da empresa depois da inscrição de perfil um trabalho com êxito.

  A aplicação Portal da empresa para Android pode ser ativada em qualquer altura no perfil de pessoal ao navegar para [Portal da empresa na Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) e ao tocar em **ativar**.

- **Portal para Windows 8.1 e Windows Phone 8.1 Mover para sustaining modo de empresa**<!--1428681-->    
 Foi adicionado um aviso para anunciar que aplicações de Portal da empresa para Windows 8.1 e Windows Phone 8.1 estão a mover para sustaining modo. Para obter mais informações, consulte [avisos](#notices).  

- **Inscrição de dispositivos Samsung Knox não suportado de bloco**<!-- 1490695 -->    
  A aplicação Portal da empresa tenta apenas inscrever dispositivos Samsung Knox suportados. Para evitar erros de ativação de KNOX que impedem a inscrição MDM, inscrição de dispositivos é tentada apenas se o dispositivo é apresentado no [lista de dispositivos publicados pelo Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Dispositivos Samsung podem ter números de modelo que suportam KNOX enquanto outros que não. Verificar a compatibilidade de Knox com o seu revendedor a partir do dispositivo antes de compra e implementação. Pode encontrar a lista completa dos dispositivos verificados o [as definições de política do Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).

- **Fim de suporte para Android 4.3 e inferior**<!--1171126, 1326920 -->    
  Um aviso foi adicionada para o fim de suporte para Android 4.3 e inferior. Para obter mais informações, consulte [avisos](#notices).

- **Informar os utilizadores finais as informações do dispositivo podem ser vistas em dispositivos inscritos**<!--1165314-->    
  Que estamos a adicionar **o tipo de propriedade** para o ecrã de detalhes do dispositivo em todas as aplicações do Portal da empresa. Isto permitirá aos utilizadores encontrar mais informações sobre privacidade diretamente a partir de [as informações da sua empresa pode ver?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) artigo. Isto irá ser disponibilizando em todas as aplicações do Portal da empresa num futuro próximo. Isto é comunicada para iOS no [Setembro](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 




## <a name="september-2017"></a>Setembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Atualizar ação adicionada à aplicação Portal da empresa para Windows 10**<!-- 1132468 -->    
    Aplicação Portal da empresa para Windows 10 permite aos utilizadores atualizar os dados na aplicação, a extrair para atualizar ou, em ambientes de trabalho, premir F5.

- **Informar os utilizadores finais as informações do dispositivo podem ser vistas para iOS**<!--739894-->    
    Foi adicionado **o tipo de propriedade** para o ecrã de detalhes do dispositivo na aplicação Portal da empresa para iOS. Isto permitirá aos utilizadores encontrar mais informações sobre privacidade diretamente a partir desta página de documentos do utilizador final do Intune. Também irá ser capazes de localizar estas informações no ecrã Acerca. 

- **Mais fácil de compreender phrasing para a aplicação Portal da empresa para Android**<!---1396349-->       
    O processo de inscrição para a aplicação Portal da empresa para Android foi simplificado por um novo texto para tornar mais fácil para os utilizadores finais a inscrever. Se tiver de documentação da inscrição personalizada, será pretende atualizá-la para refletir ecrãs de novo. Pode encontrar as imagens de exemplo no nosso [atualizações de IU para aplicações de utilizador final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017) página.

- **Aplicação do Portal da empresa do Windows 10 adicionada ao Windows Information Protection Permitir política**<!-- 677129 -->    
    A aplicação Portal da empresa do Windows 10 foi atualizada para suportar a proteção de informações do Windows (WIP). A aplicação pode ser adicionada para o WIP Permitir política. Com esta alteração, a aplicação já não tem de ser adicionado para o **excluído** lista. 

- **Fim de aviso de suporte adicionado para o iOS 8.0**    
    Foi adicionado um aviso para o fim de suporte para o iOS 8.0. Para obter mais informações, consulte [avisos](#notices).

## <a name="august-2017"></a>Agosto de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Experiência de início de sessão iniciada novo para utilizadores do Portal da empresa para Android e utilizadores de política de proteção da aplicação**<!-- 621669 -->    
Os utilizadores finais pode procurar as aplicações, gerir dispositivos e ver contacto de TI informações utilizando a aplicação Portal da empresa Android sem inscrever os respetivos dispositivos Android. Além disso, se um utilizador final já utiliza uma aplicação protegida por políticas de proteção de aplicações do Intune e inicia o Portal da empresa Android, o utilizador final deixará de receber uma mensagem para se inscrever o dispositivo.


## <a name="july-2017"></a>Julho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Fim de avisos de suporte adicionado para Android e Windows Phone**

    Novo avisos foram adicionados para fim de suporte para versões de Android e Windows Phone. Para obter mais informações, consulte [avisos](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que se encontravam anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1706.

- [Suporte de Entrust para Entrust autoridades de certificação](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Novas definições de política de gestão de aplicações móveis](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Atualizações para o Android para a configuração de partilha de trabalho](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Novas regras de política de conformidade de dispositivo](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Novas definições de configuração para dispositivos Windows 10 que não são geridos com o cliente do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Suporte para perfis VPN macOS Cisco (IPsec)](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restrições de inscrição do Android e iOS](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 

## <a name="june-2017"></a>Junho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Alterar a autoridade MDM**

  A partir do Configuration Manager versão 1610, pode alterar a autoridade de MDM sem ter de contactar o Support da Microsoft e sem ter de anular a inscrição e inscrever-se novamente os seus dispositivos geridos existentes. Para obter mais informações, consulte [alterar a autoridade de MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Integração de proxy de aplicações e o browser gerida**

  Agora, o Browser gerido do Intune pode integrar com o serviço de Proxy de aplicações do Azure AD para permitir que os utilizadores acedam a web sites internos, mesmo quando estão a trabalhar remotamente. Os utilizadores do browser introduza o URL do site, tal como fariam normalmente e o Browser gerido encaminha o pedido através do gateway de web de proxy de aplicações. Para obter mais informações, consulte [acesso gerir Internet através de políticas de browser gerido](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **Aplicação do Portal da empresa para Android tem agora uma nova experiência de utilizador final para as políticas de proteção da aplicação**

  Com base nos comentários de clientes, iremos tiver modificado a aplicação do Portal da empresa para Android mostrar um **acesso da empresa conteúdo** botão. A intenção é impedir que os utilizadores finais desnecessariamente percorrer o processo de inscrição quando apenas precisam de aceder a aplicações que suportam a aplicação de políticas de proteção, uma funcionalidade de gestão de aplicações móveis do Intune. Pode ver estas alterações no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Nova ação de menu remover facilmente o Portal da empresa**

  Com base nos comentários dos utilizadores, a aplicação Portal da empresa para Android adicionou uma ação de menu novo para iniciar a remoção do Portal da empresa do seu dispositivo. Esta ação remove o dispositivo da gestão do Intune para que a aplicação pode ser removida do dispositivo pelo utilizador. Pode ver estas alterações no [Novidades na aplicação da IU](https://docs.microsoft.com/intune/whats-new-app-ui) página e no [documentação do utilizador final Android](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Melhoramentos à aplicação a sincronizar com o Windows 10 criadores Update**

  Aplicação Portal da empresa para Windows 10 agora inicia automaticamente uma sincronização para pedidos de instalação de aplicações para dispositivos com o Windows 10 criadores Update (versão 1703). Isto reduz o problema de instalações stalling durante o estado de "Sincronizar pendente". Além disso, os utilizadores conseguem iniciar manualmente a sincronizar a partir da aplicação. Pode ver estas alterações no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Nova experiência orientada para o Portal da empresa do Windows 10**

  Aplicação Portal da empresa para Windows 10 inclui uma explicação passo a passo experiência orientada do Intune para dispositivos que não foram identificados ou inscritos. A nova experiência fornece instruções passo a passo que o guiam de utilizador através do registo no Azure Active Directory (necessário para funcionalidades de acesso condicional) e a inscrição MDM (necessário para funcionalidades de gestão de dispositivos). A experiência orientada estará acessível a partir da home page do Portal da empresa. Os utilizadores podem continuar a utilizar a aplicação se não concluir o registo e a inscrição, mas irá ocorrer funcionalidade limitada.

  Esta atualização só é visível em dispositivos com Windows 10 aniversário da atualização (compilação 1607) ou superior. Pode ver estas alterações no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Melhoramentos para os mosaicos de aplicação na aplicação Portal da empresa para iOS**

  Atualizámos o design dos mosaicos na home page da aplicação para refletir a cor de imagem corporativa definido para o Portal da empresa. Para obter mais informações, consulte [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Selecionador de conta agora disponível para a aplicação do Portal da empresa para iOS**

  Os utilizadores de dispositivos iOS poderão ver o nosso novo selecionador de conta quando iniciam sessão no Portal da empresa se poderem utilizam o seu trabalho conta escolar ou profissional para iniciar sessão em outras aplicações da Microsoft. Para obter mais informações, consulte [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novo no Configuration Manager Technical Preview 1706

- **Novas definições de política de gestão de aplicações móveis**    

  As seguintes definições de política de gestão (MAM) de aplicações móveis estão agora disponíveis:

  - **Bloquear captura de ecrã (apenas dispositivos Android):** Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.
  - **Desative a sincronização de contactos:** Impede a aplicação de guardar os dados para a aplicação de contactos nativa no dispositivo.
  - **Desative a impressão:** Impede que a aplicação de trabalho de impressão ou dados escola.

  Consulte [proteger aplicações ao utilizar políticas de proteção de aplicações no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para experimentar as novas definições de política de proteção de aplicação.

- **Novas definições de item de configuração do Windows**  <!-- 1354715 -->    

  Novos itens de configuração do Windows estão disponíveis para as categorias de definição de palavra-passe, o dispositivo, o arquivo e o Microsoft Edge. Para obter mais informações, consulte [definições do item de configuração de novo Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).

- **Novas regras de política de conformidade de dispositivo**    

  Agora, pode configurar novas opções de políticas de conformidade que foram anteriormente disponíveis apenas no Intune autónomo. Para obter mais informações, consulte [melhoramentos de política de conformidade do dispositivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrições de inscrição do Android e iOS**<!-- 1290826 -->      

  Administradores agora podem especificar que os utilizadores não é possível inscrever dispositivos Android ou iOS pessoais no respetivo ambiente híbrido. Isto permite-lhe limite inscritos dispositivos para predeclared, dispositivos pertencentes à empresa ou os dispositivos iOS inscritos com o programa de inscrição de dispositivos apenas. Para obter mais informações, consulte [restrições de inscrição do Android e iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).

- **Suporte para autoridades de certificação Entrust**<!-- 1350740 -->     

  O Configuration Manager suporta agora autoridades de certificação Entrust; Isto permite que a entrega de certificado PFX para dispositivos inscritos no Microsoft Intune.    

  Pode configurar Entrust como a autoridade de certificação quando adicionar uma função de ponto de registo de certificados no Configuration Manager. Ao adicionar um novo perfil de certificado que emite certificados PFX, pode selecionar um Microsoft ou Entrust autoridade de certificação.

  **Problema de conhecido**: No 1706 technical preview, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Isto não afeta os certificados PFX importados ou perfis SCEP.

- **Suporte para perfis VPN macOS Cisco (IPsec)**  <!-- 1321367 -->    

  Pode criar um macOS perfil da VPN com o Cisco (IPsec) como o tipo de ligação. Para obter mais informações, consulte [criar perfis VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="april-2017"></a>Abril de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **MyApps disponíveis para o Browser gerido**

  Microsoft MyApps agora tem um melhor suporte no Browser gerido. Utilizadores de Browser geridos que não são direcionados para gestão encaminhados diretamente para o serviço de MyApps, onde poderem aceder às suas aplicações de SaaS aprovisionado de admin. Os utilizadores que são direcionados para a gestão do Intune continuam a ser capazes de aceder MyApps do marcador de Browser gerido incorporado.

- **Ícones de novo para o Browser gerido e o Portal da empresa**

  O Browser gerido está a receber ícones atualizados para o Android e iOS versões da aplicação. No ícone novo irá conter o destaque do Intune atualizado para o tornar mais consistentes com outras aplicações no Enterprise Mobility + Security (IT + S). Pode ver no ícone novo para o Browser gerido no [são as novidades na página de IU da aplicação Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  O Portal da empresa também está a receber ícones atualizados para os Android, iOS e Windows versões da aplicação para melhorar a consistência com outras aplicações no IT + S. Estes ícones serão lançadas gradualmente entre plataformas de Abril de Maio enlace tardio.

- **Inicie sessão no indicador de progresso no Portal da empresa para Android**

  Uma atualização para a aplicação Portal da empresa Android mostra um início de sessão no indicador de progresso quando o utilizador inicia ou retoma a aplicação. O indicador progridem Estados novos, começando com "Ligar...", em seguida, "Assinatura suplemento …", em seguida, "A verificar requisitos de segurança..." antes de permitir que o utilizador aceda à aplicação. Pode ver os novos ecrãs para a aplicação Portal da empresa para Android no [são as novidades na página de IU da aplicação Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Impedir que as aplicações acedam ao SharePoint Online**

  Agora, pode criar uma política de acesso condicional baseado na aplicação para impedir que as aplicações que não têm a aplicar políticas de proteção de aplicação para-las, acedam [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). No cenário de acesso condicional baseado em aplicações, pode especificar as aplicações que pretende que tenham acesso ao SharePoint Online com o portal do Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novo no Configuration Manager Technical Preview 1704

- **Configurar as aplicações Android com políticas de configuração de aplicação**

  Pode utilizar políticas de configuração de aplicações no System Center Configuration Manager (Configuration Manager) para distribuir definições previamente configuradas quando um utilizador executa uma aplicação no Android para dispositivos de trabalho. Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos com Android para o trabalho e aplicam a aplicações aprovadas da Play para o arquivo de trabalho. Para obter informações sobre como experimentar esta funcionalidade, consulte [Android configurar aplicações com políticas de configuração de aplicações](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).

## <a name="march-2017"></a>Março de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Nova experiência de utilizador para a aplicação Portal da empresa para Android**

  A aplicação Portal da empresa para Android tem uma aspeto e funcionalidade modernos mais a sua interface de utilizador. As atualizações importantes são:

  - Cores: Cabeçalhos de separador de Portal da empresa são coloridos no definido de IT imagem corporativa.
  - Aplicações: No **aplicações** separador, o **aplicações em destaque** e **todas as aplicações** botões são atualizados.
  - Pesquisa: No **aplicações** separador, o **pesquisa** botão é um botão de ação de vírgula flutuante.
  - Navegar aplicações: **Todas as aplicações** vista mostra uma vista de separadores **em destaque**, **todos os**, e **categorias** para navegação mais fácil.
  - Suporte: **Os meus dispositivos** e **contactar TI** separadores são atualizados para melhorar a legibilidade.

  Para obter mais informações sobre estas alterações, consulte [atualizações de IU para aplicações de utilizador final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Assinatura de Script para o Portal da empresa do Windows 10**

  Se precisar de transferir e sideload da aplicação do Portal da empresa do Windows 10, agora, pode utilizar um script para simplificar e simplificar o processo de assinatura de aplicações para a sua organização.  Para transferir o script e as instruções para utilizá-lo, consulte [Microsoft Intune assinatura de Script para Windows 10 Portal da empresa](https://aka.ms/win10cpscript) na galeria do TechNet. Para obter mais informações sobre este anúncio, consulte [a atualizar a aplicação Portal da empresa do Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) no blogue de equipa de suporte do Intune.

- **Suporte melhorado para os utilizadores de Android com base na China**

  Devido à ausência do Google Play Store na China, dispositivos Android tem de obter aplicações da marketplaces chinês. O Portal da empresa suporta este fluxo de trabalho ao redirecionar os utilizadores de Android na China transferir as aplicações Portal da empresa e o Outlook de lojas de aplicações locais. Isto melhora a experiência de utilizador quando as políticas de acesso condicional estão ativadas para gestão de dispositivos móveis e gestão de aplicações móveis. As aplicações do Portal da empresa e do Outlook para Android estão disponíveis de lojas de aplicações chinês seguintes:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Certifique-se de que as aplicações do Portal da empresa estão atualizadas**

  Dezembro de 2016, lançada uma atualização que ativar a imposição da autenticação multifator (MFA) de um grupo de utilizadores quando inscreverem um iOS, Android, Windows 8.1 + ou dispositivo Windows Phone 8.1 +. Esta funcionalidade não funciona sem determinadas versões de linha de base da aplicação Portal da empresa para Android (v5.0.3419.0 +) e iOS (v2.1.17 +).

  Capacidades de gestão do Intune estão continuamente a melhorar e muitas melhorias tem coordenado atualizações para as aplicações do Portal da empresa em todas as plataformas suportadas. Como resultado, recomendamos que mantenha as versões mais recentes das aplicações do Portal da empresa instalado nos dispositivos para tirar partido das melhorias no Intune e para a melhor experiência de utilizador.

  >[!Tip]
  > Ter os seus utilizadores a definir os respetivos dispositivos para atualizar automaticamente as aplicações da loja de aplicações adequado. Se tiver efetuado a aplicação Portal da empresa Android disponíveis numa partilha de rede, pode transferir a versão mais recente do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams está ativada para MAM em dispositivos iOS e Android**

  As aplicações de Teams da Microsoft para iOS e Android agora estão ativadas com capacidades de gestão (MAM) de aplicações móveis do Intune, pelo que pode atribuir as equipas para trabalhar livremente entre dispositivos, garantindo que conversações e dados empresariais estão protegidos em cada vez. Para obter mais detalhes, consulte [o anúncio de Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) no blogue do Enterprise Mobility e segurança.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novo no Configuration Manager Technical Preview 1703

- **Suporte adicional para cenários de Apple Volume Purchase Program**

   A partir da Technical Preview 1703, tem agora suporte para os seguintes cenários de Volume Purchase Program (VPP):

   - Licenciamento do dispositivo - aplicações que suportam licenciamento do dispositivo e são implementadas em coleções de dispositivos agora apenas requerem uma licença por dispositivo.  Anteriormente, era necessário utilizar uma licença para cada utilizador num dispositivo. Para obter mais informações, consulte [implementar aplicações iOS compradas em volume para coleções de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Utilização de vários tokens VPP para um inquilino único híbrida com ambos os tokens utilizados para gerir as aplicações VPP.
   - Utilização de tokens de educação VPP com a capacidade para distinguir entre tokens de negócio e education.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que se encontravam anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1702.

- [Android para o suporte de trabalho](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Definições de compatibilidade de aplicações não conformes](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [A criação do certificado PFX e a distribuição e o suporte de S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Android e iOS versões deixam de ser targetable em assistentes de criação para MDM híbrida](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

As seguintes funcionalidades adicionais híbrida também estão incluídas na versão 1702 do Configuration Manager (ramo atual):

- **Suporte melhorado para Apple Volume Purchase Program (VPP)**

  - Pode agora implementar aplicações licenciadas para dispositivos, bem como os utilizadores. Consoante a capacidade de aplicações suporta o licenciamento do dispositivo, uma licença adequada foi reclamada quando a implementá-la, da seguinte forma:

    | Versão do Configuration Manager | Aplicação suporta o licenciamento do dispositivo? | Tipo de coleção de implementação | Licença pedida |
    |-|-|-|-|
    |Anteriores ao 1702|Sim|Utilizador|Licença de utilizador|
    |Anteriores ao 1702|Não|Utilizador|Licença de utilizador|
    |Anteriores ao 1702|Sim|Dispositivo|Licença de utilizador|
    |Anteriores ao 1702|Não|Dispositivo|Licença de utilizador|
    |1702 e posterior|Sim|Utilizador|Licença de utilizador|
    |1702 e posterior|Não|Utilizador|Licença de utilizador|
    |1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
    |1702 e posterior|Não|Dispositivo|Licença de utilizador|

  - Pode também implementar e controlar aplicações compradas do iOS Volume Purchase Program para Education.

  - Agora pode associar vários tokens de programa de compra da Apple com o Configuration Manager.

  Para mais informações sobre as aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Suporte para aplicações de linha de negócio na loja Windows para empresas**

  Agora pode sincronizar aplicações de linha de negócio personalizadas da loja Windows para empresas.

- **Defesa de ameaça Mobile novas ferramentas de monitorização**

    Tem agora novas formas para monitorizar o estado de compatibilidade com o fornecedor de serviços móveis defesa de ameaça.

    Para obter mais informações, consulte [como monitorizar a conformidade de defesa de ameaça Mobile](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Fevereiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Modernizing o Web site do Portal da empresa**

  O Web site do Portal da empresa suporta aplicações que são direcionadas para os utilizadores que não dispõe de dispositivos geridos. O Web site está alinhada com outros produtos e serviços Microsoft, utilizando um esquema de cores contrasting novo, ilustrações dinâmicas e "hamburger menu," que contém os detalhes de contacto de suporte técnico e informações sobre os dispositivos geridos existentes. A página de destino é reorganizar para destacar as aplicações que estão disponíveis para os utilizadores com carousels para aplicações em destaque e actualizado recentemente. Pode encontrar antes-e-depois de imagens disponíveis no [IU atualizações](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Novo endereço do servidor MDM para dispositivos Windows**

  O endereço do servidor MDM para inscrição de dispositivos Windows e Windows Phone foi alterado de manage.microsoft.com para enrollment.manage.microsoft.com. Notificar o utilizador a utilizar enrollment.manage.microsoft.com como o endereço do servidor MDM, se lhe for pedido para o mesmo durante a inscrição do Windows ou e o dispositivo Windows Phone. Esta atualização também necessita de qualquer CNAME no DNS que redireciona EnterpriseEnrollment.contoso.com para manage.microsoft.com ser substituído com um CNAME em DNS que redireciona EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com. Para obter informações adicionais sobre esta alteração, visite http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novo no Configuration Manager Technical Preview 1702

- **Android para o suporte de trabalho**

  Agora, pode gerir dispositivos Android que utilizam o Android de trabalho nos ambientes de MDM híbrida com 1702 de pré-visualização técnica do Configuration Manager. Dispositivos Android suportados agora podem ser inscritos como Android para dispositivos de trabalho, que cria um perfil de trabalho do dispositivo para os quais podem ser implementadas aprovadas no Play para o trabalho de aplicações. Também pode configurar e implementar itens de configuração, as políticas de conformidade e perfis de acesso a recursos para estes dispositivos. Para obter mais informações, consulte [Android para o suporte de trabalho](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Definições de compatibilidade de aplicações não conformes**

  Agora, pode criar regras de aplicações não conformes para aplicações Android e iOS nas políticas de conformidade. Se os dispositivos têm aplicações especificadas instaladas, estes são marcados "incompatíveis" e perderem o acesso aos recursos da empresa, de acordo com as políticas de acesso condicional no local. Para obter mais informações, consulte [melhoramentos de política de conformidade de dispositivos de acesso condicional](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **A criação do certificado PFX e a distribuição e o suporte de S/MIME**

  Agora pode criar e implementar certificados PFX para os utilizadores num ambiente híbrido. Estes certificados, em seguida, podem ser utilizados para encriptação de correio eletrónico de S/MIME e desencriptação pelos dispositivos que o utilizador inscreveu. Para obter mais informações, consulte [suportam certificados PFX criar com S MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Suporte para definições de configuração de iOS adicionais**
   
    Tem agora 42 definições do iOS adicionais que pode configurar como parte de um item de configuração. Foram adicionada a maioria das definições (35 em todos os) para dispositivos iOS supervisionados. Para obter mais informações, consulte [novas definições de conformidade para dispositivos iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Janeiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Suporta Android 7.1.1**

  O Intune agora totalmente suporta e gere Android 7.1.1.

- **Resolva o problema em dispositivos iOS estão inativos ou a consola de administração não consegue comunicar com os mesmos**

  Quando os dispositivos dos utilizadores perdem contacte com o Intune, pode conceder-lhes novos passos de resolução de problemas para ajudar a recuperar o acesso aos recursos da empresa. Consulte [dispositivos estão inativos, ou a consola de administração não consegue comunicar com os mesmos](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novo no Configuration Manager Technical Preview 1701

- **Android e iOS versões deixam de ser targetable em assistentes de criação para MDM híbrida**

  A partir da Technical Preview 1701 híbrida gestão de dispositivos móveis (MDM), já não tem como destino a versões específicas do Android e iOS, quando criar novas políticas e perfis de dispositivos geridos pelo Intune. Com esta alteração, implementações híbridas podem fornecer suporte mais rapidamente para novas versões de Android e iOS sem necessitar de uma nova versão do Configuration Manager ou a extensão. Para obter mais informações, consulte [versões Android e iOS já não são targetable em assistentes de criação](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Avisos

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portal para Windows 8.1 e Windows Phone 8.1 Mover para sustaining modo de empresa 
<!--1428681-->
*6 de Outubro de 2017*   
 
A partir de 2017 Outubro, irão mover as aplicações do Portal da empresa para Windows 8.1 e Windows Phone 8.1 para sustaining modo. Isto significa que as aplicações e cenários existentes, tais como a inscrição e conformidade, irão continuar a ser suportado para estas plataformas. Estas aplicações irão continuem a estar disponível para transferência através de canais de versão existentes, tais como o Microsoft Store. 

Uma vez no modo de sustaining, estas aplicações serão apenas irá receber atualizações de segurança críticas. Não haverá nenhum atualizações adicionais ou funcionalidades lançadas para estas aplicações. Para as novas funcionalidades, recomendamos que atualizar os dispositivos para Windows 10 ou Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fim de suporte para o iOS 8.0 
<!---1164477--->
Aplicações geridas e a aplicação Portal da empresa para iOS exigirá iOS 9.0 e superior para aceder a recursos da empresa. Dispositivos que não são atualizados antes de Setembro já não será possível aceder ao Portal da empresa ou a essas aplicações. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Lembrete de suporte de plataforma: Suporte de base do Windows Phone 8.1 terminou 11 de Julho de 2017
<!-- 1327781 -->
*11 de Julho de 2017*

A plataforma do Windows Phone 8.1 foi atingido o fim do suporte base. Suporte de PC do Windows 8.1 não é afetado.

Não há nenhum impacto imediato em qualquer dispositivo de Windows Phone 8.1 que é gerido pelo serviço do Intune, incluindo os que são inscritos no híbrida MDM. Dispositivos que estejam inscritos continuarão a funcionar e todas as políticas, as configurações e as aplicações continuarão a funcionar conforme esperado. Tenha em atenção, não existem nenhum melhorias visadas para a plataforma do Windows Phone 8.1 no âmbito do serviço Intune e para a aplicação Portal da empresa do Windows Phone 8.1.

Recomendamos que o serviço de atualização em dispositivos Windows Phone 8.1 elegíveis para Windows 10 Mobile na oportunidade de mais antigo.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fim de suporte para Android 4.3 e inferior
<!---1171127--->
*6 de Julho, de 2017*

Aplicações geridas e a aplicação Portal da empresa para Android exigirá Android 4.4 e superior aceder a recursos da empresa. Dispositivos que não são atualizados antes do início de Outubro já não será possível aceder ao Portal da empresa ou a essas aplicações. Por Dezembro, todos os dispositivos inscritos serão descontinuada dentro de Dezembro, resultando em perda de acesso aos recursos da empresa de imposição. Se estiver a utilizar políticas de proteção da aplicação sem MDM, as aplicações não receberão as atualizações e a qualidade dos respetivos experiência irá reduzir ao longo do tempo.


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): Suporte para gestão de dispositivos móveis híbridos terminados 10 de Abril de 2017
*11 de Janeiro de 2017*

Suporte para o System Center 2012 Configuration Manager SP1 e System Center 2012 R2 Configuration Manager RTM terminou no dia 12 de Julho de 2016. Posteriormente, suporte para estas versões ligar para o Microsoft Intune serviço para MDM híbrida termina a 10 de Abril de 2017. Após esta data, MDM híbrido irá deixar de funcionar com estas versões. Dispositivos geridos, essencialmente, ficarão fora da gestão que o conector do Intune já não irá estabelecer ligação ao serviço Intune. Dados do Configuration Manager (por exemplo, políticas e aplicações) não irão fluir até o Intune e os dados dos dispositivos geridos não irão fluir para o Configuration Manager até que uma atualização ocorre.

Se estiver a executar uma implementação híbrida com o Configuration Manager 2012 SP1 ou R2 RTM, recomendamos que 10 de Abril de 2017 antes de atualizar para o Configuration Manager (ramo atual) ou o pacote de serviço suportados mais recente do Configuration Manager 2012 (R2 SP1 ou SP2), para evitar a interrupção do serviço.

Recursos adicionais:
-   [Atualizar para o System Center Configuration Manager (ramo atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planear a atualização para System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planear a atualização para System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Carregamento do Portal da empresa do Windows Phone 8 preterido
*25 de Outubro de 2016*

A capacidade de carregar uma aplicação assinada do Portal da empresa foi removida da consola do Configuration Manager, como o suporte do Intune está a ser preterido para o Windows 8, Windows Phone 8 e Windows RT e o suporte para o Portal da empresa do Windows Phone 8 está a terminar em Novembro.  Windows 8, Windows Phone 8 e Windows RT dispositivos já inscritos continuarão a ser suportado, mas a inscrição de dispositivos adicionais com estas plataformas não será suportada.


### <a name="see-also"></a>Consulte Também

- [Decorridos desde as funcionalidades MDM híbrida](whats-new-hybrid-archive.md)
- [Novidades da MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
