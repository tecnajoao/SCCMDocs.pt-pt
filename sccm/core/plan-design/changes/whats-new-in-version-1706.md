---
title: "Nova versão 1706"
titleSuffix: Configuration Manager
description: "Obter informações sobre as alterações e novas funcionalidades introduzidas na versão 1706 do System Center Configuration Manager."
ms.custom: na
ms.date: 08/11/2017
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 2889de0709096aa481ca6203c5ab2bac1f064d5e
ms.sourcegitcommit: c4a1bafcd004638d264a93d307c70d8b6f7fe023
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/20/2017
---
# <a name="what39s-new-in-version-1706-of-system-center-configuration-manager"></a>O que &#39; s novidade na versão 1706 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1706 para o ramo atual do System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1606, 1610 ou 1702.

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalar atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1706 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura de sites

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Suporte de Cache ponto a ponto do cliente para ficheiros de instalação rápida para Windows 10 e o Office 365  
<!-- 1352486 -->
A partir desta versão, a Cache suporta a distribuição dos ficheiros de conteúdo de instalação rápida para o Windows 10 e dos ficheiros de atualização para o Office 365. Não existem configurações adicionais necessários para suportar esta alteração.

### <a name="updates-for-the-data-warehouse"></a>Atualizações para o armazém de dados
<!-- 1277922 -->
O armazém de dados já não é uma funcionalidade de pré-lançamento. Podemos também foi atualizado com os pré-requisitos para incluir suporte para a base de dados no SQL Server sempre em grupos de disponibilidade e clusters de ativação pós-falha. Para obter mais informações, consulte [ponto de serviço do armazém de dados](/sccm/core/servers/manage/data-warehouse).

