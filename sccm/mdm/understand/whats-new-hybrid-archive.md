---
title: "Arquivamento do MDM híbrido do novo | Microsoft Docs"
description: "Arquivo morto dos últimos recursos de gerenciamento de dispositivos móveis disponíveis para implantações híbridas com o System Center Configuration Manager e o Intune."
ms.custom: na
ms.date: 06/30/2017
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
ms.sourcegitcommit: ed6b65a1a5aabc0970cd0333cb033405cf6d2aea
ms.openlocfilehash: 0abd1cdcf44e778c91bacb8011efd711818ce2e9
ms.contentlocale: pt-pt
ms.lasthandoff: 07/03/2017

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Recursos anterior híbrido com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Este artigo fornece detalhes sobre o dispositivo móvel últimos recursos de gerenciamento (MDM) disponíveis para implantações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada seção deste artigo lista os recursos de híbrida em 3 categorias diferentes. Use as diretrizes a seguir para determinar a compatibilidade dos recursos em cada categoria com versões diferentes do Configuration Manager:  

|Categorias de recursos|
|-|  
|**Novo no Microsoft Intune** -em geral, todos os recursos listados nesta categoria devem funcionar com todas as versões do Configuration Manager, incluindo versões do System Center 2012 R2 Configuration Manager, pois esses recursos exigem o serviço Intune somente e não exigem a funcionalidade adicional no Configuration Manager.<br /><br /> **Novo no Configuration Manager Technical Preview** -todos os recursos listados nesta categoria só funcionam com a versão de visualização técnica especificada. Para testar esses recursos, você deve instalar a versão de visualização técnica especificada na descrição do recurso. Para obter mais informações, consulte [visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Novo no Configuration Manager (ramificação atual)** -todos os recursos listados sob esta categoria só funciona com a versão especificada do Configuration Manager (ramificação atual), como a versão 1511 ou 1602. Se você estiver usando uma versão mais antiga do Configuration Manager para sua implantação híbrida, você deve atualizar para a versão do Configuration Manager (ramificação atual) especificada na descrição do recurso. Para obter mais informações, consulte [atualizar para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="december-2016"></a>Dezembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **A autenticação multifator (MFA) no registro está migrando para o portal do Azure**

  Anteriormente, você deve ir para o console do Intune ou o console do Configuration Manager para definir o MFA para registros do Intune. Com esse recurso atualizado, você agora logon [portal do Microsoft Azure] (https://manage.windowsazure.com) usando o Intune credenciais e definir as configurações de MFA por meio do AD do Azure. Para obter mais informações, consulte [multi-factor authentication para o Microsoft Intune] (https://aka.ms/mfa_ad).

- **Aplicativo de Portal da empresa para Android já disponível na China**

  O aplicativo de Portal da empresa para Android agora está disponível na China. Devido à ausência do Google Play Store na China, dispositivos Android devem obter aplicativos de mercados de aplicativo chinês. O aplicativo de Portal da empresa para Android está disponível para download nos seguintes armazenamentos:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  O aplicativo de Portal da empresa para Android usa os serviços do Google reproduzir para se comunicar com o serviço Microsoft Intune. Como o Google executar serviços ainda não estão disponíveis na China, executar qualquer uma das seguintes tarefas pode levar até 8 horas para ser concluído.

  | Console de administração do Configuration Manager | Aplicativo do Portal da empresa do Intune para Android | Site de Portal da empresa do Intune |
  |----|----|----|      
  | Desativar/apagar (remover todos os dados)   | Remover um dispositivo remoto | Remover dispositivo (local e remoto) |
  | Desativar/apagar (remover dados de empresa)   | Redefinir o dispositivo | Redefinir o dispositivo|
  | Implantações de aplicativo novo ou atualizado | Instalar aplicativos de linha de negócios disponíveis | Redefinição de senha do dispositivo|
  | Bloqueio remoto | | |
  | Redefinição de senha | | |        


## <a name="november-2016"></a>Novembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Novo Microsoft Portal da empresa Intune disponível para dispositivos Windows 10**

  A Microsoft lançou um novo [aplicativo de Portal da empresa para dispositivos Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Este aplicativo, que aproveita o novo formato Universal do Windows 10, fornece uma experiência de usuário atualizado que é idêntica em todos os dispositivos Windows 10, PC e móveis da mesma forma, enquanto ainda permite a mesma funcionalidade fornecida por aplicativos de Portal da empresa anteriores.

  O novo aplicativo aproveita os recursos de plataforma como o logon único (SSO) e autenticação baseada em certificado em dispositivos Windows 10. O aplicativo está disponível como uma atualização para o Portal da empresa existente do Windows 8.1 e instala o Portal da empresa do Windows Phone 8.1 da Windows Store. Para obter mais detalhes, acesse o [Intune Blog da equipe de suporte](http://aka.ms/intunecp_universalapp).

  O novo aplicativo de Portal da empresa também exibe qualquer Windows Store para aplicativos de negócios marcados **disponível** no console do Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)

Os seguintes recursos que estavam anteriormente disponíveis em versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e Configuration Manager (ramificação atual) versão 1610.

* [Configurações adicionais e uma experiência aprimorada para itens de configuração](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Configurações adicionais para perfis DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Pago aplicativos da Windows Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipos de conexão nativo para perfis de VPN do Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Gráficos de conformidade do Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Solicitação para sincronização de política no console do](/sccm/mdm/deploy-use/sync-intune-device)
* [Definições de configuração do Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Os seguintes recursos híbridos adicionais também estão incluídos na versão 1610 do Configuration Manager (ramificação atual):

- **Aumento do número de dispositivos registrados**

  Agora você pode habilitar os usuários registrem dispositivos até 15. O limite anterior era 5 dispositivos por usuário.


- **Suporte de segurança adicionais**

  Além de administrador completo, as seguintes funções de segurança internas agora tem acesso completo aos itens no nó todos os dispositivos corporativos, incluindo dispositivos declaradas previamente, perfis de registro do iOS e perfis de registro do Windows:

    - Gerenciador de ativos
    - Gerenciador de acesso do recurso da empresa

  Acesso somente leitura para essas áreas do console do Configuration Manager ainda é concedido a função de analista somente leitura.

- **Acesso à VPN de disparo automático de aplicativos do Windows Information Protection**

  Você pode adicionar um domínio primário de proteção de informações do Windows para perfis de VPN do Windows 10 que faz com que todos os aplicativos associados acionar uma conexão VPN automaticamente quando eles são executados no dispositivo. Essa opção só está disponível ao escolher um tipo de conexão nativo.

- **Acesso condicional para perfis de VPN do Windows 10**

    Agora você pode exigir que o Windows 10 dispositivos registrados no Active Directory do Azure para ser compatível para ter acesso VPN por meio de perfis de VPN do Windows 10 criado no console do Configuration Manager. Isso é possível por meio do novo **habilitar o acesso condicional para esta conexão VPN** caixa de seleção na página de método de autenticação no Assistente de perfil VPN e propriedades de perfil VPN para perfis de VPN do Windows 10. Essa opção só está disponível ao escolher um tipo de conexão nativo.

    Você também pode especificar um certificado separado para autenticação de logon único se você habilitar o acesso condicional para o perfil.

## <a name="october-2016"></a>Outubro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os seguintes recursos do Intune introduzidos em outubro de 2016 funcionam em implantações híbridas.

- **Acesso condicional para o gerenciamento de aplicativos móveis**

  Você pode restringir o acesso ao Exchange Online para que o acesso vem somente de aplicativos que dão suporte a políticas de gerenciamento de aplicativos móveis do Intune, como o Outlook. [Esse novo recurso](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) pares perfeitamente com políticas MAM (gerenciamento) do aplicativo móvel do Intune, você pode bloquear o acesso para clientes de email internos ou outros aplicativos que não foram configurados com as políticas de MAM do Intune. Isso garante que os usuários estão acessando os dados de sua organização com aplicativos que podem ser protegidos usando MAM do Intune. Você pode começar no gerenciamento de aplicativo móvel do Intune por meio do portal do Azure. Procure a nova seção de acesso condicional na folha "Configurações".

-   **Ferramenta de disposição do aplicativo Intune para Android**

  Você pode habilitar seus aplicativos usar políticas MAM (gerenciamento) de aplicativos móveis do Intune usando a ferramenta de encapsulamento de aplicativos do Intune.

- **Compatibilidade Samsung KNOX Standard Android com o Intune**

  Alguns modelos do telefone Samsung Galaxy Ace não podem ser gerenciados pelo Intune como dispositivos Samsung KNOX Standard. Quando você registra esses dispositivos com o Intune, eles serão então gerenciados como dispositivos Android padrão.

  Os números de modelo afetados são:

  - G313HU SM
  - G313HY SM
  - G313M SM
  - G313MY SM
  - G313U SM

  Você e seus usuários finais não precisa executar nenhuma ação adicional. Para obter mais informações, visite o site da Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Novo no Configuration Manager Technical Preview 1610

Os seguintes novos recursos híbridos foram introduzidos em outubro de 2016 para o Configuration Manager Technical Preview 1610.

- **Solicitar uma sincronização de política no console do administrador**

  Você pode solicitar uma sincronização de política em um dispositivo móvel registrado no console do Configuration Manager, em vez de precisar solicitar a sincronização no aplicativo do Portal da empresa no dispositivo. Esta é uma nova ação chamada **enviar solicitação de sincronização** no menu de ações de dispositivo remoto, que aparece na faixa de opções quando um dispositivo móvel está selecionado no nó dispositivos.

- **Definições de configuração do Windows Defender**

  Agora você pode configurar as configurações de cliente do Windows Defender em computadores registrados pelo Intune Windows 10 com itens de configuração no console do Configuration Manager. Há um novo grupo de configuração chamado **Windows Defender** no Assistente de Item de configuração. Observe que isso é suportado apenas no Windows 10 versão 1511 e acima.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)

Não há novos recursos híbridos foram introduzidos em agosto de 2016 para o Configuration Manager (ramificação atual).

## <a name="september-2016"></a>Setembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os seguintes recursos do Intune introduzidos em setembro de 2016 funcionam em implantações híbridas.

- **Adição de "Notificações" para o Portal da empresa para Android**

  Um novo ícone de notificações foi adicionado ao Portal da empresa para Android na home page. Tocar nesse ícone acessa a página de notificações, que mostra todos os itens que exigem atenção no aplicativo Portal da empresa, como falta de conformidade do dispositivo, atualização de registro e ativação do registro de seus usuários finais. O aplicativo de Portal da empresa do iOS já tem essa experiência de notificações. Com os novos meios de página de notificações que o usuário não verá a página de configuração de acesso da empresa toda vez iniciar ou retomar o Portal da empresa, como o dispositivo já está registrado. Se você criar sua própria guia do usuário final, você talvez queira atualizar sua documentação para refletir essa alteração. Encontre capturas de tela atualizadas [aqui](https://aka.ms/androidcpupdate).

- **Alterações no suporte para o aplicativo de Portal da empresa do iOS**

  Todos os usuários do aplicativo do Portal da empresa do Microsoft Intune para iOS agora devem usar a versão mais recente. Novos usuários são capazes de baixar apenas a versão mais recente, e os usuários atuais são necessárias para atualizar a ele. A versão mais recente requer iOS 8.0 ou posterior, para que dispositivos que executam versões anteriores do iOS não é possível usar o Portal da empresa ou registrar até atualizar seu dispositivo para o iOS 8.0 ou posterior e, em seguida, atualizar o aplicativo de Portal da empresa para a versão mais recente. Os dispositivos que executam versões abaixo do iOS 8.0 continuarão a ser gerenciados e listados no Console de administração do Intune.

- **Botão de comentários adicionado ao aplicativo de Portal da empresa do Windows Phone 8.1**

  O aplicativo de Portal da empresa do Windows Phone 8.1 permite que os usuários finais enviar comentários sobre o aplicativo usando um novo botão "enviar comentários". Para localizar o botão, os usuários toque no menu "três pontos" na parte inferior direita da tela de aplicativo de Portal da empresa e, em seguida, toque em **enviar comentários**. Os comentários anônimos coletados ajudarão a Microsoft a melhorar a experiência de aplicativo de Portal da empresa para os usuários.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Novo no Configuration Manager Technical Preview 1609

Os seguintes novos recursos híbridos foram introduzidos em setembro de 2016 para o Configuration Manager Technical Preview 1609.

- **Configurações adicionais e uma experiência aprimorada para configurações de Item de configuração**

  Novas configurações foram adicionadas para Windows, iOS e Android, e somente as configurações que se aplicam às plataformas que você selecionar na página de plataformas com suporte são exibidas no assistente. Para obter mais informações, consulte [novas configurações de conformidade para itens de configuração no PA 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Configurações adicionais para perfis DEP**

  Foram adicionadas Touch ID, ApplePay e Zoom como definições configuráveis em perfis DEP para dispositivos iOS.

- **Pago aplicativos da Windows Store para empresas**

  Agora você pode adicionar pagos e gratuitos aplicativos da Windows Store para empresas e implantá-los para os usuários em sua organização. Para obter mais informações, consulte [aprimoramentos para a Windows Store para empresas no PA 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Tipos de conexão nativo para perfis de VPN do Windows 10**

  Agora você pode criar perfis de VPN do Windows 10 do MDM com tipos de conexão Microsoft Automatic, IKEv2 e PPTP no console do Configuration Manager sem usando o OMA-URI.

- **Gráficos de conformidade do Intune**

  Você pode obter uma exibição rápida de dispositivo geral motivos de conformidade e a parte superior da não conformidade usando gráficos de novo no espaço de trabalho de monitoramento. Para obter mais informações, consulte [gráficos de conformidade do Intune no PA 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)

O seguinte recurso novo introduzido em setembro de 2016 está disponível para implantações híbridas com o Microsoft Intune e Configuration Manager versão 1606 (ramificação atual).

- **suporte para iOS 10**

  Se você tiver perfis ou itens de configuração de destino para todas as plataformas do iOS, eles também serão enviados para iOS 10. Também já lançamos uma atualização à versão 1606 do Configuration Manager que permite aos perfis de destino e itens de configuração para plataformas de iOS individuais, incluindo iOS 10. Você pode instalar a atualização com o console de administração do Configuration Manager em **Administração > Visão geral > Serviços de nuvem > atualizações e manutenção**. Você pode encontrar mais informações sobre a atualização em [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="august-2016"></a>Agosto de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os seguintes recursos do Intune introduzidos em agosto de 2016 funcionam em implantações híbridas.

- **Suporte do Android 7 no aplicativo do Portal da empresa**

  O aplicativo de Portal da empresa Intune para Android oferece suporte de "dia 0" para o próximo sistema de operacional Android 7.0 para dispositivos móveis.

- **Funcionalidade em dispositivos Android 7.0 de redefinição de senha remota remoção pelo Google**

  O Google está removendo a capacidade dos administradores de TI e usuários finais de redefinir remotamente a senha de dispositivos Android 7.0. Anteriormente, os administradores de TI podiam redefinir remotamente a senha do usuário e os usuários finais podiam redefinir suas senhas do site do Portal da empresa.

- **Política de aplicativos permitidos e bloqueados para dispositivos Samsung KNOX Standard**

  Agora você pode configurar uma política personalizada para dispositivos Samsung KNOX padrão que permite que você crie um dos seguintes:

  - Uma lista de aplicativos que são impedidos de execução no dispositivo. Mesmo se instalado, um aplicativo definido na lista de bloqueados não pode ser ativado no dispositivo.
  - Uma lista de aplicativos que os usuários do dispositivo podem instalar da loja Google Play. Nenhum outro aplicativo pode ser instalado da loja.

  Essas configurações podem ser usadas apenas por dispositivos que executam o Samsung KNOX Standard. Para obter detalhes, consulte [usar políticas personalizadas para permitir e bloquear aplicativos para dispositivos Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Link de comentários do Portal da empresa para a Microsoft**

   O site de Portal da empresa permite que os usuários finais toquem em um novo link "Comentários", na parte inferior da página para enviar comentários à Microsoft sobre sua experiência com o site. Os comentários anônimos coletados ajudarão a Microsoft a melhorar a experiência do site de Portal da empresa para os usuários.

- **Versão mínima do iOS Managed Browser atualizada para 8.0**

  O aplicativo de navegador gerenciado pelo Microsoft Intune para iOS foi atualizado para dar suporte a dispositivos que executam o iOS 8.0 ou posterior. Embora os dispositivos iOS 7.1 ainda podem usar o aplicativo Managed Browser existente, incentive seus usuários para atualizar para o iOS 8.0 ou posterior para acessar e aproveitar ao máximo os recursos do Managed Browser.

### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview

Não há novos recursos híbridos foram introduzidos em agosto de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)

Não há novos recursos híbridos foram introduzidos em agosto de 2016 para o Configuration Manager (ramificação atual).

## <a name="july-2016"></a>Julho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os seguintes recursos do Intune introduzidos em julho de 2016 funcionam em implantações híbridas.

- **O SDK do Xamarin para aplicativos do Intune está disponível**

  O componente Xamarin do SDK de aplicativo Intune permite que você habilitar os recursos de gerenciamento de aplicativo móvel do Intune no seu celular aplicativos iOS e Android criados com o Xamarin. Você pode encontrar o componente no [Xamarin store](https://components.xamarin.com/view/Microsoft.Intune.MAM) ou o [página Github do Microsoft Intune](https://github.com/msintuneappsdk).

- **Experiência do usuário final melhorada ao registrar dispositivos Windows**

  Quando você estiver usando o acesso condicional, as etapas de registro para Windows 8.1, Windows 10 Desktop e Windows 10 Mobile serão esclarecidas no site do Portal da empresa. Os usuários agora encontrarão separada **registro de dispositivo** e **ingresso** etapas, tornando mais fácil para ver o status de seu dispositivo e concluir o processo se enfrentarem uma falha no local de trabalho WPJ (ingresso). As etapas separadas também são esperadas para simplificar o processo de solução de problemas para os administradores de TI. Anteriormente, quando os usuários finais tentavam se registrar e todas as etapas de registro eram bem-sucedidas exceto pelo WPJ, o dispositivo registrado não aparecia na lista de dispositivos para os usuários a identificar, causando confusão para os usuários.

 - **Apagamento completo agora disponível para dispositivos Windows 10**

    Computadores com Windows 10 e laptops registrados como dispositivos móveis possam ser apagados para redefinir o dispositivo para as configurações de fábrica. Para obter mais informações, consulte [como proteger seus dispositivos com um apagamento remoto](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Muda para gerentes de registro de dispositivo as contas no aplicativo de Portal da empresa do iOS**

  Para melhorar o desempenho e dimensionamento, o Intune não exibe todos os dispositivos de gerenciadores de registro de dispositivo (DEM) no painel meus dispositivos do aplicativo de Portal da empresa do iOS. Somente o dispositivo local executando o aplicativo é exibido e somente se ele tiver sido registrado por meio do aplicativo Portal da empresa.

  O usuário DEM pode realizar ações no dispositivo local, mas o gerenciamento remoto de outros dispositivos registrados somente pode ser executado do console de administração do Intune. Além disso, o Intune substituirá o uso de contas DEM com o programa de registro de dispositivo Apple ou a ferramenta Apple Configurator. Esses dois métodos de registro já dão suporte ao registro sem usuário para dispositivos iOS compartilhados.

  Somente use contas DEM quando o registro sem usuário para dispositivos compartilhados não estiver disponível. Para obter mais informações, consulte [registrar dispositivos corporativos com o Gerenciador de registro do dispositivo no Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Alterações para o aplicativo do Portal da empresa do Android**

  Se os usuários finais do Android virem uma mensagem de erro que o dispositivo é tem um certificado necessário, eles poderão tocar no botão "Como resolver isso" para obter as etapas para instalar o certificado ausente. Se os usuários conclua as etapas, mas um adicional de "certificado faltando" mensagem de erro, são solicitados a entrar em contato com seu administrador de TI e forneça esse link, que contém as etapas que os administradores de TI podem usar para corrigir o problema do certificado.

- **Restringir instalações de aplicativo carregado por sideload aos dispositivos Android**

  Dispositivos Android não podem mais instalar aplicativos por meio do site de Portal da empresa, a menos que os dispositivos foram registrados no Intune usando o aplicativo de Portal da empresa Intune para Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview

Não há novos recursos híbridos foram introduzidos em julho de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)

Os seguintes recursos que estavam anteriormente disponíveis em versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e Configuration Manager (ramificação atual) versão 1606.

* Localizar, gerenciar e distribuir da Windows Store para aplicativos de negócios para dispositivos Windows 10 do console do Configuration Manager ([1604](#new-in-1604-technical-preview))
*   Configuração do SmartLock para dispositivos Android ([1604](#new-in-1604-technical-preview))
*   Disparada por aplicativo VPN para Windows 10 dispositivos ([1605](#new-in-1605-technical-preview))
*   Nova experiência para ações de dispositivo remoto ([1605](#new-in-1605-technical-preview))
*   Windows Store para aplicativos de negócios ([1605](#new-in-1605-technical-preview))
*   Melhorias gerais de aplicativos adquiridos por volume ([1605](#new-in-1605-technical-preview))
*   O Windows Information Protection (WIP) ([1605](#new-in-1605-technical-preview))
*   Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI ([1605](#new-in-1605-technical-preview))
*   Categorizar automaticamente dispositivos em coleções ([1606](#new-in-1606-technical-preview))

Para obter informações sobre a nova funcionalidade, consulte a documentação da versão de visualização técnica especificado.

## <a name="june-2016"></a>Junho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune
Os seguintes recursos do Intune introduzidos em junho de 2016 funcionam em implantações híbridas.

- **Integridade do serviço Intune** informações de integridade do serviço do Intune foi movidas para um local central com outros serviços da Microsoft. Agora, você encontrará essas informações no portal de gerenciamento do Office 365 em integridade do serviço. Para obter mais informações, consulte [postagem de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Experiência aprimorada configuração de política do Windows 10 enterprise dados**

  O Intune agora tem uma experiência aprimorada para a configuração de diretiva de proteção de informações do Windows 10. As melhorias incluem melhores maneiras de criar regras de aplicativo, especifique a definição de limites de rede e outras configurações de proteção de informações do Windows. Para obter mais informações, consulte [criar uma política de proteção de informações do Windows (WIP) usando o Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Política de controle de acesso Cisco ISE rede para o Intune**

  Clientes que usam o Cisco identidade serviço de mecanismo (ISE) 2.1 e usam o Microsoft Intune também podem definir uma política de controle de acesso à rede no ISE. Usando essa política, dispositivos que precisam se conectar à rede usando Wi-Fi ou VPN devem atender às seguintes condições antes de terem permissão de acesso:

  - Deve ser gerenciado pelo Intune
  - Deve estar em conformidade com as políticas de conformidade do Intune implantadas

  Usuários finais de dispositivos não compatíveis serão solicitados a registrar e corrigir quaisquer problemas de conformidade para obter acesso.

- **Acesso condicional para navegador**

  Você pode definir uma política de acesso condicional para Exchange Online e o SharePoint Online para que eles podem ser acessados somente de navegadores da web com suporte em dispositivos com Android e iOS gerenciados e compatíveis. Os usuários finais que tentarem entrar no Outlook Web Access (OWA) e o SharePoint sites com dispositivos iOS e Android precisará registrar seu dispositivo no Intune e corrigir quaisquer problemas de não conformidade para que poderem concluir entrar. Para mais informações, consulte

  * [Restringir o acesso a email ao Exchange Online e o novo Exchange Online dedicado com o Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restringir o acesso ao SharePoint Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online dá suporte ao acesso condicional**

  Você pode definir uma política de acesso condicional para o Dynamics CRM Online para que ele somente pode ser acessado por dispositivos Android e iOS gerenciados e compatíveis. Os usuários finais que tentarem entrar aplicativo móvel do Dynamics CRM no iOS e Android precisará registrar com o Intune, bem como para corrigir quaisquer problemas de não conformidade antes de entrar concluir. Para obter mais informações, consulte [restringir o acesso ao Dynamics CRM Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Atualizações para o aplicativo do Portal da empresa do Android**

  O Intune agora tem as seguintes novas políticas que afetam os usuários do Portal da empresa Android:   

  Política  |Impacto sobre os usuários  
  ---------|---------
  Exigir que dispositivos não permitam a instalação de aplicativos de fontes desconhecidas (Android 4.0 +)     |  Os usuários finais com dispositivos Android 4.0 ou posteriores verão a mensagem, "Instalação de fontes desconhecidas deve ser desabilitada". Os usuários precisam ir para **Configurações > segurança** em seus dispositivos e desativar **fontes desconhecidas**. Um link na mensagem de conformidade permite aos usuários obter mais informações sobre a mensagem e porque eles estão sendo solicitados a desativar a configuração.
  Exigir que dispositivos não permitam a instalação de aplicativos de fontes desconhecidas (Android 4.0 +)  |    Os usuários finais com dispositivos Android 4.0 ou posteriores verão a mensagem "Verificar dispositivo contra ameaças à segurança". Os usuários precisam ir para **Configurações > Google > segurança** em seus dispositivos e ative **verificar dispositivo contra ameaças à segurança**. Um link na mensagem de conformidade permite aos usuários obter mais informações sobre a mensagem e porque eles estão sendo solicitados a ativar a configuração.     
  Exigir que a depuração de USB esteja desabilitada (Android 4.2 +)  | Os usuários finais com Android 4.2 ou dispositivos posteriores verão a mensagem, "depuração de USB deve ser desabilitada." Os usuários precisam ir para **Configurações > Opções do desenvolvedor** em seus dispositivos e desativar **depuração de USB**. Um link na mensagem de conformidade permite aos usuários obter mais informações sobre a mensagem e porque eles estão sendo solicitados a desativar a configuração.
  Nível de patch de segurança mínima do Android (Android 6.0 +)  | Os usuários finais com Android 6.0 ou dispositivos posteriores verão a mensagem, "Este dispositivo não atende o nível de patch de segurança do Android mínimo." Os usuários precisarão instalar o patch de segurança necessárias. Um link na mensagem de conformidade permite aos usuários a obter informações sobre como instalar o patch de segurança necessário e ver qual patch de segurança eles já têm instalado atualmente.

- **Atualizações para o aplicativo de Portal da empresa do iOS**

  * Quando os usuários finais instalarem aplicativos de linha de negócios, agora eles terão uma instalação de aplicativo melhor experiência. Se a instalação do aplicativo estiver demorando muito tempo, os usuários poderão sincronizar manualmente seu dispositivo para forçar o processo de sincronização a continuar. Para examinar as instruções do usuário final, consulte sincronizar seu dispositivo iOS manualmente.
  * O aplicativo de Portal da empresa do Microsoft Intune para iOS tem foi atualizado para dar suporte a iOS versão 8.0 e posterior. Essa atualização significa que os usuários finais podem instalar o aplicativo de Portal da empresa e registrar novos dispositivos no Intune somente se o dispositivo está executando o iOS versão 8.0 ou posterior. Os usuários que já registraram dispositivos que estão executando uma versão sem suporte do iOS podem continuar a usar o aplicativo de Portal da empresa que está em seu dispositivo.


### <a name="new-in-1606-technical-preview"></a>Novo no 1606 Technical Preview
Os seguintes novos recursos introduzidos em junho de 2016 estão disponíveis em implantações híbridas com o Intune e Configuration Manager Technical Preview 1606.

- **Categorizar automaticamente dispositivos em coleções**

  Você pode criar categorias de dispositivo, que podem ser usadas para colocar automaticamente os dispositivos em coleções de dispositivos quando você estiver usando o Configuration Manager com o Intune. Os usuários devem, em seguida, escolha uma categoria de dispositivo quando registram um dispositivo no Intune. Além disso, você pode alterar a categoria de um dispositivo do console do Configuration Manager. Para obter mais informações, consulte [categorizar automaticamente dispositivos em coleções](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) na [recursos no Technical Preview 1606 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > Esse recurso funciona com a versão de junho de 2016 do Microsoft Intune. Certifique-se de que você foram atualizados para esta versão antes de você experimentar esses procedimentos.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)
Não há novos recursos híbridos foram introduzidos em junho de 2016 para o Configuration Manager (ramificação atual).

##  <a name="may-2016"></a>Maio de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 Os seguintes recursos do Intune introduzidos em maio de 2016 funcionam em implantações híbridas.

- **SDK DE MAM: Configuração de comprimento do PIN de suporte**

  Agora você pode especificar o comprimento do PIN para aplicativos MAM semelhantes a um PIN do dispositivo. Isso requer que os usuários finais de acordo com as novas restrições que você definir. A tela PIN foi ligeiramente modificada a conta para a entrada mais. Para obter detalhes, consulte [configurações de política MAM para Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings), e [configurações de política MAM para iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype for Business para iOS e Android**

  Agora você pode direcionar o Skype for business com [MAM sem políticas de registro](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Quando os usuários fazer logon, as políticas de MAM serão aplicadas.  

- **Novos aplicativos disponíveis para gerenciamento com políticas de MAM**

  Os aplicativos Microsoft Word, Excel e PowerPoint para Android agora podem ser associados a políticas MAM em dispositivos que não estão registrados com o Intune. Para obter uma lista completa de aplicativos com suporte, vá para a Galeria de aplicativos móveis Microsoft Intune [parceiros de aplicativos do Microsoft Intune](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) página.  

- **Aplicativo do portal da empresa do Android: Notificações de usuário final**

  Notificações do sistema do aplicativo do Portal da empresa Android aparecem quando os usuários finais se inscrever ou remover seus dispositivos do Portal da empresa.  

- **Site do Portal da empresa: Faixa de identificação de dispositivo fornecerá mais informações para usuários finais**

  Os usuários finais agora pode identificar mais facilmente o dispositivo que selecionaram ao usarem o site de Portal da empresa. Se o dispositivo errado for selecionado, eles podem selecionar o dispositivo correto tocando a **Toque aqui** link na faixa de página inicial.  


### <a name="new-in-1605-technical-preview"></a>Novo no 1605 Technical Preview  
 Os seguintes novos recursos introduzidos em maio de 2016 estão disponíveis em implantações híbridas com o Intune e Configuration Manager Technical Preview 1605. Esses recursos exigem que você use o console do Configuration Manager para configurar e gerenciá-los.  

- **Dispositivos de VPN para Windows 10 disparada por aplicativo**

  Para dispositivos Windows 10 gerenciados usando o Configuration Manager com Intune, você pode adicionar uma lista de aplicativos que são abertos automaticamente uma conexão VPN que você configurou por meio do console de administração do Configuration Manager. Para obter mais informações, consulte [disparada por aplicativo VPN para Windows 10 dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1605) no [recursos no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nova experiência para ações de dispositivo remoto**

  A experiência para realizar ações de dispositivo remoto do console do Configuration Manager foi aprimorada.

  Ações comuns, como **desativar/apagar**, **redefinição de senha**, **bloqueio remoto**, e **Ignorar bloqueio de ativação** agora podem ser encontradas no **ações de dispositivo remoto** acessado a partir do menu de **ativos e conformidade** espaço de trabalho

  Para obter mais informações, consulte [nova experiência para ações de dispositivo remoto](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) na [recursos no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Aplicações da Loja Windows para Empresas**

  O [da Windows Store para empresas](https://www.microsoft.com/en-us/business-store) é onde você pode encontrar e comprar aplicativos para sua organização, individualmente ou em um volume. Ao conectar o armazenamento para o Configuration Manager, você pode gerenciar aplicativos adquiridos por volume no console do Configuration Manager. Para obter mais informações, consulte [da Windows Store para aplicativos de negócios](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) na [recursos no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Melhorias gerais de aplicativos adquiridos por volume**

  Aplicativos adquiridos por volume da Windows Store para empresas e iOS app store foram consolidados na mesma exibição, **informações de licença para armazenar aplicativos**. Além disso, o modo no qual você cria aplicativos adquiridos por volume para iOS foi aprimorado. Para obter mais informações, consulte[melhorias gerais de aplicativos adquiridos por volume](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) na [recursos no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI**

  Agora você pode identificar dispositivos de propriedade corporativa importando seus números IMEI (identidade) estação internacional de equipamentos móveis. Você pode carregar um arquivo de valores separados por vírgula (. csv) contendo números IMEI do dispositivo, ou você pode inserir manualmente as informações do dispositivo.  Você também pode importar números de série para dispositivos iOS.  Para obter mais informações, consulte [pré-declarar dispositivos corporativos com número de série do iOS ou IMEI](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) na [recursos no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **O Windows Information Protection (WIP)**

  Você pode criar itens de configuração que permitem que você implante as políticas de proteção de informações do Windows (WIP), incluindo permitindo que você escolha seus aplicativos protegidos, o nível de proteção de WIP e como localizar dados corporativos em rede. Para obter mais informações sobre WIP, consulte os tópicos a seguir:  

  -   [Proteger dados corporativos usando a proteção de informações do Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Criar e implantar uma política de proteção de informações do Windows (WIP) usando o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)  
 Não há novos recursos híbridos foram introduzidos em maio de 2016 para o Configuration Manager (ramificação atual).  

##  <a name="april-2016"></a>Abril de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 Os seguintes recursos do Intune introduzidos em abril de 2016 funcionam em implantações híbridas.  

- **Conformidade de usuário do MAM**

  Agora você pode exibir o status de suas políticas de gerenciamento de aplicativo para qualquer usuário em seu locatário do Azure Active Directory (AAD).  Para obter mais informações, consulte [monitorar políticas de gerenciamento de aplicativo móvel com o Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Controles de MAM para impedir a sincronização de contatos do Outlook (Android)**

  Uma nova configuração está disponível que permite impedir que um aplicativo de sincronização de contatos no catálogo de endereços nativo em dispositivos Android. Essa nova configuração tem suporte inicialmente no aplicativo Outlook em dispositivos Android. Para obter mais informações, consulte [criar e implantar políticas de gerenciamento de aplicativo móvel com o Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Aprimoramentos para o site de Portal da empresa**

  Quando os usuários de Windows 10 Mobile e Windows Phone 8.1 estiverem instalando aplicativos de linha de negócios, eles verão os novos status a seguir, que fornecem mais detalhes sobre o status da instalação:  

  -   **Aguardando a sincronização do dispositivo** – o usuário tocou em "Instalar" e o dispositivo tenta sincronizar com a infraestrutura do Intune agora. A sincronização é necessária para concluir a instalação. A mensagem "Aguardando o dispositivo sincronizar" também é um link que os usuários podem tocar para ver instruções sobre como sincronizar manualmente seu dispositivo no Intune quando o processo de sincronização está demorando muito ou fica paralisado.  

  -   **Baixando** – solicitação de download do usuário está sendo processada e o dispositivo está baixando e instalando o aplicativo.  

- **Aprimoramentos para o aplicativo do portal da empresa do Android**

  Os usuários que não tiverem registrado seus dispositivos no Intune e que não tenham o certificado correto instalado não será capazes de entrar no aplicativo de Portal da empresa Android e verão a mensagem, "Você não pode entrar porque o dispositivo não tem um certificado necessário." A mensagem inclui um link de "Como resolver o problema" que os usuários podem tocar para ver instruções para instalar o certificado. Para ver as etapas que os usuários finais seguir para resolver o problema, consulte [seu dispositivo não tem um certificado necessário](/intune/enduser/using-your-android-device-with-intune) na biblioteca do Intune.  

- **Aprimoramentos para o aplicativo de Portal da empresa do iOS**

  Foi adicionado suporte para a ação de recepção para atualizar para atualizar o conteúdo na tela inicial, que inclui os aplicativos listados, dispositivos listados e contato de TI informações. A ação de atualização de recepção não verifica as informações de conformidade ou política, que podem ser feitas selecionando o bloco do dispositivo atual e toque o **sincronização** botão.  

- **Aprimoramentos para o aplicativo do Portal Windows 10 Mobile e Windows Phone 8.1 empresa**

  Quando os usuários finais instalarem aplicativos de linha de negócios, agora eles terão uma instalação de aplicativo melhor experiência. Se a instalação do aplicativo estiver demorando muito tempo, os usuários poderão sincronizar manualmente seu dispositivo para forçar o processo de sincronização a continuar. Para examinar as instruções do usuário final, consulte [sincronizar o dispositivo manualmente para acelerar as instalações de aplicativos](/intune/enduser/using-your-windows-device-with-intune) na biblioteca do Intune.  

###  <a name="new-in-1604-technical-preview"></a>Novo no Technical Preview 1604
 Os seguintes novos recursos introduzidos em abril de 2016 estão disponíveis em implantações híbridas com o Intune e Configuration Manager Technical Preview 1604. Esses recursos exigem que você use o console do Configuration Manager para configurar e gerenciá-los.  

- **Localizar, gerenciar e distribuir da Windows Store para aplicativos de negócios para dispositivos Windows 10 do console do Configuration Manager**


  Suporte para a Windows Store para empresas está disponível no Configuration Manager Technical Preview 1604 para ajudá-lo a encontrar, gerenciar e distribuir aplicativos para os dispositivos Windows 10 que você está gerenciando. Para obter detalhes, consulte [gerenciar aplicativos adquiridos por volume da Windows Store para empresas](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) na [recursos no Technical Preview 1604 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Configuração do SmartLock para dispositivos Android**

  Uma nova configuração foi adicionada para o item de configuração de Android e Samsung KNOX Standard que lhe permite controlar o recurso SmartLock em dispositivos Android compatíveis.  Você pode usar essa configuração para impedir que os usuários finais configurem o SmartLock. Consulte [configuração do SmartLock para dispositivos Android](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) na [recursos no Technical Preview 1604 para o System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)  
 Não há novos recursos híbridos foram introduzidos em abril de 2016 para o Configuration Manager (ramificação atual).  

##  <a name="march-2016"></a>Março de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 Os seguintes recursos do Intune introduzidos em março de 2016 funcionam em implantações híbridas.  

- **Controles de MAM para impedir a sincronização de contatos do Outlook (iOS)**

  Uma nova configuração está disponível que permite impedir que um aplicativo de sincronização de contatos no catálogo de endereços nativo em dispositivos iOS. Essa nova configuração tem suporte no aplicativo Outlook em dispositivos iOS. Para obter mais detalhes sobre essa e outras configurações, consulte [criar e implantar políticas de MAM](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) na biblioteca do Intune.  

- **Skype for Business Online dá suporte ao acesso condicional**

  Você pode definir uma política de acesso condicional para o Skype for Business Online para que ele somente pode ser acessado por dispositivos Android e iOS gerenciados e compatíveis.  Para obter detalhes, consulte [gerenciar o acesso ao Skype for Business Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) na biblioteca do Intune.  

- **Suporte para iOS 9.3**

  Em 21 de março de segunda-feira, Apple anunciou a disponibilidade do iOS 9.3. Todas as funcionalidades do Intune existentes atualmente disponíveis para gerenciar dispositivos iOS continuarão a funcionar perfeitamente quando os usuários atualizarem seus dispositivos para o iOS 9.3.  

- **Pacotes de aplicativos do Windows disponíveis diretamente do site de Portal da empresa**

  Os usuários do Windows 8, Windows 8.1 e PCs com Windows RT agora podem instalar pacotes de aplicativos do Windows (com a extensão. AppX) diretamente do site de Portal da empresa. Anteriormente, você precisava implantar, ou os usuários tinham que instalar o aplicativo de Portal da empresa em seus dispositivos para instalar aplicativos.  

- **Os usuários podem bloquear remotamente seu dispositivo no site do Portal da empresa**

  Uma nova opção de bloqueio remoto adicionou o site de Portal da empresa para permitir que os usuários bloqueiem seus dispositivos no Portal remotamente se o dispositivo é perdido ou roubado.  

- **Tirar proveito do iOS "Abrir em" gerenciamento de dispositivos que são registrados em uma solução MDM de terceiros**

  Você pode usar seu fornecedor MDM (gerenciamento) do dispositivo móvel para tirar proveito do iOS do gerenciamento "Open-In". Você pode definir as restrições na configuração de definições de perfil e implantar o aplicativo usando o software de MDM. Quando o usuário instala o aplicativo gerenciado, as restrições são aplicadas. Leia os detalhes: [Políticas de gerenciamento de aplicativo móvel do Microsoft Intune e iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) na biblioteca do Intune.  

- **Aplicativos da Microsoft que dão suporte a MAM**

  A lista de aplicativos da Microsoft que você pode usar com políticas de gerenciamento de aplicativos móveis do Intune tem foi atualizada para incluir os aplicativos mais recentes (para dispositivos registrados com o Intune somente).  

- **Implantar o Adobe Reader para o Microsoft Intune para dispositivos iOS gerenciados pelo Intune em sua empresa**

  O aplicativo Adobe Reader para iOS agora pode ser gerenciado em dispositivos registrados com a política de gerenciamento de aplicativos móveis do Intune.  

- O aplicativo de compartilhamento do Rights Management é suportado para Android

  Os administradores de TI podem implantar políticas de gerenciamento de aplicativos móveis para os usuários finais podem exibir imagens, AV e PDF arquivos com mais segurança, ou não IT usa o Intune para gerenciar os dispositivos.  

- **Aprimoramentos para o aplicativo de Portal da empresa iOS e Android**

  -   Quando os usuários iniciam um aplicativo que é gerenciado pelo gerenciamento de aplicativo móvel (MAM), eles verão uma mensagem notificando que o aplicativo é gerenciado pela empresa. Os usuários agora podem tocar no link "Saiba mais" para obter mais informações sobre o que significa "aplicativos gerenciados". Eles também podem tocar em "Não mostrar novamente" para que a mensagem não apareçam quando iniciar o aplicativo.  

  -   Foram adicionadas novas telas para orientar os usuários pelo processo de registro e fornecer mais informações sobre por que os usuários devem registrar e o que os administradores de TI podem ou não veem em seus dispositivos registrados.  

  -   Mensagens de erro de registro agora são exibidas no aplicativo do Portal da empresa.  

### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview  
 Não há novos recursos híbridos foram introduzidos em março de 2016 para o Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (ramificação atual)  
 Os seguintes novos recursos introduzidos em março de 2016 estão disponíveis em implantações híbridas com o Intune e Configuration Manager (ramificação atual) versão 1602. Esses recursos exigem que você use o console do Configuration Manager para configurar e gerenciá-los.  

- **Políticas de configuração de aplicações iOS**

  Na versão 1602 do Configuration Manager (ramificação atual), você pode usar políticas de configuração de aplicativo para fornecer as configurações que podem ser necessárias quando o usuário executa um aplicativo iOS. Para obter detalhes, consulte [configurar aplicativos iOS com as políticas de configuração de aplicativo no System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Gerenciar aplicativos iOS adquiridos por volume**

  Na versão 1602 do Configuration Manager (ramificação atual), você pode implantar e gerenciar aplicativos comprados em volume da compra de Volume programa VPP (Apple), importando as informações de licença da app store e acompanhando quantas licenças você usou. Para obter detalhes, consulte [gerenciar aplicativos iOS adquiridos por volume com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Criação automática de aplicativos móveis do Office**

  Os seguintes aplicativos móveis Microsoft Office para Android e iOS a partir versão 1602 do Configuration Manager (ramificação atual), são criados quando você atualizar da versão 1511:  

  -   Microsoft Word  
  -   O Microsoft Excel  
  -   O Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (somente iOS)  
  -   O Microsoft Outlook  

  Você encontrará esses aplicativos no nó aplicativos do console do Configuration Manager. Para obter mais informações sobre como implantar aplicativos, consulte [como implantar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Configurações do modo de quiosque para dispositivos Android Samsung KNOX Standard**

  O modo Kiosk permite-lhe bloquear um dispositivo e permitir que apenas determinadas funcionalidades funcionem.  A partir versão 1602 do Configuration Manager (ramificação atual), agora você pode especificar configurações do modo de quiosque para dispositivos Samsung KNOX Standard. Para obter detalhes, consulte [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerenciados sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Bloqueio de ativação do iOS**

  A partir versão 1602 do Configuration Manager (ramificação atual), você pode gerenciar o bloqueio de ativação do iOS, um recurso do que o aplicativo buscar meu iPhone para o iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo.  Para obter detalhes, consulte [ignorar o bloqueio de ativação do iOS de gerenciar para o System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  

