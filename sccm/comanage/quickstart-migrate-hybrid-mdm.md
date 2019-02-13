---
title: Migrar do MDM híbrido
titleSuffix: Configuration Manager
description: Foi preterida a MDM híbrida, o Intune autónomo é necessário para a cogestão.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 456f32d5-8590-499f-a54d-d00618bc61f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84625c12c9cac643fe5a895c066632f44ffeacdc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156845"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Migrar da MDM híbrida para a cogestão

Gestão de dispositivos móveis híbridos (MDM) é uma funcionalidade despromovida. Suporte para MDM híbrida termina 1 de Setembro de 2019. Para obter mais informações, consulte [MDM híbrida com o Configuration Manager e o Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

Intune autónomo é a topologia de implementação recomendada e é necessário para a cogestão. Se pretender ativar a cogestão, migre de uma configuração híbrida do Intune para o Intune autónomo. 

No vídeo seguinte, gerente de programa principal Andrew McMurray e gerente de marketing de produtos sênior Mayunk Jain discutam e demonstrar a migração do MDM híbrido:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Como fazê-lo

A migração para o Intune autónomo será mais bem-sucedidos quando utilizar uma abordagem faseada. Com uma migração faseada, mover um pequeno subconjunto de utilizadores e dispositivos enquanto a maioria dos seus utilizadores e dispositivos continuam a ser gerida com hybrid MDM. Depois de verificar que a migração é efetuada com êxito, pode começar a migração de mais recursos para o Intune.

Para iniciar a migração, utilize o [ferramenta importador de dados do Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data) para recolher e automatizar o processo de recriar os objetos do Configuration Manager no seu inquilino do Intune autónomo. Em seguida, alterar a autoridade MDM de um conjunto específico de utilizadores e testar a funcionalidade no Intune autónomo. Quando esta verificação é realizada, altere a sua autoridade MDM para o Intune autónomo para todos os utilizadores.

> [!Important]  
> Se estiver a utilizar acesso condicional no local no Configuration Manager, esta funcionalidade requer atualmente híbrida do Intune.  

Para obter mais informações sobre este processo de migração, consulte [migrar dispositivos e utilizadores MDM híbrida para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Estudos de caso

Microsoft IT recentemente movido ciência tem 130.000 utilizadores do Intune híbrido para o Intune autónomo em três meses. Para obter mais informações, consulte [como a Microsoft utiliza o acesso condicional - 1812 de zona do ponto de extremidade](https://youtu.be/offk-KH7eIA?t=651). Este vídeo é uma conversa entre Microsoft vice-presidente Brad Anderson e diretor de informações de segurança da Microsoft Bret Arsenault, quem oversaw pessoalmente a migração. 

Uma grande empresa farmacêutica movido 10.000 usuários da híbrida do Intune para o Intune autónomo dentro de algumas semanas.

Uma grande empresa de consultoria TI na Índia migradas 40.000 utilizadores do Intune híbrido, para o Intune autónomo em menos de um mês.



## <a name="contact-fasttrack"></a>Entre em contato com FastTrack

Se precisar de assistência de migração do MDM híbrido a qualquer momento no processo, aceda a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sessão e pedir assistência. 

Para obter mais informações, consulte [Obtenha ajuda de FastTrack](/sccm/comanage/quickstart-fasttrack). 

