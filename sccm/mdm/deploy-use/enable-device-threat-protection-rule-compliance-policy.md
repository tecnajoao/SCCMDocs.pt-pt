---
title: "Ativar regra de proteção de dispositivo na política de conformidade | Documentos do Microsoft"
description: "Ative regra de proteção de ameaça móvel a política de conformidade do dispositivo."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: faa92e150686e615164ce3f5435b77a65305aab3
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Ativar regra de proteção de ameaça de dispositivo a política de conformidade

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Intune com a proteção de ameaça móveis atento dá-lhe a capacidade de detetar ameaças móveis e efetuar uma avaliação de riscos no dispositivo. Pode criar uma regra de política de conformidade no Configuration Manager para incluir a avaliação de riscos para determinar se o dispositivo é compatível. Em seguida, pode utilizar a política de acesso condicional para permitir ou bloquear o acesso ao Exchange, SharePoint e outros serviços com base em conformidade do dispositivo.

Para que a deteção de ameaça atento dispositivo influenciar a política de conformidade para o dispositivo:

* O **dispositivo ameaça proteção** regra tem de estar ativada na política de conformidade.

* O **atento estado** página no **consola do administrador do Intune** tem Mostrar como **Active Directory**. Consulte o [ligação ativar MTP atento no Intune](enable-lookout-connection-in-intune.md) tópico para obter mais detalhes e instruções sobre como ativar a integração da atento.


Antes de criar a regra de proteção do dispositivo ameaça na política de compliancy, recomendamos que lhe [configurar a sua subscrição com a proteção de ameaça de dispositivo atento](set-up-your-subscription-with-lookout.md), [ativar a ligação de atento no Intune](enable-lookout-connection-in-intune.md), e [configurar atento para a aplicação de trabalho](configure-and-deploy-lookout-for-work-apps.md). A regra de conformidade imposta apenas depois de concluída a configuração.

Para ativar a regra de proteção de ameaça de dispositivo, pode utilizar uma política de conformidade existente ou crie um novo.

Como parte da configuração de proteção de ameaça do dispositivo de atento, no [consola atento](https://aad.lookout.com), é criada uma política que classifica ameaças vários em níveis de alto, médias e baixos. A política de conformidade do Intune utilizará o nível de ameaça para definir o nível de ameaça permitidos máximo.

No **regras** página do Assistente de política de conformidade, definir uma nova regra com as seguintes informações:
  * Condição: Nível de risco máximo de proteção de ameaça de dispositivo.
  * Value: O valor pode ser um dos seguintes procedimentos:
    * **Nenhum (protegidos)**: Esta é a mais segura. Isto significa que o dispositivo não pode ter qualquer ameaças. Se não for encontrada qualquer nível de ameaças, o dispositivo é avaliado como não conformidade.
    * **Low**: O dispositivo é avaliado como compatível se apenas ameaças de nível baixas estão presentes. Nada superior coloca o dispositivo num Estado de conformidade.
    * **Média**: O dispositivo é avaliado como compatível se as ameaças encontradas no dispositivo são nível médio ou baixo. Se forem detetadas ameaças de nível elevadas, o dispositivo é determinado como não conformidade.
    * **Elevada**: Esta é a menos segura. Resumindo, isto permite que todos os níveis de ameaça e talvez apenas úteis se estiver a utilizar esta solução apenas para efeitos de relatórios.

Se criar políticas de acesso condicional para o Office 365 e outros serviços, a avaliação da conformidade acima é levada em consideração e dispositivos não conformes são impedidos de aceder aos recursos da empresa enquanto a ameaça não for resolvida.

O estado de proteção de ameaça de dispositivo é apresentado no **segurança** nó o **monitorização** área de trabalho.
É apresentado um resumo do Estado com um nível de vários threads num gráfico visual. Pode clicar nas secções individuais do gráfico para obter mais informações, como, o número de dispositivos que reportem como não conformidade, por plataforma e quaisquer erros que são enviados.
Também pode ver o estado de dispositivo individuais no **ativos e compatibilidade** área de trabalho, em **dispositivos**.  Pode adicionar o **conformidade do dispositivo ameaça** e **nível de ameaças de dispositivo** colunas para ver o estado.  Estas colunas não são apresentadas por predefinição.

