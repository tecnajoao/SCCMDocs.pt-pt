---
title: Novidades da MDM híbrido
titleSuffix: Configuration Manager
description: Saiba mais sobre as novas funcionalidades de gestão do dispositivo móvel disponíveis para implementações híbridas com o Configuration Manager e o Intune.
ms.date: 05/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 72aeff7874456c3866ccb658395b8706057bdfaf
ms.sourcegitcommit: 7bec1331c4f3096e6a278ff9ea0e929cff0a9cb9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/10/2018
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Novidades na gestão de dispositivos móveis híbrida com o Configuration Manager e o Microsoft Intune

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



## <a name="may-2018"></a>De 2018 Maio

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Pedir ajuda no Portal da empresa para Windows 10 
<!--1874137-->
Portal da empresa para Windows 10 agora registos de aplicações diretamente para a Microsoft quando envia o utilizador inicia o fluxo de trabalho para obter ajuda com um problema. Este comportamento torna mais fácil resolver problemas que são gerados para a Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Suporte para novas versões de cliente de Cisco AnyConnect para iOS
<!--1357393-->
Pode ativar o suporte para Cisco AnyConnect para o iOS versão 4.0.7 ou posterior. Se o fizer, os perfis de VPN do Cisco AnyConnect existentes são etiquetados **Cisco AnyConnect de legado**e continuar a funcionar como anteriormente. O **Cisco AnyConnect** opção é para perfis de VPN nova, que funcionam com Cisco AnyConnect 4.0.7 de versão do iOS ou posterior.

Para obter mais informações sobre como ativar esta funcionalidade, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

> [!Note]  
> Continuar a utilizar o **Cisco AnyConnect de legado** opção macOS para perfis de VPN. 



## <a name="april-2018"></a>De 2018 Abril

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>Intune feita Fluent de estrutura de sistema na aplicação Portal da empresa para Windows 10 
<!--1195010-->
A aplicação Portal da empresa do Intune para Windows 10 foi atualizada com o [vista de navegação do sistema Design Fluent](/windows/uwp/design/basics/navigation-basics). Ao longo do lado da aplicação Repare uma lista estática, vertical de todas as páginas de nível superior. Clique em qualquer ligação para ver e alternar entre páginas rapidamente. Esta atualização é o primeiro dos vários verá como parte do nosso esforço em curso para criar uma experiência mais adaptável, empathetic e familiar no Intune. Para ver o aspeto atualizado, aceda à [Novidades na aplicação IU](/intune/whats-new-app-ui).

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>Mosaicos de dispositivo melhorada no Portal de empresa do Windows 10
<!--2213364-->
Os mosaicos foram atualizados para ser mais acessível a utilizadores de visão baixa e para realizar melhor para ler as ferramentas do ecrã.


#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>O Portal da empresa para macOS em máquinas virtuais de teste
<!--2216679-->
Iremos tiver publicado orientações para ajudar os administradores de TI testar a aplicação Portal da empresa para macOS em máquinas virtuais no ambiente de trabalho Parallels e Fusion de VMware. Para obter mais informações, consulte [inscrever máquinas de virtuais macOS para fins de teste](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing).


#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>Enviar relatórios de diagnóstico na aplicação Portal da empresa para macOS
<!--2216677-->
A aplicação do Portal da empresa em dispositivos de macOS foi atualizada para melhorar a forma como os utilizadores comunicar erros relacionados com o Intune. A partir da aplicação Portal da empresa, os seus empregados podem:

- Carrega os relatórios de diagnóstico diretamente para a equipa de programador da Microsoft.
- O ID da sua empresa um incidente de correio eletrónico IT equipa de suporte.


#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Experiência de ajuda atualizada na aplicação Portal da empresa para Android 
<!--1631531-->
Atualizámos a experiência de ajuda na aplicação Portal da empresa para Android alinhar com as melhores práticas para a plataforma Android. Agora quando os utilizadores encontram um problema na aplicação, podem tocar **Menu** > **ajudar** e:
- Carregar os registos de diagnóstico para a Microsoft.
- Envie uma mensagem de e-mail que descreve o ID do problema e incidente a uma pessoa de suporte da empresa.


#### <a name="update-where-to-configure-your-app-protection-policies"></a>Atualizar onde pretende configurar políticas de proteção de aplicações 
<!--2144597-->
No portal do Azure no âmbito do serviço do Microsoft Intune, vamos temporariamente redirecioná-lo do **proteção de aplicação do Intune** painel de serviço para o **aplicação móvel** painel. Tenha em atenção que todas as suas políticas de proteção da aplicação já estão no **aplicação móvel** painel no Intune, em configuração de aplicação. Em vez de ir para a proteção de aplicação do Intune, pode irá aceder apenas ao Intune. Em Abril de 2018, iremos parar o redirecionamento e remover completamente o **proteção de aplicação do Intune** service painel, pelo que não haja apenas uma localização para políticas de proteção de aplicações no Intune. 

**Como Isto afeta-me?** Esta alteração afetará clientes do Intune autónomo e clientes híbridos (Intune com o Configuration Manager). Esta integração ajudará a simplificar a administração de gestão de nuvem.

