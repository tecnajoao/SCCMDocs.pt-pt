---
title: O que há de novo no MDM híbrida
titleSuffix: Configuration Manager
description: Saiba mais sobre as novas funcionalidades de gestão do dispositivo móvel disponíveis para implementações híbridas com o Configuration Manager e o Intune.
ms.date: 08/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cdb5720778366cea951476ad9b314b69bdd0c492
ms.sourcegitcommit: 6e0e5b4b7779ce03e2b56b3b5f68f4ace1acedd8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39467611"
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Quais são as novidades na gestão de dispositivos móveis híbrida com o Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre o dispositivo móvel novas funcionalidades de gestão (MDM) disponíveis para implementações híbridas com o System Center Configuration Manager e o Microsoft Intune.     

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



## <a name="july-2018"></a>Julho de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="support-for-security-enhancement-in-intune-service"></a>Suporte para a melhoria de segurança no serviço Intune
<!--2520152--> Agora pode especificar que os dispositivos sem quaisquer políticas de conformidade atribuída não são conformes com a híbrida. Configure esta definição no Intune no portal do Azure. Recomendamos vivamente que ative esta funcionalidade proteger os recursos internos.

Esta funcionalidade está desativada por predefinição em inquilinos híbrida. Quando ativa esta funcionalidade, os dispositivos que não têm uma política de conformidade atribuída são considerados incompatíveis. Se também ativar o acesso condicional, estes dispositivos perdem o acesso aos recursos internos. Esses recursos podem ser Outlook ou o SharePoint, com base nas políticas de acesso condicional no seu ambiente. Se deixar esta definição de fora, estes dispositivos continuam a ter o mesmo nível de acesso, como fazem atualmente.

