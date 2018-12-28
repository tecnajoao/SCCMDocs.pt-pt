---
title: Nova versão 1706
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1706 do System Center Configuration Manager.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a9fe9c0b2f779558161e7995a01863e6415838ee
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423087"
---
# <a name="what39s-new-in-version-1706-of-system-center-configuration-manager"></a>O que&#39;s novo na versão 1706 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualização 1706 para o ramo atual do System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1606, 1610 ou 1702.

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalar atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre alterações e novas funcionalidades introduzidas na versão 1706 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Suporte de Cache ponto a ponto do cliente para ficheiros de instalação rápida do Windows 10 e Office 365  
<!-- 1352486 --> A partir desta versão, Cache ponto a ponto suporta a distribuição de ficheiros de conteúdo de instalação rápida para o Windows 10 e de ficheiros de atualização para o Office 365. Sem configurações adicionais necessários para suportar esta alteração.

### <a name="updates-for-the-data-warehouse"></a>Atualizações para o armazém de dados
<!-- 1277922 --> O armazém de dados já não é uma funcionalidade de pré-lançamento. Também atualizámos os pré-requisitos para incluir suporte para a base de dados no SQL Server sempre em grupos de disponibilidade e clusters de ativação pós-falha. Para obter mais informações, consulte [ponto de serviço do armazém de dados a](/sccm/core/servers/manage/data-warehouse).

