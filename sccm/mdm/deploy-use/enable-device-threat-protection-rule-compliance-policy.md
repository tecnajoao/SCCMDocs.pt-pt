---
title: "Ativar regra de proteção de dispositivo numa política de conformidade"
titleSuffix: Configuration Manager
description: "Ative regra de proteção de ameaça móvel na política de conformidade de dispositivo."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
caps.latest.revision: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: d74360ce800f030e85e2b87defc1de3376c6aee5
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Ativar regra de proteção de ameaça do dispositivo na política de conformidade

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Intune com a proteção de ameaça móveis Lookout dá-lhe a capacidade para detetar ameaças móveis e efetuar uma avaliação de risco no dispositivo. Pode criar uma regra de política de conformidade no Configuration Manager para incluir a avaliação de risco para determinar se o dispositivo está em conformidade. Em seguida, pode utilizar a política de acesso condicional para permitir ou bloquear o acesso ao Exchange, SharePoint e outros serviços com base na conformidade do dispositivo.

Para que a deteção de ameaças de dispositivo Lookout influenciar a política de conformidade do dispositivo:

* O **proteção contra ameaças do dispositivo** regra tem de estar ativada na política de conformidade.

* O **Lookout estado** página no **consola de administrador do Intune** deve mostrar como **Active Directory**. Consulte o [ligação ativar o Lookout MTP no Intune](enable-lookout-connection-in-intune.md) tópico para obter mais detalhes e instruções sobre como ativar a integração de Lookout.


Antes de criar a regra de proteção de ameaça do dispositivo na política de conformidade era, recomendamos que lhe [configurar a sua subscrição com a proteção contra ameaças do Lookout dispositivo](set-up-your-subscription-with-lookout.md), [ativar a ligação de Lookout no Intune](enable-lookout-connection-in-intune.md), e [configurar o Lookout for work aplicação](configure-and-deploy-lookout-for-work-apps.md). A regra de conformidade imposta apenas depois de concluída a configuração.

Para ativar a regra de proteção de ameaça do dispositivo, pode utilizar uma política de conformidade existente ou crie um novo.

Como parte da configuração de proteção de ameaça do dispositivo de Lookout, no [consola Lookout](https://aad.lookout.com), criou uma política que classifica ameaças vários em níveis de altas, médias e baixas. A política de conformidade do Intune utilizará o nível de ameaças para definir o nível máximo ameaça permitidos.

No **regras** página do Assistente de política de conformidade, definir uma nova regra com as seguintes informações:
  * Condição: Nível de risco máxima de proteção de ameaças de dispositivo.
  * Value: O valor pode ser um dos seguintes:
    * **Nenhum (protegidos)**: Esta é a mais segura. Isto significa que o dispositivo não pode ter qualquer ameaças. Se não for encontrada qualquer nível de ameaças, o dispositivo for avaliado como não conforme.
    * **Baixa**: O dispositivo for avaliado como compatível se apenas baixas ameaças nível estão presentes. Nada superior coloca o dispositivo num Estado de não conformidade.
    * **Média**: O dispositivo for avaliado como compatível se as ameaças encontradas num dispositivo são nível médio ou baixo. Se forem detetadas ameaças de nível elevadas, o dispositivo é determinado como não conforme.
    * **Elevada**: É uma situação menos segura. Essencialmente, isto permite que todos os níveis de ameaças e talvez apenas útil se estiver a utilizar esta solução apenas para efeitos de relatórios.

Se criar políticas de acesso condicional para o Office 365 e outros serviços, a avaliação de compatibilidade acima é levada em consideração e não conformes dispositivos estão bloqueados de aceder aos recursos da empresa até a ameaça está resolvida.

O estado de proteção de ameaça do dispositivo é apresentado no **segurança** no nó de **monitorização** área de trabalho.
É apresentado um resumo do Estado com um nível de vários threads de um gráfico de visual. Pode clicar nas secções individuais do gráfico para ver mais informação, como o número de dispositivos que reportem como não conformes por plataforma e quaisquer erros que são reportados.
Também pode ver o estado do dispositivo individual no **ativos e compatibilidade** área de trabalho, em **dispositivos**.  Pode adicionar o **conformidade do dispositivo ameaça** e **nível de ameaças de dispositivo** colunas para ver o estado.  Estas colunas não são apresentadas por predefinição.