### <a name="accessibility-improvements"></a>Melhoramentos de acessibilidade
<!-- 1253000 -->
Ter adicionámos os melhoramentos adicionais para acessibilidade para a consola do Configuration Manager. Para obter mais informações, consulte [funcionalidades de acessibilidade](/sccm/core/understand/accessibility-features).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Melhoramentos para o SQL Server Always On nos grupos de disponibilidade
<!-- 1352094 -->
Com esta versão, agora, pode utilizar réplicas com consolidação assíncrona na SQL Server Always On nos grupos de disponibilidade que utilizar com o Configuration Manager. Isto significa que pode adicionar réplicas adicionais para os grupos de disponibilidade para utilizar como as cópias de segurança (remotas) fora das instalações e, em seguida, utilizá-los num cenário de recuperação após desastre.  
  -   O Configuration Manager suporta utilizando a réplica de consolidação assíncrona para recuperar a réplica síncrona. Consulte [opções de recuperação de base de dados do site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico cópia de segurança e recuperação para obter informações sobre como efetuar este procedimento.
  -   Esta versão não suporta a ativação pós-falha para utilizar a réplica de consolidação assíncrona como a base de dados do site.
Para obter mais informações, consulte [preparar a utilização de grupos de disponibilidade Always](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="update-reset-tool"></a>Ferramenta de reposição de atualização
<!-- 1324589 -->
Início com versão 1706, sites de administração central e sites primários do Configuration Manager, incluir a atualização de reposição de ferramenta do Configuration Manager, **CMUpdateReset.exe**. Utilize esta ferramenta com qualquer versão do ramo atual, que permanece no suporte, para corrigir os problemas quando as atualizações na consola tem problemas de transferir ou replicar. Para obter mais informações, consulte [ferramenta de reposição de atualização](/sccm/core/servers/manage/update-reset-tool).

### <a name="high-dpi-console-support"></a>Suporte da consola PPP elevado  
<!-- 1353476 -->
Com esta versão, problemas com como a consola do Configuration Manager dimensiona e apresenta as diferentes partes da IU quando são visualizados em dispositivos de PPP elevados (como uma superfície book) devem ser corrigidos.

### <a name="improved-boundary-groups-for-software-update-points"></a>Grupos de limites melhorada para pontos de atualização de software
<!-- 1324591 -->
Esta versão inclui melhoramentos para como funcionam os pontos de atualização de software com grupos de limites. O seguinte resume o novo comportamento de contingência:
-   Agora, a contingência para pontos de atualização de software utiliza um período de tempo configurável para contingência aos grupos de limites de vizinho.
-   Independentemente da configuração de contingência, um cliente tenta contactar o último ponto de atualização de software que é utilizado para 120 minutos. Após a conseguir aceder esse servidor para 120 minutos, o cliente procurará em seguida o conjunto de pontos de atualização de software disponíveis, para que possa encontrar um novo.
-   Depois de conseguir contactar o respetivo servidor original de duas horas, o cliente muda para um ciclo mais curto para contactar um ponto de atualização de software novo. Isto significa que o se um cliente não conseguir estabelecer ligação com um novo servidor, rapidamente seleciona o servidor seguinte do seu agrupamento de servidores disponíveis e tentará entrar em contacto de um.

Para obter mais informações, consulte [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) o tópico de grupos de limites para o ramo atual.

### <a name="azure-ad-integration-with-configuration-manager"></a>Integração do AD do Azure com o Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
Com esta versão, iremos tem melhorado a integração do Configuration Manager e o Azure Active Directory (Azure AD).  Estas melhorias simplificam como configurar os serviços do Azure que utiliza com o Configuration Manager e ajudá-lo a gerir os clientes e utilizadores que autenticarem apesar do Azure AD.

A integração melhorada possibilita o seguinte:  
  -   Assistente de serviços do Azure – este assistente fornece uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os seguintes serviços do Azure que utiliza com o Configuration Manager.
      - **Gestão de nuvem** permitir que os clientes autenticar com o Azure Active Directory (Azure AD). Também pode configurar a deteção de utilizador do Azure AD.
      - **Conector do OMS** ligar aos dados do Operations Manager Suite (OMS) e a sincronização, como coleções para análise de registos do OMS.
      - **Preparação para a atualização** ligar a preparação de atualização e ver dados de compatibilidade de atualização de cliente.
      - **Loja Windows para empresas** ligar para a loja online para a loja Windows para empresas e obter aplicações da sua organização que pode implementar com o Configuration Manager.


  Isto é feito utilizando um [aplicação de web do servidor do Azure](/azure/azure/app-service/app-service-authentication-overview#service-to-service-authentication) para fornecer os detalhes da subscrição e a configuração que introduziu, caso contrário, sempre que configurou um novo componente do Configuration Manager ou o serviço com o Azure. Para obter mais informações, consulte [Assistente de serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).

-   Utilize o Azure AD para autenticar clientes na Internet para aceder os sites do Configuration Manager. Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação de cliente. Isto requer a função de sistema de sites de gateway de gestão de nuvem. Para obter mais informações, consulte [instale e atribua clientes do Configuration Manager a partir da Internet com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Instalar e gerir o cliente do Configuration Manager em computadores que estão localizados na Internet. Isto requer a utilização da função de sistema de site de gateway de gestão de nuvem. Para obter mais informações, consulte [instale e atribua clientes do Configuration Manager a partir da Internet com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Configure a deteção de utilizador do Azure AD.  Utilize o Assistente de serviços do Azure para configurar este novo método de deteção. Este novo método de consulta o seu Azure AD para dados de utilizador, em seguida, pode utilizar dados de deteção tradicional no lado a lado.  Sincronização completa e diferenças são suportadas.  Para obter mais informações consulte [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

### <a name="peer-cache-improvements"></a>Melhorias da cache ponto a ponto
<!-- 1252345 -->
Cache ponto a ponto já não utiliza a conta de acesso de rede para autenticar pedidos de transferência de elementos. Há uma advertência a esta quando a conta permanece necessário por parte dos clientes. Este permanece um requisito para clientes que arrancam no WinPE e, em seguida, aceder aos conteúdos de uma origem de cache ponto a ponto. Para obter mais informações, consulte [requisitos e considerações para a cache ponto a ponto](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Novas definições de configuração para dispositivos Windows 10 que não são geridos com o cliente do Configuration Manager
<!-- 1354715 -->
Nesta versão, adicionámos novas definições de item de configuração para dispositivos Windows 10 que estão inscritos no Intune ou geridos no local pelo Configuration Manager. As definições são:

- **Palavra-passe**
    - Encriptação de dispositivos
- **Dispositivo**
    - Modificação de definições de região (apenas ambiente de trabalho)
    - Modificação de definições de energia e o modo de suspensão
    - Modificação das definições de idioma
    - Modificação de hora do sistema
    - Modificação de nome de dispositivo
- **Arquivo**
    - As aplicações da loja de atualização automática
    - Utilizar apenas o arquivo privado
    - Armazenar iniciação da aplicação teve origem
- **Microsoft Edge**
    - Bloquear o acesso ao sobre: sinalizadores
    - Substituição de linha de comandos do SmartScreen
    - Substituição de linha de comandos SmartScreen de ficheiros
    - Endereço IP localhost WebRTC
    - Motor de busca predefinido
    - URL de OpenSearch XML
    - Homepages (apenas ambiente de trabalho)

Para detalhes de todas as definições do Windows 10, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).

### <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade de dispositivo

* **Tipo de palavra-passe obrigatório**. Especifique se o utilizador tem de criar uma palavra-passe alfanumérica ou uma palavra-passe numérico. Palavras-passe alfanuméricos, também especificar o número mínimo de conjuntos de carateres que a palavra-passe tem de ter. Os quatro conjuntos de carateres são: Letras minúsculas, maiúsculas, símbolos e números.

 **Suportado no:**
 * Windows Phone 8+
 * Windows 8.1 +
 * iOS 6+
<br></br>
* **Depuração USB de bloco no dispositivo**. Não é necessário configurar esta definições como a depuração USB já está desativada no Android para dispositivos de trabalho.

 **Suportado no:**
 * Android 4.0+
 * Samsung KNOX Standard 4.0+
<br></br>
* **Impedir que as aplicações a partir de origens desconhecidas**. Exigir que os dispositivos impeçam a instalação de aplicações a partir de origens desconhecidas. Não é necessário configurar esta definição, tal como Android, para dispositivos de trabalho sempre restringir a instalação a partir de origens desconhecidas.

  **Suportado no:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Necessária análise de ameaças nas aplicações**. Esta definição especifica que a funcionalidade de aplicações de Verifique está ativada no dispositivo.

 **Suportado no:**
 * Android 4.2 através de 4.4
 * Samsung KNOX Standard 4.0+

Consulte [criar e implementar uma política de conformidade do dispositivo](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) para experimentar as novas regras de conformidade do dispositivo

## <a name="application-management"></a>Gestão de Aplicações

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Executar scripts do PowerShell a partir da consola do Configuration Manager
<!-- 1236459 -->

No Configuration Manager, pode implementar scripts de utilização de pacotes e programas em dispositivos cliente. Nesta versão, adicionámos novas funcionalidades que lhe permite efetuar as seguintes ações:

- Importar Scripts do PowerShell para o Configuration Manager
- Editar os scripts a partir da consola do Configuration Manager (para apenas scripts não assinados)
- Scripts de marca como aprovado ou negado, para melhorar a segurança
- Executar scripts em coleções de computadores de cliente do Windows e no local geridos Windows PCs. Não implementa scripts, em vez disso, são sejam executados em tempo real nos dispositivos cliente.
- Examine os resultados devolvidos pelo script na consola do Configuration Manager.

Para obter mais informações, consulte [criar e executadas scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

### <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis    
<!--1324760-->
A partir desta versão, pode utilizar três novas aplicações móveis (MAM) definições de política:

- **Bloquear captura de ecrã (apenas dispositivos Android):** Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.

Consulte [proteger aplicações ao utilizar políticas de proteção de aplicações no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para experimentar as novas definições de política de proteção de aplicação.


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="hardware-inventory-collects-secure-boot-information"></a>Inventário de hardware recolhe informações de arranque seguro
Inventário de hardware agora recolhe informações sobre se o arranque seguro está ativado nos clientes. Esta informação é armazenada no **SMS_Firmware** classe (introduzida na versão 1702) e de hardware ativado no inventário por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="collapsible-task-sequence-groups"></a>Grupos de sequências de tarefas expansível
Esta versão apresenta a capacidade para expandir e fechar a grupos de sequências de tarefas. Pode expandir ou fechar grupos individuais ou expandir ou fechar todos os grupos em simultâneo.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Volte a carregar as imagens de arranque com a versão atual do Windows PE
Quando executa **atualizar pontos de distribuição** numa imagem de arranque selecionada, agora, pode escolher recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de arranque. Para obter mais informações, consulte [atualizar pontos de distribuição com a imagem de arranque](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Atualizações de software

### <a name="improvements-to-express-update-download-time"></a>Tempo de transferência de melhorias à atualização Express
Nesta versão, podemos ter melhorado significativamente o tempo de transferência Express atualizações. Para obter mais informações, consulte [ficheiros de instalação gerir Express para Windows 10 das atualizações](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

### <a name="manage-microsoft-surface-driver-updates"></a>Gerir atualizações de controladores Microsoft Surface
<!-- 1098490 -->
Agora, pode utilizar o Configuration Manager para gerir atualizações de controladores Microsoft Surface.    


#### <a name="prerequisites"></a>Pré-requisitos
- Todos os pontos de atualização de software devem executar o Windows Server 2016.    
- Esta é uma funcionalidade de pré-lançamento que tem de ativar para que fique disponível. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Para gerir atualizações de controladores superfície

1. Ative a sincronização para o Microsoft Surface. Utilize o procedimento no [configurar classificação e produtos](/sccm/sum/get-started/configure-classifications-and-products) e selecione o **incluem o Microsoft Surface controladores e as atualizações de firmware** caixa de verificação no **classificações** separador para ativar a superfície controladores.
2. [Sincronizar os controladores Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates).
3. [Implementar controladores de Microsoft Surface sincronizadas](/sccm/sum/deploy-use/deploy-software-updates)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar o Windows Update para as políticas de diferimento por de negócio
<!-- 1290890 -->
Agora, pode configurar políticas de diferimento por para atualizações de funcionalidade do Windows 10 ou qualidade atualizações para o Windows 10 dispositivos geridos diretamente pelo Windows Update for Business. Pode gerir as políticas de diferimento por na nova **Windows Update para as políticas de negócio** nó **biblioteca de Software** > **manutenção do Windows 10**.

Para obter mais informações, consulte [integração com o Windows Update for Business no Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Melhorado notificações de utilizador para atualizações do Office 365
Foram efetuados melhoramentos ao tirar partido a experiência de utilizador do Office Clique para execução quando um cliente instala uma atualização do Office 365. Isto inclui uma experiência de contagem decrescente e notificações de pop-up e na aplicação. Para obter mais informações, consulte [reinício notificações de comportamento e o cliente de atualizações do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)

## <a name="reporting"></a>Relatórios

### <a name="use-windows-analytics-with-configuration-manager"></a>Utilize a análise do Windows com o Configuration Manager
<!-- 1318608 -->
A análise do Windows é um conjunto de soluções que são executados no Operations Management Suite. As soluções permitem-lhe conhecimentos aprofundados de formulário para o estado atual do seu ambiente. Dispositivos no seu ambiente reportam dados de telemetria do Windows. Os dados podem ser acedidos através do portal web do Operations Management Suite. No caso de preparação de atualizar os dados estão diretamente disponíveis no nó de monitorização da consola do Configuration Manager.

Para obter mais informações, consulte [utilize Windows Analytics com o Configuration Manager](/sccm/core/clients/manage/monitor-windows-analytics).


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="updates-to-android-for-work-sharing-configuration"></a>Atualizações para o Android para a configuração de partilha de trabalho
<!-- 1338403 -->
Com esta versão, os valores para o **permitir partilha de dados entre a vida profissional e a pessoal perfil** definição o **trabalhar perfil** a definição de grupo foram atualizadas. Também adicionámos um personalizado definição para bloquear o copiar-colar entre perfis pessoais e de trabalho.

Para obter mais informações, consulte [itens de configuração para Android para dispositivos de trabalho](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client).

### <a name="android-and-ios-enrollment-restrictions"></a>Restrições de inscrição do Android e iOS
<!-- 1290826 -->
Com esta versão, pode agora especificar que os utilizadores não é possível inscrever dispositivos pessoais, Android ou iOS. Novas definições de restrição de dispositivo permitem-lhe limitar a inscrição de dispositivos Android predeclared dispositivos. Para dispositivos iOS, pode bloquear a inscrição de todos os dispositivos, exceto aos que estão inscritos no programa de inscrição de dispositivos da Apple, configurador da Apple ou a conta de Gestor de inscrição de dispositivos do Intune.
- Para obter mais informações sobre restrições de inscrição de dispositivos Android, consulte [configurar a gestão de dispositivos Android](/sccm/mdm/deploy-use/enroll-hybrid-android).
- Para obter mais informações sobre restrições de inscrição de iOS, consulte [configurar restrições de inscrição de iOS](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Incluir confiança para pastas e ficheiros específicos numa política de proteção de dispositivos
<!--1324676-->
Nesta versão, adicionámos mais capacidades para gestão de políticas de proteção de dispositivos.

Opcionalmente, agora pode adicionar o confiança para ficheiros específicos para pastas numa política Device Guard. Isto permite-lhe:

- Ultrapassar problemas com os comportamentos de instalador gerido
- Aplicações de linha de negócio de confiança que não não possível implementar com o Configuration Manager
- As aplicações que estão incluídas numa imagem de implementação do sistema operativo de confiança

Para obter mais detalhes, consulte [gestão Device Guard com o Configuration Manager](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