**O que é necessário para se preparar para que esta alteração?** . Tag **Intune** como um favorito em vez do **proteção de aplicação do Intune** painel de serviço e certifique-se de que está familiarizado com o fluxo de trabalho da política de proteção aplicação no **Mobile** Painel de aplicação no Intune. Vamos redirecionar durante um curto período de tempo e, em seguida, remova o **aplicação proteção** painel. Lembre-se que todas as políticas de proteção da aplicação já estão no Intune e pode modificar qualquer uma das suas políticas de acesso condicional. Para obter mais informações sobre como modificar as políticas de acesso condicional, consulte [acesso condicional no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Para obter mais informações, consulte [quais são as políticas de proteção da aplicação?](/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Atualização de experiência de utilizador para a aplicação do Portal da empresa para iOS 
<!--1412866-->
Foi lançada uma atualização de experiência de utilizador principais para a aplicação Portal da empresa para iOS. A atualização inclui uma conclusão recriar visual que inclui um aspeto e funcionalidade modernized. Iremos tiver mantida a funcionalidade da aplicação, mas aumenta a capacidade de utilização e acessibilidade.  

Também verá:
- Suporte para iPhone X.
- Mais rápido iniciação da aplicação e carregar respostas, para poupar tempo de utilizadores.
- Barras de progresso adicionais para fornecer aos utilizadores com as informações de estado mais atualizadas.
- Melhoramentos para os utilizadores de forma carregar registos, pelo que se algo não bate certo, é mais fácil de relatório.  

Para ver o aspeto atualizado, aceda a [Novidades na aplicação IU](/intune/whats-new-app-ui).



## <a name="march-2018"></a>De 2018 Março

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>Opção de comentários enviar Windows empresa Portal poderá deixará de funcionar
<!--2070166-->
A aplicação Portal da empresa do Windows tem uma opção de 'Enviar Comentários' permitir que os utilizadores para enviar comentários sobre a aplicação à Microsoft. De 30 de Abril de 2018, esta opção continua a ser suportada apenas na aplicação Portal da empresa do Windows 10 em execução no Windows 10 versão 1607 e posterior.   

**Como Isto afeta-me?**

Se não tiver a aplicação Portal da empresa do Windows instalada para os utilizadores finais,. a ignorar esta mensagem.

Se tiver qualquer um dos seus utilizadores finais a aplicação Portal da empresa, tenha em atenção que a partir 30 de Abril, o botão 'Enviar Comentários' já não funciona para a aplicação nos seguintes cenários:  

 - Aplicação do Portal da empresa do Windows 10 no Windows 10 versão 1507 e a versão 1511  

 - Aplicação do Portal da empresa do Windows Phone 8.1  

Para os dispositivos afetados, a opção 'Enviar Comentários' falha e não for bem sucedido, mesmo em Repetir. Para enviar comentários à Microsoft sobre experiências nas plataformas seguintes, existem comentários alternativo canais listados abaixo.

**O que é necessário para se preparar para que esta alteração?**

Volte a informar os utilizadores finais desta alteração e atualizar as orientações para o utilizador, se necessário. 

Informe os utilizadores finais utilizando o Portal da empresa no Windows Phone 8.1, Windows 10 versão 1507 e Windows 10 versão 1511 que têm dois canais de comentários alternativo disponíveis. Estes requisitos podem:  

- Utilize os comentários Hub aplicação no Windows 10  
- Envie um e-mail para WinCPfeedback@microsoft.com  

Peça aos utilizadores finais no Windows 10 versão 1607 ou posterior para atualizar para a versão mais recente do Windows Portal da empresa disponíveis no Microsoft Store.



#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>Azure Active Directory web sites pode exigir a aplicação de Browser gerido do Intune e suporta o início de sessão único para o Browser gerido (pré-visualização pública)
<!-- 710595 --> 
Utilizar o Azure Active Directory (Azure AD), pode agora restringir o acesso aos sites nos dispositivos móveis para a aplicação de Browser gerido do Intune. Num browser gerido, os dados do web site irão permanecer segura e separado dos dados pessoais do utilizador final. Além disso, o Browser gerido irá suportar capacidades de início de sessão único para os sites protegidos pelo Azure AD. Iniciar sessão para o Browser gerido ou utilizar o Browser gerido num dispositivo com outra aplicação gerida pelo Intune, permite que o Browser gerido aceder aos sites empresariais protegidos pelo Azure AD sem o necessidade de introduzir as respetivas credenciais do utilizador. Esta funcionalidade aplica-se a sites, como o Outlook Web Access (OWA) e ao SharePoint Online, bem como outros sites empresariais, como recursos de intranet acedidos através do Proxy de aplicações do Azure.



## <a name="february-2018"></a>De 2018 Fevereiro

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **macOS suporte de Portal da empresa para inscrições que utilizam o Gestor de inscrição de dispositivos**  
    Os utilizadores podem agora utilizar o Gestor de inscrição de dispositivos ao inscrever com o macOS Portal da empresa.
    <!-- 1352411 -->


## <a name="january-2018"></a>De 2018 Janeiro

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Aprovar a aplicação do Portal da empresa para Android para o trabalho**  
  Se a sua organização utiliza o Android de trabalho, aprove manualmente a aplicação Portal da empresa para Android. Em seguida, continua a receber atualizações automáticas do Google Play store gerida.
  <!--1797090 -->  

- **Políticas de acesso condicional para o Intune só estão disponíveis no portal do Azure**   
  A partir desta versão, tem de configurar e gerir as políticas de acesso condicional no [portal do Azure](https://portal.azure.com) de **do Azure Active Directory** > **acesso condicional** . Para sua comodidade, também pode aceder neste painel do Intune no portal do Azure em **Intune** > **acesso condicional**.
  <!-- 1737088 1634311 --> 

- **Atualizações para e-mails de conformidade**    
  Quando é enviado um e-mail para reportar um dispositivo não conforme, os detalhes sobre os dispositivos não conformes estão incluídos. 
  <!--1637547 -->

- **Novas funcionalidades para a ação "Resolve" para dispositivos Android**    
  A aplicação Portal da empresa para Android é expandir a ação "Resolve" para **atualizar as definições de dispositivo** resolver [problemas de encriptação de dispositivos](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Bloqueio remoto disponível na aplicação Portal da empresa para Windows 10**    
  Os utilizadores finais podem agora bloquear remotamente os seus dispositivos a partir da aplicação Portal da empresa para Windows 10. Esta ação não é apresentada para o dispositivo local que está a utilizar ativamente.
  <!--676506-->

- **Resolução mais fácil de problemas de conformidade para a aplicação do Portal da empresa para Windows 10**   
  Os utilizadores finais com dispositivos Windows podem tocar o motivo de não conformidade na aplicação Portal da empresa. Sempre que possível, esta ação demora-los diretamente para a localização correta na aplicação definições para corrigir o problema.
  <!--676546-->    



## <a name="december-2017"></a>Dezembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Implementações de aplicações disponível agora suportadas para Android da empresa**    
  Pode agora implementar aplicações da empresa Android (anteriormente Android para trabalho) como **disponível**, para além **necessário**. Para obter mais informações, consulte [Android criar aplicações com o System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).



## <a name="november-2017"></a>Novembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Protocolos de texto permitido a partir de aplicações geridas**  
  Aplicações geridas pelo SDK da aplicação Intune conseguem enviar mensagens SMS.
  <!-- 1414050  -->   

- **Aplicação do Portal da empresa para macOS está disponível**   
  O Portal da empresa do Intune no macOS tem uma experiência atualizada. Está otimizado para apresentar corretamente todas as notificações de informações e conformidade que os utilizadores precisam para todos os dispositivos que tenham sido inscritos. E, depois do Portal da empresa do Intune tem sido implementado num dispositivo, Microsoft AutoUpdate para macOS fornece atualizações ao mesmo. Transfira o novo Portal de empresa do Intune para macOS, iniciando sessão no site de Portal da empresa do Intune a partir de um dispositivo macOS.
  <!--1541700-->   

- **Microsoft Planner faz agora parte da lista de gestão (MAM) de aplicação móvel de aplicações aprovadas**    
  A aplicação Microsoft Planner para iOS e Android faz agora parte das aplicações aprovadas para gestão de aplicações móveis (MAM). Configure a aplicação através do painel de proteção de aplicação do Intune no portal do Azure para todos os inquilinos. Para obter mais informações, consulte [lista MAM das aplicações aprovadas](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Acesso a registos de aplicações geridas para iOS**    
  Os utilizadores finais com o Browser gerido instalado pode agora ver o estado de gestão da Microsoft todas as aplicações publicadas e enviar registos para as suas aplicações iOS geridas de resolução de problemas.
  <!-- 1469920 -->    

  Aprenda a ativar o modo de resolução de problemas num Browser gerido num dispositivo iOS, consulte [como acesso gerido registos de aplicação utilizando o Browser gerido em dispositivos iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

- **Melhoramentos ao dispositivo configurar fluxo de trabalho no Portal da empresa para iOS versão 2.9.0**    
  Iremos tiver melhorado o fluxo de trabalho do programa de configuração do dispositivo na aplicação Portal da empresa para iOS. O idioma é mais intuitivo e iremos tiver combinado ecrãs sempre que possível. Também efetuamos o idioma mais específica da sua empresa utilizando o nome da sua empresa em todo o texto de configuração. Pode ver este fluxo de trabalho atualizado no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017) página.

- **Pedidos de comentários para a aplicação Portal da empresa para Android**    
  A aplicação Portal da empresa para Android agora pedidos de comentários do utilizador final. Estes comentários é enviado diretamente para a Microsoft e proporciona aos utilizadores finais com uma oportunidade para rever a aplicação na loja do Google Play pública. Comentários não são necessário e podem ser dispensados facilmente para que os utilizadores podem continuar a utilizar a aplicação. 
  <!--1165249-->    

- **Informar os utilizadores finais podem ser vistas as informações do dispositivo para dispositivos Windows 10**    
  Foi adicionado **o tipo de propriedade** para o ecrã de detalhes do dispositivo na aplicação Portal da empresa para Windows 10. Estas informações permitem aos utilizadores encontrar mais informações sobre privacidade diretamente a partir de documentos do utilizador final do Intune. Eles também podem localizar estas informações no **sobre** ecrã.
  <!--1337920-->    

- **Nova ação 'Resolver' disponível para dispositivos Android**    
  A aplicação Portal da empresa para Android está a introduzir uma ação 'Resolva' no _atualizar as definições de dispositivo_ página. A seleção desta opção demora o utilizador final diretamente para a definição que está a causar o respetivo dispositivo para estar em conformidade. A aplicação Portal da empresa para Android suporta atualmente esta ação para o [código de acesso do dispositivo](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [a encriptação de dispositivos](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [depuração USB](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android), e [desconhecido Origens](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android) definições. 
  <!--1583480-->    


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

- **Ações de não conformidade**    
  Agora, pode configurar uma sequência ordenada de tempo das ações que são aplicadas aos dispositivos que deixarem de estar em conformidade. Por exemplo, pode notificar os utilizadores de dispositivos não conformes por correio eletrónico ou marcar os dispositivos não conformes. Para obter mais informações, consulte [configurar as ações de não conformidade](/sccm/mdm/deploy-use/actions-for-noncompliance).
  <!--1321366 -->

- **Novas definições de política de gestão de aplicações móveis**     
  Foram adicionadas as seguintes definições para as definições de política de gestão de aplicações móveis:
  - **Desativar a sincronização de contactos**: Impede a aplicação de guardar os dados para a aplicação de contactos nativa no dispositivo.
  - **Desativar a impressão**: Impede que a aplicação de trabalho de impressão ou dados escola.
  <!-- 1324760 -->    

  Consulte [proteger aplicações ao utilizar políticas de proteção de aplicações no Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para experimentar as novas definições de política de proteção de aplicação.

- **Suporte de dispositivos Windows 10 ARM64**     
  Cenários de gestão (MDM) de dispositivos móveis híbridos são suportados em dispositivos ARM64 com o Windows 10 quando estes dispositivos estão disponíveis. Para obter mais informações, consulte [suporte de dispositivos Windows 10 ARM64](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Experiência melhorada de perfil VPN na consola do Configuration Manager**     
  Com esta versão, atualizámos as páginas de assistente e propriedades de perfil VPN para apresentar as definições adequadas da plataforma selecionada. Esta funcionalidade não estava anteriormente disponível na 1709 de pré-visualização técnica do Configuration Manager. Está agora disponível em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1710. Para obter mais informações, consulte [experiência de perfil de VPN melhorada na consola do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Novo no Configuration Manager Technical Preview 1711

- **Novas opções de política de conformidade para o Windows 10**   
  Agora, pode configurar novas opções de políticas de conformidade para dispositivos Windows 10. As novas definições incluem as políticas de Firewall, o controlo de conta de utilizador, o Windows Defender antivírus e controlo de versões de compilação do SO. Para obter mais informações, consulte [novas opções de política de conformidade para o Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## <a name="october-2017"></a>Outubro de 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Novo no Configuration Manager Technical Preview 1709

- **Experiência melhorada de perfil da VPN na consola do Configuration Manager**      
  Definições do perfil VPN agora são filtradas de acordo com a plataforma. Quando criar novos perfis VPN, cada plataforma suportada contém apenas as definições adequadas para a plataforma. Perfis VPN existentes não são afetados. Pode ler mais sobre esta alteração [aqui](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1313282 -->


### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  

- **Ajudar as utilizadores ajuda próprios com a aplicação Portal da empresa para Android**     
  A aplicação Portal da empresa para Android adicionou instruções aos utilizadores finais ajudar a compreender e possivelmente automática resolver em casos de utilização de novo.
    - Se os utilizadores finais atingiu o número máximo de dispositivos que estão autorizados a adicionar, são orientados para o [portal do Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile) para remover um dispositivo.
    - Os utilizadores finais são fornecidos os passos a seguir para ajudá-los [corrija os erros de ativação em Samsung Knox dispositivos](https://go.microsoft.com/fwlink/?linkid=859718) ou [desativar o modo de energia-guardar](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Se nenhuma destas soluções resolver seu problema, fornecemos uma explicação de como [submeter os registos para a Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Indicador de progresso do programa de configuração de dispositivo no Portal da empresa para Android**    
  A aplicação Portal da empresa para Android mostra um indicador de progresso do programa de configuração de dispositivo quando um utilizador inscrever o respetivo dispositivo. O indicador apresenta Estados novos, começando com "Como configurar o seu dispositivo …", em seguida, "Registar o seu dispositivo …", em seguida, "A concluir a registar o seu dispositivo...", em seguida, "A concluir a configuração do seu dispositivo...".  
  <!--1565657-->    

- **Suporte para autenticação baseada em certificado no Portal da empresa para iOS**    
  Foi adicionado suporte para autenticação baseada em certificado (CBA) na aplicação Portal da empresa para iOS. Os utilizadores com CBA introduza o nome de utilizador, em seguida, toque na ligação de "Iniciar sessão com um certificado". CBA já é suportado nas aplicações do Portal da empresa para Android e Windows. Pode saber mais sobre o [iniciar sessão na aplicação Portal da empresa](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal) página.
  <!--1029830-->   

- **Melhoramentos ao fluxo de trabalho de configuração de dispositivo no Portal da empresa**     
  Iremos tiver melhorado o fluxo de trabalho do programa de configuração do dispositivo na aplicação Portal da empresa para Android. O idioma mais amigável de utilizador e específica da sua empresa e tenha combinado ecrãs sempre que possível. Pode ver estas melhorias no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017) página.
  <!--1490692-->     

- **Melhorado orientações sobre o pedido de acesso para contactos em dispositivos Android**     
  A aplicação Portal da empresa para Android requer, muitas vezes, o utilizador final aceitar a permissão de contactos. Se um utilizador final recusar este acesso, verá uma notificação na aplicação que alertas-los para conceder acesso condicional. 
  <!--1484985-->     

- **Remediação de arranque seguro para Android**     
  Os utilizadores finais com dispositivos Android podem tocar o motivo de não conformidade na aplicação Portal da empresa. Sempre que possível, esta ação demora-los diretamente para a localização correta na aplicação definições para corrigir o problema. 
  <!--1490712-->    

- **Notificações de push adicionais para os utilizadores finais na aplicação Portal da empresa para Android Oreo**    
  Os utilizadores finais veem notificações adicionais para indicar-lhes quando a aplicação Portal da empresa para Android Oreo está a efetuar tarefas em segundo plano, tais como obtenção de políticas do serviço do Intune. As notificações aumentam transparência para os utilizadores finais sobre quando o Portal da empresa está a realizar tarefas administrativas no respetivo dispositivo. Este melhoramento faz parte o gerais [Otimização da IU de Portal da empresa](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para a aplicação do Portal da empresa para Android Oreo. 
  <!--1475932 -->     

- **Novo comportamentos para a aplicação Portal da empresa para Android com perfis de trabalho**     
  Quando inscreve um Android para dispositivos de trabalho com um perfil de trabalho, é a aplicação Portal da empresa no perfil de trabalho que executa tarefas de gestão no dispositivo. 

  A menos que estiver a utilizar uma aplicação ativada para MAM no perfil de pessoal, a aplicação Portal da empresa para Android já não serve qualquer utilização. Para melhorar a experiência de perfil de trabalho, o Intune oculta automaticamente pessoal aplicação Portal da empresa depois da inscrição de perfil um trabalho com êxito.

  A aplicação Portal da empresa para Android pode ser ativada em qualquer altura no perfil de pessoal ao navegar para [Portal da empresa na Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) e ao tocar em **ativar**.
  <!--1485783-->    

- **Portal para Windows 8.1 e Windows Phone 8.1 Mover para sustaining modo de empresa**    
  Foi adicionado um aviso para anunciar que aplicações de Portal da empresa para Windows 8.1 e Windows Phone 8.1 estão a mover para sustaining modo. Para obter mais informações, consulte [avisos](#notices).  
  <!--1428681-->    

- **Bloquear a inscrição de dispositivos Samsung Knox não suportada**   
  A aplicação Portal da empresa tenta apenas inscrever dispositivos Samsung Knox suportados. Para evitar erros de ativação de KNOX que impedem a inscrição MDM, inscrição de dispositivos é tentada apenas se o dispositivo é apresentado no [lista de dispositivos publicados pelo Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Dispositivos Samsung podem ter números de modelo que suportam KNOX enquanto outros que não. Verificar a compatibilidade de Knox com o seu revendedor a partir do dispositivo antes de compra e implementação. Pode encontrar a lista completa dos dispositivos verificados o [as definições de política do Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
  <!-- 1490695 -->     

- **Fim de suporte para Android 4.3 e inferior**     
  Um aviso foi adicionada para o fim de suporte para Android 4.3 e inferior. Para obter mais informações, consulte [avisos](#notices).
  <!--1171126, 1326920 -->     

- **Informar os utilizadores finais as informações do dispositivo podem ser vistas em dispositivos inscritos**     
  Que estamos a adicionar **o tipo de propriedade** para o ecrã de detalhes do dispositivo em todas as aplicações do Portal da empresa. Estas informações permitem aos utilizadores encontrar mais informações sobre privacidade diretamente a partir de [as informações da sua empresa pode ver?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) artigo. Este melhoramento lança em todas as aplicações do Portal da empresa num futuro próximo. Iremos anunciada esta funcionalidade para iOS no [Setembro](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
  <!--1165314-->     



## <a name="september-2017"></a>Setembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Atualizar ação adicionada à aplicação Portal da empresa para Windows 10**    
    Aplicação Portal da empresa para Windows 10 permite aos utilizadores atualizar os dados na aplicação, a extrair para atualizar ou, em ambientes de trabalho, premir F5.
    <!-- 1132468 -->     

- **Informar os utilizadores finais as informações do dispositivo podem ser vistas para iOS**   
    Adicionámos **o tipo de propriedade** para o ecrã de detalhes do dispositivo na aplicação Portal da empresa para iOS. Estas informações permitem aos utilizadores encontrar mais informações sobre privacidade diretamente a partir de documentos do utilizador final do Intune. Eles também podem localizar estas informações no ecrã Acerca. 
    <!--739894-->    

- **Mais fácil de compreender phrasing para a aplicação Portal da empresa para Android**   
    O processo de inscrição para a aplicação Portal da empresa para Android foi simplificado por um novo texto para tornar mais fácil para os utilizadores finais a inscrever. Se tiver de documentação da inscrição personalizada, atualizá-la para refletir ecrãs de novo. Pode encontrar as imagens de exemplo no nosso [atualizações de IU para aplicações de utilizador final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017) página.
    <!---1396349-->    

- **Política de permitir a aplicação Portal da empresa do Windows 10 adicionada à proteção de informações do Windows**    
    A aplicação Portal da empresa do Windows 10 foi atualizada para suportar a proteção de informações do Windows (WIP). A aplicação pode ser adicionada para o WIP Permitir política. Com esta alteração, a aplicação já não tem de ser adicionado para o **excluído** lista. 

    Apenas um item de configuração de WIP único pode ser fornecido para um dispositivo. Se dois itens de configuração de WIP são direcionadas para o mesmo dispositivo, nenhuma política WIP aplica-se.
    <!-- 677129 -->    

- **Fim de aviso de suporte adicionado para o iOS 8.0**    
    Foi adicionado um aviso para o fim de suporte para o iOS 8.0. Para obter mais informações, consulte [avisos](#notices).



## <a name="august-2017"></a>Agosto de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Experiência de início de sessão iniciada novo para utilizadores do Portal da empresa para Android e utilizadores de política de proteção de aplicações**    
  Os utilizadores finais pode procurar as aplicações, gerir dispositivos e ver contacto de TI informações utilizando a aplicação Portal da empresa Android sem inscrever os respetivos dispositivos Android. Além disso, se um utilizador final já utiliza uma aplicação protegida por políticas de proteção de aplicações do Intune e inicia o Portal da empresa Android, o utilizador final deixará de receber uma mensagem para se inscrever o dispositivo.
  <!-- 621669 -->



## <a name="july-2017"></a>Julho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Fim de avisos de suporte adicionado para Android e Windows Phone**    
    Novo avisos foram adicionados para fim de suporte para versões de Android e Windows Phone. Para obter mais informações, consulte [avisos](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As funcionalidades seguintes foram anteriormente disponíveis nas versões do Configuration Manager Technical Preview. Estas funcionalidades estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1706.

- [Suporte de Entrust para Entrust autoridades de certificação](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Novas definições de política de gestão de aplicações móveis](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Atualizações para o Android para a configuração de partilha de trabalho](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Novas regras de política de conformidade de dispositivo](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Novas definições de configuração para dispositivos Windows 10 que não são geridos com o cliente do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Suporte para perfis VPN macOS Cisco (IPsec)](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restrições de inscrição do Android e iOS](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 



## <a name="june-2017"></a>Junho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Alterar a autoridade de MDM**    
  A partir do Configuration Manager versão 1610, pode alterar a autoridade de MDM sem ter de contactar o Support da Microsoft. Também não tem de anular a inscrição e inscrever-se novamente os seus dispositivos geridos existentes. Para obter mais informações, consulte [alterar a autoridade de MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Integração de proxy de aplicações e o browser gerida**    
  Agora, o Browser gerido do Intune pode integrar com o serviço de Proxy de aplicações do Azure AD para permitir que os utilizadores acedam a web sites internos, mesmo quando estão a trabalhar remotamente. Os utilizadores do browser introduza o URL do site, tal como fariam normalmente e o Browser gerido encaminha o pedido através do gateway de web de proxy de aplicações. Para obter mais informações, consulte [acesso gerir Internet através de políticas de browser gerido](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **Aplicação do Portal da empresa para Android tem agora uma nova experiência de utilizador final para as políticas de proteção da aplicação**  
  Com base nos comentários de clientes, iremos tiver modificado a aplicação do Portal da empresa para Android mostrar um **acesso da empresa conteúdo** botão. A intenção é impedir que os utilizadores finais desnecessariamente percorrer o processo de inscrição quando apenas precisam de aceder a aplicações que suportam a aplicação de políticas de proteção, uma funcionalidade de gestão de aplicações móveis do Intune. Pode ver estas alterações no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Nova ação de menu remover facilmente o Portal da empresa**  
  Com base nos comentários dos utilizadores, a aplicação Portal da empresa para Android adicionou uma ação de menu novo para iniciar a remoção do Portal da empresa do seu dispositivo. Esta ação remove o dispositivo da gestão do Intune para que a aplicação pode ser removida do dispositivo pelo utilizador. Pode ver estas alterações no [Novidades na aplicação da IU](https://docs.microsoft.com/intune/whats-new-app-ui) página e no [documentação do utilizador final Android](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Melhoramentos à aplicação a sincronizar com o Windows 10 criadores Update**  
  Aplicação Portal da empresa para Windows 10 agora inicia automaticamente uma sincronização para pedidos de instalação de aplicações para dispositivos com o Windows 10 criadores Update (versão 1703). Este comportamento reduz o problema de instalações stalling durante o estado de "Sincronizar pendente". Além disso, os utilizadores conseguem iniciar manualmente a sincronizar a partir da aplicação. Pode ver estas alterações no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Nova experiência orientada para o Portal da empresa do Windows 10**  
  Aplicação Portal da empresa para Windows 10 inclui uma explicação passo a passo experiência orientada do Intune para dispositivos que ainda não foi identificado ou inscritos. A nova experiência fornece instruções passo a passo que o orienta o utilizador através do registo no Azure Active Directory (necessário para funcionalidades de acesso condicional) e a inscrição MDM (necessário para funcionalidades de gestão de dispositivos). A experiência orientada é acessível a partir da home page do Portal da empresa. Se os utilizadores não concluir o registo e a inscrição, podem continuar a utilizar a aplicação, mas experiência funcionalidade limitada.

  Esta atualização só é visível em dispositivos com Windows 10 aniversário da atualização (compilação 1607) ou superior. Pode ver estas alterações no [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui) página.

- **Melhoramentos para os mosaicos de aplicação na aplicação Portal da empresa para iOS**  
  Atualizámos o design dos mosaicos na home page da aplicação para refletir a cor de imagem corporativa definido para o Portal da empresa. Para obter mais informações, consulte [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Selecionador de conta agora disponível para a aplicação do Portal da empresa para iOS**  
  Se os utilizadores de dispositivos iOS utilizam o seu trabalho conta escolar ou profissional para iniciar sessão em outras aplicações da Microsoft, poderão ver a nossa nova selecionador de conta quando iniciam sessão no Portal da empresa. Para obter mais informações, consulte [Novidades na aplicação IU](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novo no Configuration Manager Technical Preview 1706

- **Novas definições de item de configuração do Windows**      
  Novos itens de configuração do Windows estão disponíveis para as categorias de definição de palavra-passe, o dispositivo, o arquivo e o Microsoft Edge. Para obter mais informações, consulte [definições do item de configuração de novo Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).
  <!-- 1354715 -->

- **Novas regras de política de conformidade de dispositivo**   
  Agora, pode configurar novas opções de políticas de conformidade que foram anteriormente disponíveis apenas no Intune autónomo. Para obter mais informações, consulte [melhoramentos de política de conformidade do dispositivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrições de inscrição do Android e iOS**       
  Administradores agora podem especificar que os utilizadores não é possível inscrever dispositivos Android ou iOS pessoais no respetivo ambiente híbrido. Esta ação permite-lhe limite inscritos dispositivos para predeclared, dispositivos pertencentes à empresa ou os dispositivos iOS inscritos com o programa de inscrição de dispositivos apenas. Para obter mais informações, consulte [restrições de inscrição do Android e iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).
  <!-- 1290826 -->

- **Suporte para Entrust autoridades de certificação**      
  O Configuration Manager suporta agora Entrust autoridades de certificação. Este suporte permite a entrega de certificado PFX para dispositivos inscritos no Microsoft Intune.    
  <!-- 1350740 -->

  Pode configurar Entrust como a autoridade de certificação quando adicionar uma função de ponto de registo de certificados no Configuration Manager. Ao adicionar um novo perfil de certificado que emite certificados PFX, pode selecionar um Microsoft ou Entrust autoridade de certificação.

  **Problema de conhecido**: No 1706 technical preview, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Este problema não afeta os certificados PFX importados ou perfis SCEP.

- **Suporte para perfis VPN macOS Cisco (IPsec)**      
  Pode criar um macOS perfil da VPN com o Cisco (IPsec) como o tipo de ligação. Para obter mais informações, consulte [criar perfis VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).
  <!-- 1321367 -->


## <a name="april-2017"></a>Abril de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **MyApps disponíveis para o Browser gerido**  
  Microsoft MyApps agora tem um melhor suporte no Browser gerido. Utilizadores de Browser geridos que não são direcionados para gestão são colocados diretamente para o serviço de MyApps, onde poderem aceder às suas aplicações de SaaS aprovisionado de admin. Os utilizadores que são direcionados para a gestão do Intune continuam a aceder MyApps do marcador de Browser gerido incorporado.

- **Ícones de novo para o Browser gerido e o Portal da empresa**  
  O Browser gerido está a receber ícones atualizados para o Android e iOS versões da aplicação. No ícone novo contém o destaque do Intune atualizado para o tornar mais consistentes com outras aplicações no Enterprise Mobility + Security (IT + S). Pode ver no ícone novo para o Browser gerido no [são as novidades na página de IU da aplicação Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  O Portal da empresa também está a receber ícones atualizados para os Android, iOS e Windows versões da aplicação para melhorar a consistência com outras aplicações no IT + S. Estes ícones gradualmente são lançadas em plataformas de Abril de Maio enlace tardio.

- **Indicador de progresso do início de sessão no Portal da empresa para Android**  
  Uma atualização para a aplicação Portal da empresa Android mostra um indicador de progresso do início de sessão quando o utilizador inicia ou retoma a aplicação. O indicador progridem Estados novos, começando com "Ligar...", em seguida, "Assinatura suplemento …", em seguida, "A verificar requisitos de segurança..." antes de permitir que o utilizador aceda à aplicação. Pode ver os novos ecrãs para a aplicação Portal da empresa para Android no [são as novidades na página de IU da aplicação Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Impedir que as aplicações acedam ao SharePoint Online**  
  Agora, pode criar uma política de acesso condicional baseado na aplicação para impedir que as aplicações que não têm a aplicar políticas de proteção de aplicação para-las, acedam [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). No cenário de acesso condicional baseado em aplicações, pode especificar as aplicações que pretende que tenham acesso ao SharePoint Online com o portal do Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novo no Configuration Manager Technical Preview 1704

- **Configurar as aplicações Android com políticas de configuração de aplicação**  
  Quando um utilizador executa uma aplicação no Android, para dispositivos de trabalho, utilize as políticas de configuração de aplicações no Configuration Manager para distribuir definições previamente configuradas. Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos com o Android de trabalho. Estas políticas aplicam-se às aplicações aprovadas da Play para o arquivo de trabalho. Para obter mais informações, consulte [Android configurar aplicações com políticas de configuração de aplicações](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).



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
  Se precisar de transferir e sideload da aplicação do Portal da empresa do Windows 10, agora, pode utilizar um script para simplificar e simplificar o processo de assinatura de aplicações para a sua organização. Para transferir o script e as instruções para utilizá-lo, consulte [Microsoft Intune assinatura de Script para Windows 10 Portal da empresa](https://aka.ms/win10cpscript) na galeria do TechNet. Para obter mais informações sobre este anúncio, consulte [a atualizar a aplicação Portal da empresa do Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) no blogue de equipa de suporte do Intune.

- **Suporte melhorado para os utilizadores de Android com base na China**  
  Devido à ausência do Google Play Store na China, dispositivos Android tem de obter aplicações da marketplaces chinês. O Portal da empresa suporta este fluxo de trabalho. Será redirecionado Android que os utilizadores na China transferir as aplicações Portal da empresa e o Outlook de lojas de aplicações locais. Este comportamento melhora a experiência de utilizador quando as políticas de acesso condicional estão ativadas para gestão de dispositivos móveis e gestão de aplicações móveis. As aplicações do Portal da empresa e do Outlook para Android estão disponíveis de lojas de aplicações chinês seguintes:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Certifique-se de que as aplicações do Portal da empresa estão atualizadas**  
  Dezembro de 2016, lançada uma atualização que ativar a imposição da autenticação multifator (MFA) de um grupo de utilizadores quando inscreverem um iOS, Android, Windows 8.1 + ou dispositivo Windows Phone 8.1 +. Esta funcionalidade não funciona sem determinadas versões de linha de base da aplicação Portal da empresa para Android (v5.0.3419.0 +) e iOS (v2.1.17 +).

  Capacidades de gestão do Intune são melhorar continuamente. Muitas melhorias tem coordenado atualizações para as aplicações do Portal da empresa em todas as plataformas suportadas. Recomendamos que mantenha as versões mais recentes das aplicações do Portal da empresa em instaladas em dispositivos. Esta prática tira partido das melhorias no Intune e para a melhor experiência de utilizador.

  >[!Tip]
  > Ter os seus utilizadores a definir os respetivos dispositivos para atualizar automaticamente as aplicações da loja de aplicações adequado. Se tiver efetuado a aplicação Portal da empresa Android disponíveis numa partilha de rede, pode transferir a versão mais recente do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams está ativada para MAM em dispositivos iOS e Android**  
  As aplicações de Teams da Microsoft para iOS e Android agora estão ativadas com capacidades de gestão (MAM) de aplicações móveis do Intune. Capacitar as equipas para trabalhar livremente entre dispositivos, garantindo que conversações e dados empresariais estão protegidos. Para obter mais informações, consulte [o anúncio de Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) no blogue do Enterprise Mobility e segurança.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novo no Configuration Manager Technical Preview 1703

- **Suporte adicional para cenários de Apple Volume Purchase Program**  
   A partir da Technical Preview 1703, tem agora suporte para os seguintes cenários de Volume Purchase Program (VPP):

   - Licenciamento do dispositivo - aplicações que suportam licenciamento do dispositivo e são implementadas em coleções de dispositivos agora apenas requerem uma licença por dispositivo. Anteriormente, era necessário utilizar uma licença para cada utilizador num dispositivo. Para obter mais informações, consulte [implementar aplicações iOS compradas em volume para coleções de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Utilização de vários tokens VPP para um inquilino único híbrida com ambos os tokens utilizados para gerir as aplicações VPP.
   - Utilização de tokens de educação VPP com a capacidade para distinguir entre tokens de negócio e education.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As funcionalidades seguintes foram anteriormente disponíveis nas versões do Configuration Manager Technical Preview. Estas funcionalidades estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1702.

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

- **Suporte para aplicações de linha de negócio no Microsoft Store para empresas**  
  Agora pode sincronizar personalizadas aplicações de linha de negócio da Store Microsoft para empresas.

- **Defesa de ameaça Mobile novas ferramentas de monitorização**  
    Tem agora novas formas para monitorizar o estado de compatibilidade com o fornecedor de serviços móveis defesa de ameaça.

    Para obter mais informações, consulte [como monitorizar a conformidade de defesa de ameaça Mobile](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).



## <a name="notices"></a>Avisos

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portal para Windows 8.1 e Windows Phone 8.1 Mover para sustaining modo de empresa 
<!--1428681-->
*6 de Outubro de 2017*   
 
As aplicações do Portal da empresa para Windows 8.1 e Windows Phone 8.1 a partir de 2017 Outubro, mova para sustaining modo. Este modo significa que as aplicações e cenários existentes, tais como a inscrição e conformidade, continuam a ser suportada para estas plataformas. Estas aplicações continuam a estar disponíveis para transferência através de canais de versão existentes, tais como o Microsoft Store. 

Assim que o destas aplicações na sustaining modo, recebem apenas atualizações de segurança críticas. Não existem atualizações adicionais ou funcionalidades serão lançadas para estas aplicações. Para as novas funcionalidades, recomendamos que atualizar os dispositivos para Windows 10 ou Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fim de suporte para o iOS 8.0 
<!---1164477--->
Aplicações geridas e a aplicação Portal da empresa para iOS requerem iOS 9.0 e superior para aceder a recursos da empresa. Dispositivos que não são atualizados antes de Setembro já não são capazes de aceder ao Portal da empresa ou essas aplicações. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Lembrete de suporte de plataforma: Suporte de base do Windows Phone 8.1 terminou 11 de Julho de 2017
<!-- 1327781 -->
*11 de Julho de 2017*

A plataforma do Windows Phone 8.1 foi atingido o fim do suporte base. Suporte de PC do Windows 8.1 não é afetado.

Não há nenhum impacto imediato em qualquer dispositivo de Windows Phone 8.1 que é gerido pelo serviço do Intune, incluindo os dispositivos inscritos na MDM híbrida Os dispositivos inscritos continuam a funcionar. Todas as políticas, as configurações e as aplicações continuem a funcionar conforme esperado. Tenha em atenção de que existem não melhorias visadas para a plataforma do Windows Phone 8.1 no âmbito do serviço Intune e para a aplicação Portal da empresa do Windows Phone 8.1.

Recomendamos que o serviço de atualização em dispositivos Windows Phone 8.1 elegíveis para Windows 10 Mobile na oportunidade de mais antigo.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fim de suporte para Android 4.3 e inferior
<!---1171127--->
*6 de Julho de 2017*

Aplicações geridas e a aplicação Portal da empresa para Android requerem Android 4.4 e superior para aceder a recursos da empresa. Dispositivos que não são atualizados antes do início do Outubro deixam de ser capazes de aceder ao Portal da empresa ou essas aplicações. Por Dezembro, todos os dispositivos inscritos estão force descontinuado dentro de Dezembro, resultando em perda de acesso aos recursos da empresa. Se estiver a utilizar políticas de proteção da aplicação sem MDM, as aplicações não irão receber as atualizações e a qualidade dos respetivos experiência diminui ao longo do tempo.



## <a name="see-also"></a>Consulte Também

- [Passado híbrida MDM funcionalidades e avisos](whats-new-hybrid-archive.md)
- [Novidades da MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
