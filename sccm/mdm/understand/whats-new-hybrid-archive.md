---
title: "Arquivo de Novidades híbridas novo MDM"
titleSuffix: Configuration Manager
description: "Arquivo de últimos funcionalidades de gestão de dispositivos móveis disponíveis para implementações híbridas com o System Center Configuration Manager e o Intune."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: dougeby
ms.author: dougeby
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 23b43e85a0ad698a377f51ce4b0d70fe197e9344
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Últimos híbrida funcionalidades com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre o dispositivo móvel passado funcionalidades de gestão (MDM) disponíveis para implementações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada secção deste artigo apresenta uma lista de funcionalidades híbridas em 3 diferentes categorias. Utilize as seguintes orientações para determinar a compatibilidade das funcionalidades em cada categoria com diferentes versões do Configuration Manager:  

|Categorias de funcionalidade|
|-|  
|**Novo no Microsoft Intune** -em geral, todas as funcionalidades listadas nesta categoria devem funcionar com todas as versões do Configuration Manager, incluindo versões do System Center 2012 R2 Configuration Manager, uma vez que estas funcionalidades apenas requerem o serviço do Intune e não necessitam de funcionalidades adicionais no Configuration Manager.<br /><br /> **Novo no Configuration Manager Technical Preview** -todas as funcionalidades listados desta categoria só funcionam com a versão de pré-visualização técnica especificada. Para experimentar estas funcionalidades, tem de instalar a versão de pré-visualização técnica especificada na descrição da funcionalidade. Para obter mais informações, consulte [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Novo no Configuration Manager (ramo atual)** -todas as funcionalidades listados neste trabalho única categoria com a versão especificada do Configuration Manager (ramo atual), tais como a versão 1511 ou 1602. Se estiver a utilizar uma versão mais antiga do Configuration Manager para a implementação híbrida, tem de atualizar para a versão do Configuration Manager (ramo atual) especificada na descrição da funcionalidade. Para obter mais informações, consulte [atualizar para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="december-2016"></a>Dezembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Autenticação Multifator (MFA) durante a inscrição está a mover para o portal do Azure**

  Anteriormente, passará a consola do Intune ou a consola do Configuration Manager para configurar a MFA para inscrições através do Intune. Com esta funcionalidade atualizada, pode agora iniciar sessão no [portal do Microsoft Azure] (https://manage.windowsazure.com) com o Intune credenciais e configurar as definições da MFA através do Azure AD. Para obter mais informações, consulte [multi-factor authentication do Microsoft Intune] (https://aka.ms/mfa_ad).

- **Aplicação do Portal da empresa para Android, agora disponível na China**

  A aplicação Portal da empresa para Android está agora disponível na China. Devido à ausência do Google Play Store na China, dispositivos Android tem de obter aplicações da marketplaces aplicação chinês. A aplicação Portal da empresa para Android está disponível para transferência nos arquivos de seguintes:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  A aplicação Portal da empresa para Android utiliza serviços Google Play para comunicar com o serviço Microsoft Intune. Uma vez que os serviços Google Play ainda não estão disponíveis na China, efetuar qualquer uma das seguintes tarefas pode demorar até 8 horas a concluir.

  | Consola de administração do Configuration Manager | Aplicação do Portal da empresa do Intune para Android | Site de Portal da empresa do Intune |
  |----|----|----|      
  | Extinguir/apagar (remover todos os dados)   | Remover um dispositivo remoto | Remover dispositivo (local e remoto) |
  | Extinguir/apagar (remover dados de empresa)   | Repor o dispositivo | Repor o dispositivo|
  | Implementações de aplicação nova ou atualizada | Instalar aplicações de linha de negócio disponíveis | Repor código de acesso de dispositivo|
  | Bloqueio remoto | | |
  | Repor código de acesso | | |        


## <a name="november-2016"></a>Novembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Portal da empresa do Intune Microsoft novo disponível para dispositivos Windows 10**

  Microsoft lançou um novo [aplicação do Portal da empresa para dispositivos Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Esta aplicação, que aproveita o novo formato Universal do Windows 10, fornece uma experiência de utilizador atualizado que é idêntica em todos os dispositivos Windows 10, o PC e Mobile igual, permitindo as mesmas funcionalidades fornecidas pelo anteriores aplicações do Portal da empresa.

  A nova aplicação tira partido das funcionalidades de plataforma como-início de sessão único (SSO) e a autenticação baseada em certificado em dispositivos Windows 10. A aplicação está disponível como uma atualização para o Portal de empresa de existente do Windows 8.1 e instala o Portal da empresa do Windows Phone 8.1 a partir da loja Windows. Para obter mais detalhes, visite o [blogue da equipa de suporte do Intune](http://aka.ms/intunecp_universalapp).

  A nova aplicação do Portal da empresa também apresenta qualquer loja Windows para aplicações empresariais marcadas **disponível** na consola do Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que se encontravam anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1610.

* [Definições adicionais e experiência melhorada para itens de configuração](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Definições adicionais para perfis DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Paga aplicações na loja Windows para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipos de ligação de nativo para perfis de VPN do Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Gráficos de conformidade do Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Pedido para sincronização de política a partir da consola](/sccm/mdm/deploy-use/sync-intune-device)
* [Definições de configuração do Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

As seguintes funcionalidades adicionais híbrida também estão incluídas na versão 1610 do Configuration Manager (ramo atual):

- **Aumento do número de dispositivos inscritos**

  Agora pode permitir aos utilizadores inscrever dispositivos até 15. O limite anterior era 5 dispositivos por utilizador.


- **Suporte de segurança adicionais**

  Para além de administrador global, as seguintes funções de segurança incorporadas agora tem acesso total aos itens no nó de todos os dispositivos de empresa, incluindo dispositivos Predeclared, perfis de inscrição de iOS e perfis de inscrição do Windows:

    - Gestor do Asset Intelligence
    - Gestor de acesso a recursos da empresa

  Acesso só de leitura para estas áreas da consola do Configuration Manager ainda é concedido para a função do analista só de leitura.

- **Acesso VPN de acionamento automático de aplicações do Windows Information Protection**

  Pode adicionar um domínio principal do Windows Information Protection para perfis de VPN do Windows 10 que faz com que todas as aplicações associadas a acionar automaticamente uma ligação VPN quando são executados no dispositivo. Esta opção só está disponível ao escolher um tipo de ligação nativo.

- **Acesso condicional para perfis de VPN do Windows 10**

    Agora pode exigir a Windows 10 dispositivos inscritos no Azure Active Directory para estar em conformidade para ter acesso VPN através de perfis de VPN do Windows 10 criadas na consola do Configuration Manager. Isto é possível através de novo **ativar o acesso condicional para esta ligação VPN** caixa de verificação na página do método de autenticação no Assistente do perfil VPN e propriedades de perfil VPN para perfis de VPN do Windows 10. Esta opção só está disponível ao escolher um tipo de ligação nativo.

    Também pode especificar um certificado diferente para autenticação de início de sessão único se ativar o acesso condicional para o perfil.

## <a name="october-2016"></a>Outubro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas no Outubro de 2016 funcionam em implementações híbridas.

- **Acesso condicional para gestão de aplicações móveis**

  Pode restringir o acesso ao Exchange Online, para que o acesso é fornecido apenas a partir de aplicações que suportam as políticas de gestão de aplicações móveis do Intune como o Outlook. [Esta nova funcionalidade](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) pares perfeitamente com políticas de gestão (MAM) de aplicações móveis do Intune, pode bloquear o acesso para clientes de correio incorporado ou outras aplicações que não tenham sido configuradas com as políticas de MAM do Intune. Isto garante que os utilizadores acedem aos dados da sua organização com as aplicações que podem ser protegidos através de MAM do Intune. Pode começar a utilizar na gestão de aplicações móveis do Intune através do portal do Azure. Procure a nova secção de acesso condicional no painel "Definições".

-   **Ferramenta de encapsulamento de aplicações do Intune para Android**

  Pode ativar as suas aplicações a utilizar políticas de gestão (MAM) de aplicações móveis do Intune utilizando a ferramenta de encapsulamento de aplicações do Intune.

- **Compatibilidade Samsung KNOX Standard Android com o Intune**

  Determinados modelos de telemóvel Samsung Galaxy Ace não podem ser geridos pelo Intune, como dispositivos Samsung KNOX Standard. Quando inscrever estes dispositivos com o Intune, em vez disso, irá ser geridos como dispositivos Android padrão.

  Os números de modelo afetados são:

  - SM G313HU
  - SM G313HY
  - SM G313M
  - SM G313MY
  - SM G313U

  E os utilizadores finais não precisa de tomar nenhuma ação adicional. Para obter mais informações, visite o Web site do Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Novo no Configuration Manager Technical Preview 1610

As novas funcionalidades híbridas foram introduzidas no Outubro de 2016 para 1610 de pré-visualização técnica do Configuration Manager.

- **Pedir uma sincronização de política a partir da consola do administrador**

  Pode pedir uma sincronização de política num dispositivo móvel inscrito da consola do Configuration Manager, em vez de necessidade de solicitar a sincronização na aplicação Portal da empresa no dispositivo propriamente dito. Esta é uma nova ação chamada **enviar pedido de sincronização** no menu ações do dispositivo remoto, que aparece no friso quando um dispositivo móvel é selecionado o nó de dispositivos.

- **Definições de configuração do Windows Defender**

  Agora, pode configurar as definições de cliente do Windows Defender em computadores Windows 10 inscritos no Intune, utilizar itens de configuração na consola do Configuration Manager. Há um novo grupo de definição chamado **Windows Defender** no Assistente de Item de configuração. Tenha em atenção que isto é suportado apenas no Windows 10 versão 1511 e superior.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

Não existem novas funcionalidades híbridas foram introduzidas no Agosto de 2016 para o Configuration Manager (ramo atual).

## <a name="september-2016"></a>Setembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas Setembro de 2016 funcionam em implementações híbridas.

- **Inclusão de "Notificações" no portal da empresa para Android**

  Foi adicionado um novo ícone de notificações no portal da empresa para Android na home page. Tocar neste ícone acede a página de notificações, que mostra os utilizadores finais todos os itens que requerem atenção na aplicação Portal da empresa, como não conformidade de dispositivo, atualizações de inscrições e ativação da inscrição. A aplicação Portal da empresa iOS já tem esta experiência de notificações. Com os novos significa de página de notificações que o utilizador não verão a página de configuração de acesso da empresa sempre iniciar ou retomar o Portal da empresa, desde que o dispositivo já está inscrito. Se criar a sua própria documentação de orientação do utilizador final, pode querer atualizar a documentação para refletir esta alteração. Capturas de ecrã atualizadas [aqui](https://aka.ms/androidcpupdate).

- **Alterações ao suporte para a aplicação do Portal da empresa iOS**

  Todos os utilizadores da aplicação do Portal da empresa do Microsoft Intune para iOS são agora necessárias para utilizar a versão mais recente. Os novos utilizadores são capazes de transferir apenas a versão mais recente e os utilizadores atuais são necessários para atualizar para a mesma. A versão mais recente requer o iOS 8.0 ou posterior, para que os dispositivos que executem versões anteriores do iOS não é possível utilizar o Portal da empresa nem inscrever enquanto os atualizarem para o iOS 8.0 ou posterior e, em seguida, atualizar a aplicação do Portal da empresa para a versão mais recente. Os dispositivos inscritos que executem versões anteriores ao iOS 8.0 continuarão a ser geridos e listados na consola de administração do Intune.

- **Botão de comentários adicionado à aplicação Portal da empresa do Windows Phone 8.1**

  A aplicação de Portal da empresa do Windows Phone 8.1 permite que os utilizadores finais enviar comentários sobre a aplicação através da utilização de um novo botão "Enviar comentários". Para localizar o botão, os utilizadores toque no menu "reticências" na parte inferior direita do ecrã de aplicação do Portal da empresa e, em seguida, toque em **enviar comentários**. Os comentários recolhidos são anónimos e vão ajudar a Microsoft a melhorar a experiência de aplicação do Portal da empresa para utilizadores.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Novo no Configuration Manager Technical Preview 1609

As novas funcionalidades híbridas foram introduzidas Setembro de 2016 para 1609 de pré-visualização técnica do Configuration Manager.

- **Definições adicionais e experiência melhorada para as definições do Item de configuração**

  Foram adicionadas novas definições de Android, iOS e Windows, e apenas as definições que se aplicam para as plataformas que selecionar na página de plataformas suportadas são apresentadas no assistente. Para obter mais informações consulte [novas definições de conformidade de itens de configuração TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Definições adicionais para perfis DEP**

  Foram adicionadas TouchID, ApplePay e Zoom como as definições configuráveis em perfis DEP para dispositivos iOS.

- **Paga aplicações na loja Windows para empresas**

  Agora pode adicionar aplicações pagas e livres para a loja Windows para empresas e implementá-las aos utilizadores na sua organização. Para obter mais informações consulte [melhoramentos à loja Windows para empresas no TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Tipos de ligação de nativo para perfis de VPN do Windows 10**

  Agora, pode criar perfis de VPN do Windows 10 para MDM com o Microsoft Automatic, PPTP e IKEv2, tipos de ligação na consola do Configuration Manager sem utilizar definições OMA-URI.

- **Gráficos de conformidade do Intune**

  Pode obter uma vista rápida de dispositivos geral os motivos de conformidade e superior inconformidade utilizando gráficos novos na área de trabalho monitorização. Para obter mais informações, consulte [gráficos de conformidade do Intune no TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

A seguinte nova funcionalidade introduzida no Setembro de 2016 está disponível para implementações híbridas com o Microsoft Intune e Configuration Manager versão 1606 (ramo atual).

- **suporte do iOS 10**

  Se tiver perfis ou itens de configuração direcionadas para todas as plataformas iOS, estes também serão enviados para o iOS 10. Também tiver lançada uma atualização do Configuration Manager versão 1606 que lhe permite perfis de destino e itens de configuração para as plataformas iOS individuais, incluindo iOS 10. Pode instalar a atualização com a consola de administração do Configuration Manager em **administração > Descrição geral > Serviços Cloud > atualizações e manutenção**. Pode encontrar mais informações sobre a atualização na [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="august-2016"></a>Agosto de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas em Agosto de 2016 funcionam em implementações híbridas.

- **Suporte de 7 Android na aplicação Portal da empresa**

  A aplicação Portal da empresa do Intune para Android fornece suporte de "dia 0" para o lançamento sistema de operativo Android 7.0 para dispositivos móveis.

- **Google remoção do código de acesso remoto de reposição de capacidade em dispositivos Android 7.0**

  Google está a remover a capacidade dos administradores de TI e os utilizadores finais repor remotamente o código de acesso de dispositivos Android 7.0. Anteriormente, os administradores de TI podiam repor remotamente o código de acesso de um utilizador e os utilizadores finais foi possível repor os códigos de acesso a partir do site do Portal da empresa.

- **Política de aplicações permitidas e bloqueadas para dispositivos Samsung KNOX Standard**

  Agora, pode configurar uma política personalizada para dispositivos Samsung KNOX Standard que lhe permite criar um dos seguintes:

  - Uma lista de aplicações que estão bloqueadas de executar no dispositivo. Mesmo que se instalada, uma aplicação definida na lista de bloqueadas não pode ser ativada no dispositivo.
  - Uma lista de aplicações que os utilizadores do dispositivo estão autorizados a instalar a partir da loja do Google Play. Não existem outras aplicações podem ser instaladas da loja.

  Estas definições só podem ser utilizadas pelos dispositivos que executem o Samsung KNOX Standard. Para obter mais informações, consulte [utilizar as políticas personalizadas para permitir e bloquear aplicações para dispositivos Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Ligação de comentários do Portal da empresa para a Microsoft**

   O Web site do Portal da empresa permite aos utilizadores finais tocar numa hiperligação "Comentários" novo, na parte inferior da página, para enviar comentários à Microsoft sobre as suas experiências com o site. Os comentários recolhidos são anónimos e vão ajudar a Microsoft a melhorar a experiência de Web site do Portal da empresa para utilizadores.

- **Versão do Browser gerido iOS mínima atualizada para 8.0**

  A aplicação de Browser gerido do Microsoft Intune para iOS foi atualizada para suportar dispositivos que executam o iOS 8.0 ou posterior. Embora os dispositivos iOS 7.1 ainda podem utilizar a aplicação de Browser gerido atual, encorajar os utilizadores atualizarem para o iOS 8.0 ou posterior para aceder e tirar partido das novas funcionalidades de Browser gerido.

### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview

Não existem novas funcionalidades híbridas foram introduzidas no Agosto de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

Não existem novas funcionalidades híbridas foram introduzidas no Agosto de 2016 para o Configuration Manager (ramo atual).

## <a name="july-2016"></a>Julho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

As seguintes funcionalidades do Intune introduzidas em Julho de 2016 funcionam em implementações híbridas.

- **SDK Xamarin para aplicações do Intune está disponível**

  O componente Xamarin do Intune App SDK permite-lhe ativar as funcionalidades de gestão de aplicações móveis do Intune no seu móveis aplicações iOS e Android criadas com Xamarin. Pode encontrar o componente no [arquivo Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) ou no [página do Microsoft Intune Github](https://github.com/msintuneappsdk).

- **Experiência de utilizador final melhorada quando a inscrição de dispositivos Windows**

  Quando estiver a utilizar o acesso condicional, os passos de inscrição para Windows 8.1, ambiente de trabalho do Windows 10 e Windows 10 Mobile foram clarificados no Web site do Portal da empresa. Os utilizadores irão ver agora separadas **inscrição de dispositivos** e **Workplace Join** passos, tornando mais fácil para os mesmos para ver o estado dos respetivos dispositivos e concluir o processo se se depararem com uma falha de área de trabalho Join (WPJ). Os passos separados também são esperados para simplificar o processo de resolução de problemas para os administradores de TI. Anteriormente, quando os utilizadores finais tentavam inscrever e todos os passos de inscrição foi concluída com êxito, menos a WPJ, o dispositivo inscrito não aparecia na lista de dispositivos para os utilizadores identificarem, confundindo-os utilizadores.

 - **Eliminação completa, agora disponível para dispositivos Windows 10**

    Windows 10 PCs e portáteis inscritos como dispositivos móveis podem ser apagados repor o dispositivo para as definições de fábrica. Para obter mais informações, consulte [como proteger os seus dispositivos com a eliminação remota](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Alterações às contas na aplicação Portal da empresa iOS para os gestores de inscrição de dispositivos**

  Para melhorar o desempenho e dimensionamento, o Intune já não mostra todos os dispositivos de gestores de inscrição de dispositivos (DEM) no painel meus dispositivos da aplicação Portal da empresa iOS. Apenas o dispositivo local que executa a aplicação é apresentado e apenas se estiver inscrito através da aplicação do Portal da empresa.

  O utilizador DEM pode executar ações no dispositivo local, mas a gestão remota de outros dispositivos inscritos só pode ser efetuada da consola de administração do Intune. Além disso, Intune está a descontinuar a utilização de contas DEM com o programa de inscrição de dispositivos da Apple ou a ferramenta Apple Configurator. Ambos os métodos de inscrição já suportam a inscrição de utilizadores para dispositivos iOS partilhados.

  Utilize apenas contas DEM quando a inscrição de utilizadores para dispositivos partilhados não está disponível. Para obter mais informações, consulte [inscrever dispositivos pertencentes à empresa com o Gestor de inscrição do dispositivo no Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Alterações para a aplicação do Portal da empresa para Android**

  Se os utilizadores finais vir uma mensagem de erro que indica o dispositivo está em falta um certificado necessário, podem tocar num botão "How to resolve this" para obter passos para instalar o certificado em falta. Se os utilizadores de concluir os passos, mas consulte um adicional "certificado em falta" mensagem de erro, são-lhe pedidos para contactar o administrador de TI e fornecer esta ligação, que contém os passos que os administradores de TI podem utilizar para corrigir o problema do certificado.

- **Restringir instalações de aplicações sideload em dispositivos Android inscritos**

  Dispositivos Android já não podem instalar aplicações através do site do Portal da empresa, a menos que os dispositivos que tenham sido inscritos no Intune através da aplicação Portal da empresa do Intune para Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview

Não existem novas funcionalidades híbridas foram introduzidas no Julho de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)

As seguintes funcionalidades que se encontravam anteriormente disponíveis em versões do Configuration Manager Technical Preview estão agora disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1606.

* Localizar, gerir e distribuir da loja Windows para empresas aplicações para dispositivos Windows 10 na consola do Configuration Manager ([1604](#new-in-1604-technical-preview))
*   Definição de SmartLock para dispositivos Android ([1604](#new-in-1604-technical-preview))
*   Dispositivos de VPN para Windows 10 acionada por aplicações ([1605](#new-in-1605-technical-preview))
*   Nova experiência para as ações do dispositivo remoto ([1605](#new-in-1605-technical-preview))
*   Loja Windows para aplicações empresariais ([1605](#new-in-1605-technical-preview))
*   Melhoramentos gerais para as aplicações compradas em volume ([1605](#new-in-1605-technical-preview))
*   O Windows Information Protection (WIP) ([1605](#new-in-1605-technical-preview))
*   Pré-declarar dispositivos pertencentes à empresa com o número de série iOS ou IMEI ([1605](#new-in-1605-technical-preview))
*   Categorizar automaticamente os dispositivos para coleções ([1606](#new-in-1606-technical-preview))

Para obter informações sobre a nova funcionalidade, consulte a documentação para a versão de pré-visualização técnica especificada.

## <a name="june-2016"></a>Junho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune
As seguintes funcionalidades do Intune introduzidas em Junho de 2016 funcionam em implementações híbridas.

- **Estado de funcionamento do serviço Intune** informações de estado de funcionamento do serviço do Intune foi movidas para uma localização central com outros serviços Microsoft. Agora encontrar estas informações no portal de gestão do Office 365 em estado de funcionamento do serviço. Para obter mais informações, consulte este [blogue](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Experiência avançada configuração de política de dados do Windows 10 enterprise**

  Intune tem agora uma experiência melhorada para configurar a política de proteção de informações do Windows 10. As melhorias incluem melhor formas para criar regras de aplicação, especifique a definição de limites de rede e outras definições de proteção de informações do Windows. Para obter mais informações, consulte [criar uma política de proteção de informações do Windows (WIP) através do Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Política de controlo do acesso do Cisco ISE rede para o Intune**

  Os clientes que utilizam o Cisco identidade do serviço de motor (ISE) 2.1 e também utilizam o Microsoft Intune podem definir uma política de controlo de acesso de rede no ISE. Utilizar esta política, dispositivos que necessitam para ligar à rede através de Wi-Fi ou VPN devem cumprir seguintes condições antes de lhes ser concedido acesso:

  - Tem de ser gerido pelo Intune
  - Deve ser compatível com todas políticas de conformidade do Intune implementadas

  Os utilizadores finais de dispositivos não conformes serão solicitados a inscrição e retificar quaisquer problemas de compatibilidade para obter acesso.

- **Acesso condicional para browser**

  Pode definir uma política de acesso condicional para Exchange Online e SharePoint Online, para que apenas pode ser acedidos de browsers suportados em dispositivos geridos e conformes iOS e Android. Serão solicitados aos utilizadores finais que tentarem iniciar sessão sites do Outlook Web Access (OWA) e ao SharePoint com dispositivos iOS e Android para inscrever o respetivo dispositivo no Intune, bem como que corrijam quaisquer problemas de não conformidade, para que poderem concluir o início de sessão. Para mais informações, consulte

  * [Restringir o acesso ao e-mail no Exchange Online e Exchange Online dedicado com o Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restringir o acesso ao SharePoint Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online suporta o acesso condicional**

  Pode definir uma política de acesso condicional para o Dynamics CRM Online, para que apenas possa ser acedida por dispositivos geridos e conformes iOS e Android. Os utilizadores finais que tentarem iniciar sessão na aplicação móvel Dynamics CRM no iOS e Android será pedido que se inscrevam primeiro no Intune e que corrijam quaisquer problemas de não conformidade para concluir o início de sessão. Para obter mais informações, consulte [restringir o acesso ao Dynamics CRM Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Atualizações da aplicação Portal da empresa para Android**

  Agora, o Intune tem as seguintes novas políticas que irão afetar os utilizadores do Portal da empresa para Android:   

  Política  |Efeito nos utilizadores  
  ---------|---------
  Exigir que dispositivos não permitam a instalação de aplicações a partir de origens desconhecidas (Android 4.0 +)     |  Os utilizadores finais com Android 4.0 ou dispositivos posteriores irão ver a mensagem, "Instalação a partir de origens desconhecidas tem de ser desativada." Os utilizadores terão de ir para **definições > segurança** nos seus dispositivos e desative **origens desconhecidas**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obterem mais informações sobre a mensagem e por que motivo é necessário desativar a definição.
  Exigir que dispositivos não permitam a instalação de aplicações a partir de origens desconhecidas (Android 4.0 +)  |    Os utilizadores finais com Android 4.0 ou dispositivos posteriores irão ver a mensagem "Analisar se o dispositivo apresenta ameaças de segurança." Os utilizadores terão de ir para **definições > Google > segurança** nos seus dispositivos e ative **analisar se o dispositivo apresenta ameaças de segurança**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obterem mais informações sobre a mensagem e por que motivo é necessário para ativar a definição.     
  Exigir que a depuração USB esteja desativada (Android 4.2 +)  | Os utilizadores finais com Android 4.2 ou dispositivos posteriores irão ver a mensagem, "a depuração de USB deve ser desativada." Os utilizadores terão de ir para **definições > Opções de programador** nos seus dispositivos e desative **depuração USB**. Uma ligação na mensagem de compatibilidade permite aos utilizadores obterem mais informações sobre a mensagem e por que motivo é necessário desativar a definição.
  Nível de patch de segurança Android mínimo (Android 6.0 +)  | Os utilizadores finais com Android 6.0 ou dispositivos posteriores irão ver a mensagem, "este dispositivo não cumpre o nível de patch de segurança Android mínimo." Os utilizadores terão de instalar o patch de segurança necessário. Uma ligação na mensagem de compatibilidade permite aos utilizadores obter informações sobre como instalar o patch de segurança necessárias e para ver que patch de segurança que está atualmente instalado.

- **Atualizações da aplicação do Portal da empresa iOS**

  * Quando os utilizadores finais estiverem a instalar aplicações de linha de negócio, irão ver agora uma experiência de instalação de aplicações melhorada. Se a instalação da aplicação estiver a demorar muito tempo, os utilizadores podem sincronizar manualmente os respetivos dispositivos para forçar o continuação do processo de sincronização. Para consultar as instruções do utilizador final, consulte Sincronizar o dispositivo iOS manualmente.
  * A aplicação Portal da empresa do Microsoft Intune para iOS foi atualizada para suportar a versão do iOS 8.0 e posterior. Esta atualização significa que os utilizadores finais podem instalar a aplicação Portal da empresa e inscrever novos dispositivos no Intune apenas se o dispositivo está a executar o iOS versão 8.0 ou posterior. Os utilizadores que já inscreveram dispositivos que executem uma versão não suportada do iOS podem continuar a utilizar a aplicação Portal da empresa que está nos dispositivos deles.


### <a name="new-in-1606-technical-preview"></a>Novo no 1606 Technical Preview
As seguintes novas funcionalidades introduzidas no Junho de 2016 estão disponíveis nas implementações híbridas com o Intune e 1606 de pré-visualização técnica do Configuration Manager.

- **Categorizar automaticamente os dispositivos para coleções**

  Pode criar categorias de dispositivo, que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando estiver a utilizar o Configuration Manager com o Intune. Os utilizadores, em seguida, são necessários para escolher uma categoria de dispositivo quando inscreverem um dispositivo no Intune. Além disso, pode alterar a categoria de um dispositivo da consola do Configuration Manager. Para obter mais informações, consulte [automaticamente categorizar os dispositivos para coleções](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) no [capacidades no 1606 de pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > Esta capacidade funciona com a versão de Junho de 2016 do Microsoft Intune. Certifique-se de que lhe foram atualizadas para esta versão antes de experimentar estes procedimentos.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)
Não existem novas funcionalidades híbridas foram introduzidas para o Configuration Manager (ramo atual) de Junho de 2016.

##  <a name="may-2016"></a>Maio de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas no Maio de 2016 funcionam em implementações híbridas.

- **SDK DE MAM: Configuração de comprimento do PIN de suporte**

  Agora pode especificar o comprimento do PIN para aplicações MAM, semelhante a um PIN do dispositivo. Isto requer que os utilizadores finais estão em conformidade com as novas restrições que definiu. O ecrã PIN ligeiramente modificado para a conta para a entrada mais. Para obter mais informações, consulte [definições de política MAM para Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings), e [definições de política MAM para iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype para empresas para iOS e Android**

  Agora pode visar o Skype para empresas com [MAM sem políticas de inscrição](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Assim que os utilizadores iniciar sessão, as políticas MAM serão aplicadas.  

- **Novas aplicações disponíveis para a gestão com as políticas de MAM**

  As aplicações Microsoft Word, Excel e PowerPoint para Android podem agora ser associadas a políticas de MAM em dispositivos que não estão inscritos no Intune. Para obter uma lista completa de aplicações suportadas, aceda à Galeria de aplicações móveis do Microsoft Intune no [parceiros de aplicações do Microsoft Intune](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) página.  

- **Aplicação do portal da empresa para Android: Notificações de alerta do utilizador final**

  Notificações de alerta da aplicação Portal da empresa Android apresentada quando os utilizadores finais inscrever ou remover os respetivos dispositivos no Portal da empresa.  

- **Web site do Portal da empresa: Faixa de identificação do dispositivo vai dar mais informações aos utilizadores finais**

  Os utilizadores finais podem agora identificar mais facilmente o dispositivo que selecionaram quando estão a utilizar o Web site do Portal da empresa. Se for selecionado o dispositivo incorreto, pode selecionar o dispositivo correto ao tocar no **tocar aqui** ligação na faixa da página inicial.  


### <a name="new-in-1605-technical-preview"></a>Novo no 1605 Technical Preview  
 As seguintes novas funcionalidades introduzidas no Maio de 2016 estão disponíveis nas implementações híbridas com o Intune e Configuration Manager Technical Preview 1605. Estas funcionalidades requerem a utilizar a consola do Configuration Manager para configurar e geri-los.  

- **Dispositivos de acionada por aplicações de VPN para Windows 10**

  Para dispositivos do Windows 10 geridos com o Configuration Manager com o Intune, pode adicionar uma lista de aplicações que abra automaticamente uma ligação de VPN que tiver configurado através da consola de administração do Configuration Manager. Para obter mais informações, consulte [acionada por aplicação VPN para dispositivos com Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1605) no [funcionalidades no Technical Preview 1605 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nova experiência para as ações do dispositivo remoto**

  A experiência para efetuar ações do dispositivo remoto a partir da consola do Configuration Manager foi melhorada.

  Ações comuns, tais como **extinguir/limpar**, **repor código de acesso**, **bloqueio remoto**, e **ignorar bloqueio de ativação** agora podem ser encontrados no **ações do dispositivo remoto** acedido a partir do menu de **ativos e compatibilidade** área de trabalho

  Para obter mais informações, consulte [nova experiência para as ações do dispositivo remoto](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) no [funcionalidades no Technical Preview 1605 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Aplicações da Loja Windows para Empresas**

  O [loja Windows para empresas](https://www.microsoft.com/en-us/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja ao Configuration Manager, pode gerir aplicações compradas em volume a partir da consola do Configuration Manager. Para obter mais informações, consulte [da loja Windows para aplicações empresariais](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) no [funcionalidades no Technical Preview 1605 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Melhoramentos gerais para as aplicações compradas em volume**

  Aplicações compradas na loja Windows para empresas e a iOS app store tem foram consolidadas para a mesma vista **informações de licença para armazenar aplicações**. Além disso, a forma como os que cria as aplicações compradas em volume para iOS foi melhorado. Para obter mais informações, consulte[melhoramentos gerais para as aplicações compradas em volume](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) no [funcionalidades no Technical Preview 1605 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Pré-declarar dispositivos pertencentes à empresa com o número de série iOS ou IMEI**

  Agora pode identificar dispositivos pertencentes ao importar os respetivos números de identidade (IMEI) estação internacional do equipamento móvel. Pode carregar um ficheiro de valores separados por vírgulas (. csv) contendo os números IMEI de dispositivo ou pode introduzir manualmente as informações do dispositivo.  Também pode importar os números de série para dispositivos iOS.  Para obter mais informações, consulte [pré-declarar dispositivos pertencentes à empresa com o número de série iOS ou IMEI](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) no [funcionalidades no Technical Preview 1605 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **O Windows Information Protection (WIP)**

  Pode criar itens de configuração que permitem-lhe implementar as políticas de proteção de informações do Windows (WIP), incluindo, permitindo-lhe escolher as aplicações protegidas, o nível de proteção de WIP e como dados empresariais são localizados na rede. Para obter mais informações sobre WIP, consulte os tópicos seguintes:  

  -   [Proteger os dados de enterprise através de proteção de informações do Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Criar e implementar uma política de proteção de informações do Windows (WIP) com o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 Não existem novas funcionalidades híbridas foram introduzidas na Maio de 2016 para o Configuration Manager (ramo atual).  

##  <a name="april-2016"></a>Abril de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas no Abril de 2016 funcionam em implementações híbridas.  

- **Conformidade de utilizadores MAM**

  Agora, pode ver o estado das suas políticas de gestão de aplicações para qualquer utilizador no seu inquilino do Azure Active Directory (AAD).  Para obter mais informações consulte [monitorizar políticas de gestão de aplicações móveis com o Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Controlos de MAM para impedir a sincronização de contactos do Outlook (Android)**

  Uma nova definição está disponível que lhe permite impedir que uma aplicação a sincronização de contactos no livro de endereços nativo em dispositivos Android. Esta nova definição é suportada inicialmente pela aplicação Outlook em dispositivos Android. Para obter mais informações, consulte [criar e implementar políticas de gestão de aplicações móveis com o Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Melhoramentos para o Web site do Portal da empresa**

  Quando os utilizadores do Windows 10 Mobile e Windows Phone 8.1 estiverem a instalar aplicações de linha de negócio, irão ver agora os seguintes Estados novos, que fornecem mais detalhes sobre o estado da instalação:  

  -   **A aguardar sincronização do dispositivo** – o utilizador tocou em "Instalar" e o dispositivo tenta agora sincronizar com a infraestrutura do Intune. A sincronização é necessária para concluir a instalação. A mensagem "A aguardar sincronização do dispositivo" também é uma ligação a que os utilizadores podem tocar para ver instruções sobre como sincronizar manualmente o respetivo dispositivo no Intune se o processo de sincronização está a demorar muito tempo ou ficar parado.  

  -   **Transferir** – o pedido de transferência do utilizador está a ser processado e que o dispositivo está a transferir e instalar a aplicação.  

- **Melhoramentos para a aplicação do portal da empresa para Android**

  Os utilizadores que não inscreveram o seu dispositivo no Intune e que não tenham o certificado correto instalado não conseguirá iniciar sessão na aplicação do Portal da empresa para Android e verão a mensagem, "não pode iniciar sessão porque o seu dispositivo está em falta um certificado necessário." A mensagem inclui uma ligação "How to resolve this" que os utilizadores podem tocar para ver instruções para instalar o certificado. Para ver os passos que os utilizadores finais seguir para resolver o problema, consulte [o dispositivo está em falta um certificado necessário](/intune/enduser/using-your-android-device-with-intune) na biblioteca do Intune.  

- **Melhoramentos para a aplicação Portal da empresa iOS**

  Foi adicionado suporte para a ação de solicitação para atualizar atualizar o conteúdo do ecrã principal, que inclui as aplicações listadas, os dispositivos listados e contacto de TI informações. A ação de atualização de extração verifica se existem informações de conformidade ou de política, que podem ser efetuadas selecionando o mosaico para o seu dispositivo atual e tocando o **sincronização** botão.  

- **Melhoramentos à aplicação do Portal Windows 10 Mobile e da empresa do Windows Phone 8.1**

  Quando os utilizadores finais estiverem a instalar aplicações de linha de negócio, irão ver agora uma experiência de instalação de aplicações melhorada. Se a instalação da aplicação estiver a demorar muito tempo, os utilizadores podem sincronizar manualmente os respetivos dispositivos para forçar o continuação do processo de sincronização. Para consultar as instruções do utilizador final, consulte o artigo [sincronizar o seu dispositivo manualmente para acelerar a instalações de aplicações](/intune/enduser/using-your-windows-device-with-intune) na biblioteca do Intune.  

###  <a name="new-in-1604-technical-preview"></a>No 1604 Technical Preview
 As seguintes novas funcionalidades introduzidas no Abril de 2016 estão disponíveis nas implementações híbridas com o Intune e Configuration Manager Technical Preview 1604. Estas funcionalidades requerem a utilizar a consola do Configuration Manager para configurar e geri-los.  

- **Localizar, gerir e distribuir da loja Windows para empresas aplicações para dispositivos Windows 10 na consola do Configuration Manager**


  Suporte para a loja Windows para empresas está disponível no Configuration Manager Technical Preview 1604 para o ajudar a localizar, gerir e distribuir aplicações para os dispositivos Windows 10 que estiver a gerir. Para obter mais informações, consulte [gerir aplicações compradas na loja Windows para empresas](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) no [funcionalidades no Technical Preview 1604 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Definição de SmartLock para dispositivos Android**

  Foi adicionada uma nova definição para o item de configuração do Android e Samsung KNOX Standard que lhe permite controlar a funcionalidade de SmartLock em dispositivos Android compatíveis.  Pode utilizar esta definição para impedir que os utilizadores finais configurem o SmartLock. Consulte [definição de SmartLock para dispositivos Android](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) no [funcionalidades no Technical Preview 1604 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 Não existem novas funcionalidades híbridas foram introduzidas no Abril de 2016 para o Configuration Manager (ramo atual).  

##  <a name="march-2016"></a>Março de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 As seguintes funcionalidades do Intune introduzidas no Março de 2016 funcionam em implementações híbridas.  

- **Controlos de MAM para impedir a sincronização de contactos do Outlook (iOS)**

  Uma nova definição está disponível que lhe permite impedir que uma aplicação a sincronização de contactos no livro de endereços nativo em dispositivos iOS. Esta nova definição é suportada pela aplicação Outlook em dispositivos iOS. Para obter mais detalhes acerca desta e de outras definições, consulte [criar e implementar políticas de MAM](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Skype para empresas Online suporta o acesso condicional**

  Pode definir uma política de acesso condicional para o Skype para empresas Online, para que apenas possa ser acedida por dispositivos geridos e conformes iOS e Android.  Para obter mais informações, consulte [gerir o acesso ao Skype para empresas Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) na biblioteca do Intune.  

- **Suporte para iOS 9.3**

  Na segunda-feira, 21 de Março, a Apple anunciou a disponibilidade do iOS 9.3. Todas as funcionalidades existentes do Intune atualmente disponíveis para gerir dispositivos iOS continuarão a funcionar de forma totalmente integrada quando os utilizadores atualizarem os respetivos dispositivos para iOS 9.3.  

- **Pacotes de aplicações do Windows disponíveis diretamente a partir do site do Portal da empresa**

  Os utilizadores de PCs Windows 8, Windows 8.1 e Windows RT podem agora instalar pacotes de aplicações do Windows (com a extensão. AppX) diretamente a partir do site do Portal da empresa. Anteriormente, era necessário implementar, ou os utilizadores tinham de instalar a aplicação do Portal da empresa nos respetivos dispositivos para instalar aplicações.  

- **Os utilizadores podem bloquear remotamente o dispositivo do Web site do Portal da empresa**

  Uma nova opção de bloqueio remoto foi adicionada ao site do Portal da empresa para permitir que os utilizadores bloqueiem remotamente o respetivo dispositivo a partir do Portal se o dispositivo é perdido ou roubado.  

- **Tirar partido do iOS "Open-in" gestão de dispositivos que estão inscritos numa solução MDM de terceiros**

  Pode utilizar o fornecedor de gestão (MDM) de dispositivos móveis de terceiros para tirar partido do iOS gestão "Open-In". Pode configurar as restrições na configuração de definições de perfil e implementar a aplicação utilizando o software MDM. Quando o utilizador instala a aplicação gerida, são aplicadas as restrições. Lê os detalhes: [Políticas de gestão de aplicações móveis do Microsoft Intune e iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) na biblioteca do Intune.  

- **Aplicações da Microsoft que suportam MAM**

  A lista de aplicações da Microsoft que pode utilizar com políticas de gestão de aplicações móveis do Intune foi atualizada para incluir as aplicações mais recentes (para dispositivos inscritos com o Intune apenas).  

- **Implementar o Adobe Reader para Microsoft Intune para dispositivos iOS geridos pelo Intune na sua empresa**

  A aplicação Adobe Reader para iOS pode agora ser gerida em dispositivos inscritos com a política de gestão de aplicações móveis do Intune.  

- A aplicação de partilha Rights Management é suportada para Android

  Os administradores de TI podem implementar políticas de gestão de aplicações móveis para os utilizadores finais podem ver imagens, AV e PDF ficheiros de forma mais segura, ou não IT utiliza o Intune para gerir os dispositivos.  

- **Melhoramentos para a aplicação Portal da empresa iOS e Android**

  -   Quando os seus utilizadores iniciarem uma aplicação que é gerida pela gestão de aplicações móveis (MAM), verão uma mensagem a indicar que a aplicação é gerida pela empresa. Os utilizadores podem agora tocar numa hiperligação "Mais informações" para obter mais informações aqui sobre "aplicações geridas". Estes também podem tocar em "Não voltar a mostrar" para que a mensagem deixa de aparecer quando iniciarem a aplicação.  

  -   Foram adicionados novos ecrãs para orientar os utilizadores ao longo do processo de inscrição e fornecer mais informações sobre o motivo pelo qual os utilizadores devem inscrever e que os administradores de TI podem e não podem ver nos seus dispositivos inscritos.  

  -   Mensagens de erro de inscrição são agora apresentadas na aplicação Portal da empresa.  

### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview  
 Não existem novas funcionalidades híbridas foram introduzidas no Março de 2016, para o Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramo atual)  
 As seguintes novas funcionalidades introduzidas no Março de 2016 estão disponíveis em implementações híbridas com o Intune e Configuration Manager (ramo atual) versão 1602. Estas funcionalidades requerem a utilizar a consola do Configuration Manager para configurar e geri-los.  

- **Políticas de configuração de aplicações iOS**

  Na versão 1602 do Configuration Manager (ramo atual) pode utilizar políticas de configuração de aplicação para fornecer definições que poderão ser necessárias quando o utilizador executa uma aplicação iOS. Para obter mais informações, consulte [configurar aplicações iOS com políticas de configuração de aplicações no System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Gerir aplicações iOS compradas em volume**

  Na versão 1602 do Configuration Manager (ramo atual), pode implementar e gerir aplicações adquiridas em volume da Apple Volume-Purchase Program (VPP) ao importar as informações da licença da loja de aplicações e ao controlar o número de licenças que utilizou. Para obter mais informações, consulte [gerir aplicações iOS compradas em volume com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Criação automática de aplicações móveis do Office**

  As seguintes aplicações móveis Microsoft Office para Android e iOS a partir da versão 1602 do Configuration Manager (ramo atual), são criadas durante a atualização da versão 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (apenas iOS)  
  -   Microsoft Outlook  

  Encontrará estas aplicações no nó de aplicações de consola do Configuration Manager. Para obter mais informações sobre como implementar aplicações, consulte [como implementar aplicações com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Definições do modo de local público para dispositivos Android Samsung KNOX Standard**

  O modo Kiosk permite-lhe bloquear um dispositivo e permitir que apenas determinadas funcionalidades funcionem.  A partir da versão 1602 do Configuration Manager (ramo atual), pode agora especificar definições do modo de local público para dispositivos Samsung KNOX Standard. Para obter mais informações, consulte [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard geridos sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Bloqueio de ativação de iOS**

  A partir da versão 1602 do Configuration Manager (ramo atual), pode gerir o bloqueio de ativação de iOS, uma funcionalidade da aplicação encontrar o meu iPhone para iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo.  Para obter mais informações, consulte [ignorar o bloqueio de ativação de iOS de gerir para o System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  
