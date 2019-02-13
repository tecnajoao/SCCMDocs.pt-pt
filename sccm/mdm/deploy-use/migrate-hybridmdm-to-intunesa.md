---
title: Migrar recursos MDM híbrida para o Intune autónomo
titleSuffix: Configuration Manager
description: Saiba como migrar dispositivos e utilizadores MDM híbrida para o Intune no Azure.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.collection: M365-identity-device-management
ms.openlocfilehash: e2b62362bfcc9a76e407e9c0124306f83ac4a782
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134474"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Migrar os utilizadores e dispositivos da MDM híbrida para o Intune autónomo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Este artigo é a migração da MDM híbrida para uma experiência de apenas na cloud com o Intune no Azure. 

> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


Começar a migrar para o Intune autónomo, de forma faseada. Com esta abordagem, testar um pequeno subconjunto de utilizadores e dispositivos enquanto a maioria dos seus utilizadores e dispositivos continuam a ser gerida com hybrid MDM. Depois de verificar a funcionalidade do Intune, comece a migrar mais recursos para o Intune.    

Para obter mais informações, veja os artigos seguintes:    
  
1.  [Importar os dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md)   

    A ferramenta importador de dados do Intune:  

    - Recolhe dados sobre os objetos que selecionar na hierarquia do Configuration Manager  

    - Fornece detalhes sobre os objetos que pode selecionar para importação   

    - Fornece informações sobre por que alguns objetos não podem ser importados  

    - Permite-lhe importar objetos selecionados para o seu inquilino do Microsoft Intune  

    Este passo é opcional. Pode economizar seu tempo ao automatizar o processo para recriar objetos do Configuration Manager para o Intune.  

2.  [Preparar o Intune para a migração de utilizadores](migrate-prepare-intune.md)    

    - Validar objetos importados do Configuration Manager  

    - Criar novos objetos  

    - Criar grupos do Azure AD e faz as atribuições de objeto a estes grupos  

    - Instalar o NDES e conectores do Exchange  

    Quando concluir os passos e iniciar a migração para o Intune autónomo, não há nenhum impacto significativo aos seus utilizadores.   

3.  [Alterar a autoridade MDM para utilizadores específicos (autoridade MDM mista)](migrate-mixed-authority.md)    

    Configure uma autoridade MDM mista no mesmo inquilino. Selecione alguns utilizadores para serem geridos no Intune, enquanto continua a gerir todos os outros dispositivos com a MDM híbrida Teste de funcionalidade do Intune está a funcionar nos dispositivos para que um pequeno subconjunto de utilizadores antes de começar a migrar os utilizadores adicionais.   

4.  [Alterar a sua autoridade MDM para o Intune autónomo](change-mdm-authority.md)     

    Altere a autoridade MDM de nível de inquilino no Configuration Manager para o Intune. Todos os utilizadores e dispositivos restantes são migrados para o Intune autónomo. Depois de ter testado exaustivamente funcionalidades do Intune no passo anterior e migrou a maioria ou todos os seus utilizadores, em seguida, altere a autoridade MDM de inquilinos.



## <a name="request-assistance"></a>Pedido de assistência
<!--Intune bug 2339232--> Para pedir assistência do programa Microsoft FastTrack, começar a utilizar ao aceder [FastTrack para Microsoft 365](https://fasttrack.microsoft.com/microsoft365/capabilities?view=security).

1. Clique em "Iniciar sessão" e introduza o seu ID da organização.  

2. Aceda ao Dashboard e siga as instruções para aceder a **pedido para obter assistência** formulário.    

3. A Microsoft analisa o seu pedido e encaminha o mesmo para a equipa adequada para atender suas necessidades específicas e elegibilidade.  

Neste dashboard, também encontre melhores práticas, ferramentas e recursos de especialistas FastTrack para o ajudar a tornar a sua experiência com o Microsoft Cloud um excelente.