### <a name="accessibility-improvements"></a>Melhorias de acessibilidade
<!-- 1253000 --> Adicionámos aprimoramentos adicionais para acessibilidade para a consola do Configuration Manager. Para obter detalhes, consulte [funcionalidades de acessibilidade](/sccm/core/understand/accessibility-features).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Melhorias para o SQL Server, grupos de disponibilidade Always On
<!-- 1352094 --> Com esta versão, agora, pode utilizar réplicas de consolidação assíncrona dos grupos de disponibilidade Always On do SQL Server na que utiliza com o Configuration Manager. Isso significa que pode adicionar réplicas adicionais aos seus grupos de disponibilidade para utilizar como cópias de segurança externas (remotas) e, em seguida, utilizá-los num cenário de recuperação após desastre.  
  -   O Configuration Manager suporta a utilizar a réplica de consolidação assíncrona para recuperar sua réplica síncrona. Ver [opções de recuperação de base de dados do site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico cópia de segurança e recuperação para obter informações sobre como fazer isso.
  -   Esta versão não suporta a ativação pós-falha para utilizar a réplica de consolidação assíncrona como a base de dados do site.
Para obter mais informações, consulte [preparar a utilização de grupos de Disponibilidade AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="update-reset-tool"></a>Ferramenta de reposição de atualizações
<!-- 1324589 --> Que começa com a versão 1706, sites de administração central e sites primários do Configuration Manager, incluir a atualização de reposição de ferramenta do Configuration Manager, **CMUpdateReset.exe**. Utilize esta ferramenta com qualquer versão do ramo atual no suporte, para corrigir os problemas quando as atualizações na consola tem problemas ao transferir ou replicar. Para obter mais informações, consulte [ferramenta de reposição de atualizações](/sccm/core/servers/manage/update-reset-tool).

### <a name="high-dpi-console-support"></a>Suporte da consola DPI alta  
<!-- 1353476 --> Com esta versão, os problemas com como a consola do Configuration Manager pode ser dimensionada e apresenta diferentes partes da interface do Usuário quando visualizadas em dispositivos DPI altos (como um livro superfície) devem ser corrigidos.

### <a name="improved-boundary-groups-for-software-update-points"></a>Grupos de limites melhorada para os pontos de atualização de software
<!-- 1324591 --> Esta versão inclui melhoramentos para como os pontos de atualização de software trabalham com grupos de limites. Os itens abaixo resumem o novo comportamento de contingência:
-   Agora, a contingência para pontos de atualização de software utiliza um horário configurável para contingência aos grupos de limite vizinho.
-   Independentemente da configuração de contingência, um cliente tenta contactar o último ponto de atualização de software, utilizada para 120 minutos. Depois de a conseguir chegar a esse servidor para 120 minutos, o cliente verifica, em seguida, seu pool de pontos de atualização de software disponíveis, para que ele possa encontrar um novo.
-   Depois de a conseguir contactar o respetivo servidor original de duas horas, o cliente muda para um ciclo mais curto para entrar em contato com um novo ponto de atualização de software. Isso significa que se um cliente não conseguir estabelecer ligação com um novo servidor, ele, rapidamente, seleciona o próximo servidor a partir do seu pool de servidores disponíveis e tenta contactar o que um.

Para obter mais informações, consulte [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) o tópico de grupos de limites para o ramo atual.

### <a name="azure-ad-integration-with-configuration-manager"></a>Integração do Azure AD com o Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 --> Com esta versão, melhorámos a integração do Configuration Manager e o Azure Active Directory (Azure AD).  Esses aprimoramentos simplificam como configurar os serviços do Azure que utiliza com o Configuration Manager e ajudá-lo a gerir os clientes e os utilizadores que autenticam, embora, do Azure AD.

A integração aprimorada possibilita o seguinte:  
  -   Assistente de serviços do Azure – este assistente fornece uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os seguintes serviços do Azure que utilizar com o Configuration Manager.
      - **Gestão da cloud** permitem que os clientes autenticar com o Azure Active Directory (Azure AD). Também pode configurar a deteção de utilizador do Azure AD.
      - **Conector de análise de registo** ligar ao Azure Log Analytics e sincronizar dados de coleção.
      - **Preparação de atualizações** ligar à preparação de atualizações e ver dados de compatibilidade de atualização de cliente.
      - **Windows Store para empresas** Connect para a loja online para a Windows Store para empresas e obter aplicações para a sua organização que pode implementar com o Configuration Manager.


  Isso é feito usando uma [o servidor do Azure web app](/azure/azure/app-service/app-service-authentication-overview#service-to-service-authentication) para fornecer os detalhes de subscrição e a configuração que caso contrário, introduzir sempre que configurou um novo componente do Configuration Manager ou o serviço com o Azure. Para obter mais informações, consulte [Assistente de serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).

-   Utilize o Azure AD para autenticar clientes na Internet para aceder aos seus sites do Configuration Manager. O Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação de cliente. Isto requer a função de sistema de sites de gateway de gestão de cloud. Para obter mais informações, consulte [instalar e atribuir clientes do Configuration Manager a partir da Internet com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Instalar e gerir o cliente do Configuration Manager em computadores que estão localizados na Internet. Isto requer a utilização da função de sistema de sites de gateway de gestão de cloud. Para obter mais informações, consulte [instalar e atribuir clientes do Configuration Manager a partir da Internet com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Configure a deteção de utilizador do Azure AD.  Utilize o Assistente de serviços do Azure para configurar este novo método de deteção. Este novo método de consulta do Azure AD para os dados de utilizador, em seguida, pode utilizar os dados de deteção do tradicional ao longo de lado.  Sincronização diferenciais e completas são suportadas.  Para obter mais informações, consulte [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

### <a name="peer-cache-improvements"></a>Melhorias da cache ponto a ponto
<!-- 1252345 --> Cache ponto a ponto já não utiliza a conta de acesso de rede para autenticar pedidos de transferência de colegas. Há um probleminha aqui quando o conta permanece solicitados pelos clientes. Isto continua a ser um requisito para clientes que arrancam no WinPE e, em seguida, aceder a conteúdo de uma origem de cache ponto a ponto. Para obter mais informações, consulte [requisitos e considerações para a cache ponto a ponto](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Novas definições de configuração para dispositivos Windows 10 que não são geridos com o cliente do Configuration Manager
<!-- 1354715 --> Nesta versão, adicionámos novas definições de item de configuração para dispositivos Windows 10 que estão inscritos no Intune ou geridos no local pelo Configuration Manager. As definições são:

- **Palavra-passe**
    - Encriptação de dispositivos
- **Dispositivo**
    - Modificação das definições de região (apenas ambiente de trabalho)
    - Modificação das definições de energia e suspensão
    - Modificação de definições de idioma
    - Modificação da hora do sistema
    - Modificação do nome do dispositivo
- **Store**
    - Atualização automática de aplicações da loja
    - Utilizar apenas loja privada
    - Lançamento de aplicação originado pela Store
- **Microsoft Edge**
    - Bloquear o acesso a about: flags
    - Substituição do pedido SmartScreen
    - Substituição do pedido SmartScreen para ficheiros
    - Endereço IP de localhost do WebRTC
    - Motor de busca predefinido
    - URL XML do OpenSearch
    - Home Pages (apenas ambiente de trabalho)

Para obter detalhes de todas as definições do Windows 10, veja [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).

### <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade de dispositivo

* **Tipo de palavra-passe obrigatório**. Especifique se o utilizador tem de criar uma palavra-passe de alfanumérica ou de uma palavra-passe numérica. Para as palavras-passe de alfanuméricas, também especificar o número mínimo de conjuntos de carateres que a palavra-passe tem de ter. Os conjuntos de quatro caracteres são: Letras em minúsculas, letras maiúsculas, símbolos e números.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
  <br></br>
* **Depuração de USB de bloco no dispositivo**. Não é necessário configurar esta definição, como a depuração USB já se encontra desativada em dispositivos Android para dispositivos de trabalho.

  **Suportado no:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Bloquear aplicações de origens desconhecidas**. Exigir que os dispositivos impeçam a instalação de aplicações de origens desconhecidas. Não tem de configurar esta definição como dispositivos Android for Work restringem sempre a instalação de origens desconhecidas.

  **Suportado no:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Exigir análise de ameaças nas aplicações**. Esta definição especifica que a funcionalidade de aplicações Verifique se está ativada no dispositivo.

  **Suportado no:**
  * Android 4.2 a 4.4 através de
  * Samsung KNOX Standard 4.0+

Ver [criar e implementar uma política de conformidade do dispositivo](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) para experimentar as novas regras de conformidade do dispositivo

## <a name="application-management"></a>Gestão de Aplicações

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Executar scripts do PowerShell a partir da consola do Configuration Manager
<!-- 1236459 -->

No Configuration Manager, pode implementar scripts em dispositivos de cliente através de pacotes e programas. Nesta versão, adicionámos novas funcionalidades que lhe oferece as seguintes ações:

- Importar Scripts do PowerShell para o Configuration Manager
- Editar os scripts a partir da consola do Configuration Manager (para apenas scripts não assinados)
- Scripts de Mark como aprovado ou negado, para melhorar a segurança
- Executar scripts em coleções de PCs de cliente do Windows e no local geridos Windows PCs. Não precisa implementar scripts, em vez disso, estas são executadas em tempo real nos dispositivos cliente.
- Examine os resultados devolvidos pelo script na consola do Configuration Manager.

Para obter mais informações, consulte [criar e executar scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

### <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis    
<!--1324760--> A partir desta versão, pode utilizar três novas definições de política do aplicações móveis (MAM) de gestão:

- **Bloquear captura de ecrã (apenas dispositivos Android):** Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.

Ver [proteger aplicações através de políticas de proteção de aplicações no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para experimentar as novas definições de política de proteção de aplicações.


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="hardware-inventory-collects-secure-boot-information"></a>Inventário de hardware recolhe informações de arranque seguro
Agora o inventário de hardware recolhe informações sobre se o arranque seguro está ativado nos clientes. Essas informações são armazenadas no **SMS_Firmware** classe (introduzida na versão 1702) e ativado no hardware de inventário por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="collapsible-task-sequence-groups"></a>Grupos de sequências de tarefas minimizáveis
Esta versão apresenta a capacidade para expandir e recolher grupos de sequências de tarefas. Pode expandir ou fechar grupos individuais ou expandir ou fechar todos os grupos de uma só vez.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Volte a carregar imagens de arranque com a versão atual do Windows PE
Quando executa **atualizar pontos de distribuição** numa imagem de arranque selecionada, pode agora escolher recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de arranque. Para obter mais informações, consulte [atualizar pontos de distribuição com a imagem de arranque](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Atualizações de software

### <a name="improvements-to-express-update-download-time"></a>Tempo de transferência de melhorias ao Express Update
Nesta versão, podemos melhoraram significativamente o tempo de transferência para atualizações de Express. Para obter mais informações, consulte [ficheiros de instalação de gerir Express para Windows 10 das atualizações](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

### <a name="manage-microsoft-surface-driver-updates"></a>Gerir atualizações de controladores do Microsoft Surface
<!-- 1098490 --> Agora, pode utilizar o Configuration Manager para gerir atualizações de controladores do Microsoft Surface.    


#### <a name="prerequisites"></a>Pré-requisitos
- Todos os pontos de atualização de software devem executar o Windows Server 2016.    
- Esta é uma funcionalidade de pré-lançamento que tem de ativar para que fique disponível. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Para gerir atualizações de controlador do Surface

1. Ative a sincronização para controladores do Microsoft Surface. Utilize o procedimento [configurar a classificação e produtos](/sccm/sum/get-started/configure-classifications-and-products) e selecione o **drivers de incluir o Microsoft Surface e atualizações de firmware** caixa de seleção o **classificações**separador para ativar os controladores superfície.
2. [Sincronizar os controladores do Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates).
3. [Implementar controladores sincronizados do Microsoft Surface](/sccm/sum/deploy-use/deploy-software-updates)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar a atualização do Windows para políticas de diferimento de negócios
<!-- 1290890 --> Agora, pode configurar políticas de diferimento para atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para o Windows 10 dispositivos geridos diretamente pelo Windows Update para empresas. Pode gerir as políticas de diferimento no novo **Windows Update para políticas de negócio** no nó **biblioteca de Software** > **manutenção do Windows 10**.

Para obter detalhes, consulte [integração com o Windows Update for Business no Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Melhorada a notificações de utilizador para atualizações do Office 365
Foram feitos aprimoramentos para aproveitar a experiência de utilizador do Office Click-to-Run, quando um cliente instala uma atualização do Office 365. Isto inclui notificações de pop-up e na aplicação e uma experiência de contagem regressiva. Para obter mais informações, consulte [reiniciar as notificações de comportamento e de cliente para atualizações do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)

## <a name="reporting"></a>Relatórios

### <a name="use-windows-analytics-with-configuration-manager"></a>Utilize o Windows Analytics com o Configuration Manager
<!-- 1318608 --> A análise do Windows é um conjunto de soluções que permitem-lhe informações de formulário para o estado atual do seu ambiente. Dispositivos no seu ambiente reportam dados de telemetria do Windows. Os dados podem ser acedidos através do portal do Azure. No caso de preparação de atualizações, os dados estão diretamente disponíveis no nó de monitorização da consola do Configuration Manager.

Para obter mais informações, consulte [utilize o Windows Analytics com o Configuration Manager](/sccm/core/clients/manage/monitor-windows-analytics).


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="updates-to-android-for-work-sharing-configuration"></a>Atualizações para o Android for Work a configuração de partilha
<!-- 1338403 --> Com esta versão, os valores para o **permitir a partilha de dados entre o perfil profissional e pessoal** definição **perfil de trabalho** a definição de grupo foram atualizados. Também adicionámos um personalizado na definição de bloquear copiar-colar entre perfis pessoais e de trabalho.

Para obter mais informações, consulte [itens de configuração para Android para dispositivos de trabalho](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client).

### <a name="android-and-ios-enrollment-restrictions"></a>Restrições de inscrição de Android e iOS
<!-- 1290826 --> Com esta versão, agora pode especificar que os utilizadores podem inscrever dispositivos Android ou iOS pessoais. Novas definições de restrição de dispositivos permitem-lhe limitar a inscrição de dispositivos Android para dispositivos pré-declarados. Para dispositivos iOS, pode bloquear a inscrição de todos os dispositivos, exceto aqueles inscrito no programa de inscrição de dispositivos da Apple, Apple Configurator ou a conta de Gestor de inscrição de dispositivos do Intune.
- Para obter mais informações sobre restrições de inscrição de dispositivos Android, consulte [configurar a gestão de dispositivos Android](/sccm/mdm/deploy-use/enroll-hybrid-android).
- Para obter mais informações sobre restrições de inscrição do iOS, veja [configurar restrições de inscrição de iOS](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Incluir a fidedignidade para ficheiros específicos e pastas numa política de Device Guard
<!--1324676--> Nesta versão, adicionámos mais capacidades para gestão de políticas de Device Guard.

Agora pode adicionar opcionalmente confiança em arquivos específicos para pastas de uma política do Device Guard. Isto permite-lhe:

- Resolver problemas com os comportamentos de instalador gerido
- Confiar em aplicações de linha de negócio que não não possível implementar com o Configuration Manager
- Confiar em aplicações que estão incluídas numa imagem de implantação do sistema operativo

Para obter mais detalhes, consulte [gestão de Device Guard com o Configuration Manager](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
