---
titleSuffix: Configuration Manager
description: Saiba mais sobre a funcionalidade de informações de gestão disponível na consola do Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
caps.latest.revision: ''
caps.handback.revision: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2d6a58bd5aba873ea35c5bcf511a3cc22514b51
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="management-insights-in-system-center-configuration-manager"></a>Informações de gestão no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Informações de gestão no System Center Configuration Manager fornecem informações sobre o estado atual do seu ambiente. As informações é com base na análise de dados a partir da base de dados do site. Insights ajudam-para melhor compreender o seu ambiente e atue com base nas informações. Esta funcionalidade foi lançada no Configuration Manager versão 1802. <!--1353967-->

## <a name="review-management-insights-in-the-configuration-manager-console"></a>Reveja as informações de gestão na consola do Configuration Manager 
O **ler site** permissão é necessária para ver as regras.

1. Abra a consola do Configuration Manager. 
2. Vá para o **administração** nó e clique em **gestão Insights**.
3. Selecione **todas as informações**
4. Faça duplo clique no **nome do grupo de gestão conhecimentos aprofundados** pretende rever. Em alternativa, destacá-la e clique em **Mostrar Insights** no Friso. 
5. Existem quatro separadores estão disponível para revisão juntamente com os pré-requisitos necessários para executar a regra. 
    - **Todas as regras**: Fornece a lista completa das regras do grupo de gestão conhecimentos aprofundados escolhido.
    - **Completa**:  Apresenta uma lista de regras em que é necessária nenhuma ação. 
    - **Em curso**: Mostra as regras em que alguns, mas nem todos os pré-requisitos estiverem concluídos.
    - **É necessária uma ação**: Regras necessitar as ações executadas estão listadas. Clique com botão direito e selecione **mais detalhes** obter itens específicos em que é necessária uma ação. 
    - **Pré-requisitos**: Se precisar de uma regra de itens concluídas antes de estes serem executados, os itens requeridos serão listados aqui.   
    
    **Todas as regras e pré-requisitos para o grupo de serviços em nuvem** ![regras de todos os insights de gestão e de pré-requisitos para o grupo de serviços cloud](./media/Management-insights-all-cloud-rules.png)

## <a name="management-insights-reevaluation-and-logging"></a>Registo e de reavaliação de informações de gestão
As regras de informações de gestão reevaluate sua aplicabilidade com base numa agenda semanal. Novamente, pode avaliar uma regra a pedido clicar a regra e selecionando **reavaliar**.

**Ficheiro de regras de gestão de informações de registo**: SMS_DataEngine.log
## <a name="management-insights-groups-and-rules"></a>Grupos de informações de gestão e regras
As regras são organizadas em grupos de informações de gestão diferentes. Quando são adicionadas a grupos e as regras, serão adicionados à lista seguinte:

**Aplicações**: Insights para a gestão de aplicações.

- **Aplicações sem implementações** -lista as aplicações no seu ambiente que não tem implementações ativas. Esta regra ajuda a localizar e eliminar as aplicações não utilizadas para simplificar a lista de aplicações apresentada na consola do. 

**Serviços em nuvem**: Ajuda a integrar com vários serviços de cloud; Ativar a gestão moderna dos seus dispositivos. 
 - **Avaliar a preparação de gestão conjunta** -ajuda-o a compreender os passos necessários para ativar a gestão conjunta. Esta regra tem pré-requisitos. 
 - **Ativar os dispositivos para ser híbrida associados ao Azure Active Directory** -dispositivos associados a um AD do Azure permitem aos utilizadores iniciar sessão com as credenciais de domínio ao garantir que os dispositivos cumprem as normas de segurança e conformidade da organização. 
 - **Modernize a infraestrutura de identidade e acesso** -serviço de nuvem do Azure AD com a autenticação multifator integrada protege os dados confidenciais e aplicações no local e na nuvem. 
 - **Atualizar os clientes para o Windows 10, versão 1709 ou acima** -Windows 10, versão 1709 ou superior melhora e modernizes a informática experiência dos utilizadores. 


**Coleções**: Insights que ajudam a simplificam a gestão de limpeza e reconfigurar a coleções.
   - **Vazio coleções** -apresenta uma lista de coleções no seu ambiente sem membros. 

**Uma gestão simplificada**: Informações que o ajudam a simplificam a gestão diária do seu ambiente. 
   - **Versões de cliente de desatualizada** -apresenta uma lista de todos os clientes cujas versões são mais antigas do que dois anos. 

**Centro de software**: Insights para gerir o Centro de Software. 
   - **Direcionar os utilizadores ao centro de Software em vez do catálogo de aplicações** -Verifique se os utilizadores tem instalado ou pedidos aplicações a partir do catálogo de aplicações nos últimos 14 dias. A funcionalidade principal do catálogo de aplicações está agora incluída no Centro de Software. Suporte para as extremidades de Web site do catálogo de aplicações com a primeira atualização lançada após 1 de Junho de 2018
   - **Utilize a versão nova do Centro de Software** -a versão anterior do Centro de Software já não é suportada. Configurar clientes para utilizar o novo Centro de Software, Ativando a definição de cliente **agente do computador** >**utilizar o novo Centro de Software**.

**Windows 10**: Informações relacionadas com a implementação e manutenção do Windows 10. O grupo de informações de gestão do Windows 10 está disponível quando mais de metade dos clientes executam o Windows 7, Windows 8 ou Windows 8.1.
   - **Configurar a telemetria do Windows e a chave de ID comercial** -para utilizar dados de preparação de atualização, os dispositivos tem de ser configurados com uma chave de ID comerciais e tiver ativada a telemetria. Dispositivos Windows 10 tem de ser definida para o nível de telemetria de avançado (limitado) ou superior.
   - **Ligar o Configuration Manager para atualizar preparação** -tire partido preparação de atualização a fim de acelerar as implementações do Windows 10 antes do Windows 7 ficar fora de suporte. **Configurar a telemetria do Windows e a chave de ID comercial** é um pré-requisito.

     **As regras de informações de gestão do Windows 10**
    ![insights-as regras de gestão para o Windows 10](./media/Windows-10-insights-group.png)
    