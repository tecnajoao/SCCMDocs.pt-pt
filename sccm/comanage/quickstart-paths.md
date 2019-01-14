---
title: Caminhos de cogestão
titleSuffix: Configuration Manager
description: Compreenda os pré-requisitos para as duas principais formas para que possa configurar cogestão.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 619b411dfa0d6949e84d52d5610621eb3cb10f5b
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54251141"
---
# <a name="paths-to-co-management"></a>Caminhos de cogestão

Existem duas formas principais para configurar cogestão. É importante compreender os pré-requisitos para cada caminho. Cada um deles requer alguma combinação dos Azure Active Directory (Azure AD), o Configuration Manager, o Microsoft Intune e o Windows 10. 

1. [Inscrição automática de dispositivos geridos pelo Configuration Manager existentes no Intune](#bkmk_path1)  
2. [Inicializar o cliente do Configuration Manager com o aprovisionamento moderna](#bkmk_path2)  

![Diagrama de caminhos de cogestão](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Caminho 1: Inscrição automática de clientes existentes

Levando esse caminho, pode obter seus dispositivos geridos pelo Configuration Manager existentes rapidamente inscritos no Intune. A gestão desses dispositivos do Configuration Manager não é diferente de antes de ativar a cogestão. Agora, obter todos os benefícios com base na cloud. Este caminho é transparente para os seus utilizadores.

Eis o que precisa de configurá-lo:
- Azure AD híbrido
    - Active Directory Federation Services (ADFS) com a autenticação pass-through (PTA)
    - Do Azure AD Connect
    - Licença do Azure AD Premium
    - Configurar híbrido do Azure AD join (escolher uma opção):
        - Para domínios geridos
        - Nos domínios federados
- Agente de cliente para híbrido do Azure AD join
- Configurar a inscrição automática de dispositivos ao Intune
- Atribuir licenças de utilizador do Intune
- Ativar a cogestão no Configuration Manager

Para um tutorial sobre esse caminho, consulte [Tutorial: Ativar a cogestão para os clientes existentes do Configuration Manager](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Caminho 2: Inicializar com aprovisionamento moderna

Eis o que precisa de configurá-lo:

1. [Configuração avançada de HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Criar os serviços cloud no Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configurar o ponto de gestão e os clientes para utilizar o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Utilizar o Intune para implementar o cliente do Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Um tutorial para este caminho estará disponível brevemente.

