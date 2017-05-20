---
title: "Arquivo do que há de novo híbrida MDM | Documentos do Microsoft"
description: "Arquivo de últimos funcionalidades de gestão de dispositivos móveis disponíveis para implementações híbridas com o System Center Configuration Manager e o Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 623a30eddebcae196ff345ef5debc8183ecd6ae6
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Últimos híbrida funcionalidades com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre o dispositivo móvel nos últimos funcionalidades de gestão (MDM) disponíveis para implementações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada secção deste artigo apresenta uma lista de funcionalidades de híbrida em 3 categorias diferentes. Utilize as orientações seguintes para determinar a compatibilidade das funcionalidades em cada categoria com diferentes versões do Configuration Manager:  

|Categorias de funcionalidade|
|-|  
|**Novo no Microsoft Intune** -em geral, todas as funcionalidades listadas sob esta categoria devem trabalhar com todas as versões do Configuration Manager incluindo versões do System Center 2012 R2 Configuration Manager, uma vez que estas funcionalidades requerem o serviço Intune apenas e não necessitam de funcionalidades adicionais no Configuration Manager.<br /><br /> **Novo no Configuration Manager Technical Preview** -todas as funcionalidades listadas sob esta categoria só funcionam com a versão de pré-visualização técnica especificada. Para experimentar estas funcionalidades, tem de instalar a versão de pré-visualização técnica especificada na descrição da funcionalidade. Para obter mais informações, consulte o artigo [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Novo no Configuration Manager (ramo atual)** -todas as funcionalidades listadas sob este trabalho única categoria com a versão especificada do Configuration Manager (ramo atual), tal como versão 1511 ou 1602. Se estiver a utilizar uma versão mais antiga do Configuration Manager para a sua implementação híbrida, tem de atualizar para a versão do Configuration Manager (ramo atual) especificada na descrição da funcionalidade. Para obter mais informações, consulte o artigo [atualizar para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="new-hybrid-features-in-october-2016"></a>Novas funcionalidades de híbrida no Outubro de 2016

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas no Outubro de 2016 funcionam em implementações híbridas.

- **Acesso condicional para gestão de aplicações móveis**

  Pode restringir o acesso ao Exchange Online para que o access inclui apenas a partir das aplicações que suportam as políticas de gestão de aplicações móveis do Intune, como o Outlook. [Esta nova funcionalidade](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) pares de exatamente com políticas de gestão (MAM) de aplicação móvel do Intune, pode bloquear o acesso para clientes de correio incorporada ou outras aplicações que não tenham sido configuradas com as políticas do Intune MAM. Isto garante que os seus utilizadores estão a aceder a dados da sua organização com as aplicações que podem ser protegidos com o Intune MAM. Introdução na gestão de aplicações móveis do Intune através do portal do Azure. Procure a nova secção de acesso condicional no painel "Definições".

-    **Ferramenta de encapsulamento de aplicações do Intune aplicação para Android**

  Pode ativar as suas aplicações para utilizar políticas de gestão (MAM) de aplicações móveis do Intune utilizando a ferramenta de encapsulamento de aplicações do Intune.

- **Compatibilidade Samsung KNOX Standard Android com o Intune**

  Determinados modelos do telefone Samsung Galaxy Ace não podem ser geridos pelo Intune como dispositivos Samsung KNOX Standard. Ao inscrever estes dispositivos com o Intune, será em vez disso ser geridos como dispositivos Android padrão.

  Os números de modelo afetados são:

  - SM G313HU
  -    SM G313HY
  -    SM G313M
  -    SM G313MY
  -    SM G313U

  E os seus utilizadores finais não precisa de tomar nenhuma ação adicional. Para mais informações, visite o Web site Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Novo no Configuration Manager Technical Preview 1610

As seguintes novas funcionalidades de híbrida foram introduzidas no Outubro de 2016 para 1610 de pré-visualização técnica do Configuration Manager.

- **Pedir uma sincronização de política a partir da consola de administração**

  Pode pedir uma sincronização de política num dispositivo móvel inscrito da consola do Configuration Manager, em vez de necessário especificá-las solicitar a sincronização na aplicação do Portal da empresa no dispositivo automaticamente. Esta é uma nova ação denominada **enviar pedido de sincronização** no menu de ações de dispositivo remotas, que é apresentado no friso quando um dispositivo móvel é seleccionado no nó de dispositivos.

- **Definições de configuração do Windows Defender**

  Agora pode configurar as definições de cliente do Windows Defender em computadores Windows 10 inscritos Intune utilizar itens de configuração na consola do Configuration Manager. Existe um novo grupo de definição denominado **Windows Defender** no Assistente de Item de configuração. Tenha em atenção que isto é suportado apenas em 1511 de versão do Windows 10 e superior.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

Não existem novas funcionalidades de híbrida foram introduzidas no Agosto de 2016 para o Configuration Manager (ramo atual).

## <a name="new-hybrid-features-in-september-2016"></a>Novas funcionalidades de híbrida no Setembro de 2016

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas no Setembro de 2016 funcionam em implementações híbridas.

- **Adição de "Notificações" para o Portal da empresa para Android**

  Foi adicionado um novo ícone de notificações para o Portal da empresa para Android na home page. Tocar este ícone acede a página de notificações, que mostra aos utilizadores finais todos os itens que necessitam da atenção na aplicação do Portal da empresa, tais como não conformidade do dispositivo, atualização de inscrição e ativação de inscrição. A aplicação de Portal da empresa iOS, já tem esta experiência de notificações. Ter os meios de página nova notificações esse utilizador não verá a página de configuração de acesso de empresa sempre iniciar ou retomar o Portal da empresa, desde que o dispositivo já estar inscrito. Se criar as suas próprias orientações de utilizador final, pode querer atualizar a documentação para refletirem esta alteração. Encontrar capturas de ecrã atualizadas [aqui](https://aka.ms/androidcpupdate).

- **Alterações ao suporte para a aplicação de Portal da empresa iOS**

  Todos os utilizadores da aplicação do Portal da empresa do Microsoft Intune para iOS agora são necessários para utilizar a versão mais recente. Novos utilizadores são capazes de transferir apenas a versão mais recente, e os utilizadores atuais são necessárias para atualizar para o mesmo. A versão mais recente requer iOS 8.0 ou posterior, para que dispositivos que executam versões mais antigas do iOS não é possível utilizar o Portal da empresa ou inscrever até conseguirem atualizar os respetivos dispositivos iOS 8.0 ou posterior e, em seguida, atualizar a aplicação de Portal da empresa para a versão mais recente. Os dispositivos inscritos a executar versões abaixo iOS 8.0 irão continuar a ser geridos e listado na consola de administração do Intune.

- **Botão de comentários adicionado à aplicação Portal da empresa do Windows Phone 8.1**

  A aplicação de Portal da empresa do Windows Phone 8.1 permite aos utilizadores finais enviar comentários sobre a aplicação utilizando um novo botão "Enviar comentários". Para encontrar o botão, os utilizadores toque no menu de "reticências" na parte inferior direita do ecrã da aplicação de Portal da empresa e, em seguida, toque em **enviar comentários**. Os comentários recolhidos, são anónimos ajudarão a Microsoft a melhorar a experiência de aplicação do Portal da empresa para utilizadores.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Novo no Configuration Manager Technical Preview 1609

As seguintes novas funcionalidades de híbrida foram introduzidas no Setembro de 2016 para 1609 de pré-visualização técnica do Configuration Manager.

- **Definições adicionais e experiência melhorada para definições de Item de configuração**

  Foram adicionadas novas definições para Android, iOS e Windows e apenas as definições que se aplicam às plataformas que selecionou na página de plataformas suportadas são apresentadas no assistente. Para mais informações consulte [novas definições de compatibilidade para itens de configuração no TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Definições adicionais para perfis DEP**

  Foram adicionadas como as definições configuráveis nos perfis DEP para dispositivos iOS TouchID, ApplePay e Zoom.

- **Paga aplicações na loja Windows para empresas**

  Agora pode adicionar aplicações pagas e gratuitas para a loja Windows para empresas e implementá-los a utilizadores na sua organização. Para mais informações consulte [melhoramentos à loja Windows para empresas no TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Tipos de ligação nativo para perfis VPN do Windows 10**

  Agora pode criar perfis VPN do Windows 10 para MDM com Microsoft Automatic, IKEv2 e PPTP tipos de ligação na consola do Configuration Manager sem utilizar o OMA-URI.

- **Gráficos de conformidade do Intune**

  Pode obter uma vista rápida do dispositivo geral de início e de conformidade motivos para não utilizar gráficos de novo na área de trabalho monitorização conformidade. Para obter mais informações, consulte o artigo [gráficos de conformidade do Intune no TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

A seguinte nova funcionalidade introduzida no Setembro de 2016 está disponível para implementações híbridas com o Microsoft Intune e do Configuration Manager versão 1606 (ramo atual).

- **suporte do iOS 10**

  Se tiver perfis ou direcionadas para todas as plataformas de iOS de itens de configuração, estas serão também adiadas para iOS 10. Lançada-tenha também uma atualização para o Configuration Manager versão 1606 que lhe permite aos perfis de destino e itens de configuração para iOS individuais plataformas incluindo iOS 10. Pode instalar a atualização com a consola de administração do Configuration Manager em **administração > Descrição geral > Serviços em nuvem > atualizações e a manutenção**. Pode encontrar mais informações sobre a atualização na [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="new-hybrid-features-in-august-2016"></a>Novas funcionalidades de híbrida no Agosto de 2016

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas no Agosto de 2016 funcionam em implementações híbridas.

- **Suporte Android 7 na aplicação do Portal da empresa**

  Intune aplicação Portal da empresa para Android fornece suporte de "dia 0" para o sistema de operativo Android 7.0 forthcoming para dispositivos móveis.

- **Remoção do Google do código de acesso remoto repor capacidade em dispositivos Android 7.0**

  Google está a remover a capacidade dos administradores de TI e os utilizadores finais de remotamente repor o código de acesso de dispositivos Android 7.0. Anteriormente, os administradores de TI remotamente foi possível repor o código de acesso de um utilizador e os utilizadores finais foi possível repor os códigos de acesso a partir do Web site do Portal da empresa.

- **Política de aplicações permitidas e bloqueadas para dispositivos Samsung KNOX Standard**

  Agora pode configurar uma política personalizada para dispositivos Samsung KNOX Standard que lhe permite criar um dos seguintes procedimentos:

  - Uma lista de aplicações que estão bloqueados relativamente a ser executado no dispositivo. Mesmo que se instalada, uma aplicação definida na lista de bloqueados não pode ser ativada no dispositivo.
  - Uma lista de aplicações que os utilizadores do dispositivo estão autorizados a instalar a partir da Google Play store. Não existem outras aplicações podem ser instaladas da loja.

  Estas definições só podem ser utilizadas pelos dispositivos que executem o Samsung KNOX Standard. Para obter mais detalhes, consulte o artigo [utilizar as políticas personalizadas para permitir e bloquear aplicações para dispositivos Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Ligação de comentários no Portal da empresa para a Microsoft**

   O site do Portal da empresa permite aos utilizadores finais toque uma nova ligação de "Comentários do", na parte inferior da página, para enviar comentários à Microsoft sobre as respetivas experiências com o site. Os comentários recolhidos, são anónimos ajudarão a Microsoft a melhorar a experiência de Web site do Portal da empresa para utilizadores.

- **Versão de Browser gerido do iOS mínimo atualizado para 8.0**

  A aplicação de Browser gerido do Microsoft Intune para iOS tiver sido atualizada para suportar dispositivos que executam o iOS 8.0 ou posterior. Apesar dos dispositivos iOS 7.1 ainda podem utilizar a aplicação de Browser gerido existente, encoraje os seus utilizadores para atualizar para iOS 8.0 ou posterior ao access e tirar o máximo partido das novas funcionalidades de Browser gerido.

### <a name="new-in-configuration-manager-technical-preview"></a>Novidades do Configuration Manager Technical Preview

Não existem novas funcionalidades de híbrida foram introduzidas no Agosto de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

Não existem novas funcionalidades de híbrida foram introduzidas no Agosto de 2016 para o Configuration Manager (ramo atual).

## <a name="new-hybrid-features-in-july-2016"></a>Novas funcionalidades de híbrida no Julho de 2016

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas no Julho de 2016 funcionam em implementações híbridas.

- **SDK de Xamarin para aplicações do Intune está disponível**

  O componente de Xamarin de SDK do Intune App permite-lhe ativar as funcionalidades de gestão de aplicações móveis do Intune na sua móveis iOS e Android aplicações criadas com Xamarin. Pode encontrar o componente no [Xamarin arquivo](https://components.xamarin.com/view/Microsoft.Intune.MAM) ou no [página do Microsoft Intune Github](https://github.com/msintuneappsdk).

- **Experiência de utilizador final melhorada quando inscrever dispositivos Windows**

  Quando estiver a utilizar o acesso condicional, os passos de inscrição para o Windows 8.1, o ambiente de trabalho do Windows 10 e Windows 10 Mobile tem sido foi esclarecidos no Web site do Portal da empresa. Os utilizadores irão agora vê separado **inscrição de dispositivos** e **associação** passos, tornando mais fácil para os mesmos para ver o estado dos respetivos dispositivos e para concluir o processo se podem ocorrer uma falha de associação de área de trabalho (WPJ). Os passos separados também são esperados para simplificar o processo de resolução de problemas para administradores de TI. Anteriormente, quando os utilizadores finais tentou inscrever e todos os passos de inscrição foi concluída com êxito, exceto para WPJ, o dispositivo inscrito não aparecerá na lista de dispositivos para os utilizadores a identificar, a causar confusão para os utilizadores.

 - **Eliminação completa agora disponível para dispositivos Windows 10**

    Windows 10 PCs e portáteis inscritos como dispositivos móveis, podem ser apagados repor o dispositivo para as respetivas definições de fábrica. Para obter mais informações, consulte o artigo [como pretende proteger os seus dispositivos com a eliminação remota](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Muda para gestores de inscrição de dispositivos contas na aplicação de Portal da empresa iOS**

  Para melhorar o desempenho e dimensionamento, o Intune já não apresenta todos os dispositivos de gestores de inscrição de dispositivos (DEM) no painel de dispositivos da minha da aplicação de Portal da empresa iOS. Apenas o dispositivo local executar a aplicação é apresentado e apenas se este é inscrito através da aplicação de Portal da empresa.

  O utilizador DEM poderá executar ações no dispositivo local, mas só pode ser efetuada a gestão remota de outros dispositivos inscritos a partir da consola de administração do Intune. Além disso, o Intune é deprecating utilização de contas DEM com o programa de inscrição de dispositivos da Apple ou ferramenta Apple Configurator. Ambos os métodos de inscrição estas já suportem à inscrição de utilizadores para dispositivos iOS partilhado.

  Utilize contas DEM apenas quando a inscrição de utilizadores para dispositivos partilhados não está disponível. Para obter mais informações, consulte o artigo [inscrever os dispositivos da empresa com o Gestor de inscrição do dispositivo no Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Alterações para a aplicação do Portal da empresa Android**

  Se os utilizadores finais Android ver uma mensagem de erro que diz o respetivo dispositivo está em falta um certificado necessários, estes podem toque um botão "Como resolver este problema" ao obter os passos para instalar o certificado em falta. Se os utilizadores de concluir os passos, mas consulte um adicional "em falta certificado" mensagem de erro, são-lhe pedidos para contactar o administrador de TI e forneça esta ligação, que inclua os passos que os administradores de TI podem utilizar para corrigir o problema do certificado.

- **Restringir as instalações da aplicação side-loaded inscritos em dispositivos Android**

  Dispositivos Android já não podem instalar aplicações através do Web site do Portal da empresa, a menos que os dispositivos que tenham sido inscritos no Intune através da aplicação Portal da empresa do Intune para Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Novidades do Configuration Manager Technical Preview

Não existem novas funcionalidades de híbrida foram introduzidas no Julho de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que se encontravam anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com Intune e Configuration Manager (ramo atual) versão 1606.

* Localizar, gerir e distribuir da loja Windows para aplicações de negócio para dispositivos Windows 10 a partir da consola do Configuration Manager ([1604](#new-in-1604-technical-preview))
*     Definição de SmartLock para dispositivos Android ([1604](#new-in-1604-technical-preview))
*    Dispositivos de VPN para o Windows 10 acionado de aplicação ([1605](#new-in-1605-technical-preview))
*    Nova experiência de ações de remota do dispositivo ([1605](#new-in-1605-technical-preview))
*    Loja Windows para aplicações empresariais ([1605](#new-in-1605-technical-preview))
*    Melhoramentos gerais para aplicações adquirido de volume ([1605](#new-in-1605-technical-preview))
*    Proteção de informações do Windows (WIP) ([1605](#new-in-1605-technical-preview))
*    Pré-declarar os dispositivos da empresa com o número de série IMEI ou iOS ([1605](#new-in-1605-technical-preview))
*    Categorizar automaticamente dispositivos para coleções ([1606](#new-in-1606-technical-preview))

Para obter informações sobre a nova funcionalidade, consulte a documentação para a versão de pré-visualização técnica especificada.

## <a name="new-hybrid-features-in-june-2016"></a>Novas funcionalidades de híbrida no de 2016 de Junho

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune
As seguintes funcionalidades do Intune introduzidas no Junho de 2016 funcionam em implementações híbridas.

- **Estado de funcionamento do serviço do Intune** informações de estado de funcionamento do serviço do Intune foi movidas para uma localização central com outros serviços Microsoft. Agora irá encontrar estas informações no portal de gestão do Office 365 em estado de funcionamento do serviço. Para obter mais informações, consulte este [mensagem no blogue](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Experiência melhorada configuração de política de dados do Windows 10 enterprise**

  Intune tem agora uma experiência melhorada para configurar a política de proteção de informações do Windows 10. Melhoramentos incluem melhores formas de criar regras de aplicação, especifique a definição de limite de rede bem como outras definições de proteção de informações do Windows. Para obter mais informações, consulte o artigo [criar uma política de proteção de informações do Windows (WIP) através do Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Política de controlo do acesso do Cisco ISE rede para o Intune**

  Os clientes que utilizam a Cisco identidade de serviço de motor (ISE) 2.1 e também utilizam o Microsoft Intune podem definir uma política de controlo de acesso de rede na ISE. Utilizar esta política, dispositivos que precisa de ligar à rede através de Wi-Fi ou VPN tem de cumprir as seguintes condições antes de estes são permissão de acesso:

  - Tem de ser gerido pelo Intune
  - Deve ser compatível com as políticas de conformidade implementadas do Intune

  Os utilizadores finais de dispositivos não conformes serão solicitados para inscrever e retificar quaisquer problemas de compatibilidade para obter acesso.

- **Acesso condicional para o browser**

  Pode definir uma política de acesso condicional para Exchange Online e SharePoint Online para que apenas possa ser acedidos a partir de browsers suportados em dispositivos geridos e conformes iOS e Android. Os utilizadores finais que tenta iniciar sessão Outlook Web Access (OWA) e o SharePoint sites com dispositivos iOS e Android serão solicitados para inscrever os respetivos dispositivos com o Intune, bem como a corrigir quaisquer problemas de não conformidade, antes de poderem podem concluir início de sessão. Para mais informações, consulte

  * [Restringir o acesso ao e-mail com o Exchange Online e novo Exchange Online dedicado com o Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restringir o acesso ao SharePoint Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online suporta acesso condicional**

  Pode definir uma política de acesso condicional para o Dynamics CRM Online para que apenas possa ser acedido por dispositivos geridos e conformes iOS e Android. Os utilizadores finais que tenta iniciar sessão aplicação móvel no iOS e Android Dynamics CRM serão pedidos ao inscrever-se com o Intune, bem como para retificar quaisquer problemas de não conformidade, antes de início de sessão pode concluir. Para obter mais informações, consulte o artigo [restringir o acesso ao Dynamics CRM Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Atualizações da aplicação Portal da empresa Android**

  Intune tem agora as seguintes novas políticas que irão afetar os utilizadores do Portal da empresa Android:   

  Política  |Efeito de utilizadores  
  ---------|---------
  Exigir que dispositivos não permitir a instalação de aplicações a partir de origens desconhecidas (Android 4.0 +)     |  Os utilizadores finais com Android 4.0 ou posterior irão ver a mensagem, "Tem de ser desativada instalação a partir de origens desconhecidas." Os utilizadores terão de ir para **definições > segurança** os respetivos dispositivos e desative a funcionalidade de **origens desconhecidas**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obter mais informações sobre a mensagem e por que motivo estão a ser necessários para desativar a definição.
  Exigir que dispositivos não permitir a instalação de aplicações a partir de origens desconhecidas (Android 4.0 +)  |    Os utilizadores finais com Android 4.0 ou posterior irão ver a mensagem, "De análise de dispositivo para ameaças de segurança." Os utilizadores terão de ir para **definições > Google > segurança** os respetivos dispositivos e ative **dispositivo de análise de ameaças de segurança**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obter mais informações sobre a mensagem e por que motivo estão a ser necessários para ativar a definição.     
  Exigir que USB depuração está desativado (Android 4.2 +)  | Os utilizadores finais com Android 4.2 ou posterior irão ver a mensagem, "USB depuração deve ser desativada." Os utilizadores terão de ir para **definições > Opções de programador** os respetivos dispositivos e desative a funcionalidade de **USB depuração**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obter mais informações sobre a mensagem e por que motivo estão a ser necessários para desativar a definição.
  Nível de patch de segurança Android mínimas (Android 6.0 +)  | Os utilizadores finais com Android 6.0 ou posterior irão ver a mensagem, "este dispositivo não cumpre o nível de patch de segurança Android mínimas." Os utilizadores terão de instalar o patch de segurança necessárias. Uma ligação na mensagem de compatibilidade permite aos utilizadores obter informações sobre como instalar o patch de segurança necessárias e para ver qual patch de segurança que tem atualmente instalado.

- **Atualizações da aplicação de Portal da empresa iOS**

  * Quando os utilizadores finais estiverem a instalar aplicações de linha de negócio, irão agora vê uma instalação de aplicações melhorada experiência. Se a instalação da aplicação está a demorar muito tempo, os utilizadores podem sincronizar manualmente os respetivos dispositivos para forçar o processo de sincronização para retomar. Para rever as instruções do utilizador final, consulte manualmente a sincronização do seu dispositivo iOS.
  * Aplicação do Portal da empresa do Microsoft Intune para iOS tem sido atualizada para suportar o iOS versão 8.0 e posterior. Esta atualização significa que os utilizadores finais podem instalar a aplicação de Portal da empresa e inscrever novos dispositivos no Intune apenas se o dispositivo está a executar o iOS versão 8.0 ou posterior. Os utilizadores que já inscreveram dispositivos que executem uma versão não suportada do iOS podem continuar a utilizar a aplicação de Portal da empresa que está nos dispositivos deles.


### <a name="new-in-1606-technical-preview"></a>Novo no 1606 pré-visualização técnica
As seguintes funcionalidades novas introduzidas no Junho de 2016 estão disponíveis em implementações híbridas com Intune e 1606 de pré-visualização técnica do Configuration Manager.

- **Categorizar automaticamente os dispositivos em coleções**

  Pode criar categorias de dispositivo, o que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando está a utilizar o Configuration Manager com o Intune. Os utilizadores, em seguida, são necessários para escolher uma categoria de dispositivo quando estes inscreverem um dispositivo no Intune. Além disso pode alterar a categoria de um dispositivo a partir da consola do Configuration Manager. Para obter mais informações, consulte o artigo [automaticamente categorizar dispositivos em coleções](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) no [funcionalidades no 1606 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > Esta capacidade é funciona com a versão de Junho de 2016 do Microsoft Intune. Certifique-se de que lhe foram atualizadas para esta versão antes de experimentar estes procedimentos.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)
Não existem novas funcionalidades de híbrida foram introduzidas em Junho de 2016 para o Configuration Manager (ramo atual).

##  <a name="new-hybrid-features-in-may-2016"></a>Novas funcionalidades de híbrida no Maio de 2016  

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas no Maio de 2016 funcionam em implementações híbridas.

- **MAM SDK: Configuração de comprimento PIN de suporte**

  Já pode especificar o comprimento do PIN para aplicações MAM semelhantes a um PIN de dispositivo. Isto requer que os utilizadores finais estar em conformidade com as restrições novo definiu. O ecrã PIN é ligeiramente modificado à conta para a entrada mais. Para obter mais detalhes, consulte o artigo [definições de política MAM para Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings), e [definições de política MAM para iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype para empresas para iOS e Android**

  Agora pode visar Skype para empresas com [MAM sem políticas de inscrição](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Depois dos utilizadores a iniciar sessão, as políticas MAM serão aplicadas.  

- **Novas aplicações disponíveis para a gestão com as políticas de MAM**

  As aplicações do Microsoft Word, Excel e PowerPoint para Android podem agora ser associadas a políticas MAM nos dispositivos que não estão inscritos no Intune. Para obter uma lista completa de aplicações suportadas, aceda a Galeria de aplicações móveis do Microsoft Intune no [parceiros de aplicações do Microsoft Intune](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) página.  

- **Aplicação do portal da empresa Android: Notificações de toast do utilizador final**

  Toast notificações da aplicação Portal da empresa Android aparecem quando os utilizadores finais inscrever ou remover os respetivos dispositivos no Portal da empresa.  

- **Site do Portal da empresa: Faixa de identificação do dispositivo irá fornecer mais informações aos utilizadores finais**

  Os utilizadores finais pode atualmente identificar mais facilmente o dispositivo que selecionou quando estão a utilizar o Web site do Portal da empresa. Se o dispositivo errado estiver selecionado, podem selecionar o dispositivo correto tocando o **toque aqui** ligação na faixa página inicial.  


### <a name="new-in-1605-technical-preview"></a>Novo no 1605 pré-visualização técnica  
 As seguintes funcionalidades novas introduzidas no Maio de 2016 estão disponíveis em implementações híbridas com Intune e 1605 de pré-visualização técnica do Configuration Manager. Estas funcionalidades necessitam que utilize a consola do Configuration Manager para configurar e geri-los.  

- **Aplicação acionada dispositivos VPN para o Windows 10**

  Para dispositivos Windows 10 geridos através do Configuration Manager com o Intune, pode adicionar uma lista de aplicações que abra automaticamente uma ligação de VPN que tiver configurado através da consola do administrador do Configuration Manager. Para obter mais informações, consulte o artigo [dispositivos acionado aplicação VPN para Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1605) no [funcionalidades no 1605 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nova experiência de ações de remota do dispositivo**

  A experiência para realizar ações de remota do dispositivo a partir da consola do Configuration Manager foi melhorada.

  Ações comuns, tais como **extinguir/apagar**, **repor o código de acesso**, **bloqueio remoto**, e **omissão de bloqueio de ativação** agora pode ser encontrado no **ações de dispositivo remotas** acedido a partir do menu a **ativos e compatibilidade** área de trabalho

  Para obter mais informações, consulte o artigo [nova experiência de ações de dispositivo remoto](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) no [funcionalidades no 1605 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Para aplicações de empresas da loja Windows**

  O [da loja Windows para empresas](https://www.microsoft.com/en-us/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar-se no arquivo do Configuration Manager, pode gerir aplicações adquirido o volume a partir da consola do Configuration Manager. Para obter mais informações, consulte o artigo [da loja Windows para aplicações de negócio](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) no [funcionalidades no 1605 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Melhoramentos gerais para aplicações adquirido de volume**

  Comprou volume aplicações a partir da loja Windows para empresas e iOS app store tem sido consolidadas na mesma vista, **informações de licença para armazenar aplicações**. Além disso, a forma na qual criar adquirido volume aplicações para iOS foi melhorada. Para obter mais informações, consulte o artigo[melhoramentos gerais para aplicações adquirido volume](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) no [funcionalidades no 1605 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Pré-declarar os dispositivos da empresa com o número de série IMEI ou iOS**

  Agora pode identificar dispositivos pertencentes ao importar os seus números de identidade (IMEI) do estação internacional do equipamento móvel. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI do dispositivo ou pode introduzir manualmente as informações de dispositivo.  Também pode importar os números de série para dispositivos iOS.  Para obter mais informações, consulte o artigo [previamente declarar os dispositivos da empresa com o número de série IMEI ou iOS](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) no [funcionalidades no 1605 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Proteção de informações do Windows (WIP)**

  Pode criar itens de configuração que permitem-lhe implementar as políticas de proteção de informações do Windows (WIP), incluindo permitindo que a escolher as suas aplicações protegidas, o nível de proteção WIP e como localizar dados empresariais na rede. Para mais informações sobre WIP, consulte os seguintes tópicos:  

  -   [Proteger os dados de empresa através da proteção de informações do Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Criar e implementar uma política de proteção de informações do Windows (WIP) com o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 Não existem novas funcionalidades de híbrida foram introduzidas na Maio de 2016 para o Configuration Manager (ramo atual).  

##  <a name="new-hybrid-features-in-april-2016"></a>Novas funcionalidades de híbrida no Abril de 2016  

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas no Abril de 2016 funcionam em implementações híbridas.  

- **Conformidade de utilizadores MAM**

  Agora pode ver o estado das suas políticas de gestão de aplicação para qualquer utilizador no seu inquilino do Azure Active Directory (AAD).  Para mais informações consulte [monitorizar as políticas de gestão de aplicações móveis com o Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Controlos de MAM para impedir a sincronização de contactos do Outlook (Android)**

  Está disponível uma nova definição que permite-lhe impedir que uma aplicação de sincronização de contactos ao livro de endereços nativo em dispositivos Android. Esta nova definição é inicialmente suportada pela aplicação Outlook em dispositivos Android. Para obter mais informações, consulte o artigo [criar e implementar políticas de gestão de aplicações móveis com o Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Melhoramentos para o site do Portal da empresa**

  Quando os utilizadores do Windows 10 Mobile e Windows Phone 8.1 estiverem a instalar aplicações de linha de negócio, irão agora vê os seguintes Estados novos, que dê-lhes mais detalhes sobre o estado da instalação:  

  -   **A aguardar que o dispositivo sincronizar** – o utilizador tem tocou "Instalar" e o dispositivo agora tentará sincronizar com a infraestrutura do Intune. A sincronização é obrigatório para pode concluir a instalação. A mensagem "Aguardar que o dispositivo sincronizar" também é uma ligação que os utilizadores podem tocar para ver as instruções sobre como sincronizar manualmente o respetivo dispositivo no Intune se o processo de sincronização está a demorar muito tempo ou obtém parado.  

  -   **Transferir** – o pedido de transferência do utilizador está a ser processado e que o dispositivo é transferir e instalar a aplicação.  

- **Melhoramentos para a aplicação do portal da empresa Android**

  Os utilizadores que não tenham inscritos os respetivos dispositivos no Intune e que não têm o certificado correto instalado não será possível iniciar sessão na aplicação de Portal da empresa Android e irão ver a mensagem, "Não é possível iniciar sessão porque o seu dispositivo está em falta um certificado necessário." A mensagem inclui uma ligação de "Como resolver este problema" que os utilizadores podem tocar para ver as instruções para instalar o certificado. Para ver os passos que os utilizadores finais seguir para resolver o problema, consulte o artigo [seu dispositivo está em falta um certificado necessários](/intune/enduser/using-your-android-device-with-intune) na biblioteca do Intune.  

- **Melhoramentos à aplicação de Portal da empresa do iOS**

  Foi adicionado suporte para a ação de atualização de solicitação atualizar o conteúdo no ecrã principal, que inclui as aplicações indicadas, dispositivos listados e contacto de TI informações. A ação de atualização de solicitação não verifica se existem informações de conformidade ou a política, que podem ser efetuadas ao selecionar o mosaico para o seu dispositivo atual e ao tocar o **sincronização** botão.  

- **Melhorias na aplicação de Portal do Windows 10 Mobile e da empresa do Windows Phone 8.1**

  Quando os utilizadores finais estiverem a instalar aplicações de linha de negócio, irão agora vê uma instalação de aplicações melhorada experiência. Se a instalação da aplicação está a demorar muito tempo, os utilizadores podem sincronizar manualmente os respetivos dispositivos para forçar o processo de sincronização para retomar. Para rever as instruções do utilizador final, consulte o artigo [sincronizar o seu dispositivo manualmente para acelerar a instalações de aplicações](/intune/enduser/using-your-windows-device-with-intune) na biblioteca do Intune.  

###  <a name="new-in-1604-technical-preview"></a>Novo no 1604 pré-visualização técnica
 As seguintes funcionalidades novas, introduzidas no Abril de 2016 estão disponíveis em implementações híbridas com Intune e 1604 de pré-visualização técnica do Configuration Manager. Estas funcionalidades necessitam que utilize a consola do Configuration Manager para configurar e geri-los.  

- **Localizar, gerir e distribuir da loja Windows para aplicações de negócio para dispositivos Windows 10 a partir da consola do Configuration Manager**


  Suporte para a loja Windows para empresas está disponível no Configuration Manager técnica 1604 de pré-visualização para o ajudar a localizar, gerir e distribuir aplicações para dispositivos Windows 10 que estiver gerir. Para obter mais detalhes, consulte o artigo [gerir adquirido volume aplicações da loja Windows para empresas](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) no [funcionalidades no 1604 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Definição de SmartLock para dispositivos Android**

  Foi adicionada uma nova definição para o item de configuração do Android e Samsung KNOX Standard que lhe permite controlar a funcionalidade de SmartLock em dispositivos Android compatíveis.  Pode utilizar esta definição para impedir que os utilizadores finais SmartLock a configurar. Consulte o artigo [SmartLock definição para dispositivos Android](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) no [funcionalidades no 1604 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 Não existem novas funcionalidades de híbrida foram introduzidas no Abril de 2016 para o Configuration Manager (ramo atual).  

##  <a name="new-hybrid-features-in-march-2016"></a>Novas funcionalidades de híbrida no Março de 2016  

### <a name="new-in-microsoft-intune"></a>Novidades no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas em Março de 2016 funcionam em implementações híbridas.  

- **Controlos de MAM para impedir a sincronização de contactos do Outlook (iOS)**

  Está disponível uma nova definição que permite-lhe impedir que uma aplicação de sincronização de contactos ao livro de endereços nativo em dispositivos iOS. Esta nova definição é suportada pela aplicação do Outlook em dispositivos iOS. Para obter mais detalhes acerca desta e outras definições, consulte o artigo [criar e implementar políticas MAM](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Skype para empresas Online suporta acesso condicional**

  Pode definir uma política de acesso condicional para o Skype para empresas Online para que apenas possa ser acedido por dispositivos geridos e conformes iOS e Android.  Para obter mais detalhes, consulte o artigo [gerir o acesso a Skype para empresas Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) na biblioteca do Intune.  

- **Suporte para iOS 9.3**

  Na segunda 21 de Março, Apple comunicadas a disponibilidade de iOS 9.3. Todas as funcionalidades existentes do Intune atualmente disponíveis para gerir dispositivos iOS irão continuar a funcionar de forma totalmente integrada como utilizadores atualizam os respetivos dispositivos para iOS 9.3.  

- **Pacotes de aplicações do Windows disponíveis diretamente a partir do Web site do Portal da empresa**

  Os utilizadores do Windows 8, Windows 8.1 e Windows RT PCs poderá agora instalar pacotes de aplicações do Windows (com a extensão de ficheiro. AppX) diretamente a partir do Web site do Portal da empresa. Anteriormente, era necessário que implementar ou utilizadores tinham que instalar a aplicação de Portal da empresa nos respetivos dispositivos para instalar aplicações.  

- **Os utilizadores podem bloquear remotamente o dispositivo a partir do Web site do Portal da empresa**

  Foi adicionada uma nova opção de bloqueio remoto para o Web site do Portal da empresa para permitir aos utilizadores bloquear remotamente o respetivo dispositivo a partir do Portal se o dispositivo é perdido ou roubado.  

- **Tirar partido do iOS "Abrir em" gestão de dispositivos inscritos numa solução MDM do fornecedor de terceiros**

  Pode utilizar o seu fornecedor de gestão (MDM) de dispositivos móveis de terceiros para tirar partido do iOS "Abrir em" gestão. Pode configurar as restrições na configuração de definições de perfil e implementar a aplicação utilizando o software MDM. Quando o utilizador instala a aplicação gerida por, são aplicadas as restrições. Ler os detalhes: [Políticas de gestão de aplicações móveis do Microsoft Intune e iOS abrir em](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) na biblioteca do Intune.  

- **Aplicações da Microsoft que suportam MAM**

  A lista de aplicações da Microsoft que pode utilizar com políticas de gestão de aplicações móveis do Intune tiver sido atualizada para incluir as aplicações mais recentes (para dispositivos inscritos com o Intune apenas).  

- **Implementar o Adobe Reader para o Microsoft Intune para iOS gerido pelo Intune dispositivos na sua empresa**

  A Adobe Reader a aplicação para iOS pode agora ser gerida em dispositivos inscritos com a política de gestão de aplicações móveis do Intune.  

- A aplicação de partilha Rights Management é suportada para Android

  Os administradores de TI podem implementar políticas de gestão de aplicações móveis para que os utilizadores finais possam ver imagens, AV e PDF ficheiros de forma mais segura, quer esteja ou não IT utiliza o Intune para gerir os dispositivos.  

- **Melhoramentos para a aplicação de Portal da empresa iOS e Android**

  -   Quando os seus utilizadores iniciar uma aplicação que é gerida pelo gestão de aplicações móveis (MAM), verão uma mensagem notificá-los de que a aplicação é gerida pela sua empresa. Os utilizadores agora podem tocar numa ligação "Mais informações" para obter mais informações aqui sobre o que significa "aplicações geridas". Eles também podem tocar "Não mostrar novamente" para que a mensagem deixa de aparecer ao poderem iniciar a aplicação.  

  -   Foram adicionadas novas ecrãs guia utilizadores através do processo de inscrição e fornecer mais informações sobre a razão pela qual os utilizadores devem inscrever e o que os administradores de TI podem e não é possível ver nos respetivos dispositivos inscritos.  

  -   Mensagens de erro de inscrição são agora apresentadas na aplicação do Portal da empresa.  

### <a name="new-in-configuration-manager-technical-preview"></a>Novidades do Configuration Manager Technical Preview  
 Não existem novas funcionalidades de híbrida foram introduzidas no Março de 2016 para o Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 As seguintes funcionalidades novas introduzidas em Março de 2016 estão disponíveis em implementações híbridas com Intune e Configuration Manager (ramo atual) versão 1602. Estas funcionalidades necessitam que utilize a consola do Configuration Manager para configurar e geri-los.  

- **políticas de configuração de aplicação iOS**

  Na versão 1602 do Configuration Manager (ramo atual) pode utilizar as políticas de configuração de aplicação para fornecer definições que poderão ser necessárias quando o utilizador executa uma aplicação iOS. Para obter mais detalhes, consulte o artigo [configurar aplicações iOS com as políticas de configuração da aplicação no System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Gerir as aplicações iOS adquiridos de volume**

  Na versão 1602 do Configuration Manager (ramo atual), pode implementar e gerir as aplicações que comprou no volume a partir do programa de compra de Volume do Apple (VPP) ao importar as informações da licença da loja de aplicações e controlar o número das licenças que utilizou. Para obter mais detalhes, consulte o artigo [gerir as aplicações iOS adquirido o volume com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Criação automática de aplicações móveis do Office**

  A partir na versão 1602 do Configuration Manager (ramo atual), são criadas as seguintes aplicações móveis Microsoft Office para Android e iOS ao atualizar a partir da versão 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (apenas iOS)  
  -   Microsoft Outlook  

  Irá encontrar estas aplicações no nó de aplicações da consola do Configuration Manager. Para obter mais informações sobre a implementação de aplicações, consulte o artigo [como implementar aplicações com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Definições do modo de local público para dispositivos Android Samsung KNOX Standard**

  O modo Kiosk permite-lhe bloquear um dispositivo e permitir que apenas determinadas funcionalidades funcionem.  A partir na versão 1602 do Configuration Manager (ramo atual), já pode especificar definições do modo de local público para dispositivos Samsung KNOX Standard. Para obter mais detalhes, consulte o artigo [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard geridos sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **iOS bloqueio de ativação**

  A partir na versão 1602 do Configuration Manager (ramo atual), pode gerir bloqueio de ativação, uma funcionalidade do meu iPhone a aplicação para iOS 7.1 localizar dispositivos iOS e posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo.  Para obter mais detalhes, consulte o artigo [gerir iOS bloqueio de ativação ignorar para o System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  

