---
title: "Migrar os utilizadores MDM híbrida e de dispositivos para o Intune autónomo"
titleSuffix: Configuration Manager
description: "Saiba como migrar os utilizadores MDM híbrida e de dispositivos para o Intune no Azure."
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: a6e430248fdeedd310087c9a32c6d69ca1864a09
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/17/2017
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

<!--
The following provides a typical workflow for migrating users from hybrid MDM to Intune standalone:
1.  Admin runs the Microsoft Intune Data Importer Tool, selecting which objects and assignments to import. Selected objects are imported into Intune standalone.
    1. Some objects cannot be imported because they contain settings the tool does not understand or setting that are not available in Intune standalone.
    2. Assignments are migrated. However, only if the collection an object was targeted to is based on a single Active Directory (AD) security group and the same group exists in Azure Active Directory (AAD).
    > [!Note]    
    > If you want, you can skip this step and create the objects that you want directly in Intune in the Azure portal without running the Intune Data Importer Tool. 
2.  Admin logs into the Intune on Azure portal
    1. Creates any additional objects required for their organization that were not imported by the Microsoft Intune Data Importer tool.
    2. Creates any required AAD groups and makes any additional assignments for each object to AAD groups.
    3. Installs the NDES connector on an on-premises server if using SCEP or PFX certificate deployment.
    4. Installs the Exchange connector on an on-premises server if using conditional access. 
3.  Admin ensures that all existing Intune users in their organization have an Intune license assigned to them using AAD or the Office administrator portal.
4.  Admin selects some test users to migrate to Intune standalone and removes them from the collection associated with the Intune subscription in Configuration Manager.
5.  Once removed from the collection, the user and all devices are managed by Intune in the Azure portal. Remaining users and devices continue to be managed by hybrid mobile device management in Configuration Manager. 
6.  Admin validates that things are working as expected on the device and moves more users to Intune standalone by removing them from the collection associated with the Intune subscription in Configuration Manager.
7.  Once the admin is comfortable with the functionality in Intune standalone, they can move the rest of their users and devices by switching their MDM authority to Intune standalone. This can be done by removing the Intune subscription from SCCM and choosing to change the MDM authority. Tenant level policies will be automatically migrated to Intune standalone, all objects and assignments in Intune standalone will remain, and devices will not be required to re-enroll.
-->