Para ajudar a determinar o impacto de ativar esta funcionalidade, fornecemos uma [script na galeria do TechNet](https://gallery.technet.microsoft.com/SQL-Query-for-Hybrid-MDM-5bcb8695). Quando executa esse script em sua base de dados do Configuration Manager, lista os dispositivos que não são visados pelas políticas de conformidade.

Para obter mais informações, consulte os artigos seguintes:
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



## <a name="june-2018"></a>Junho de 2018

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
 
Para obter mais informações, consulte os artigos seguintes:
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
<!-- 710595 --> Utilizar o Azure Active Directory (Azure AD), pode restringir o acesso a sites da web em dispositivos móveis para a aplicação de Browser gerido do Intune. No browser gerido, dados dos sites permanecerão protegidos e separados dos dados pessoais do utilizador final. Além disso, o Managed Browser suporta as capacidades de início de sessão único para sites protegidos pelo Azure AD. A iniciar sessão para o Managed Browser, ou utilizar o Managed Browser num dispositivo com outra aplicação gerida pelo Intune, permite que o Managed Browser aceder a sites empresariais protegidos pelo Azure AD sem que o utilizador ter de introduzir as respetivas credenciais. Esta funcionalidade aplica-se para sites como o Outlook Web Access (OWA) e o SharePoint Online, bem como outros sites empresariais como recursos de intranet acedidos através do Proxy de aplicações do Azure.



## <a name="february-2018"></a>Fevereiro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **suporte do Portal da empresa do macOS para inscrições que utilizam o Gestor de inscrição de dispositivos**  
    Os utilizadores agora podem utilizar o Gestor de inscrição de dispositivos ao inscrever-se com o Portal da empresa do macOS.
    <!-- 1352411 -->


## <a name="january-2018"></a>Janeiro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Aprovar a aplicação do Portal da empresa para Android for Work**  
  Se a sua organização utiliza o Android for Work, aprove manualmente a aplicação Portal da empresa para Android. Em seguida, continua a receber atualizações automáticas da Google Play store gerida.
  <!--1797090 -->  

- **Políticas de acesso condicional para o Intune só estão disponíveis no portal do Azure**   
  Começando com esta versão, tem de configurar e gerir as políticas de acesso condicional no [portal do Azure](https://portal.azure.com) partir **Azure Active Directory** > **acesso condicional** . Para sua comodidade, pode também aceder a estas definições do Intune no portal do Azure em **Intune** > **acesso condicional**.
  <!-- 1737088 1634311 --> 

- **Atualizações em e-mails de conformidade**    
  Quando uma mensagem de e-mail é enviada para comunicar um dispositivo não conforme, detalhes sobre o dispositivo não conforme, são incluídos. 
  <!--1637547 -->

- **Nova funcionalidade para a ação "Resolver" para dispositivos Android**    
  A aplicação Portal da empresa para Android está a expandir a ação "Resolver" para **atualizar definições do dispositivo** resolver [problemas de encriptação de dispositivos](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Bloqueio remoto disponível na aplicação Portal da empresa para Windows 10**    
  Os utilizadores finais podem agora bloquear remotamente os dispositivos a partir da aplicação Portal da empresa para Windows 10. Esta ação não for apresentada no dispositivo local que estejam a utilizar.
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
  A aplicação Microsoft Planner para iOS e Android agora faz parte das aplicações aprovadas para gestão de aplicações móveis (MAM). Configure a aplicação de proteção de aplicações do Intune no portal do Azure para todos os inquilinos. Para obter detalhes, consulte [lista MAM de aplicações aprovadas](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Acesso a registos de aplicações geridas para iOS**    
  Os utilizadores finais com o managed Browser instalado podem agora ver o estado de gestão da Microsoft de todas as aplicações publicadas da e enviar registos para resolver problemas das respetivas aplicações iOS geridas.
  <!-- 1469920 -->    

  Saiba como ativar o modo de resolução de problemas no Managed Browser num dispositivo iOS, veja [geridos de como aceder aos registos de aplicações através do Managed Browser no iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

- **Melhorias ao dispositivo configurar fluxo de trabalho no Portal da empresa para iOS na versão 2.9.0**    
  Melhorámos o fluxo de trabalho do programa de configuração do dispositivo na aplicação Portal da empresa para iOS. A linguagem é mais amigável e combinámos os ecrãs sempre que possível. Também tornámos o idioma mais específicas para a sua empresa com o nome da sua empresa em todo o texto de configuração. Pode ver este fluxo de trabalho atualizado sobre o [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017) página.

- **Pedidos de comentários para a aplicação Portal da empresa para Android**    
  A aplicação Portal da empresa para Android solicita agora comentários do utilizador final. Este comentário é enviado diretamente para a Microsoft e fornece aos usuários finais uma oportunidade para reverem a aplicação na Google Play store pública. Comentários não não necessário e podem ser dispensados facilmente para que os utilizadores podem continuar a utilizar a aplicação. 
  <!--1165249-->    

- **Informe os utilizadores finais informações do dispositivo que podem ser vistas para dispositivos Windows 10**    
  Adicionámos **tipo de propriedade** na tela de detalhes do dispositivo na aplicação Portal da empresa para Windows 10. Esta informação permite aos utilizadores obter mais informações sobre privacidade diretamente a partir da documentação do utilizador final do Intune. Eles também podem localizar estas informações no **sobre** ecrã.
  <!--1337920-->    

- **Nova ação "Resolver" disponível para dispositivos Android**    
  A aplicação Portal da empresa para Android está a introduzir uma ação "Resolver" sobre o _atualizar definições do dispositivo_ página. A seleção desta opção leva o usuário final diretamente para a definição que está a causar o respetivo dispositivo não esteja em conformidade. A aplicação Portal da empresa para Android suporta atualmente esta ação para o [código de acesso do dispositivo](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [encriptação do dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [depuração de USB](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android), e [desconhecido Origens](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android) definições. 
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
    - Os utilizadores finais recebem os passos a seguir para ajudá-los [corrigir erros de ativação no Samsung Knox dispositivos](https://go.microsoft.com/fwlink/?linkid=859718) ou a [desativar o modo de poupança de energia](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Se nenhuma dessas soluções resolver o problema, disponibilizamos uma explicação de como [enviar registos para a Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Indicador de progresso de configuração do dispositivo no Portal da empresa para Android**    
  A aplicação Portal da empresa para Android mostra um indicador de progresso do programa de configuração de dispositivo quando um utilizador está a inscrever o respetivo dispositivo. O indicador mostra novos Estados, a começar com "Configuração do dispositivo...", em seguida, "A registar o dispositivo...", em seguida, "A concluir a registar o dispositivo...", em seguida, "A concluir a configuração do dispositivo...".  
  <!--1565657-->    

- **Suporte de autenticação com base em certificado no Portal da empresa para iOS**    
  Foi adicionado suporte para autenticação baseada em certificados (CBA) na aplicação Portal da empresa para iOS. Os utilizadores com cba devem introduzir o respetivo nome de utilizador, em seguida, toquem na ligação "Iniciar sessão com um certificado de". CBA já é suportado nas aplicações do Portal da empresa para Android e Windows. Pode saber mais sobre o [inicie sessão na aplicação Portal da empresa](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal) página.
  <!--1029830-->   

- **Melhorias ao fluxo de trabalho de configuração de dispositivos no Portal da empresa**     
  Melhorámos o fluxo de trabalho do programa de configuração do dispositivo na aplicação Portal da empresa para Android. A linguagem é mais fácil de utilizar e adequado à sua empresa e combinámos os ecrãs sempre que possível. Pode ver esses aprimoramentos no [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017) página.
  <!--1490692-->     

- **O pedido de acesso aos contactos em dispositivos Android orientação melhorada**     
  A aplicação Portal da empresa para Android requer, muitas vezes, o utilizador final aceitar a permissão de contactos. Se um utilizador final recusar este acesso, verão uma notificação na aplicação que o alerta para o conceder para acesso condicional. 
  <!--1484985-->     

- **Remediação de arranque seguro para Android**     
  Os utilizadores finais com dispositivos Android poderão tocar no motivo de não conformidade na aplicação Portal da empresa. Sempre que possível, esta ação leva-los diretamente para a localização correta na aplicação de definições para corrigir o problema. 
  <!--1490712-->    

- **Notificações push adicionais para utilizadores finais na aplicação Portal da empresa para Android Oreo**    
  Os utilizadores finais verão notificações adicionais a indicar quando a aplicação Portal da empresa para Android Oreo está a efetuar tarefas em segundo plano, como a obtenção de políticas do serviço Intune. As notificações de aumentam a transparência para os utilizadores finais sobre o quando o Portal da empresa está a efetuar tarefas administrativas nos respetivos dispositivos. Esta melhoria é parte do geral [Otimização da interface de Usuário do Portal da empresa](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para a aplicação Portal da empresa para Android Oreo. 
  <!--1475932 -->     

- **Novo comportamentos para a aplicação Portal da empresa para Android com perfis de trabalho**     
  Quando inscreve um dispositivo Android for Work com um perfil de trabalho, é a aplicação Portal da empresa no perfil de trabalho que executa tarefas de gestão no dispositivo. 

  A menos que estiver a utilizar uma aplicação com MAM ativada no perfil pessoal, a aplicação Portal da empresa para Android já não terá qualquer utilidade. Para melhorar a experiência de perfil de trabalho, o Intune oculta automaticamente a aplicação Portal da empresa pessoa depois de uma inscrição de perfil de trabalho com êxito.

  A aplicação Portal da empresa para Android pode ser ativada em qualquer altura no perfil pessoal, navegue para [Portal da empresa na Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) e ao tocar em **ativar**.
  <!--1485783-->    

- **Portal para o Windows 8.1 e Windows Phone 8.1 mudar para o modo de suporte da empresa**    
  Um aviso foi adicionado ao anunciar que as aplicações do Portal da empresa para Windows 8.1 e Windows Phone 8.1 estão a mover para o modo de suporte. Para obter detalhes, consulte [avisos](#notices).  
  <!--1428681-->    

- **Bloquear a inscrição de dispositivos Samsung Knox não suportados**   
  A aplicação Portal da empresa apenas tenta inscrever dispositivos Samsung Knox suportados. Para evitar erros de ativação de KNOX que impedem a inscrição MDM, inscrição de dispositivos é tentada apenas se o dispositivo aparece na [lista de dispositivos publicados pela Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Dispositivos Samsung poderão ter números de modelo que suportem o KNOX enquanto outros não. Verifique a compatibilidade de Knox com o revendedor de dispositivo antes da compra e implementação. Pode encontrar a lista completa de dispositivos verificados na [definições de política do Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
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
    A aplicação Portal da empresa para Windows 10 permite aos utilizadores atualizar os dados na aplicação, ao pedir para atualizar ou, em ambientes de trabalho, prima F5.
    <!-- 1132468 -->     

- **Informe os utilizadores finais informações do dispositivo que podem ser vistas para iOS**   
    Adicionámos **tipo de propriedade** na tela de detalhes do dispositivo na aplicação Portal da empresa para iOS. Esta informação permite aos utilizadores obter mais informações sobre privacidade diretamente a partir da documentação do utilizador final do Intune. Eles também podem localizar estas informações no ecrã Acerca. 
    <!--739894-->    

- **Mais fácil de compreender frases para a aplicação Portal da empresa para Android**   
    O processo de inscrição para a aplicação Portal da empresa para Android foi simplificado para facilitar para os utilizadores finais inscreverem o texto. Se tiver documentação de inscrição personalizada, atualizá-la para refletir os novos ecrãs. Pode encontrar imagens de exemplo na nossa [atualização da IU para aplicações de utilizadores finais do Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017) página.
    <!---1396349-->    

- **Política de permissão da aplicação Portal da empresa do Windows 10 adicionada à proteção de informações do Windows**    
    A aplicação Portal da empresa do Windows 10 foi atualizada para oferecer suporte a Windows Information Protection (WIP). A aplicação pode ser adicionada para o WIP permitir que a política. Com esta alteração, a aplicação já não deve ser adicionado para o **excluídos** lista. 

    Apenas um item de configuração de WIP único pode ser fornecido para um dispositivo. Se dois itens de configuração do WIP são direcionadas para o mesmo dispositivo, aplica-se nenhuma política WIP.
    <!-- 677129 -->    

- **Fim do aviso de suporte adicionado para o iOS 8.0**    
    Um aviso foi adicionado para o fim do suporte para iOS 8.0. Para obter detalhes, consulte [avisos](#notices).



## <a name="august-2017"></a>Agosto de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Experiência de início de sessão iniciada novo para os utilizadores do Portal da empresa para Android e políticas de proteção de aplicações**    
  Os utilizadores finais podem agora procurar aplicações, gerir dispositivos e ver contacto de TI informações utilizando a aplicação Portal da empresa para Android sem inscrever os respetivos dispositivos Android. Além disso, se um utilizador final já utilizar uma aplicação protegida por políticas de proteção de aplicações do Intune e iniciar o Portal da empresa Android, o utilizador final deixará de receber um pedido para inscrever o dispositivo.
  <!-- 621669 -->



## <a name="july-2017"></a>Julho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Fim de notificações de suporte adicionado para Android e Windows Phone**    
    Avisos de novos foram adicionados para o fim do suporte para versões do Android e Windows Phone. Para obter detalhes, consulte [avisos](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades foram anteriormente disponíveis em versões do Configuration Manager Technical Preview. Estas funcionalidades estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1706.

- [Suporte para autoridades de certificação da Entrust da Entrust](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Novas definições de política de gestão de aplicações móveis](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Atualizações para o Android for Work a configuração de partilha](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Novas regras de política de conformidade de dispositivo](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Novas definições de configuração para dispositivos Windows 10 que não são geridos com o cliente do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Suporte do Cisco (IPsec) para perfis VPN do macOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restrições de inscrição de Android e iOS](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 



## <a name="june-2017"></a>Junho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Alterar a autoridade MDM**    
  A partir do Configuration Manager versão 1610, pode alterar a autoridade MDM sem ter de contactar Support da Microsoft. Também não é preciso anular a inscrição e inscrever novamente os seus dispositivos geridos existentes. Para obter detalhes, consulte [alterar a sua autoridade MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Integração de proxy de navegador e a aplicação gerida**    
  Agora, o Intune Managed Browser pode integrar com o serviço de Proxy de aplicações do Azure AD para permitir aos utilizadores acederem a sites internos mesmo quando trabalham remotamente. Os utilizadores do browser de introduzir o URL do site como fariam normalmente e o Managed Browser encaminha o pedido através do gateway de web de proxy de aplicação. Para obter mais informações, consulte [acesso à Internet de gerir através de políticas de browser gerido](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **Aplicação do Portal da empresa para Android tem agora uma nova experiência de utilizador final para políticas de proteção de aplicações**  
  Com base nos comentários dos clientes, modificámos a aplicação Portal da empresa para Android para apresentar uma **acesso a conteúdos da empresa** botão. O objetivo é evitar que os utilizadores finais desnecessariamente pelo processo de inscrição quando apenas precisarem de aceder a aplicações que suportam políticas de proteção de aplicações, uma funcionalidade de gestão de aplicações móveis do Intune. Pode ver estas alterações na [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Nova ação de menu para remover facilmente o Portal da empresa**  
  Com base nos comentários dos utilizadores, a aplicação Portal da empresa para Android adicionou uma nova ação de menu para iniciar a remoção do Portal da empresa a partir do seu dispositivo. Esta ação remove o dispositivo da gestão do Intune para que a aplicação pode ser removida do dispositivo pelo utilizador. Pode ver estas alterações na [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui) página e, no [documentação do utilizador final Android](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Melhorias na sincronização da aplicação com o Windows 10 Creators Update**  
  A aplicação Portal da empresa para Windows 10 agora inicia automaticamente uma sincronização para pedidos de instalação de aplicações para dispositivos com Windows 10 Creators Update (versão 1703). Este comportamento reduz a edição da aplicação interrupção durante o estado "Sincronização pendente" da instalação. Além disso, os utilizadores conseguem iniciar manualmente uma sincronização a partir da aplicação. Pode ver estas alterações na [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Nova experiência orientada para o Portal da empresa do Windows 10**  
  A aplicação Portal da empresa para Windows 10 inclui uma experiência de instruções orientada do Intune para dispositivos que ainda não foram identificados ou inscritos. A nova experiência disponibiliza instruções passo a passo que orientam o utilizador a registar no Azure Active Directory (necessário para funcionalidades de acesso condicional) e a inscrição de MDM (necessário para funcionalidades de gestão de dispositivos). A experiência guiada está acessível a partir da home page do Portal da empresa. Se os utilizadores não concluírem o registo e a inscrição, eles podem continuar a utilizar a aplicação, mas terão funcionalidades limitadas.

  Esta atualização só é visível em dispositivos com Windows 10 Anniversary Update (compilação 1607) ou superior. Pode ver estas alterações na [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Melhorias dos mosaicos de aplicação na aplicação Portal da empresa para iOS**  
  Atualizámos a estrutura dos mosaicos de aplicação na home page para refletir a cor corporativa que configurou para o Portal da empresa. Para obter mais informações, consulte [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Seletor de conta agora disponível para a aplicação Portal da empresa para iOS**  
  Se os utilizadores de dispositivos iOS utilizam a sua conta escolar ou profissional para iniciar sessão em outras aplicações da Microsoft, poderão ver nosso novo Seletor de conta quando iniciarem sessão no Portal da empresa. Para obter mais informações, consulte [quais são as novidades na IU da aplicação](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novo no Configuration Manager Technical Preview 1706

- **Novas definições de item de configuração do Windows**      
  Novos itens de configuração do Windows estão disponíveis para as categorias de definição de palavra-passe, o dispositivo, o Store e o Microsoft Edge. Para obter mais informações, consulte [definições de item de configuração do novo Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).
  <!-- 1354715 -->

- **Novas regras de política de conformidade de dispositivo**   
  Agora pode configurar novas opções para políticas de conformidade que foram anteriormente disponíveis apenas no Intune autónomo. Para obter detalhes, consulte [melhorias de política de conformidade do dispositivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrições de inscrição de Android e iOS**       
  Os administradores podem agora especificar que os utilizadores podem inscrever dispositivos Android ou iOS pessoais nos respetivos ambientes híbridos. Esta ação permite que limite inscritos dispositivos pré-declarados pretencentes, dispositivos pertencentes à empresa ou dispositivos iOS inscritos com o programa de inscrição de dispositivos apenas. Para obter detalhes, consulte [restrições de inscrição de Android e iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).
  <!-- 1290826 -->

- **Suporte para autoridades de certificação da Entrust**      
  O Configuration Manager suporta agora a autoridades de certificação da Entrust. Este suporte permite a entrega de certificado PFX para dispositivos inscritos no Microsoft Intune.    
  <!-- 1350740 -->

  Pode configurar a Entrust como a autoridade de certificação, ao adicionar uma função de ponto de registo de certificados no Configuration Manager. Ao adicionar um novo perfil de certificado que emite certificados PFX, pode selecionar autoridade de certificação de um Microsoft ou da Entrust.

  **Problema conhecido**: No 1706 technical preview, não são emitidos certificados PFX para autoridades de certificação da Microsoft. Este problema não afeta os certificados PFX importados ou perfis de SCEP.

- **Suporte do Cisco (IPsec) para perfis VPN do macOS**      
  Pode criar um macOS perfil da VPN com o Cisco (IPsec) como o tipo de ligação. Para obter mais informações, consulte [criar perfis VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).
  <!-- 1321367 -->



## <a name="notices"></a>Avisos

### <a name="plan-for-change-upcoming-macos-and-intune-password-enforcement-change"></a>Planear a alteração: MacOS futuros e alterações de imposição de palavra-passe do Intune
<!--1873216--> Na versão do serviço de Setembro, o Intune planos para integrar da Apple recentemente lançou definição de "Palavra-passe alterações na autenticação seguinte" para dispositivos MacOS 10.13 de versões e superior. Antes desta definição foi introduzida, fornecedores MDM não tinham nenhuma forma de verificar que o código de acesso num dispositivo foi alterado para garantir a conformidade. Configuração e de conformidade as políticas do Intune apenas validadas que da próxima vez que uma palavra-passe foi alterada no dispositivo, ele pode ser marcado como compatível. Os utilizadores do macOS irão receber um pedido para atualizar a palavra-passe quando podemos integrar esse novo recurso de Apple, mesmo que a palavra-passe já está em conformidade.

#### <a name="how-does-this-change-affect-me"></a>Como essa alteração me afeta?
Esta alteração afeta apenas o Intune autónomo ou híbrida MDM os clientes com uma política de dispositivos macOS. Apple introduziu a alterar palavra-passe na definição de autenticação de novo. Agora o Intune pode forçar os usuários a atualizar a palavra-passe para um que esteja em conformidade quando os emitir uma política de palavra-passe. Se bloquear recursos da empresa até que o dispositivo é marcado como em conformidade, sabe, em seguida, que os utilizadores finais podem ser impedidos de aceder a recursos da empresa como e-mail ou sites do SharePoint, até que a reposição de palavra-passe. No futuro, todas as atualizações das políticas de palavra-passe de configuração e de conformidade irão forçar utilizadores direcionados para atualizar as respetivas palavras-passe.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso fazer para se preparar para esta alteração?
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

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso fazer para se preparar para esta alteração?

Verificar a existência de dispositivos ou utilizadores que são afetados na sua organização. No Intune no portal do Azure, aceda a **dispositivos** > **todos os dispositivos**e filtre por **SO**.  Clique em **colunas** para detalhes de superfície, como a versão do SO. Solicite que os utilizadores atualizarem os seus dispositivos para uma versão de SO suportada antes de Setembro.


### <a name="plan-for-change-intune-moving-to-tls-12"></a>Planear a alteração: Intune mudar para o TLS 1.2

A partir de 31 de Outubro de 2018, o Intune suportará versão do protocolo Transport Layer Security (TLS) 1.2 para fornecer encriptação de melhor em classe, para garantir que o nosso serviço é mais seguro por padrão e para se alinhar com outros serviços Microsoft como o Microsoft Office 365. Office comunicar essa alteração no MC128929.

#### <a name="how-does-this-change-affect-me"></a>Como essa alteração me afeta?

A partir de 31 de Outubro de 2018, o Intune já não suporta as versões de protocolo do TLS 1.0 ou 1.1. Todas as combinações de servidor de cliente e servidor de browser devem utilizar o TLS versão 1.2 para garantir que a ligação sem problemas para o Intune. Esta alteração irá afetar os dispositivos de utilizadores finais que não são suportados pelo Intune, mas continua a receber a política através do Intune e que não é possível utilizar o TLS versão 1.2. Estes dispositivos incluem os que executam o Android 4.3 e anterior. Para obter uma lista de browsers e dispositivos afetados, consulte o link abaixo.

Após 31 de Outubro de 2018, se ocorrer um problema relacionado com a utilização de uma versão antiga do TLS, atualize para o TLS 1.2 ou para um dispositivo que suporte a TLS 1.2 como parte da resolução.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso fazer para se preparar para esta alteração?

Recomendamos que, proativamente, remover o TLS 1.0 e 1.1 dependências nos seus ambientes e desativar TLS 1.0 e 1.1 ao nível do sistema operativo, sempre que possível. Comece a planejar sua migração para o TLS 1.2 hoje mesmo. Verifique a mensagem de blogue de suporte abaixo para obter a lista de dispositivos que não são suportadas pelo Intune hoje em dia, mas ainda pode receber políticas e que não será capaz de se comunicar usando o protocolo TLS versão 1.2. Poderá ter de notificar os utilizadores finais vai de perder o acesso aos recursos empresariais.

Para obter mais informações, consulte [Intune mudar para o TLS 1.2 para a encriptação](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/).


### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portal para o Windows 8.1 e Windows Phone 8.1 mudar para o modo de suporte da empresa 
<!--1428681-->
*6 de Outubro de 2017*   
 
A partir de Outubro de 2017, mova as aplicações Portal da empresa para Windows 8.1 e Windows Phone 8.1 para modo de suporte. Neste modo, significa que as aplicações e os cenários existentes, tais como inscrição e conformidade, continuarão a ter suporte nestas plataformas. Estas aplicações continuam a estar disponível para download por meio de canais de lançamento existentes, como a Microsoft Store. 

Uma vez no modo de suporte, estas aplicações só receção atualizações críticas de segurança. Não existem atualizações ou funcionalidades adicionais serão lançadas para estas aplicações. Para novos recursos, recomendamos que Atualize os dispositivos Windows 10 ou Windows 10 Mobile. 

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
