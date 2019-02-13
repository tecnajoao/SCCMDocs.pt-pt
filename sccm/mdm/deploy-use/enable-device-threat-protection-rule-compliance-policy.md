---
title: Ativar a regra de proteção do dispositivo na política de conformidade
titleSuffix: Configuration Manager
description: Ative a regra de proteção contra ameaças móveis na política de conformidade do dispositivo.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0bae054d3daa5aea8e343fef05aa4578221f17b6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133991"
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Ativar a regra de proteção contra ameaças de dispositivo na política de conformidade

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Intune com proteção contra ameaças móveis do Lookout dá-lhe a capacidade de detetar ameaças e avaliar os riscos no dispositivo. Pode criar uma regra de política de conformidade no Configuration Manager para incluir a avaliação de riscos para determinar se o dispositivo está em conformidade. Em seguida, pode utilizar a política de acesso condicional para permitir ou bloquear o acesso ao Exchange, SharePoint e outros serviços com base na conformidade do dispositivo.

Para ter a deteção de ameaças de dispositivos do Lookout influencie a política de conformidade do dispositivo:

* O **Device Threat Protection** regra tem de estar ativada na política de conformidade.

* O **estado do Lookout** página no **consola do administrador do Intune** tem de apresentar **Active**. Consulte a [ligação de ativar o Lookout MTP no Intune](enable-lookout-connection-in-intune.md) tópico para obter mais detalhes e instruções sobre como ativar a integração do Lookout.


Antes de criar a regra de proteção de ameaças de dispositivos na política de conformidade, recomendamos que [configurar a sua subscrição com a proteção de ameaças de dispositivos do Lookout](set-up-your-subscription-with-lookout.md), [ativar a ligação do Lookout no Intune](enable-lookout-connection-in-intune.md), e [configurar a aplicação Lookout for work](configure-and-deploy-lookout-for-work-apps.md). A regra de conformidade aplicada apenas quando a configuração estiver concluída.

Para ativar a regra de proteção de ameaças de dispositivos, pode utilizar uma política de conformidade existente ou crie um novo.

Como parte da configuração proteção de ameaças de dispositivos do Lookout, na [consola do Lookout](https://aad.lookout.com), criou uma política que classifica as várias ameaças nos níveis alto, médios e baixos. Na política de conformidade do Intune irá utilizar o nível de ameaça para definir o nível de ameaça máximo permitido.

Sobre o **regras** página do Assistente de política de conformidade, definir uma nova regra com as seguintes informações:
  * Condição: Nível de risco máximo de proteção de ameaças de dispositivos.
  * Value: O valor pode ser um dos seguintes:
    * **Nenhum (seguro)**: Esta é a mais segura. Isso significa que o dispositivo não pode ter qualquer ameaça. Se for encontrado qualquer nível de ameaças, o dispositivo é avaliado como não conforme.
    * **Baixa**: O dispositivo é avaliado como conforme se só estiverem presentes ameaças de nível baixo. Qualquer nível mais alto coloca o dispositivo num Estado de conformidade.
    * **Médio**: O dispositivo é avaliado como conforme se as ameaças encontradas no dispositivo forem de nível baixo ou médio. Se forem detetadas ameaças de nível alto, o dispositivo é identificado como não conforme.
    * **Alta**: Este é o nível menos seguro. Essencialmente, isso permite que todos os níveis de ameaças e possivelmente só será útil se estiver a utilizar esta solução apenas para fins de relatórios.

Se criar políticas de acesso condicional para o Office 365 e outros serviços, a avaliação de conformidade é considerada e os dispositivos não compatíveis são impedidos de aceder a recursos da empresa, até que a ameaça esteja resolvida.

O estado de proteção contra ameaças do dispositivo é apresentado no **Security** nó a **monitorização** área de trabalho.
É apresentado um resumo do Estado com o nível de thread vários num gráfico visual. Pode clicar nas secções individuais do gráfico para ver mais informações, como o número de dispositivos que comunicam como não conforme pela plataforma e quaisquer erros comunicados.
Também pode ver o estado do dispositivo individuais no **ativos e compatibilidade** área de trabalho, em **dispositivos**.  Pode adicionar os **conformidade de ameaça do dispositivo** e o **nível de ameaça do dispositivo** colunas para ver o estado.  Estas colunas não são apresentadas por predefinição.
