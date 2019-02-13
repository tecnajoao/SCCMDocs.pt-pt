---
title: Cogestão para os dispositivos com Windows 10
titleSuffix: Configuration Manager
description: Saiba como ao mesmo tempo gerir dispositivos Windows 10 com o Configuration Manager e o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: c88bf98e035499c271de8acf9d8fa222e5058447
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132629"
---
# <a name="what-is-co-management"></a>O que é a cogestão?

<!-- 1350871 --> A cogestão é uma das formas de ligar a sua implementação do Configuration Manager existente para a cloud do Microsoft 365 primárias. Ele ajuda a desbloquear funcionalidades adicionais com tecnologia de cloud, como o acesso condicional. 

A cogestão permite-lhe ao mesmo tempo gerir dispositivos Windows 10 com o Configuration Manager e o Microsoft Intune. Ele permite que anexe na cloud de seu investimento existente no Configuration Manager ao adicionar novas funcionalidades. Usando a cogestão, tem a flexibilidade para utilizar a solução de tecnologia que funciona melhor para a sua organização. 

Quando um dispositivo Windows 10 tem o cliente do Configuration Manager e é inscrito no Intune, obtém os benefícios de ambos os serviços. Pode controlar quais cargas de trabalho, se houver, que mudar a autoridade do Configuration Manager para o Intune. O Configuration Manager continua a gerir todas as outras cargas de trabalho, incluindo essas cargas de trabalho que não mude para o Intune e não oferece suporte a todos os outros recursos do Configuration Manager que cogestão.

Também pode criar um piloto de uma carga de trabalho com um conjunto separado de dispositivos. Criação de pilotos permite-lhe testar a funcionalidade do Intune com um subconjunto de dispositivos antes de mudar de um grupo maior. 

![Diagrama de descrição geral de cogestão](media/co-management-overview.png)



## <a name="paths-to-co-management"></a>Caminhos para a cogestão

Existem dois caminhos principais para entrar em contacto cogestão:  

- **Os clientes existentes do Configuration Manager**: Tiver dispositivos Windows 10 que já são clientes do Configuration Manager. Configurar o Azure AD híbrido e inscrevê-los no Intune.  

- **Novos dispositivos baseados na internet**: Tem novos dispositivos Windows 10 associados ao Azure AD e inscreverem-se automaticamente para o Intune. Instalar o cliente do Configuration Manager para atingir um Estado de cogestão.  

Para obter mais informações sobre os caminhos, consulte [caminhos para a cogestão](/sccm/comanage/quickstart-paths).



## <a name="benefits"></a>Benefícios 

Quando inscreve os clientes existentes do Configuration Manager na cogestão, obterá o seguinte valor de imediato:  

- Acesso condicional com a conformidade do dispositivo  

- Ações de remotas baseada no Intune, por exemplo: reinício, controlo remoto ou reposição de fábrica

- Visibilidade centralizada do Estado de funcionamento do dispositivo  

- Associar utilizadores, dispositivos e aplicações com o Azure Active Directory (Azure AD)  

- Modernos de aprovisionamento com o Windows Autopilot  

- Ações remotas

Para obter mais informações sobre este valor imediato da cogestão, consulte a série de guias de introdução para [Cloud connect com cogestão](/sccm/comanage/quickstarts).

