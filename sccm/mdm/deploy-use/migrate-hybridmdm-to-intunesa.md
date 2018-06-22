---
title: Migrar os utilizadores MDM híbrida e de dispositivos para o Intune autónomo
titleSuffix: Configuration Manager
description: Saiba como migrar os utilizadores MDM híbrida e de dispositivos para o Intune no Azure.
author: aczechowski
manager: dougeby
ms.date: 09/12/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 4e2471b06c1767bcf914000d626bb22b6ee2bd6b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346326"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Migrar os utilizadores MDM híbrida e de dispositivos para o Intune autónomo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Quando decidir que estiver pronto para começar a migrar do híbrida MDM (Intune integrado com o Configuration Manager) para uma experiência de apenas na nuvem através do Intune no Azure, este é o artigo é para si. Se ainda não souber, consulte [escolha entre o Microsoft Intune de autónomo e híbrida de gestão de dispositivos móveis com o System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management). 

Pode começar a migrar para o Intune autónomo, utilizando uma abordagem faseada que permite-lhe testar um pequeno subconjunto de utilizadores e dispositivos, enquanto a maioria dos seus utilizadores e dispositivos ainda é gerida com híbrida MDM. Em seguida, depois de verificar a funcionalidade do Intune, pode começar a migrar mais utilizadores ao Intune.    

Os tópicos seguintes fornecem os passos para migrar os seus utilizadores ao Intune autónomo, utilizando uma abordagem faseada.    
  
1.  [Importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md)   
    A ferramenta do importador de dados do Intune recolhe dados sobre os objetos que selecionar na hierarquia do Configuration Manager, que fornece detalhes sobre os objetos que pode selecionar para importação e informações sobre o motivo pelo qual não não possível importar alguns objetos e permite-lhe que importar selecionado objetos no seu inquilino do Microsoft Intune. Enquanto este passo é opcional, este pode poupar muito tempo ao automatizar o processo de recriar objetos do Configuration Manager para o Intune. 
2.  [Preparar o Intune para a migração de utilizador](migrate-prepare-intune.md)    
    Validar objetos importados do Configuration Manager, criar novos objetos, criar grupos do AAD e tornar as atribuições de objeto a estes grupos, instalar os conectores do NDES e o Exchange, etc. Quando concluir os passos e iniciar a migração para o Intune autónomo, deve ser transparente para os seus utilizadores.  
3.  [Alterar a autoridade de MDM para utilizadores específicos (misturadas autoridade de MDM)](migrate-mixed-authority.md)    
    Configure uma autoridade MDM mista no mesmo inquilino ao selecionar a alguns utilizadores para serem geridos no Intune e todos os outros dispositivos continuam a ser geridos com híbrida MDM (Intune integrado com o Configuration Manager). Pode testar a funcionalidade do Intune está a funcionar conforme esperado nos dispositivos para que um pequeno subconjunto de utilizadores antes de começar a migrar utilizadores adicionais. 
4.  [Alterar a autoridade de MDM ao Intune autónomo](change-mdm-authority.md)     
    Altere a autoridade de MDM de inquilinos do Configuration Manager para o Intune. Todos os restantes utilizadores e dispositivos são migrados para o Intune autónomo. Irá alterar a autoridade de MDM de inquilinos depois de ter testado exaustivamente funcionalidade do Intune no passo anterior e provavelmente migraram a maioria ou todos os utilizadores já.