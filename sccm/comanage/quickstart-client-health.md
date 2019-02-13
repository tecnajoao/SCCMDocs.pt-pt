---
title: Estado de funcionamento do cliente com cogestão
titleSuffix: Configuration Manager
description: Manter a visibilidade do Estado de funcionamento de cliente do Configuration Manager do Intune no portal do Azure
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6838371a80530d5ab66abd9d8a976af41513e15
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126182"
---
# <a name="client-health-with-co-management"></a>Estado de funcionamento do cliente com cogestão

O estado de funcionamento da sua rede está ligado diretamente para o estado de funcionamento dos dispositivos saem-lo. Intune possa comunicar com um cliente de mau estado de funcionamento, mesmo quando não estiver em sua rede. Utilize a cogestão para combinar esta funcionalidade com capacidade do Configuration Manager para relatar 98% em bom estado de clientes conhecido. Em seguida, pode detetar, avaliar e fornecer visibilidade em todos os clientes em tempo real. O Intune também adiciona o suporte necessário para atualizações de conformidade em todos os clientes ligados.

No vídeo seguinte, gerente de programas sênior Rob Iorque e marketing Ainley Locky do Gestor de produtos discutem e demonstrar o estado de funcionamento do cliente com cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Benefícios

Avaliar o estado de funcionamento do cliente é uma prioridade. System Center 2012 Configuration Manager adicionou **CCMeval**. Esse utilitário é externo para o cliente do Configuration Manager. Ele fornece cliente remediação automática e monitorização de estado de funcionamento. No entanto, este relatório baseia-se num dispositivo que está a ser fisicamente ou virtualmente em sua rede interna. Cogestão ajuda a resolver este problema.

Com a cogestão, pode reportar o estado de funcionamento do cliente Intune. Fornece informações de timestamp a validade dos dados. Estas informações informa se os seus dispositivos estão em bom estado, pode estabelecer uma ligação, pode instalar aplicações, ou podem atualizar para o sistema operacional obrigatório baseia-se. 

Para obter uma descrição detalhada desta funcionalidade, veja este vídeo do [o que há de novo no Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) sessão na Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Quando o Configuration Manager fornece o estado do dispositivo que o cliente é instalado, mas não é, o Intune pode fornecer mais informações sem terem de se ligar ao cliente. As informações de estado de funcionamento do dispositivo no Intune são fácil de entender. Se o estado for algo diferente de **bom estado de funcionamento**, ele fornece recomendações e os passos seguintes para resolver problemas e corrigi-lo.

> [!Note]  
> Os seguintes benefícios estão planeados para uma versão futura:
> - O Configuration Manager irá incluir funcionalidades adicionais em CCMeval  
> - É mais fácil identificar computadores potencialmente problemáticos no Configuration Manager e o Intune  
> - Pode agrupar os dados de estado de funcionamento do cliente no Intune  



## <a name="value-proposition"></a>Proposta de valor

Com esta funcionalidade, tem agora uma origem de dados externos com o Intune. Permite-lhe determinar as próximas etapas quando uma grande diversidade de problemas do cliente de resolução de problemas. Agora que não precisa de criar relatórios adicionais ou utilizar outras ferramentas para extrair dados de cliente.

Quando tiver clientes íntegros, prontamente atualizou a conformidade de patch. Melhor conformidade de patch significa uma maior segurança.



## <a name="configure"></a>Configurar

Para começar a utilizar com esta funcionalidade, utilize os seguintes passos:

- Atualizar os dispositivos para Windows 10, versão 1709 ou posterior  

- [Ativar a cogestão](/sccm/comanage/how-to-enable)  
    - Não precisa de alternar qualquer carga de trabalho para o Intune  

- Atualizar o site do Configuration Manager e os clientes *versão 1806* ou posterior  


### <a name="review-configuration-manager-client-health-in-intune"></a>Reveja o estado de funcionamento de cliente de Configuration Manager no Intune

1. Inicie sessão no [Portal do Azure](https://portal.azure.com/).  

2. Selecione **Todos os serviços** > **Intune**. O Intune encontra-se na secção **Monitorização + Gestão**.  

3. Assim que tiver aberto o **Microsoft Intune** painel, no menu sob **ajuda e suporte**, aceda ao **resolução de problemas** página.  

4. Utilize o **selecionar utilizador** opção, encontrar o dispositivo específico na **dispositivos** lista e selecione-o para abrir a página do dispositivo.  

5. Informações de cogestão são mostradas na parte inferior da página do dispositivo. Estas informações incluem os seguintes campos para o estado de funcionamento do cliente:  
    - **Estado do agente do Configuration Manager**  
    - **Última verificação de agente do Configuration Manager no tempo**  

> [!Tip]  
> Ligarem dispositivos inscritos no Intune para o serviço em nuvem três vezes por dia, aproximadamente a cada oito horas. 