Cogestão também lhe permite orquestrar com o Intune para várias cargas de trabalho. Para obter mais informações, consulte a [cargas de trabalho](#workloads) secção. 



## <a name="prerequisites"></a>Pré-requisitos

Cogestão tem estes pré-requisitos nas seguintes áreas:

- [Licenciamento](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Funções e permissões](#permissions-and-roles)  

### <a name="licensing"></a>Licensing

- Azure AD Premium 
- Licença do Intune ou do EMS para todos os utilizadores  

    > [!Note]  
    > Uma Enterprise Mobility + Security (EMS) a subscrição inclui o Azure Active Directory Premium e o Microsoft Intune.

> [!Tip]  
> Certifique-se de que atribuir uma licença do Intune à conta que utiliza para iniciar sessão no seu inquilino. Caso contrário, início de sessão falhar com a mensagem de erro "O utilizador não reconhecido".  


### <a name="configuration-manager"></a>Configuration Manager

Cogestão requer o Configuration Manager versão 1710 ou posterior.

A partir do Configuration Manager versão 1806, pode ligar várias instâncias do Configuration Manager para um único inquilino do Intune. <!--1357944-->  

Ativar a cogestão em si não requer que carregar seu site com o Azure AD. Para o [segundo cenário de caminho](#paths-to-co-management), a clientes baseados na internet do Configuration Manager requerem o [gateway de gestão da nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG). O CMG requer o site é [integrado com o Azure AD para gestão na cloud](/sccm/core/servers/deploy/configure/azure-services-wizard). 


### <a name="azure-ad"></a>Azure AD

- Dispositivos Windows 10 têm de ser associados ao Azure AD. Eles podem ser qualquer um dos seguintes tipos:  

    - [Azure híbrido associado ao AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), em que o dispositivo é associado ao Active Directory no local e registado com o Azure Active Directory.  

    - [Azure AD associado](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) apenas. (Este tipo é por vezes referido como "cloud associados a um domínio")<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [Configurar o Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Ativar a inscrição automática do Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> Se tiver um ambiente de MDM híbrido (Intune integrado com o Configuration Manager), não é possível ativar a cogestão. No entanto, pode começar a migrar utilizadores para o Intune autónomo e, em seguida, ativar os dispositivos Windows 10 associados para a cogestão. Para obter mais informações sobre a migração para o Intune autónomo, consulte [iniciar a migração da MDM híbrida para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  
> 
> Se estiver a utilizar [misto autoridade](/sccm/mdm/deploy-use/migrate-mixed-authority), primeiro concluir a migração para o Intune autónomo. Em seguida, defina a autoridade de MDM ao Intune antes de configurar cogestão.<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

Atualize os seus dispositivos para Windows 10, versão 1709 ou posterior. Para obter mais informações, consulte [adotar o Windows como um serviço](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não suportam a cogestão.


### <a name="permissions-and-roles"></a>Funções e permissões
<!--SCCMDocs issue #667-->

| Action | Função necessária |
|----|----|
| Configurar um gateway de gestão de nuvem no Configuration Manager | Azure **Gestor de subscrições** |
| Criar aplicações do Azure AD a partir do Configuration Manager | O Azure AD **Administrador Global** |
| Importar aplicações do Azure no Configuration Manager | O Configuration Manager **administrador total**<br>Não existem funções do Azure adicionais necessárias |
| Ativar a cogestão no Configuration Manager | Um utilizador do Azure AD<br>O Configuration Manager **administrador total** com **todos os** definir o âmbito direitos.<!--SCCMDoc issue 626--> | 

Para obter mais informações sobre as funções do Azure, consulte [compreender as diferentes funções](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Para obter mais informações sobre funções do Configuration Manager, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).


## <a name="workloads"></a>Cargas de trabalho 

Não tem de mudar as cargas de trabalho, ou pode fazê-los individualmente quando estiver pronto. O Configuration Manager continua a gerir todas as outras cargas de trabalho, incluindo essas cargas de trabalho que não mude para o Intune e não oferece suporte a todos os outros recursos do Configuration Manager que cogestão.

Cogestão suporta as seguintes cargas de trabalho:

- Políticas de conformidade  

- Políticas de atualização do Windows  

- Políticas de acesso de recursos  

- Endpoint Protection  

- Configuração do dispositivo  

- Aplicações de clique-e-Use do Office  

- Aplicações de cliente  

Para obter mais informações, consulte [cargas de trabalho](/sccm/comanage/workloads).



## <a name="monitor-co-management"></a>Monitorizar a cogestão

O dashboard de cogestão ajuda-o a rever as máquinas que fazem cogeridas no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que possam necessitar de atenção.

![Captura de ecrã do dashboard de cogestão](media/co-management-dashboard.png)

Para obter mais informações, consulte [como monitorizar a cogestão](/sccm/comanage/how-to-monitor).



## <a name="next-steps"></a>Passos seguintes

- [Saiba mais sobre o valor imediato e começar a cogestão](/sccm/comanage/quickstarts)  

- [Tutorial: Ativar a cogestão para os clientes existentes do Configuration Manager](/sccm/comanage/tutorial-co-manage-clients)  

