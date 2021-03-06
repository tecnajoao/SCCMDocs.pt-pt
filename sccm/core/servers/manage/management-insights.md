---
title: Informações de gestão
titleSuffix: Configuration Manager
description: Saiba mais sobre a funcionalidade de informações de gestão disponível na consola do Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8621f759a2e79090c6cd6dac5f2f3749147cabed
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133355"
---
# <a name="management-insights-in-configuration-manager"></a>Informações de gestão no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Informações de gestão no Configuration Manager fornecem informações sobre o estado atual do seu ambiente. As informações baseia-se na análise de dados da base de dados do site. Insights ajudá-lo para melhor compreender o seu ambiente e tome medidas com base nas informações. Esta funcionalidade foi lançada na versão 1802 de versão do Configuration Manager. <!--1353967-->



## <a name="review-management-insights"></a>Reveja as informações de gestão 

Para ver as regras, a conta tem do **ler** permissão sobre a **site** objeto.

1. Abra a consola do Configuration Manager.  

2. Vá para o **Administration** área de trabalho, expanda **informações de gestão**e selecione **todas as informações**.  

    > [!Note]  
    > A partir da versão 1810, quando seleciona a **informações de gestão** nó, mostra o [dashboard de conhecimentos de gestão](#bkmk_insights).  

3. Abra as informações de gestão que pretende rever de nome do grupo. Selecione **Mostrar Insights** na faixa de opções.  

Os seguintes quatro separadores estão disponíveis para revisão: 

- **Todas as regras**: Fornece uma lista completa das regras para o grupo de informações de gerenciamento escolhido.  

- **Completa**:  Apresenta uma lista de regras em que é necessária nenhuma ação.  

- **Em curso**: Mostra regras em que alguns, mas nem todos os pré-requisitos estiverem concluídos.  

- **Ação necessária**: As regras que precisam de ações executadas são listadas. Selecione **mais detalhes** para recuperar itens específicos em que é necessária qualquer ação.  

O **pré-requisitos** painel lista os itens necessários necessários para executar a regra.

#### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Todas as regras e pré-requisitos para o grupo de serviços cloud
![Regras de insights-All de gestão e pré-requisitos para o grupo de serviços cloud](./media/Management-insights-all-cloud-rules.png)


Selecione uma regra e, em seguida, selecione **mais detalhes** para ver os detalhes da regra.



## <a name="operations"></a>Operações

As regras de informações de gestão reavaliar a sua aplicabilidade com base numa agenda semanal. Para reavaliar uma regra a pedido, a regra com o botão direito e selecione **reavaliar**.

O ficheiro de registo para as regras de informações de gestão está **SMS_DataEngine.log** no servidor do site.

<!--1357930--> A partir da versão 1806, algumas regras permitem-lhe tomar medidas. Selecione uma regra, selecione **mais detalhes**e, se selecionar disponíveis **agir**. 

Consoante a regra, esta ação tem um dos seguintes comportamentos:  

- Navegar automaticamente na consola para o nó em que pode qualquer ação adicional. Por exemplo, se as informações de gestão recomenda alterar uma definição de cliente, tomar navega para o nó de definições de cliente. Em seguida, qualquer ação adicional ao modificar o padrão ou um objeto de definições de cliente personalizadas.  

- Navegue para uma exibição filtrada com base numa consulta. Por exemplo, realizar a ação na regra de coleções vazias mostra apenas essas coleções na lista de coleções. Em seguida, qualquer ação adicional, como a eliminação de uma coleção ou modificar as suas regras de associação.  



## <a name="bkmk_insights"></a> Dashboard de conhecimentos de gestão
<!--1357979-->

A partir da versão 1810, o **informações de gestão** nó inclui um dashboard gráfico. Este dashboard mostra uma descrição geral dos Estados de regra, que torna mais fácil para que possa mostrar o progresso. 

Utilize os seguintes filtros na parte superior do dashboard para refinar a vista:
- Mostrar concluídas
- Opcional
- Recomendado
- Crítico

O dashboard inclui os seguintes mosaicos:  

- **Índice de informações de gestão**: Controla o progresso global em regras de informações de gestão. O índice é uma média ponderada. Regras críticas valem o máximo. Esse índice oferece o peso, pelo menos, a regras opcionais.  

- **Grupos de informações de gestão**: Mostra a percentagem de regras em cada grupo, honrar os filtros. Selecione um grupo para desagregar até as regras específicas neste grupo.  

- **Prioridade de informações de gestão**: Mostra a percentagem de regras por prioridade, honrar os filtros.   

- **Todas as informações**: Uma tabela de informações, incluindo a prioridade e estado. Utilize o **filtro** campo na parte superior da tabela de acordo com cadeias de caracteres em qualquer uma das colunas disponíveis. O dashboard ordena a tabela pela seguinte ordem:
    - Status: Ação necessária, concluído, desconhecido  
    - Prioridade: Crítico, recomendado, opcional  
    - Última Changed: datas mais antigas na parte superior   

![Captura de ecrã do dashboard de conhecimentos de gestão](media/1357979-management-insights-dashboard.png)



## <a name="groups-and-rules"></a>Grupos e regras

As regras estão organizadas nas seguintes grupos de informações de gestão:
- [Aplicações](#applications)  
- [Serviços cloud](#cloud-services)  
- [Coleções](#collections)  
- [Manutenção pró-ativa](#proactive-maintenance)  
- [Segurança](#security)  
- [Gestão simplificada](#simplified-management)  
- [Software Center](#software-center)  
- [Windows 10](#windows-10)  


### <a name="applications"></a>Aplicações

Informações para a gestão de aplicações.

- **Aplicações sem implementações**: Lista as aplicações no seu ambiente que não têm implementações ativas. Esta regra ajuda-o a localizar e eliminar aplicações não utilizadas para simplificar a lista de aplicações apresentadas na consola do. Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).  


### <a name="cloud-services"></a>Serviços em nuvem

Ajuda-o a integrar com vários serviços cloud, que permitem a gestão moderna dos seus dispositivos. 

- **Avaliar a prontidão de co-gestão**: Ajuda-o a compreender quais os passos são necessárias para ativar a cogestão. Esta regra tem pré-requisitos. Para obter mais informações, consulte [descrição geral de cogestão](/sccm/comanage/overview).  

- **Configurar os serviços do Azure para utilização com o Configuration Manager**: Esta regra ajuda a integrar o Configuration Manager para o Azure AD, que permite aos clientes autenticar com o site com o Azure AD. Para obter mais informações, consulte [dos serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- **Permitir que os dispositivos para serem híbridos associados ao Azure Active Directory**: Dispositivos associados ao AD Azure permitem aos utilizadores iniciar sessão com as respetivas credenciais de domínio ao garantir que os dispositivos cumprem os padrões de segurança e conformidade da organização. Para obter mais informações, consulte [considerações de design de identidade do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Atualizar clientes para a versão mais recente do Windows 10**: Windows 10, versão 1709 ou superior melhora e moderniza a experiência de computação dos seus utilizadores. Para obter mais informações, consulte [artigos sobre como adotar o Windows como um serviço de chave](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).  


### <a name="collections"></a>Coleções

Informações que o ajudam a simplificam a gestão ao limpar e reconfigurar as coleções.

- **Esvaziar coleções**: Apresenta uma lista de coleções no seu ambiente que não têm membros. Para obter mais informações, consulte [como gerir coleções](/sccm/core/clients/manage/collections/manage-collections).  


### <a name="proactive-maintenance"></a>Manutenção pró-ativa
<!--1352184--> A partir da versão 1806, as regras neste grupo de realçam potenciais problemas de configuração para evitar por meio de conservação de objetos do Configuration Manager.    

- **Grupos de limites com nenhuma sistemas de site atribuído**: Sem sistemas de site atribuído, só podem ser utilizados grupos de limites para atribuição de sites. Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Grupos de limites com nenhum membro**: Grupos de limites não são aplicáveis para a atribuição de site ou pesquisa de conteúdo se eles não têm nenhum membro. Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Pontos de distribuição não servir conteúdo aos clientes**: Pontos de distribuição que ainda não o conteúdo servido para clientes nos últimos 30 dias. Estes dados baseia-se em relatórios de clientes do respetivo histórico de transferências. Para obter mais informações, consulte [instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

- **Ativar a limpeza WSUS**: Verifica-se de que ativou a opção executar a limpeza WSUS nas propriedades do componente de ponto de atualização de software. Esta opção ajuda a melhorar o desempenho do WSUS. Para obter mais informações, consulte [manutenção de atualização de Software](/sccm/sum/deploy-use/software-updates-maintenance).  

- **Imagens de arranque não utilizados**: Imagens de arranque não referenciadas para utilização de sequência de arranque ou a tarefa PXE. Para obter mais informações, consulte [gerir imagens de arranque](/sccm/osd/get-started/manage-boot-images).  

- **Itens de configuração não utilizados**: Itens de configuração que não fazem parte de uma linha de base de configuração e têm mais de 30 dias. Para obter mais informações, consulte [criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines).  

- **Atualizar origens de cache ponto a ponto para a versão mais recente do cliente do Configuration Manager**: Identificar os clientes que servem como uma origem de cache ponto a ponto, mas ainda não tiver atualizado a partir de uma versão de cliente de pré-1806. Pré-1806 clientes não podem servir como uma origem de cache ponto a ponto para clientes que executam a versão 1806 ou posterior. Selecione **agir** para abrir uma vista de dispositivo que apresenta a lista de clientes.<!--1358008-->  


### <a name="security"></a>Segurança
Informações para melhorar a segurança dos seus dispositivos e infraestrutura. 

- **Versões de cliente de antimalware não suportadas**: Mais de 10% dos clientes está a executar versões do System Center Endpoint Protection que não são suportadas. Para obter mais informações, consulte [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  


### <a name="simplified-management"></a>Gestão simplificada

Informações que o ajudam a simplificam o gerenciamento diário do seu ambiente. 

- **Versões de cliente não CB**: Apresenta uma lista de todos os clientes cujas versões não são uma compilação atual do branch (CB). Para obter mais informações, consulte [atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients).  


### <a name="software-center"></a>Software Center

Informações para gerir o Centro de Software. 

- **Direcionar os utilizadores ao centro de Software em vez do catálogo de aplicações**: Verifique se os utilizadores têm instalado ou pediu aplicações a partir do catálogo de aplicações nos últimos 14 dias. A funcionalidade principal do catálogo de aplicações agora está incluída no Centro de Software. Suporte para o site do catálogo de aplicações terminado na versão 1806. Para obter mais informações, consulte [funcionalidades preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features).  

- **Utilizar a nova versão do Centro de Software**: A versão anterior do Centro de Software já não é suportada. Configure os clientes para utilizar o novo Centro de Software ao ativar a definição de cliente **utilizar o novo Centro de Software** no **agente do computador** grupo. Para obter mais informações, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#use-new-software-center).  


### <a name="windows-10"></a>Windows 10

Informações relacionadas à implantação e manutenção do Windows 10. O grupo de informações de gestão do Windows 10 só está disponível quando mais da metade dos clientes estão a executar o Windows 7, Windows 8 ou Windows 8.1.

- **Configurar telemetria do Windows e a chave do ID comercial**: Para utilizar dados de preparação de atualizações, configurar dispositivos com uma chave de ID comercial e ativar a telemetria. Definir os dispositivos Windows 10 para o nível de telemetria avançado (limitado) ou superior. Para obter mais informações, consulte [configurar clientes para dados de relatório para o Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).  

- **Ligar o Configuration Manager para o Upgrade Readiness**: Tire partido da preparação para acelerar as implantações do Windows 10 antes de fim do suporte do Windows 7. Para obter mais informações, consulte [integrar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics).   

#### <a name="windows-10-management-insights-rules"></a>Regras de informações de gestão do Windows 10
![Insights-regras de gestão para o Windows 10](./media/Windows-10-insights-group.png)
