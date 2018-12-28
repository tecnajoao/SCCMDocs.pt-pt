---
title: Novidades sobre a MDM híbrida
titleSuffix: Configuration Manager
description: Saiba mais sobre as novas funcionalidades de gestão do dispositivo móvel disponíveis para implementações híbridas com o Configuration Manager e o Intune.
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7cf1adf7d73e60fba0d748022ab7c241d60ffed7
ms.sourcegitcommit: c60e057075a83f07d1ca2577c3de1c7d7c8e9cec
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53626502"
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Quais são as novidades na gestão de dispositivos móveis híbrida com o Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre o dispositivo móvel novas funcionalidades de gestão (MDM) disponíveis para implementações híbridas com o System Center Configuration Manager e o Microsoft Intune.     

> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


> [!Note]    
> O Intune no Azure é a solução MDM recomendada da Microsoft.     
> - Para obter detalhes sobre os novos recursos e atualizações no Intune autónomo, consulte [o que há de novo no Intune](https://docs.microsoft.com/intune/whats-new).    
> - Para obter detalhes sobre como migrar para o Intune autónomo, consulte [migrar dispositivos e utilizadores MDM híbrida para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).
> - Para obter detalhes sobre as atualizações da interface do Usuário para o Intune e MDM híbrida, veja [atualização da IU para aplicações de utilizadores finais do Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 



##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

Cada secção deste artigo apresenta uma lista de funcionalidades híbridas em três categorias diferentes. Utilize as seguintes orientações para determinar a compatibilidade dos recursos em cada categoria com diferentes versões do Configuration Manager:  

|Categorias de funcionalidade|Descrição|
|-|-|
|**Novo no Microsoft Intune** | Em geral, todos os recursos listados nesta categoria devem funcionar com todas as versões do Configuration Manager. Versões este incluindo System Center 2012 R2 Configuration Manager, uma vez que estas funcionalidades requerem o serviço do Intune apenas e não necessitam de funcionalidades adicionais no Configuration Manager.|
|**Novo no Configuration Manager Technical Preview**| Todos os recursos listados nesta categoria só funcionam com o ramo de pré-visualização técnica especificado. Para experimentar estas funcionalidades, tem de instalar a versão de pré-visualização técnica especificada na descrição do recurso. Para obter mais informações, consulte [pré-visualização técnica do Configuration Manager](/sccm/core/get-started/technical-preview).|
|**Novo no Configuration Manager (ramo atual)**| Todos os recursos listados nesta categoria só funcionam com a versão especificada do Configuration Manager (ramo atual). Se estiver a utilizar uma versão mais antiga do Configuration Manager para a sua implementação híbrida, atualize para a versão do Configuration Manager (ramo atual) especificada na descrição do recurso. Para obter mais informações, consulte [atualizar para o Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).|



## <a name="december-2018"></a>Dezembro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="microsoft-auto-update-version-450-required-for-macos-devices"></a>Versão de atualização automática de Microsoft 4.5.0 necessária para dispositivos macOS
<!--3503442--> Para continuar a receber atualizações para o Portal da empresa e outros aplicativos do Office, dispositivos macOS geridos pelo Intune tem de atualizar para a atualização automática do Microsoft 4.5.0. Os utilizadores poderão já ter esta versão para seus aplicativos do Office.

#### <a name="the-intune-app-sdk-will-support-256-bit-encryption-keys"></a>O SDK da aplicação Intune irá suportar as chaves de encriptação de 256 bits 
<!--1832174--> O SDK da aplicação Intune para Android utiliza agora as chaves de encriptação de 256 bits quando a encriptação está ativada por políticas de proteção de aplicações. O SDK irá continuar a fornecer suporte de chaves de 128 bits para compatibilidade com o conteúdo e aplicações que utilizam versões mais antigas do SDK.

#### <a name="intune-requires-macos-1012-or-later"></a>O Intune necessita de macOS 10.12 ou posterior 
<!--2827778--> O Intune requer agora macOS versão 10.12 ou posterior. Dispositivos com versões anteriores do macOS não é possível utilizar o Portal da empresa para inscrição no Intune. Para receber suporte e os novos recursos, os utilizadores tem de atualizar o dispositivo para macOS 10.12 ou posterior e atualize o Portal da empresa para a versão mais recente.

Para obter mais informações, consulte [planear a alteração: O Intune suporta o macOS 10.12 e superior em Dezembro](#plan-for-change-intune-supports-macos-1012-and-higher-in-december).



## <a name="november-2018"></a>Novembro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="new-intune-device-subscription-sku"></a>Nova subscrição de dispositivo do Intune SKU
<!--3312071--> Para ajudar a reduzir o custo de gestão de dispositivos nas empresas, uma subscrição com base no dispositivo novo SKU está agora disponível. Este SKU de dispositivo do Intune é licenciado por dispositivo mensalmente. O preço varia pelo programa de licenciamento. Está disponível no canal direto, Enterprise Agreement (EA), Products da Microsoft e programa de serviços (MPSA) e aberto e fornecedor de soluções Cloud (CSP).

#### <a name="new-apps-support-with-app-protection-policies"></a>Suportam a novas aplicações com políticas de proteção de aplicações 
<!--3330037--> Agora pode gerir as seguintes aplicações com [políticas de proteção de aplicações do Intune](https://docs.microsoft.com/intune/app-protection-policies):

- Stream (iOS)  
- Para fazer (Android, iOS)  
- PowerApps (Android, iOS)  
- Fluxo (Android, iOS)  

Utilize políticas de proteção de aplicações para proteger a empresa transferência de dados e controle de dados para estas aplicações, como outra aplicações geridas por políticas do Intune. 

> [!Note]  
> Se ainda não está visível na consola do fluxo, adicione fluxo ao criar ou editar quaisquer políticas de proteção de aplicações. Selecione **mais aplicações**e, em seguida, especifique a *ID de aplicação* do Flow no campo de entrada. Para Android utilizam `com.microsoft.flow`, e para iOS utilize `com.microsoft.procsimo`.  



## <a name="october-2018"></a>Outubro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="updates-for-application-transport-security"></a>Atualizações de segurança de transporte de aplicações 
<!--748318--> O Microsoft Intune suporta Transport Layer Security (TLS) 1.2 + para fornecer encriptação de melhor em classe, para garantir que o Intune é mais seguro por padrão e para se alinhar com outros serviços Microsoft como o Microsoft Office 365. Para cumprir este requisito, portais de empresa do iOS e macOS irão impor requisitos segurança de transporte de aplicações (ATS) atualizados da Apple que também requerem TLS 1.2 +. A ATS é utilizada para impor medidas de segurança mais rigorosas em todas as comunicações feitas por aplicações através de HTTPS. Esta alteração irá afetar os clientes do Intune a utilizar as aplicações de Portal da empresa iOS e macOS. Para obter mais informações, consulte [Intune mudar para o TLS 1.2 para a encriptação](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/).

#### <a name="remove-an-email-profile-from-a-device-even-when-theres-only-one-email-profile"></a>Remover um perfil de e-mail de um dispositivo, mesmo quando o perfil tem apenas um e-mail 
<!--1818139--> Anteriormente, não foi possível remover um perfil de e-mail de um dispositivo se for o único perfil de e-mail. Com esta atualização, esse comportamento muda. Agora, pode remover um perfil de e-mail, mesmo se for o único perfil de e-mail no dispositivo. 

#### <a name="remove-pkcs-and-scep-certificates-from-your-devices"></a>Remover certificados PKCS e SCEP dos seus dispositivos 
<!--3218390--> Em alguns cenários, os certificados PKCS e SCEP permaneceram em dispositivos, mesmo quando remover uma política de um grupo, a eliminação de uma configuração ou implantação de conformidade ou um administrador atualizar um perfil SCEP ou PKCS existente. 

Esta atualização altera o comportamento. Existem alguns cenários onde os certificados PKCS e SCEP são removidos de dispositivos e alguns cenários em que estes certificados permanecem no dispositivo. 

#### <a name="access-to-key-profile-properties-using-the-company-portal-app"></a>Acesso às propriedades de perfil de chave a utilizar a aplicação portal da empresa
<!--772203-->  
Os utilizadores finais podem agora aceder propriedades da chave de conta e as ações, como a reposição de palavra-passe, a partir da aplicação Portal da empresa. 

#### <a name="pin-prompt-when-you-change-fingerprints-or-face-id-on-an-ios-device"></a>Pedido de PIN quando alterar as impressões digitais ou ID se deparam num dispositivo iOS  
<!--2637704-->  
É pedido aos utilizadores agora um PIN depois de efetuar alterações biométricas no dispositivo iOS. Isto inclui as alterações de impressões digitais registadas ou face ID. A temporização da linha de comandos depende da forma como a configuração do *verificar novamente os requisitos de acesso após (minutos)* tempo limite.  Quando nenhum PIN está definido, é pedido ao utilizador para configurar um.  

Esta funcionalidade só está disponível para iOS e requer a participação de aplicações que se integram o SDK da aplicação Intune para iOS, versão 8.1.1 ou posterior. Integração do SDK é necessária para que o comportamento pode ser imposto em aplicações visadas. Esta integração acontece de forma gradual e depende das equipas de aplicação específica. Algumas aplicações que participam incluem WXP, Outlook, Managed Browser e Yammer.

#### <a name="end-user-device-and-app-content-menu"></a>Menu de conteúdo dispositivos e aplicações utilizador final 
<!--2771453-->  
Os usuários finais agora pode utilizar o menu de contexto em aplicações e dispositivos para acionar ações comuns, como mudar o nome de um dispositivo ou a verificação de conformidade. 

#### <a name="windows-company-portal-keyboard-shortcuts"></a>Atalhos de teclado do Portal de empresa do Windows
<!--2771518-->  
Os usuários finais agora pode acionar ações de aplicações e de dispositivos no Portal de empresa do Windows com atalhos de teclado (Aceleradores).



## <a name="august-2018"></a>Agosto de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="new-user-experience-update-for-the-company-portal-website"></a>Nova atualização de experiência de utilizador para o site do Portal da empresa
<!--2000968--> Com base no seu feedback, adicionámos novas funcionalidades para o site do Portal da empresa. Surgirá uma melhoria significativa na funcionalidade existente e a usabilidade dos seus dispositivos Android, iOS e Windows. Áreas do site recebeu um design de nova, Moderno, capacidade de resposta. Estas áreas incluem detalhes do dispositivo, comentários e suporte e descrição geral do dispositivo. Também verá os seguintes melhoramentos:

- Fluxos de trabalho simplificados em todas as plataformas de dispositivo
- Fluxos de identificação e a inscrição de dispositivos melhorada
- Mensagens de erro mais útil
- Linguagem mais amigável, menos jargão do tech
- Capacidade de partilhar ligações diretas para aplicações
- Desempenho melhorado para grandes catálogos de aplicações
- Maior acessibilidade para todos os utilizadores



## <a name="july-2018"></a>Julho de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="updated-intune-app-sdk-for-android-is-now-available"></a>Atualizada do SDK da aplicação Intune para Android está agora disponível
<!--2744271--> Uma versão atualizada do SDK da aplicação Intune para Android está disponível para dar suporte à versão do Android 9 circular. Se for um programador de aplicações e utiliza o SDK do Intune para Android, instale a versão atualizada do SDK da aplicação do Intune. Esta atualização torna-se de que essa funcionalidade do Intune nas suas aplicações Android continuam a funcionar conforme esperado nos dispositivos Android 9 circular. Esta versão do SDK da aplicação Intune fornece um plug-in interno que executa as atualizações SDK. Não vai precisar reescrever nenhum código existente que está integrado. Para obter mais informações, consulte [SDK do Intune para Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android). 

Se estiver a utilizar o estilo de badging antigo para o Intune, mude para utilizar o ícone de pasta. Para obter mais informações sobre a identidade visual, consulte a [sistema de Badging de aplicação do Intune](https://github.com/msintuneappsdk/intune-app-partner-badge).


#### <a name="support-for-security-enhancement-in-intune-service"></a>Suporte para a melhoria de segurança no serviço Intune
<!--2520152--> Agora pode especificar que os dispositivos sem quaisquer políticas de conformidade atribuída não são conformes com a híbrida. Configure esta definição no Intune no portal do Azure. Recomendamos vivamente que ative esta funcionalidade proteger os recursos internos.

Esta funcionalidade está desativada por predefinição em inquilinos híbrida. Quando ativa esta funcionalidade, os dispositivos que não têm uma política de conformidade atribuída são considerados incompatíveis. Se também ativar o acesso condicional, estes dispositivos perdem o acesso aos recursos internos. Esses recursos podem ser Outlook ou o SharePoint, com base nas políticas de acesso condicional no seu ambiente. Se deixar esta definição de fora, estes dispositivos continuam a ter o mesmo nível de acesso, como fazem atualmente.

Para ajudar a determinar o impacto de ativar esta funcionalidade, fornecemos uma [script na galeria do TechNet](https://gallery.technet.microsoft.com/SQL-Query-for-Hybrid-MDM-5bcb8695). Quando executa esse script em sua base de dados do Configuration Manager, lista os dispositivos que não são visados pelas políticas de conformidade.

Para obter mais informações, veja os artigos seguintes:
- [Melhorias de segurança no serviço do Intune](https://aka.ms/compliance_policies) mensagem de blogue 
- [Políticas de conformidade no Configuration Manager](/sccm/mdm/deploy-use/device-compliance-policies)

#### <a name="updates-to-out-of-compliance-messages-in-company-portal-app"></a>Atualizações para mensagens de fora de conformidade na aplicação Portal da empresa 
<!--1832222--> Podemos está revisando as mensagens que os utilizadores veem quando um dispositivo está fora de conformidade. Mensagens de mantém seus significados originais, mas são atualizadas com a linguagem mais amigável e menos jargão técnica. Também estamos a atualizar ligações para documentação e remediação de passos para mantê-los atualizados.  

O texto seguinte é um exemplo dos melhoramentos no sistema de mensagens que verá:  

- Antes de: *Este dispositivo não contacte o serviço do Intune no período de tempo especificado exigido pelo administrador de TI. Para resolver este problema, abra a aplicação do portal da empresa no seu dispositivo e clique no botão verificar conformidade.*  

- Depois de: *O dispositivo não verificou com a sua organização em algum tempo. Para restabelecer uma ligação, abra a aplicação Portal da empresa no seu dispositivo e toque em verificar definições para o seu dispositivo.*  

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings"></a>Selecione as categorias de dispositivos com as definições de acesso profissional ou escolar 
<!--1058963--> Se ativou [mapeamento de grupo de dispositivos](https://docs.microsoft.com/intune/device-group-mapping), os utilizadores no Windows 10 agora são solicitados a selecionar uma categoria de dispositivo após a inscrição através do **Connect** botão na **definições**  >  **Contas** > **acesso profissional ou escolar**.  

#### <a name="new-browsing-experiences-in-the-company-portal-app-for-windows"></a>Nova navegação experiências na aplicação portal da empresa para Windows 
<!--2317227--> Agora quando procurando ou pesquisando para aplicações na aplicação Portal da empresa para Windows, alternar entre o existente **mosaicos** modo de exibição e adicionados recentemente **detalhes** vista. A nova exibição de lista detalhes como nome, publicador, data de publicação e o estado da instalação da aplicação. 

O **aplicações** da página **instalado** vista permite que veja detalhes sobre instalações de aplicações em curso e concluída. Para ver o aspeto a nova vista, consulte [quais são as novidades na IU](https://docs.microsoft.com/intune/whats-new-app-ui).

#### <a name="more-opportunities-to-sync-in-the-company-portal-app-for-windows"></a>Mais oportunidades de sincronizar na aplicação portal da empresa para Windows  
<!--2683177--> A aplicação Portal da empresa para Windows agora permite-lhe iniciar uma sincronização diretamente a partir da barra de tarefas do Windows e o menu Iniciar. Esse recurso é especialmente útil se a sua única tarefa é sincronizar os dispositivos e obter acesso aos recursos empresariais. Para acessar o novo recurso, faça duplo clique no ícone do Portal da empresa que tiver afixado à sua barra de tarefas ou o menu Iniciar. Nas opções do menu, selecione **sincronizar este dispositivo**. (Esse menu é também referido como uma lista de atalhos.) É aberto o Portal da empresa para o **definições** página e inicia a sincronização. Para o procedimento de atualização, consulte [sincronizar o seu dispositivo Windows manualmente](https://docs.microsoft.com/intune/intune-user-help/sync-your-device-manually-windows#sync-from-device-taskbar-or-start-menu).



## <a name="june-2018"></a>junho de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="access-to-macos-company-portal-pre-release-build"></a>Acesso a compilação de pré-lançamento do Portal da empresa do macOS 
<!--1734766--> Usando o Microsoft AutoUpdate, inscreva-se para receber compilações de desde o início ao aderir ao programa de Insider. Inscrever-se permite-lhe utilizar o Portal da empresa atualizado antes de ser disponibilizado aos seus utilizadores finais.

#### <a name="intune-app-protection-policies-and-microsoft-edge"></a>Políticas de proteção de aplicações do Intune e o Microsoft Edge 
<!--1818968,1818969--> O browser Microsoft Edge para dispositivos móveis (iOS e Android) agora suporta políticas de proteção de aplicações do Microsoft Intune. Os utilizadores de dispositivos iOS e Android que iniciam sessão com as contas do Azure Active Directory empresariais no aplicativo de borda são protegidos pelo Intune. Em dispositivos iOS, a política para **necessitam de browser gerido para o conteúdo da web** permite aos utilizadores abrir ligações no Edge, quando é gerido.



## <a name="may-2018"></a>Maio de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Pedir ajuda no Portal da empresa para Windows 10 
<!--1874137--> O Portal da empresa para Windows 10 agora envia os registos de aplicações diretamente à Microsoft quando o usuário inicia o fluxo de trabalho para obter ajuda com um problema. Este comportamento torna mais fácil de resolver os problemas que são gerados para a Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

#### <a name="android-for-work-and-lookout-onboarding-moved-to-intune-on-azure"></a>Android para a integração do Lookout e de trabalho é movido para o Intune no Azure
<!--2355022,2357366--> Com a atualização mais recente do Intune, pode ativar e gerir Android para integração de trabalho e a integração do Lookout mobile threat defense em inquilinos de gestão de dispositivos móveis híbrida no Intune no portal do Azure. Antes da atualização, estas definições apenas foram configuráveis no portal clássico do Intune (Silverlight).
 
Nota: Lookout é o fornecedor de defesa (MTD) de ameaça móveis suportado no híbrida. Se anteriormente tiver integrado com qualquer outro fornecedor MTD, ele continua a aparecer no Intune no portal do Azure. Se eliminar o conector para o mesmo, em seguida, não pode adicioná-lo novamente.
 
Estas alterações não afetam a funcionalidade existente. Continue a utilizar a consola do Configuration Manager para gestão de aplicações relacionadas, relatórios e políticas.
 
Para obter mais informações, veja os artigos seguintes:
- [Configurar a gestão de dispositivos híbrida do Android](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [Gerir o acesso a recursos da empresa com base em riscos de aplicações, redes e dispositivos](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)


#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Suporte para novas versões de cliente do Cisco AnyConnect para iOS
<!--1357393--> Pode ativar o suporte para Cisco AnyConnect para iOS versão 4.0.7 ou posterior. Se o fizer, os perfis de VPN do Cisco AnyConnect existentes são denominados **Cisco Legacy AnyConnect**e continuar a funcionar como antes. O **Cisco AnyConnect** opção é para perfis de VPN novo profissional com o Cisco AnyConnect na versão do iOS 4.0.7 ou posterior.

  > [!Tip]  
  > Cisco AnyConnect 4.0.07x e versões posteriores para iOS foi introduzido pela primeira vez na versão 1802 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir [atualizar 4163547](https://support.microsoft.com/help/4163547) para versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  

> [!Note]  
> Continuar a utilizar o **Cisco Legacy AnyConnect** opção para perfis VPN do macOS. 



## <a name="april-2018"></a>Abril de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>Intune se adapta às Fluent de Design de sistema na aplicação Portal da empresa para Windows 10 
<!--1195010--> A aplicação Portal da empresa do Intune para Windows 10 foi atualizada com o [vista de navegação do sistema Design Fluent](/windows/uwp/design/basics/navigation-basics). No lado da aplicação observe uma lista estática, vertical de todas as páginas de nível superior. Clicar em qualquer ligação para ver e alternar entre páginas rapidamente. Esta atualização é o primeiro dos vários que verá como parte do nosso esforço contínuo para criar uma experiência mais adaptável, empathetic e familiar no Intune. Para ver a versão atualizada, aceda a [quais são as novidades na IU da aplicação](/intune/whats-new-app-ui).

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>Mosaicos de dispositivos melhorada no Portal de empresa do Windows 10
<!--2213364--> Os mosaicos foram atualizados para serem mais acessíveis para os utilizadores de visão reduzida e funcionar melhor para ler as ferramentas de ecrã.


#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>O Portal da empresa para macOS em máquinas virtuais de teste
<!--2216679--> Publicámos orientação para ajudar os administradores de TI testar a aplicação Portal da empresa para macOS em máquinas virtuais no Parallels Desktop e a VMware Fusion. Para obter mais informações, consulte [inscrever máquinas virtuais macOS para teste](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing).


#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>Enviar relatórios de diagnóstico na aplicação Portal da empresa para macOS
<!--2216677--> A aplicação Portal da empresa para dispositivos macOS foi atualizada para melhorar a como os utilizadores para relatar erros relacionados com o Intune. A partir da aplicação Portal da empresa, seus funcionários podem:

- Carrega relatórios de diagnóstico diretamente para a equipe de desenvolvedores da Microsoft.
- ID do incidente para a sua empresa de e-mail IT equipa de suporte.


#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Experiência de ajuda atualizada na aplicação Portal da empresa para Android 
<!--1631531--> Atualizámos a experiência de ajuda na aplicação Portal da empresa para Android para estarmos alinhados com as melhores práticas para a plataforma Android. Agora, quando os utilizadores detetarem um problema na aplicação, pode tocar **Menu** > **ajudar** e:
- Carregar registos de diagnóstico para a Microsoft.
- Envie um e-mail que descreve o ID de problema e incidente para um técnico de suporte da empresa.


#### <a name="update-where-to-configure-your-app-protection-policies"></a>Atualização do local configurar as políticas de proteção de aplicações 
<!--2144597--> No portal do Azure no serviço do Microsoft Intune, vamos redirecioná-lo de temporariamente a **proteção de aplicações do Intune** área para o **aplicação móvel** secção. Todas as suas políticas de proteção de aplicações já estiverem da **aplicação móvel** secção no Intune, em configuração de aplicações. Em vez de passar para a proteção de aplicações do Intune, acederá simplesmente ao Intune. Em Abril de 2018, vamos parar o redirecionamento e remover completamente **proteção de aplicações do Intune**. Após esse período, há apenas uma localização para políticas de proteção de aplicações no Intune. 

**Como essa alteração me afeta?** Esta alteração irá afetar os clientes do Intune autónomo e clientes híbridos (Intune com o Configuration Manager). Esta integração irá ajudar a simplificar a administração de gestão na cloud.

**O que preciso fazer para se preparar para esta alteração?** Marca **Intune** como um favorito em vez de **Intune App Protection**. Familiarize-se com o fluxo de trabalho da política de proteção aplicação no **aplicação móvel** área no Intune. Iremos redirecionar os utilizadores durante um curto período de tempo e, em seguida, remover **proteção de aplicações**. Lembre-se que todas as políticas de proteção de aplicações já se encontra no Intune e pode modificar as suas políticas de acesso condicional. Para obter mais informações sobre como modificar as políticas de acesso condicional, consulte [acesso condicional no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Para obter mais informações, consulte [quais são as políticas de proteção de aplicações?](https://docs.microsoft.com/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Atualização da experiência de utilizador para a aplicação Portal da empresa para iOS 
<!--1412866--> Lançámos uma atualização da experiência de utilizador principais para a aplicação Portal da empresa para iOS. A atualização apresenta uma reestruturação visual completa que inclui um aspeto e funcionalidade reestruturação. Nós já mantivemos a funcionalidade da aplicação, mas aumentámos a usabilidade e acessibilidade.  

Também verá:
- Suporte para iPhone X.
- Mais rápido lançamento de aplicação e respostas, para economizar tempo de utilizadores de carregamento.
- Barras de progresso adicionais para fornecer aos utilizadores com as informações de estado mais atualizadas.
- Melhorias para as forma como os utilizadores carregam os registos, portanto, se algo der errado, é mais fácil de relatório.  

Para ver a versão atualizada, aceda a [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui).



## <a name="march-2018"></a>Março de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>Opção de comentários enviar Windows empresa Portal podem não funcionar
<!--2070166--> A aplicação Portal da empresa de Windows tem uma opção de "Enviar Feedback" permitir que os utilizadores para enviar comentários sobre a aplicação à Microsoft. De 30 de Abril de 2018, esta opção continua a ser suportada apenas na aplicação Portal da empresa do Windows 10 em execução no Windows 10 versão 1607 e posterior.   

**Como essa alteração me afeta?**

Se não tiver a aplicação de Portal de empresa do Windows instalada para os utilizadores finais, em seguida, ignore esta mensagem.

Se qualquer um dos seus utilizadores finais tiver a aplicação Portal da empresa, em seguida, a partir de 30 de Abril no botão "Enviar Feedback" já não funciona para a aplicação nos seguintes cenários:  

 - Aplicação do Portal da empresa do Windows 10 no Windows 10 versão 1507 e a versão 1511  

 - Aplicação de Portal da empresa do Windows Phone 8.1  

Para os dispositivos afetados, a opção "Enviar Feedback" falha e não tiver êxito, mesmo ao repetir a operação. Para enviar comentários à Microsoft sobre experiências nestas plataformas, existem canais listados abaixo de feedback alternativos.

**O que preciso fazer para se preparar para esta alteração?**

Informar os utilizadores finais dessa alteração e Atualize as orientações para se necessário. 

Informe os utilizadores finais com o Portal da empresa no Windows Phone 8.1, Windows 10 versão 1507 e Windows 10 versão 1511 que têm dois canais de feedback alternativos disponíveis. Estes requisitos podem:  

- Utilize os comentários app Hub no Windows 10  
- Envie um e-mail para WinCPfeedback@microsoft.com  

Peça aos utilizadores no Windows 10 versão 1607 ou posterior para atualizar para a versão mais recente do Windows Portal da empresa disponível da Microsoft Store.



#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>Web sites do Azure Active Directory podem exigir a aplicação de Browser gerido do Intune e o suporte de início de sessão único do Managed Browser (pré-visualização pública)
<!-- 710595 --> Utilizar o Azure Active Directory (Azure AD), pode restringir o acesso a sites da web em dispositivos móveis para a aplicação de Browser gerido do Intune. No browser gerido, dados dos sites permanecerão protegidos e separados dos dados pessoais do utilizador final. Além disso, o Managed Browser suporta as funcionalidades de Início de Sessão Único para sites protegidos pelo Azure AD. Iniciar sessão no Managed Browser ou utilizá-lo num dispositivo com outra aplicação gerida pelo Intune permite que o Managed Browser aceda a sites empresariais protegidos pelo Azure AD sem que o utilizador tenha de introduzir as suas credenciais. Esta funcionalidade aplica-se a sites como o Outlook Web Access (OWA) e o SharePoint Online, bem como a outros sites empresariais como recursos de intranet acedidos através do Proxy de Aplicações do Azure.



## <a name="february-2018"></a>Fevereiro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **suporte do Portal da empresa do macOS para inscrições que utilizam o Gestor de inscrição de dispositivos**  
    Os utilizadores agora podem utilizar o Gestor de Inscrições de Dispositivos ao inscrever-se no Portal da Empresa do macOS.
    <!-- 1352411 -->


## <a name="january-2018"></a>Janeiro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Aprovar a aplicação do Portal da empresa para Android for Work**  
  Se a sua organização utiliza o Android for Work, aprove manualmente a aplicação Portal da empresa para Android. Em seguida, continua a receber atualizações automáticas da Google Play store gerida.
  <!--1797090 -->  

- **Políticas de acesso condicional para o Intune só estão disponíveis no portal do Azure**   
  A partir desta versão, tem de configurar e gerir as políticas de Acesso Condicional no [portal do Azure](https://portal.azure.com) a partir de **Azure Active Directory** > **Acesso Condicional**. Para sua comodidade, pode também aceder a estas definições do Intune no portal do Azure em **Intune** > **acesso condicional**.
  <!-- 1737088 1634311 --> 

- **Atualizações em e-mails de conformidade**    
  Quando é enviado um e-mail para comunicar um dispositivo não conforme, são incluídos detalhes sobre o mesmo. 
  <!--1637547 -->

- **Nova funcionalidade para a ação "Resolver" para dispositivos Android**    
  A aplicação Portal da Empresa para Android irá expandir a ação "Resolver" de **Atualizar definições do dispositivo** para também resolver [problemas de encriptação de dispositivos](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Bloqueio remoto disponível na aplicação Portal da empresa para Windows 10**    
  Agora os utilizadores finais podem bloquear remotamente os seus dispositivos a partir da aplicação Portal da Empresa para Windows 10. Esta ação não for apresentada no dispositivo local que estejam a utilizar.
  <!--676506-->

- **Mais fácil resolução de problemas de conformidade para a aplicação do Portal da empresa para Windows 10**   
  Os utilizadores finais com dispositivos Windows poderão tocar no motivo de não conformidade na aplicação Portal da empresa. Sempre que possível, esta ação leva-los diretamente para a localização correta na aplicação de definições para corrigir o problema.
  <!--676546-->    



## <a name="december-2017"></a>Dezembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Implementações de aplicações disponíveis agora suportadas para o Android Enterprise**    
  Agora, pode implementar aplicações Android Enterprise (anteriormente Android for Work), como **disponível**, para além **necessário**. Para obter detalhes, consulte [Android criar aplicações com o System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).



## <a name="november-2017"></a>Novembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Protocolo de texto autorizado a partir de aplicações geridas**  
  Aplicações geridas pelo SDK da aplicação Intune podem enviar mensagens SMS.
  <!-- 1414050  -->   

- **Aplicação do Portal da empresa para macOS está disponível**   
  O Portal da empresa do Intune no macOS tem uma experiência atualizada. Ela é otimizada para apresentar corretamente todas as notificações de informações e conformidade que os utilizadores precisam para todos os dispositivos que tenham inscrito. E, depois de ter sido implementado o Portal da empresa do Intune num dispositivo, o Microsoft AutoUpdate para macOS fornece atualizações ao mesmo. Baixe o novo Portal de empresa do Intune para macOS ao iniciar sessão no site do Portal da empresa do Intune de um dispositivo macOS.
  <!--1541700-->   

- **O Microsoft Planner faz agora parte da lista de gestão (MAM) de aplicação móvel de aplicações aprovadas**    
  A aplicação Microsoft Planner para iOS e Android faz agora parte das aplicações aprovadas para a gestão de aplicações móveis (MAM). Configure a aplicação de proteção de aplicações do Intune no portal do Azure para todos os inquilinos. Para obter detalhes, consulte [lista MAM de aplicações aprovadas](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Acesso a registos de aplicações geridas para iOS**    
  Agora, os utilizadores finais com o Managed Browser instalado podem ver o estado da gestão de todas as aplicações publicadas da Microsoft e enviar registos para resolver os problemas das respetivas aplicações iOS geridas.
  <!-- 1469920 -->    

  Para saber como ativar o modo de resolução de problemas num Managed Browser num dispositivo iOS, veja [How to access to managed app logs using the Managed Browser on iOS (Como aceder a registos de aplicações geridas com o Managed Browser no iOS)](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

- **Melhorias ao dispositivo configurar fluxo de trabalho no Portal da empresa para iOS na versão 2.9.0**    
  Melhorámos o fluxo de trabalho do programa de configuração do dispositivo na aplicação Portal da empresa para iOS. O tipo de linguagem é mais simples. Além disso, combinámos os ecrãs sempre que possível. Também tornámos o idioma mais específicas para a sua empresa com o nome da sua empresa em todo o texto de configuração. Pode ver este fluxo de trabalho atualizado sobre o [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017) página.

- **Pedidos de comentários para a aplicação Portal da empresa para Android**    
  A aplicação Portal da empresa para Android solicita agora comentários do utilizador final. Este feedback é enviado diretamente para a Microsoft e proporciona aos utilizadores finais a oportunidade de reverem a aplicação na Google Play Store pública. Comentários não não necessário e podem ser dispensados facilmente para que os utilizadores podem continuar a utilizar a aplicação. 
  <!--1165249-->    

- **Informe os utilizadores finais informações do dispositivo que podem ser vistas para dispositivos Windows 10**    
  Adicionámos o **Tipo de Propriedade** ao ecrã Detalhes do Dispositivo na aplicação Portal da Empresa para Windows 10. Esta informação permite aos utilizadores obter mais informações sobre privacidade diretamente a partir da documentação do utilizador final do Intune. Eles também podem localizar estas informações no **sobre** ecrã.
  <!--1337920-->    

- **Nova ação "Resolver" disponível para dispositivos Android**    
  A aplicação Portal da Empresa para Android está a introduzir a ação "Resolver" na página _Atualizar definições do dispositivo_. A seleção desta opção leva o usuário final diretamente para a definição que está a causar o respetivo dispositivo não esteja em conformidade. A aplicação Portal da empresa para Android suporta atualmente esta ação para o [código de acesso do dispositivo](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [encriptação do dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [depuração de USB](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android), e [desconhecido Origens](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android) definições. 
  <!--1583480-->    


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

- **Ações de não conformidade**    
  Agora, pode configurar uma sequência cronológica de ações que são aplicadas aos dispositivos que estão fora de conformidade. Por exemplo, pode notificar os utilizadores dos dispositivos não conformes por email ou marcar os dispositivos não conformes. Para obter detalhes, consulte [configurar as ações de não conformidade](/sccm/mdm/deploy-use/actions-for-noncompliance).
  <!--1321366 -->

- **Novas definições de política de gestão de aplicações móveis**     
  Foram adicionadas as seguintes definições para as definições de política de gestão de aplicações móveis:
  - **Desativar sincronização de contactos**: Impede que a aplicação de guardar os dados na aplicação nativa contactos no dispositivo.
  - **Desativar a impressão**: Impede que a aplicação de trabalho de impressão dados escolares ou profissionais.
  <!-- 1324760 -->    

  Ver [proteger aplicações através de políticas de proteção de aplicações no Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para experimentar as novas definições de política de proteção de aplicações.

- **Suporte para dispositivos Windows 10 ARM64**     
  Cenários de gestão (MDM) de dispositivos móveis híbrida são suportados em dispositivos de ARM64 com o Windows 10 quando estes dispositivos estão disponíveis. Para obter detalhes, consulte [suporte para dispositivos Windows 10 ARM64](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Experiência melhorada do perfil VPN na consola do Configuration Manager**     
  Com esta versão, atualizamos as páginas de assistente e propriedades de perfil VPN para apresentar as definições adequadas da plataforma selecionada. Esta funcionalidade estava anteriormente disponível no 1709 de pré-visualização técnica do Configuration Manager. Está agora disponível em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1710. Para obter mais informações, consulte [experiência de perfil VPN melhorado na consola do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->


### <a name="new-in-configuration-manger-technical-preview-1711"></a>No Configuration Manager Technical Preview 1711

- **Novas opções de política de conformidade para Windows 10**   
  Agora pode configurar novas opções para políticas de conformidade para dispositivos Windows 10. As novas definições incluem as políticas de Firewall, o controle de conta de utilizador, o antivírus do Windows Defender e controle de versão de compilação de SO. Para obter detalhes, consulte [novas opções de política de conformidade para Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## <a name="october-2017"></a>Outubro de 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Novo no Configuration Manager Technical Preview 1709

- **Experiência melhorada do perfil VPN na consola do Configuration Manager**      
  Definições do perfil VPN agora são filtradas de acordo com plataforma. Quando cria novos perfis VPN, cada plataforma suportada contém apenas as definições adequadas para a plataforma. Perfis VPN existentes não são afetados. Pode ler mais sobre esta alteração [aqui](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1313282 -->


### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  

- **Ajudar a utilizadores a resolver problemas com a aplicação Portal da empresa para Android**     
  A aplicação Portal da empresa para Android adicionou instruções aos utilizadores finais para ajudá-los a compreender e possivelmente resolver autonomamente novos casos de utilização.
    - Se os utilizadores finais tiverem atingido o número máximo de dispositivos que eles têm permissão para adicionar, são encaminhados para o [portal do Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile) para remover um dispositivo.
    - Os utilizadores finais recebem uma lista de passos a seguir para os ajudar a [corrigir erros de ativação em dispositivos Samsung Knox](https://go.microsoft.com/fwlink/?linkid=859718) ou a [desativar o modo de poupança de energia](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Se nenhuma dessas soluções resolver o problema, disponibilizamos uma explicação de como [enviar registos para a Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Indicador de progresso de configuração do dispositivo no Portal da empresa para Android**    
  A aplicação Portal da Empresa para Android mostra um indicador de progresso da configuração do dispositivo quando um utilizador está a inscrever o dispositivo. O indicador mostra novos estados, a começar por “A configurar o dispositivo…”, seguido de “A registar o dispositivo…”, “A concluir o registo do dispositivo...” e “A concluir a configuração do dispositivo...”.  
  <!--1565657-->    

- **Suporte de autenticação com base em certificado no Portal da empresa para iOS**    
  Adicionámos o suporte para a autenticação baseada em certificados (CBA) na aplicação Portal da Empresa para iOS. Os utilizadores com cba devem introduzir o respetivo nome de utilizador, em seguida, toquem na ligação "Iniciar sessão com um certificado de". A CBA já é suportada na aplicação Portal da Empresa para Android e Windows. Pode saber mais sobre o [inicie sessão na aplicação Portal da empresa](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal) página.
  <!--1029830-->   

- **Melhorias ao fluxo de trabalho de configuração de dispositivos no Portal da empresa**     
  Melhorámos o fluxo de trabalho da configuração de dispositivos na aplicação Portal da Empresa para Android. O tipo de linguagem é mais simples e específico para a sua empresa. Além disso, combinámos os ecrãs sempre que possível. Pode ver esses aprimoramentos no [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017) página.
  <!--1490692-->     

- **O pedido de acesso aos contactos em dispositivos Android orientação melhorada**     
  A aplicação Portal da Empresa para Android exige frequentemente que o utilizador final aceite as permissões de Contactos. Se um utilizador final recusar este acesso, verão uma notificação na aplicação que o alerta para o conceder para acesso condicional. 
  <!--1484985-->     

- **Remediação de arranque seguro para Android**     
  Os utilizadores finais com dispositivos Android poderão tocar no motivo de não conformidade na aplicação Portal da empresa. Sempre que possível, esta ação leva-los diretamente para a localização correta na aplicação de definições para corrigir o problema. 
  <!--1490712-->    

- **Notificações push adicionais para utilizadores finais na aplicação Portal da empresa para Android Oreo**    
  Os utilizadores finais verão notificações adicionais a indicar quando a aplicação Portal da empresa para Android Oreo está a efetuar tarefas em segundo plano, como a obtenção de políticas do serviço Intune. As notificações de aumentam a transparência para os utilizadores finais sobre o quando o Portal da empresa está a efetuar tarefas administrativas nos respetivos dispositivos. Esta melhoria é parte do geral [Otimização da interface de Usuário do Portal da empresa](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para a aplicação Portal da empresa para Android Oreo. 
  <!--1475932 -->     

- **Novo comportamentos para a aplicação Portal da empresa para Android com perfis de trabalho**     
  Quando inscreve um dispositivo Android for Work num perfil de trabalho, é a aplicação Portal da Empresa no perfil de trabalho que executa as tarefas de gestão no dispositivo. 

  A menos que estiver a utilizar uma aplicação com MAM ativada no perfil pessoal, a aplicação Portal da empresa para Android já não terá qualquer utilidade. Para melhorar a experiência de perfil de trabalho, o Intune oculta automaticamente a aplicação Portal da empresa pessoa depois de uma inscrição de perfil de trabalho com êxito.

  A aplicação Portal da Empresa para Android pode ser ativada em qualquer altura no perfil pessoal. para tal, navegue para o [Portal da Empresa na Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) e toque em **Ativar**.
  <!--1485783-->    

- **Portal para o Windows 8.1 e Windows Phone 8.1 mudar para o modo de suporte da empresa**    
  Um aviso foi adicionado ao anunciar que as aplicações do Portal da empresa para Windows 8.1 e Windows Phone 8.1 estão a mover para o modo de suporte. Para obter detalhes, consulte [avisos](#notices).  
  <!--1428681-->    

- **Bloquear a inscrição de dispositivos Samsung Knox não suportados**   
  A aplicação Portal da Empresa apenas tenta inscrever dispositivos Samsung Knox suportados. Para evitar erros de ativação de KNOX que impedem a inscrição MDM, inscrição de dispositivos é tentada apenas se o dispositivo aparece na [lista de dispositivos publicados pela Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Dispositivos Samsung poderão ter números de modelo que suportem o KNOX enquanto outros não. Verifique a compatibilidade com o Knox junto do revendedor do seu dispositivo antes da compra e implementação. Pode encontrar a lista completa de dispositivos verificados na [definições de política do Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
  <!-- 1490695 -->     

- **Fim do suporte para Android 4.3 e inferior**     
  Um aviso foi adicionada para o fim do suporte para Android 4.3 e inferior. Para obter detalhes, consulte [avisos](#notices).
  <!--1171126, 1326920 -->     

- **Informe os utilizadores finais informações do dispositivo que podem ser vistas nos dispositivos inscritos**     
  Estamos adicionando **tipo de propriedade** na tela de detalhes do dispositivo em todas as aplicações do Portal da empresa. Esta informação permite aos utilizadores obter mais informações sobre privacidade diretamente a partir da [que informações pode a sua empresa ver?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) artigo. Esta melhoria for implementada em todas as aplicações do Portal da empresa no futuro próximo. Anunciámos esta funcionalidade para iOS no [Setembro](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
  <!--1165314-->     



## <a name="september-2017"></a>Setembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Ação de atualizar adicionada à aplicação Portal da empresa para Windows 10**    
    A aplicação Portal da Empresa para Windows 10 permite aos utilizadores atualizar os dados na aplicação, ao pedir para atualizar ou, em computadores, ao premir F5.
    <!-- 1132468 -->     

- **Informe os utilizadores finais informações do dispositivo que podem ser vistas para iOS**   
    Adicionámos **tipo de propriedade** na tela de detalhes do dispositivo na aplicação Portal da empresa para iOS. Esta informação permite aos utilizadores obter mais informações sobre privacidade diretamente a partir da documentação do utilizador final do Intune. Eles também podem localizar estas informações no ecrã Acerca. 
    <!--739894-->    

- **Mais fácil de compreender frases para a aplicação Portal da empresa para Android**   
    O texto do processo de inscrição da aplicação Portal da Empresa para Android foi simplificado para facilitar a inscrição dos utilizadores finais. Se tiver documentação de inscrição personalizada, atualizá-la para refletir os novos ecrãs. Poderá encontrar imagens de exemplo na nossa página de [Atualização da IU para aplicações de utilizadores finais do Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017).
    <!---1396349-->    

- **Política de permissão da aplicação Portal da empresa do Windows 10 adicionada à proteção de informações do Windows**    
    A aplicação Portal da Empresa do Windows 10 foi atualizada para suportar o Windows Information Protection (WIP). A aplicação pode ser adicionada à política de permissão do WIP. Com esta alteração, a aplicação já não tem de ser adicionada à lista **Excluídas**. 

    Apenas um item de configuração de WIP único pode ser fornecido para um dispositivo. Se dois itens de configuração do WIP são direcionadas para o mesmo dispositivo, aplica-se nenhuma política WIP.
    <!-- 677129 -->    

- **Fim do aviso de suporte adicionado para o iOS 8.0**    
    Um aviso foi adicionado para o fim do suporte para iOS 8.0. Para obter detalhes, consulte [avisos](#notices).



## <a name="august-2017"></a>Agosto de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Experiência de início de sessão iniciada novo para os utilizadores do Portal da empresa para Android e políticas de proteção de aplicações**    
  Os utilizadores finais podem agora procurar aplicações, gerir dispositivos e ver informações de contacto de TI com a aplicação Portal da Empresa para Android sem inscrever os respetivos dispositivos Android. Além disso, se um utilizador final já utilizar uma aplicação protegida por políticas de proteção de aplicações do Intune e iniciar o Portal da empresa Android, o utilizador final deixará de receber um pedido para inscrever o dispositivo.
  <!-- 621669 -->



## <a name="notices"></a>Avisos

### <a name="plan-for-change-intune-supports-macos-1012-and-higher-in-december"></a>Planear a alteração: O Intune suporta o macOS 10.12 e superior em Dezembro 
<!--2970975--> 

Apple lançada macOS 10.14, portanto, a partir de Dezembro de 2018, o Intune irá suportar macOS 10.12 e superior. 

#### <a name="how-does-this-affect-me"></a>Como é que isto me afeta?

A partir de Dezembro, os utilizadores em dispositivos com macOS 10.11 e anterior não é possível utilizar o Portal da empresa para inscrição no Intune. Para continuar a receber suporte e os novos recursos, eles precisarão de atualizar o dispositivo para macOS 10.12 ou superior e atualizar a aplicação Portal da empresa para a versão mais recente. 

O MacOS 10.12 e superiores de versões atualmente é suportado em: 
- MacBook (tarde 2009 ou mais recente)  
- iMac (tarde 2009 ou mais recente)
- MacBook ar (tarde 2010 ou mais recente)  
- MacBook Pro (tarde 2010 ou mais recente)  
- Mac Mini (tarde 2010 ou mais recente)  
- Mac Pro (tarde 2010 ou mais recente)  

Depois de Dezembro, os utilizadores finais com dispositivos que não aqueles listados acima não é possível aceder a versão mais recente da aplicação Portal da empresa para macOS. Pode continuar a gerir os dispositivos inscritos existentes que executem versões anteriores não suportados macOS 10.12.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso de fazer para me preparar para esta alteração?

- Solicite que os utilizadores atualizarem os seus dispositivos para uma versão de SO suportada antes de Dezembro de 2018.  
- Verifique os relatórios de Intune no portal do Azure, para ver que utilizadores ou dispositivos que podem ser afetados. Aceda a **dispositivos** > **todos os dispositivos**e filtre por **SO**. Pode adicionar colunas adicionais para ajudar a identificar quem na sua organização tiver dispositivos com macOS 10.11.  
- Se estiver a utilizar gestão de dispositivos móveis híbridos (MDM), na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho e selecione o **dispositivos** nó. Com o botão direito as colunas para adicionar o **sistema operativo** e **versão de cliente** colunas. Em seguida, ordene pela versão do SO. Tenha em atenção que a MDM híbrida foi agora preterida e deve avançar para o Intune no Azure logo que possível. 
 
#### <a name="additional-information"></a>Informações Adicionais
Para obter mais informações, consulte [inscrever o seu dispositivo macOS no Intune com a aplicação Portal da empresa](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-macos-cp).


### <a name="plan-for-change-new-intune-support-experience-for-premier-customers"></a>Planear a alteração: Experimente o novo suporte do Intune para Premier clientes 
<!--2828727-->

atualização de 12/4/2018: Estamos tentando tornar esse processo melhor para. Não possível desativar a criação do pedido de suporte no MPO 3 de Dezembro. Vamos informá-sei através do Centro de mensagens e atualizar esta publicação em breve para partilhar as linhas do tempo para que esta alteração.

Como um cliente Premier da Microsoft, pode utilizar o [portal do Microsoft Premier Online (MPO)](https://premier.microsoft.com) e [Intune no Azure](https://portal.azure.com) para criar pedidos de suporte do Intune. A partir de 3 de Dezembro de 2018, para continuar a melhorar o Premier experiência de suporte, será capaz de criar pedidos de suporte apenas no Intune no Azure.

#### <a name="how-does-this-affect-me"></a>Como é que isto me afeta?
Depois de 3 de Dezembro, não é possível criar pedidos de suporte no MPO. Se tentar, verá uma linha de comandos que não é possível dispensar a redirecioná-lo para o Intune no Azure. Quando cria um pedido de suporte no portal do Azure, é encaminhado para a Support da Microsoft dedicado do Intune. Eles diagnosticar e resolver o problema em tempo hábil. Se criar um pedido de suporte no portal do MPO, não é possível vê-lo no portal do Azure. Comece a criar apenas pedidos de suporte no Intune no Azure.  

Se utilizar a gestão de dispositivos móveis híbridos (MDM híbrida) ou cogestão, continue a utilizar o MPO para criar pedidos de suporte para o Configuration Manager, mas utilizar o portal do Azure para criar pedidos de suporte para o Intune. Como lembrete, MDM híbrida foi preterida e deve planear mover para o Intune no Azure logo que possível. Para obter mais informações, consulte [mover da gestão de dispositivos móveis híbrida para o Intune no Azure](https://aka.ms/hybrid_notification).

Tenha em atenção que apenas os utilizadores com funções de Administrador Global, administrador de serviço do Intune e o administrador de suporte do serviço podem criar pedidos de suporte no portal do Azure.

#### <a name="what-can-i-do-to-prepare-for-this-change"></a>O que posso fazer para se preparar para esta alteração?
- Pare de utilizar o MPO para pedidos de suporte relacionados com o Intune. Utilize o Intune no Azure para criar e gerir todos os pedidos de suporte do Intune.  
- Notificar a sua documentação de suporte técnico e de atualização, se necessário.  
- Se tiver utilizadores sem Administrador Global ou funções de administrador de serviço do Intune atualmente a criar pedidos de suporte no MPO, atribuí-las a função de administrador de suporte de serviços no Azure Active Directory. Os usuários exigem uma destas funções para criar pedidos de suporte no portal do Azure.  

#### <a name="additional-information"></a>Informações Adicionais
Para obter mais informações, consulte a [postagem do blog de equipe do Microsoft Intune suporte](https://aka.ms/IntuneSupport_MPO_to_Azure).


### <a name="plan-for-change-use-intune-on-azure-now-for-your-mdm-management"></a>Planear a alteração: Utilizar o Intune no Azure agora para a gestão de MDM 
<!--1227338--> Ao longo de um ano atrás, anunciámos [pré-visualização pública do Intune no Azure](https://cloudblogs.microsoft.com/enterprisemobility/2016/12/07/public-preview-of-intune-on-azure/) e, seis meses, lançámos a [disponibilidade geral da nova experiência de administrador](https://cloudblogs.microsoft.com/enterprisemobility/2017/06/08/the-new-intune-and-conditional-access-admin-consoles-are-ga/) para o Intune. A partir de 31 de Agosto de 2018, vamos desativar a gestão de dispositivos móveis (MDM) na consola Silverlight clássica para os clientes que utilizam o Intune autónomo. Em alternativa, utilize [Intune no Azure](https://aka.ms/Intune_on_Azure) para suas necessidades de MDM. Se ainda estiver a utilizar a consola clássica para MDM, pare e familiarize-se com o Intune no Azure. Não Esperamos nenhum impacto de utilizador final com esta alteração. Gestão clássica do PC com o Intune permanece no Silverlight. Para obter mais informações, consulte a [mensagem de blogue da equipa de suporte de Intune](https://aka.ms/Intune_on_Azure_mdm).


### <a name="plan-for-change-upcoming-macos-and-intune-password-enforcement-change"></a>Planear a alteração: MacOS futuros e alterações de imposição de palavra-passe do Intune
<!--1873216--> Na versão do serviço de Setembro, o Intune planos para integrar da Apple recentemente lançou definição de "Palavra-passe alterações na autenticação seguinte" para dispositivos MacOS 10.13 de versões e superior. Antes desta definição foi introduzida, fornecedores MDM não tinham nenhuma forma de verificar que o código de acesso num dispositivo foi alterado para garantir a conformidade. Configuração e de conformidade as políticas do Intune apenas validadas que da próxima vez que uma palavra-passe foi alterada no dispositivo, ele pode ser marcado como compatível. Os utilizadores do macOS irão receber um pedido para atualizar a palavra-passe quando podemos integrar esse novo recurso de Apple, mesmo que a palavra-passe já está em conformidade.

#### <a name="how-does-this-change-affect-me"></a>Como essa alteração me afeta?
Esta alteração afeta apenas o Intune autónomo ou híbrida MDM os clientes com uma política de dispositivos macOS. Apple introduziu a alterar palavra-passe na definição de autenticação de novo. Agora o Intune pode forçar os usuários a atualizar a palavra-passe para um que esteja em conformidade quando os emitir uma política de palavra-passe. Se bloquear recursos da empresa até que o dispositivo é marcado como em conformidade, sabe, em seguida, que os utilizadores finais podem ser impedidos de aceder a recursos da empresa como e-mail ou sites do SharePoint, até que a reposição de palavra-passe. No futuro, todas as atualizações das políticas de palavra-passe de configuração e de conformidade irão forçar utilizadores direcionados para atualizar as respetivas palavras-passe.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso de fazer para me preparar para esta alteração?
Pode querer permitir que o suporte técnico de saber. Se não pretende aplicar esta política de dispositivo macOS, anular a atribuição ou eliminar a política de macOS existente. A nossa pesquisa de cliente antes da implementação dessa alteração indicou a maioria dos clientes não serão afetados por esta alteração. Normalmente, os utilizadores finais atualizar a palavra-passe depois de receber um pedido para inscrever-se com uma palavra-passe ou repor a palavra-passe para permanecerem compatíveis.  


### <a name="plan-for-change-intune-moving-to-support-ios-10-and-later-in-september-2018"></a>Planear a alteração: Intune mover para suportar o iOS 10 e posterior em Setembro de 2018 
<!--2454656-->

Em Setembro de 2018, é esperada que Apple iOS 12 de versão. Logo depois do lançamento, vamos passar Intune inscrição, o Portal da empresa e o browser gerido para suportar o iOS 10 e posterior.

#### <a name="how-does-this-change-affect-me"></a>Como essa alteração me afeta?

Aplicações móveis do Office 365 são suportadas no iOS 10 e posterior, pelo que poderá já tiver atualizado o sistema operacional ou dispositivos. Se assim for, essa mudança não afetarão.

No entanto, se tiver todos os dispositivos listados abaixo, ou pretenda inscrever todos os dispositivos listados abaixo, eles somente oferecem suporte iOS 9 e versões anteriores. Para continuar a aceder ao Portal da empresa do Intune, tem de atualizar estes dispositivos até Setembro para dispositivos que suportam o iOS 10 ou posterior: 

- iPhone 4S
- iPod Touch 
- iPad 2
- iPad (terceira geração)
- iPad Mini (primeira geração)

A partir de Julho, os dispositivos inscritos na MDM com o iOS 9 e o Portal da empresa irão receber um pedido para atualizar o respetivo SO ou o dispositivo. Se utilizar políticas de proteção de aplicações, também pode definir o definição de acesso "Exigir sistema operativo iOS mínimo (aviso apenas)".  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso de fazer para me preparar para esta alteração?

Verificar a existência de dispositivos ou utilizadores que são afetados na sua organização. No Intune no portal do Azure, aceda a **dispositivos** > **todos os dispositivos**e filtre por **SO**.  Clique em **colunas** para detalhes de superfície, como a versão do SO. Solicite que os utilizadores atualizarem os seus dispositivos para uma versão de SO suportada antes de Setembro.


### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portal para o Windows 8.1 e Windows Phone 8.1 mudar para o modo de suporte da empresa 
<!--1428681-->
*6 de Outubro de 2017*   
 
A partir de Outubro de 2017, mova as aplicações Portal da empresa para Windows 8.1 e Windows Phone 8.1 para modo de suporte. Neste modo, significa que as aplicações e os cenários existentes, tais como inscrição e conformidade, continuarão a ter suporte nestas plataformas. Estas aplicações continuam a estar disponível para download por meio de canais de lançamento existentes, como a Microsoft Store. 

Uma vez no modo de suporte, estas aplicações só receção atualizações críticas de segurança. Não existem atualizações ou funcionalidades adicionais serão lançadas para estas aplicações. Para obter novas funcionalidades, recomendamos que atualize os dispositivos para Windows 10 ou Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fim do suporte para iOS 8.0 
<!---1164477---> Aplicações geridas e a aplicação Portal da empresa para iOS requerem o iOS 9.0 e superior para aceder a recursos da empresa. Dispositivos que não forem atualizados antes de Setembro já não são capazes de acessar o Portal da empresa ou a essas aplicações. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Lembrete de suporte de plataforma: Suporte de base do Windows Phone 8.1 terminou a 11 de Julho de 2017
<!-- 1327781 -->
*11 de Julho de 2017*

A plataforma Windows Phone 8.1 atingiu o fim do suporte base. Suporte de PCs com Windows 8.1 não é afetado.

Não há nenhum impacto imediato para todos os dispositivos Windows Phone 8.1 que é gerido pelo serviço do Intune, incluindo os dispositivos inscritos na MDM híbrida Os dispositivos inscritos continuam a funcionar. Todas as políticas, configurações e aplicações continuam a funcionar conforme esperado. Tenha em atenção que existem existem melhorias para a plataforma Windows Phone 8.1 no serviço do Intune e para a aplicação Portal da empresa do Windows Phone 8.1.

Recomendamos que Atualize os dispositivos Windows Phone 8.1 elegíveis para Windows 10 Mobile quando for possível.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fim do suporte para Android 4.3 e inferior
<!---1171127--->
*6 de Julho de 2017*

Aplicações geridas e a aplicação Portal da empresa para Android exigem Android 4.4 e superior para aceder a recursos da empresa. Dispositivos que não forem atualizados antes do início de Outubro já não são capazes de acessar o Portal da empresa ou a essas aplicações. Até Dezembro, todos os dispositivos inscritos são retirados em Dezembro, resultando na perda do acesso aos recursos da empresa à força. Se estiver a utilizar políticas de proteção de aplicações sem MDM, as aplicações não receber atualizações e a qualidade da experiência diminui ao longo do tempo.



## <a name="see-also"></a>Consulte Também

- [Últimos híbrida MDM funcionalidades e avisos](whats-new-hybrid-archive.md)
- [Quais são as novidades da MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
