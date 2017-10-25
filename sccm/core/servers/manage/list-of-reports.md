---
title: "Lista de relatórios | Microsoft Docs"
description: "Reveja uma lista de relatórios que são fornecidos com o Configuration Manager. Os relatórios são apresentados em várias categorias."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 1480c38a6a3afef76b2e8759eaafd47d28f978f4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="list-of-reports-in-system-center-configuration-manager"></a>Lista de relatórios no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Vários relatórios incorporados são fornecidos com o System Center Configuration Manager, que abrangem muitas das tarefas de criação de relatórios que poderá querer efetuar. Também pode utilizar as instruções SQL nestes relatórios para ajudá-lo a escrever os seus próprios relatórios. Utilize as informações neste tópico para saber mais sobre os relatórios que são fornecidos com o Configuration Manager.  

## <a name="list-of-built-in-configuration-manager-reports"></a>Lista de relatórios do Configuration Manager incorporados  
 Os seguintes relatórios estão incluídos com o Configuration Manager. Os relatórios são apresentados em várias categorias.  

### <a name="administrative-security"></a>Segurança administrativa  
 Os seguintes relatórios estão listados no **segurança administrativa** categoria.  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Registo de atividade de administração**|Mostra um registo das alterações administrativas realizadas para utilizadores administrativos, direitos de acesso, âmbitos de segurança e coleções.|  
|**Atribuições de segurança dos utilizadores administrativos**|Mostra utilizadores administrativos, os respetivos direitos de acesso associados e os âmbitos de segurança associados a cada direito de acesso de cada utilizador.|  
|**Objetos protegidos por um único âmbito de segurança**|Mostra objetos que estão protegidos por um âmbito de segurança especificado e que estão atribuídos apenas a esse âmbito de segurança. Este relatório não mostra objetos associados a mais do que um âmbito de segurança.|  
|**Segurança para um ou vários objetos do Configuration Manager**|Mostra objetos com capacidade de segurança, os âmbitos de segurança associados aos objetos e os utilizadores administrativos com acesso aos objetos.|  
|**Resumidas de funções de segurança**|Apresenta as funções de segurança e administradores do Configuration Manager associados a cada função.|  
|**Resumo dos âmbitos de segurança**|Mostra os âmbitos de segurança e os utilizadores administrativos do Configuration Manager e os grupos de segurança associados a cada âmbito.|  

### <a name="alerts"></a>Alertas  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Tabela de indicadores de alerta**|Mostra um resumo de todos os alertas adiados que foram gerados entre o início especificado e a data de conclusão.|  
|**Alertas gerados mais frequentemente**|Mostra um resumo dos alertas gerados mais frequentemente entre o dia de hoje e a data anterior especificada na área de função especificada.|  

### <a name="asset-intelligence"></a>Asset Intelligence  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Hardware 01A - resumo de computadores numa coleção específica**|Mostra uma vista de resumo de Asset Intelligence dos computadores numa coleção especificada por si.|  
|**Hardware 03A - utilizadores primários do computador**|Mostra os utilizadores e em quantos computadores são o utilizador primário.|  
|**Hardware 03B - computadores para um utilizador principal da consola específico**|Mostra todos os computadores em que um utilizador especificado é o utilizador primário da consola.|  
|**Hardware 04A - computadores com utilizadores múltiplos (partilhados)**|Mostra os computadores que não têm um utilizador primário porque nenhum utilizador tem uma percentagem de tempo de sessão da consola superior a 66%.|  
|**Hardware 05A - utilizadores de consola num computador específico**|Mostra todos os utilizadores da consola num computador especificado.|  
|**Hardware 06A - computadores para que a consola não foi possível determinar utilizadores**|Ajuda os utilizadores administrativos a identificar computadores que têm de ter o registo de segurança ativado.|  
|**Hardware 07A - dispositivos USB por fabricante**|Mostra os dispositivos USB agrupados por fabricante.|  
|**Hardware 07B - dispositivos USB por fabricante e descrição**|Mostra os dispositivos USB agrupados por fabricante e descrição.|  
|**Hardware 07c - computadores com um dispositivo USB específico**|Mostra todos os computadores com um dispositivo USB especificado.|  
|**Hardware 07d - dispositivos USB num computador específico**|Mostra todos os dispositivos USB num computador especificado.|  
|**Hardware 08A - Hardware não preparado para uma atualização de software**|Mostra o hardware que não cumpre os requisitos mínimos de hardware.|  
|**Hardware 09A - pesquisar computadores**|Mostra um sumário do Gestor de Asset Intelligence dos computadores que correspondam aos filtros de palavra-chave no nome do computador, site do Configuration Manager, domínio, utilizador principal de consola, sistema operativo, fabricante ou modelo.|  
|**Hardware 10A - computadores numa coleção especificada que foram alterados durante um período de tempo especificado**|Mostra uma lista de computadores numa coleção especificada onde uma classe de hardware foi alterada durante um período de tempo especificado.|  
|**Hardware 10B - alterações num computador especificado durante um período de tempo especificado**|Mostra as classes alteradas num computador especificado durante um período de tempo especificado.|  
|**Licença 01A - ledger de licenciamento em Volume da Microsoft para instruções de licença Microsoft**|Mostra um inventário de todos os títulos de software da Microsoft que estão disponíveis no programa de Licenciamento em Volume da Microsoft.|  
|**Licença 01B - item de ledger de licenciamento em Volume da Microsoft por canal de vendas**|Identifica e mostra o canal de vendas para software Microsoft Volume Licensing inventariado.|  
|**Licença 01c - computadores com uma licença de Volume da Microsoft ledger item específico e vendas canal**|Identifica e mostra os computadores com um item especificado a partir do ledger de licenciamento em Volume da Microsoft.|  
|**Licença 01d - produtos de ledger de licenciamento em Volume da Microsoft num computador específico**|Identifica e mostra todos os itens de ledger de Licenciamento em Volume da Microsoft num computador especificado.|  
|**Licença 02A - contagem de licenças prestes a expirar por intervalos de tempo**|Mostra uma contagem das licenças prestes a expirar por um intervalo de tempo especificado. São apresentados os produtos cujas licenças são geridas pelo Serviço de Licenciamento de Software.|  
|**Licença 02B - computadores com licenças prestes a expirar**|Mostra os computadores especificados com licenças prestes a expirar.|  
|**Licença 02c - informações de licença num computador específico**|Mostra os produtos num computador especificado cujas licenças são geridas pelo Serviço de Licenciamento de Software.|  
|**Licença 03A - contagem de licenças por Estado de licença**|Mostra os produtos, por estado de licença, cujas licenças são geridas pelo Serviço de Licenciamento de Software.|  
|**Licença 03B - computadores com um Estado da licença específico**|Mostra os produtos, com um estado de licença especificado, cujas licenças são geridas pelo serviço de licenciamento de Software.|  
|**Licença 04A - contagem de produtos geridos por licenciamento de software**|Mostra uma contagem de produtos cujas licenças são geridas pelo Serviço de Licenciamento de Software.|  
|**Licença 04B - computadores com um produto específico gerido pelo serviço de licenciamento de Software**|Mostra os computadores, geridos pelo Serviço de Licenciamento de Software, que contêm um produto especificado.|  
|**Licença 05A - computadores a fornecer serviço de gestão de chaves**|Mostra os computadores que atuam como Servidores de Gestão de Chaves.|  
|**Licença 06A - processador contagens para produtos licenciados por processador**|Mostra o número de processadores em computadores com produtos Microsoft que suportam o licenciamento por processador.|  
|**Licença 06B - computadores com um produto específico que suporta o licenciamento por processador**|Mostra uma lista dos computadores onde um produto Microsoft especificado que suporta o licenciamento por processador está instalado.|  
|**Licença 14A - relatório de reconciliação de licenciamento em Volume da Microsoft**|Mostra a reconciliação das licenças de software adquiridas através do Contrato de Licenciamento em Volume da Microsoft e a contagem de inventário real.|  
|**Licença 14B - lista de inventário de software Microsoft não encontrado no MVLS**|Este relatório mostra os títulos de software da Microsoft em utilização que não se encontram no Contrato de Licenciamento em Volume da Microsoft.|  
|**Licença 15A - relatório de reconciliação de licenças gerais**|Mostra a reconciliação das licenças de software gerais adquiridas e a contagem de inventário real.|  
|**Licença 15b-relatório de reconciliação de licenças gerais por computador global**|Mostra os computadores com o produto licenciado com uma versão especificada instalado.|  
|**Software 01A - resumo de software instalado numa coleção específica**|Mostra um resumo do software instalado ordenado pelo número de instâncias encontradas no inventário.|  
|**Software 02A - famílias de produtos para uma coleção específica**|Mostra as famílias de produtos e a contagem de software na família para uma coleção especificada.|  
|**Software 02B - categorias de produto para uma família de produtos específica**|Mostra as categorias de produtos numa família de produto especificada e a contagem de software na categoria.|  
|**Software 02c - Software numa categoria e família de produtos específica**|Mostra todos os softwares que se encontram na categoria e família de produtos especificadas.|  
|**Software 02D - computadores com software específico instalado**|Mostra todos os computadores com um software especificado instalado.|  
|**Software 02E - software instalado num computador específico**|Mostra todos os softwares instalados num computador especificado.|  
|**Software 03A - software não categorizados**|Mostra o software categorizado como desconhecido ou sem categorização.|  
|**Software 04A - Software configurado para executar automaticamente em computadores**|Mostra uma lista do software configurado para ser executado automaticamente em computadores.|  
|**Software 04B - computadores com software específico configurado para executar automaticamente**|Mostra todos os computadores com software específico configurado para ser executado automaticamente.|  
|**Software 04c - Software configurado para executar automaticamente num computador específico**|Mostra o software instalado que está configurado para ser executado automaticamente num computador especificado.|  
|**Software 05A - objetos auxiliares de Browser**|Mostra os Objetos de Programa Auxiliar de Browser instalados em computadores numa coleção específica.|  
|**Software 05B - computadores com um objeto de programa auxiliar de Browser específico**|Mostra todos os computadores com um Objeto de Programa Auxiliar de Browser especificado.|  
|**Software 05c - objetos de programa auxiliar de Browser num computador específico**|Mostra todos os Objetos de Programa Auxiliar de Browser no computador especificado.|  
|**Software 06A - procurar software instalado**|Este relatório fornece um resumo do software instalado, ordenado pelo número de instâncias com base nos critérios de pesquisa do nome do produto, fabricante ou versão.|  
|**Software 06B - Software por nome de produto**|Mostra um resumo do software instalado, ordenado pelo número de instâncias com base no nome de um produto especificado.|  
|**Software 07A - programas executáveis utilizados recentemente pela contagem de computadores**|Mostra os programas executáveis utilizados recentemente com uma contagem de computadores em que foram utilizados. Para ver este relatório, a medição de software deve estar ativada para este site.|  
|**Software 07B - computadores que utilizaram recentemente um programa executável especificado**|Mostra os computadores nos quais um programa executável especificado foi utilizado recentemente, quando ativa a definição do cliente de medição de software.|  
|**Software 07c - programas executáveis utilizados recentemente num computador especificado**|Mostra os ficheiros executáveis utilizados recentemente num computador especificado, quando ativa a definição do cliente de medição de software.|  
|**Software 08A - programas executáveis utilizados recentemente pela contagem de utilizadores**|Mostra os programas executáveis utilizados recentemente com uma contagem dos utilizadores mais recentes dos mesmos, quando ativa a definição do cliente da medição de software.|  
|**Software 08B - utilizadores que utilizaram recentemente um programa executável especificado**|Mostra os utilizadores que utilizaram recentemente um programa executável especificado, quando ativa a definição do cliente de medição de software.|  
|**Software 08c - programas executáveis por um utilizador especificado utilizados recentemente**|Mostra os programas executáveis utilizados recentemente por um utilizador especificado, quando ativa a definição do cliente de software de medição.|  
|**Software 09A - software raramente utilizado**|Mostra os títulos de software que não foram utilizados durante um período de tempo especificado.|  
|**Software 09B - computadores com software raramente utilizado instalado**|Mostra os computadores com software instalado que não foi utilizado durante um período de tempo especificado. O período de tempo especificado é baseado no valor especificado no relatório " Software 09A - Software raramente utilizado".|  
|**Software 10A - títulos de Software com específicos múltiplas etiquetas personalizadas definidas**|Mostra os títulos de software com base na correspondência de todos os critérios das etiquetas personalizadas especificadas. Pode selecionar até três etiquetas personalizadas para refinar uma pesquisa de títulos de software.|  
|**Software 10B - computadores com um título de software com etiqueta personalizada específico instalado**|Mostra todos os computadores nesta coleção que têm o título de software com etiqueta personalizada especificado instalado.|  
|**Software 11A - títulos de Software com uma etiqueta personalizada específica definida**|Mostra os títulos de software com base na correspondência de, pelo menos, um dos critérios especificados da etiqueta personalizada.|  
|**Software 12A - títulos de Software sem uma etiqueta personalizada**|Mostra todos os títulos de software que não têm uma etiqueta personalizada definida.|  
|**Software 14A - procurar etiqueta de identificação de software ativado de software**|Mostra a contagem do software instalado com uma etiqueta de identificação de software ativada.|  
|**Software 14B - computadores com etiqueta de identificação de software específica ativada software instalado**|Mostra todos os computadores com software instalado com uma etiqueta de identificação de software especificada ativada.|  
|**Software 14C - software identificação tag ativada software instalado num computador específico**|Mostra todos os softwares instalados com uma etiqueta de identificação de software especificada ativada num computador especificado.|  

### <a name="client-push"></a>Cliente de Push  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Detalhes do Estado de instalação de push de cliente**|Mostra as informações sobre o processo da instalação push do cliente para todos os sites.|  
|**Detalhes do Estado de instalação de push do cliente para um site especificado**|Mostra as informações sobre o processo da instalação push do cliente para um site especificado.|  
|**Resumo do Estado de instalação de push de cliente**|Mostra uma vista de resumo do estado da instalação push do cliente para todos os sites.|  
|**Estado de instalação de push de cliente resumo para um site especificado**|Mostra uma vista de resumo do estado da instalação push do cliente para um site especificado.|  

### <a name="client-status"></a>Estado do cliente  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Detalhes de remediação do cliente**|Mostra os detalhes de remediação do cliente para uma coleção que especificar.|  
|**Resumo da remediação do cliente**|Mostra um resumo das ações de remediação do cliente para uma coleção especificada.|  
|**Histórico do Estado do cliente**|Mostra uma apresentação do histórico do estado geral de cliente no site.|  
|**Resumo do Estado do cliente**|Mostra os resultados da verificação de clientes ativos para uma coleção específica.|  
|**Hora de cliente a política de pedido**|Mostra a percentagem de clientes que realizaram um pedido de política pelo menos uma vez nos últimos 30 dias. Cada dia representa uma percentagem total de clientes que realizaram um pedido de política desde o primeiro dia do ciclo.|  
|**Detalhes de verificação de clientes com o cliente falhada**|Mostra os detalhes sobre clientes cuja verificação de cliente falhou numa coleção especificada.|  
|**Detalhes de clientes Inativos**|Mostra uma lista detalhada dos clientes inativos para uma determinada coleção.|  

### <a name="company-resource-access"></a>Acesso aos Recursos da Empresa  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Histórico de emissão de certificados**|Mostra o histórico dos certificados emitidos pelo ponto de registo de certificados para utilizadores e dispositivos no período de tempo especificado.|  
|**Lista de recursos por Estado de emissão de certificados**|Mostra os utilizadores ou dispositivos num estado de emissão de certificados especificado depois da avaliação de um perfil de certificado especificado.|  
|**Lista de recursos com certificados prestes a expirar**|Mostra os dispositivos ou utilizadores com certificados que expiram na data especificada ou antes.|  

### <a name="compliance-and-settings-management"></a>Gestão de Compatibilidade e Definições  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Histórico de conformidade de uma linha de base de configuração**|Mostra o histórico de alterações da conformidade de uma linha de base da configuração no período de tempo especificado.|  
|**Histórico de conformidade de um item de configuração**|Mostra o histórico de alterações da conformidade de um item de configuração no período de tempo especificado.|  
|**Detalhes de regras de conformidade dos itens de configuração numa linha de base de configuração para um recurso**|Mostra informações sobre as regras que foram consideradas em conformidade para um item de configuração especificado, num dispositivo ou utilizador especificado.|  
|**Detalhes de regras em conflito de itens de configuração numa linha de base de configuração para um recurso**|Mostra informações sobre regras num item de configuração implementado num utilizador ou dispositivo especificado que estão em conflito com outras regras contidas no mesmo ou outro item de configuração implementado.|  
|**Detalhes de erros de itens de configuração numa linha de base de configuração para um recurso**|Mostra informações sobre erros gerados por um item de configuração especificado num dispositivo ou utilizador especificado.|  
|**Detalhes de regras não compatíveis de itens de configuração numa linha de base de configuração para um recurso**|Mostra informações sobre regras que foram consideradas incompatíveis para um item de configuração especificado, para um dispositivo ou utilizador especificado.|  
|**Detalhes de regras remediados de itens de configuração numa linha de base de configuração para um recurso**|Mostra informações sobre regras que foram remediadas por um item de configuração especificado para um dispositivo ou utilizador especificado.|  
|**Lista de recursos por Estado de conformidade para um item de configuração numa linha de base de configuração**|Mostra os dispositivos ou utilizadores num estado de conformidade especificado depois da avaliação de um item de configuração especificado.|  
|**Lista de recursos por Estado de conformidade para uma linha de base de configuração**|Mostra os utilizadores ou dispositivos num estado de conformidade especificado depois da avaliação de uma linha de base da configuração especificada.|  
|**Lista das regras em conflito com uma regra especificada para um recurso**|Mostra uma lista das regras em conflito com uma regra especificada para um item de configuração implementado num dispositivo especificado.|  
|**Lista de recursos desconhecidos para uma linha de base de configuração**|Mostra uma lista dos dispositivos ou utilizadores que ainda não reportaram dados de conformidade para uma linha de base da configuração especificada.|  
|**Lista de recursos desconhecidos de um item de configuração**|Mostra uma lista dos dispositivos ou utilizadores que ainda não forneceram dados de conformidade para um item de configuração especificado.|  
|**Regras e erros de resumo dos itens de configuração numa linha de base de configuração para um recurso**|Mostra um resumo do estado de conformidade das regras e erros de definições de um item de configuração especificado implementado num dispositivo ou utilizador especificado.|  
|**Resumo de conformidade por linha de base de configuração**|Mostra um resumo da conformidade geral das linhas de bases da configuração implementadas na hierarquia.|  
|**Resumo de conformidade por itens de configuração para uma linha de base de configuração**|Mostra um resumo da conformidade dos itens de configuração numa linha de base da configuração especificada.|  
|**Resumo de conformidade por políticas de configuração**|Mostra um resumo da conformidade das políticas de configuração.|  
|**Resumo de conformidade de uma linha de base de configuração para uma coleção**|Mostra um resumo da conformidade geral de uma linha de base da configuração especificada implementada numa coleção especificada.|  
|**Lista de aplicações e dispositivos para um utilizador especificado não conformes**|Apresenta informações sobre utilizadores e dispositivos que têm aplicações instaladas que não estão em conformidade com uma política especificada por si.|  
|**Resumo de utilizadores que têm aplicações não conformes**|Apresenta informações sobre utilizadores que têm aplicações instaladas que não estão em conformidade com uma política especificada por si.|  
|**Aceitação dos termos e condições**|Apresenta os itens de Termos e Condições e que versão foi aceite por cada utilizador.|  

### <a name="device-management"></a>Gestão de Dispositivos  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os clientes de dispositivos móveis**|Mostra informações sobre todos os clientes de dispositivos móveis. Não estão incluídos os dispositivos móveis geridos pelo conector do Exchange Server.|  
|**Problemas de certificado em dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE e que não estão em bom Estados**|Mostra informações detalhadas sobre problemas de certificado em dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE.|  
|**Falha de implementação do cliente em dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE**|Mostra informações detalhadas sobre falhas de implementação para dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE.|  
|**Detalhes de estado de implementação do cliente para dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE**|Mostra informações sobre o estado de dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE.|  
|**Sucesso de implementação do cliente para dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE**|Mostra informações detalhadas sobre o êxito da implementação para dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE.|  
|**Problemas de comunicação em dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE e que não estão em bom Estados**|Este relatório contém informações detalhadas sobre problemas de comunicação em dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE.|  
|**Estado de conformidade para os dispositivos móveis que são geridos pelo conector do Exchange Server**|Mostra um resumo do estado de conformidade com a política de caixa de correio Predefinida do Exchange ActiveSync para os dispositivos móveis geridos pelo conector do Exchange Server.|  
|**Contagem de dispositivos móveis por definições de visualização**|Este relatório mostra o número de dispositivos móveis por definições de visualização.|  
|**Contagem de dispositivos móveis por sistema operativo**|Este relatório mostra o número de dispositivos móveis por sistema operativo.|  
|**Contagem de dispositivos móveis por memória de programa**|Este relatório mostra o número de dispositivos móveis por memória de programa.|  
|**Contagem de dispositivos móveis por configurações da memória de armazenamento**|Contagem de dispositivos móveis por configurações da memória de armazenamento|  
|**Informações de estado de funcionamento para dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE**|Mostra informações detalhadas de estado de funcionamento de dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE.|  
|**Estado de funcionamento resumo para dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE**|Mostra informações de resumo de estado de funcionamento para dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE.|  
|**Dispositivos móveis Inativos que são geridos pelo conector do Exchange Server**|Mostra os dispositivos móveis geridos pelo conector do Exchange Server e que não efetuaram ligação ao Exchange Server durante um número especificado de dias.|  
|**Lista de dispositivos inscritos por utilizador no Microsoft Intune**|Mostra todos os dispositivos que um utilizador inscreveu com o Microsoft Intune.|  
|**Lista de dispositivos por Estado de acesso condicional**|Apresenta informações sobre o atual estado de acesso de conformidade e acesso condicional dos dispositivos. Pode utilizar este relatório com as políticas de acesso condicional. Este relatório está disponível a partir da versão 1602 do Configuration Manager.|  
|**Conformidade de acesso condicional para utilizador**|Fornece informações de conformidade de acesso condicional detalhadas para um utilizador específico, incluindo o nome do dispositivo e da plataforma, se o dispositivo estiver em conformidade e quando o dispositivo foi avaliado pela última vez. Este relatório está disponível a partir da versão 1602 do Configuration Manager.|  
|**Problemas do cliente local em dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE e que não estão em bom Estados**|Este relatório contém informações detalhadas sobre problemas do cliente local em dispositivos móveis que são geridos pelo cliente do Configuration Manager para Windows CE.|  
|**Informações de cliente do dispositivo móvel**|Mostra informações sobre os dispositivos móveis que tenham o cliente do Configuration Manager instalado. Pode utilizar este relatório para verificar que dispositivos móveis conseguem comunicar com um ponto de gestão com êxito.|  
|**Detalhes de conformidade de dispositivos móveis para o conector do Exchange Server**|Mostra os detalhes da conformidade do dispositivo móvel para uma política de caixa de correio predefinida do Exchange ActiveSync, configurada com o conector do Exchange Server.|  
|**Dispositivos móveis por sistema operativo**|Mostra os dispositivos móveis por sistema operativo.|  
|**Dispositivos móveis desbloqueados por jailbreak ou rooting**|Mostra os dispositivos móveis desbloqueados com jailbreak ou rooting.|  
|**Dispositivos móveis que são geridos porque concluíram a inscrição mas falharam a atribuição a um site**|Mostra os dispositivos móveis que concluíram a inscrição com o Configuration Manager e possuem um certificado, mas não foi possível concluir a atribuição de site.|  
|**Dispositivos móveis com uma quantidade específica de memória de programa livre**|Mostra todos os dispositivos móveis com a quantidade especificada de memória de programa livre.|  
|**Dispositivos móveis com uma quantidade específica de memória de armazenamento amovível livre**|Mostra todos os dispositivos móveis com a quantidade especificada de memória de armazenamento amovível livre.|  
|**Dispositivos móveis com problemas de renovação de certificado**|Mostra os dispositivos móveis inscritos cuja renovação de certificado falhou. Se o certificado não for renovado antes da data de expiração, os dispositivos móveis ficarão sem gestão.|  
|**Dispositivos móveis com memória de programa livre baixa (menos de tamanho em KB especificado)**|Mostra os dispositivos móveis com memória de programa inferior a um tamanho em KB especificado.|  
|**Dispositivos móveis com memória de armazenamento amovível livre baixa (menos de tamanho em KB especificado)**|Mostra os dispositivos móveis com memória de armazenamento amovível inferior a um tamanho em KB especificado.|  
|**Número de dispositivos inscritos por utilizador no Windows Intune**|Este relatório apresenta os utilizadores ativados para a subscrição do Microsoft Intune e o número total de dispositivos inscritos para cada utilizador.|  
|**Pedido de limpeza pendente para dispositivos móveis**|Mostra os pedidos para a ação apagar pendentes para dispositivos móveis.|  
|**Dispositivos móveis inscritos e atribuídos recentemente**|Mostra os dispositivos móveis que concluíram a inscrição com o Configuration Manager e atribuído com êxito a um site.|  
|**Dispositivos móveis apagados recentemente**|Mostra a lista de dispositivos móveis apagados com êxito recentemente.|  
|**Resumo das definições para dispositivos móveis que são geridos pelo conector do Exchange Server**|Mostra o número de dispositivos móveis que aplicam as definições para cada política de caixa de correio predefinida do ActiveSync, que é gerida pelo conector do Exchange Server.|  
|**Estado detalhado das chaves de Sideload do Windows RT**|Mostra informações de estado detalhadas para uma chave de sideload especificada do Windows RT.|  
|**Resumo das chaves de Sideload do Windows RT**|Mostra o estado das chaves de sideload do Windows RT.|  

### <a name="driver-management"></a>Gestão do Controlador  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os controladores**|Mostra a lista de todos os controladores.|  
|**Todos os controladores de uma plataforma específica**|Mostra todos os controladores de uma plataforma especificada.|  
|**Todos os controladores numa imagem de arranque específica**|Mostra todos os controladores numa imagem de arranque especificada.|  
|**Todos os controladores numa categoria específica**|Mostra todos os controladores numa categoria especificada.|  
|**Todos os controladores num pacote específico**|Mostra todos os controladores num pacote especificado.|  
|**Categorias para um controlador específico**|Mostra as categorias para um controlador especificado.|  
|**Computadores que falharam ao instalar controladores para uma coleção específica**|Mostra os computadores nos quais ocorreu um erro ao instalar os controladores para uma coleção especificada.|  
|**Relatório de uma coleção específica de correspondência do catálogo de controladores**|Mostra o relatório de correspondência do catálogo de controladores de uma coleção especificada.|  
|**Um computador específico no relatório de correspondência de controladores**|Mostra o relatório de correspondência do catálogo de controladores de um computador especificado.|  
|**Relatório de um dispositivo específico num computador específico de correspondência do catálogo de controladores**|Mostra o relatório de correspondência do catálogo de controladores de um dispositivo especificado num computador especificado.|  
|**Correspondência de controladores relatórios para computadores numa coleção específica com um dispositivo específico**|Mostra o relatório de correspondência do catálogo de controladores de computadores numa coleção especificada com um dispositivo especificado.|  
|**Controladores que falharam ao instalar num computador específico**|Mostra os controladores cuja instalação falhou num computador especificado.|  
|**Plataformas suportadas para um controlador específico**|Mostra as plataformas suportadas por um controlador especificado.|  

### <a name="endpoint-protection"></a>Endpoint Protection  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório de atividade Antimalware**|Mostra uma descrição geral da atividade antimalware.|  
|**Antimalware estado e histórico geral**|Mostra uma descrição geral do estado e histórico da atividade antimalware.|  
|**Detalhes de software maligno do computador**|Mostra detalhes sobre um computador especificado e a lista de software maligno encontrado no mesmo.|  
|**Computadores infetados**|Mostra uma lista de computadores com uma ameaça especificada detetada.|  
|**Principais utilizadores por ameaças**|Mostra a lista de utilizadores com o maior número de ameaças detetadas.|  
|**Lista de ameaças**|Mostra a lista de ameaças encontradas para uma conta de utilizador especificada.|  

### <a name="hardware---cd-rom"></a>Hardware - CD-ROM  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Informações de CD-ROM para um computador específico**|Mostra informações sobre as unidades de CD-ROM num computador especificado.|  
|**Computadores de um fabricante de CD-ROM específico**|Mostra uma lista dos computadores com uma unidade de CD-ROM criada por um fabricante especificado por si.|  
|**Unidades de CD-ROM de contagem por fabricante**|Mostra o número de unidades CD-ROM inventariadas por fabricante.|  
|**Histórico - histórico de CD-ROM para um computador específico**|Mostra o histórico de inventário das unidades CD-ROM num computador especificado.|  

### <a name="hardware---disk"></a>Hardware - disco  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com um tamanho de disco rígido específico**|Mostra uma lista dos computadores com discos rígidos de um tamanho especificado.|  
|**Computadores com pouco espaço livre em disco espaço (inferior a % livre especificada)**|Mostra uma lista de computadores numa coleção especificada que têm menos espaço livre em disco do que o especificado.|  
|**Computadores com baixa espaço livre em disco (menos do que os MB livres especificados)**|Mostra uma lista de computadores e discos com pouco espaço livre em disco. A quantidade de espaço livre a verificar é especificada em MB.|  
|**Contagem das configurações de disco físico**|Mostra o número de discos rígidos inventariados por capacidade de disco.|  
|**Informações de disco para um computador específico - discos lógicos**|Mostra informações de resumo sobre os discos lógicos num computador especificado.|  
|**Informações de disco para um computador específico - partições**|Mostra informações de resumo sobre as partições do disco num computador especificado.|  
|**Informações de disco para um computador específico - discos físicos**|Mostra informações de resumo sobre os discos físicos num computador especificado.|  
|**Histórico - histórico do espaço de disco lógico para um computador específico**|Mostra o histórico de inventário para unidades de disco lógicas num computador especificado.|  

### <a name="hardware---general"></a>Hardware - geral  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Informações de um computador específico**|Mostra informações de resumo de um computador especificado.|  
|**Computadores num domínio ou grupo de trabalho específico**|Mostra uma lista de computadores num Grupo de Trabalho ou domínio especificado.|  
|**Classes de inventário atribuídas a uma coleção específica**|Mostra as classes de inventário que estão atribuídas a uma coleção especificada.|  
|**Classes de inventário ativadas num computador específico**|Mostra as classes de inventário ativadas num computador especificado.|  

### <a name="hardware---memory"></a>Hardware - memória  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores onde a memória física foi alterada**|Mostra uma lista de computadores onde a quantidade de RAM foi alterada desde o último ciclo de inventário.|  
|**Computadores com uma quantidade específica de memória**|Mostra uma lista de computadores com uma quantidade especificada de RAM (Memória Física Total arredondada para o MB mais próximo).|  
|**Computadores com memória insuficiente (menor ou igual aos MB especificados)**|Mostra uma lista de computadores com memória insuficiente. A quantidade de memória a verificar é especificada em MB.|  
|**Contagem das configurações de memória**|Mostra o número de computadores inventariados por quantidade de RAM.|  
|**Informações de memória para um computador específico**|Mostra informações de resumo sobre a memória num computador especificado.|  

### <a name="hardware---modem"></a>Hardware - Modem  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores para um fabricante de modems especificado**|Mostra uma lista de computadores com um modem criado por um fabricante especificado.|  
|**Contagem de modems por fabricante**|Mostra o número de modems inventariados para cada fabricante de modems.|  
|**Informações de modem para um computador específico**|Mostra informações de resumo sobre o modem num computador especificado.|  

### <a name="hardware---network-adapter"></a>Hardware - placa de rede  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com um adaptador de rede específicas**|Mostra uma lista de computadores com uma placa de rede especificada.|  
|**Contagem de placas de rede por tipo**|Mostra o número de placas de rede inventariadas de cada tipo.|  
|**Informações da placa de rede para um computador específico**|Mostra informações sobre as placas de rede instaladas num computador especificado.|  

### <a name="hardware---processor"></a>Hardware - processador  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores para uma velocidade de processador específico**|Mostra uma lista de computadores que têm um processador com uma velocidade especificada.|  
|**Computadores com processadores rápidos (maiores ou igual a uma velocidade de relógio especificada)**|Mostra uma lista de computadores com processadores com uma velocidade que é mais rápida do que a velocidade especificada.|  
|**Computadores com processadores lentos (menor ou igual a uma velocidade de relógio especificada)**|Mostra uma lista de computadores com processadores que são executados com uma velocidade de relógio igual ou mais lenta do que a especificada.|  
|**Contagem de velocidades de processador**|Mostra o número de computadores inventariados por velocidade de processador.|  
|**Informações do processador para um computador específico**|Mostra informações sobre os processadores instalados num computador especificado.|  

### <a name="hardware---scsi"></a>Hardware - SCSI  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Tipo de computadores com um cartão SCSI especificado**|Mostra uma lista de computadores com um cartão de SCSI especificado instalado.|  
|**Tipos de cartão SCSI de contagem**|Mostra o número de cartões de SCSI inventariados por tipo de cartão.|  
|**Informações de cartão SCSI para um computador específico**|Mostra informações sobre os cartões SCSI instalados num computador especificado.|  

### <a name="hardware---sound-card"></a>Hardware - placa de som  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com uma placa de som especificada**|Mostra uma lista de computadores com uma placa de som especificada.|  
|**Contagem de placas de som**|Mostra o número de computadores inventariados por cada tipo de placa de som.|  
|**Informações da placa de som para um computador específico**|Mostra informações de resumo sobre as placas de som num computador especificado.|  

### <a name="hardware---video-card"></a>Hardware - placa de vídeo  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com uma placa de vídeo especificada**|Mostra uma lista de computadores com uma placa gráfica especificada.|  
|**Contagem de placas de vídeo**|Mostra uma lista de todas as placas gráficas instaladas nos computadores e o número de cada tipo de placa gráfica.|  
|**Informações da placa gráfica de um computador específico**|Mostra informações de resumo sobre as placas gráficas instaladas num computador especificado.|  

### <a name="migration"></a>Migração  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Clientes na lista de exclusão**|Mostra os clientes excluídos da migração.|  
|**Dependência de uma coleção do Configuration manager**|Mostra os objetos que dependem de uma coleção da hierarquia de origem.|  
|**Propriedades da tarefa de migração**|Este relatório mostra os conteúdos da tarefa de migração especificada.|  
|**Tarefas de migração**|Este relatório mostra a lista de tarefas de migração.|  
|**Objetos que falharam ao migrar**|Mostra uma lista de objetos cuja migração falhou durante a última tentativa.|  

### <a name="network"></a>Rede  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Contagem de endereços IP por sub-rede**|Mostra o número de endereços IP inventariados para cada sub-rede IP.|  
|**IP - todas as sub-redes por máscara de sub-rede**|Mostra uma lista de sub-redes IP e de máscaras de sub-rede.|  
|**IP - computadores numa sub-rede específica**|Mostra uma lista de computadores e informações de IP de uma sub-rede IP especificada.|  
|**IP - informações para um computador específico**|Mostra informações de resumo sobre o IP de um computador especificado.|  
|**IP - informações para um endereço IP específico**|Mostra informações de resumo sobre um endereço IP especificado.|  
|**MAC - computadores para um endereço MAC específico**|Mostra o nome do computador e o endereço IP dos computadores com o endereço MAC especificado.|  

### <a name="network-access-protection"></a>Proteção de Acesso à Rede  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Comparação das atualizações de software instaladas por implementações de atualização de software e remediação NAP.**|Mostra um resumo de comparação das atualizações de software instaladas por implementações de atualização de software e remediação NAP.|  
|**Frequência um computador da presença em remediação durante um período especificado**|Este relatório mostra com que frequência um computador foi remediado durante um período especificado.|  
|**Lista de computadores que instalaram uma atualização de software específica através de remediação durante um período especificado**|Mostra os computadores com uma atualização de software específica instalada através de remediação durante um período de tempo especificado (dias).|  
|**Lista de computadores que seriam incompatíveis com base nas actualizações de software selecionadas**|Mostra todos os computadores que não estariam em conformidade com base nas atualizações de software selecionadas.|  
|**Lista de computadores onde não foi possível detetar serviço NAP**|Mostra uma lista de computadores onde não foi possível detetar o serviço NAP.|  
|**Lista de computadores elegíveis pelo NAP**|Mostra uma lista de computadores em que o serviço NAP não está a ser executado ou tem um estado desconhecido.|  
|**Lista de políticas de proteção de acesso de rede**|Mostra as políticas de Proteção de Acesso à Rede com as respetivas datas efetivas.|  
|**Lista de computadores não conformes em remediação no último intervalo de consulta**|Mostra uma lista de computadores não conformes em remediação com as horas das suas últimas avaliações conhecidas.|  
|**Lista de computadores não conformes em remediação durante um período especificado**|Mostra uma lista de computadores não conformes em remediação durante um período de tempo especificado.|  
|**Lista de falhas de remediação para período de tempo especificado**|Mostra uma lista de falhas de remediação num número especificado de dias.|  
|**Lista de atualizações de software instaladas através de remediação**|Mostra as atualizações de software instaladas através de remediação durante um período especificado.|  
|**Resumo de computadores não conformes em remediação no último intervalo de consulta**|Mostra um resumo dos computadores não conformes em remediação no último intervalo de consulta.|  
|**Resumo de computadores não conformes em remediação durante um período especificado**|Mostra um resumo de computadores incompatíveis em remediação durante um período de tempo especificado.|  

### <a name="operating-system"></a>Sistema Operativo  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Histórico de versões de sistema operativo do computador**|Mostra o histórico de inventário do sistema operativo num computador especificado.|  
|**Computadores com um sistema operativo específico**|Mostra os computadores com um sistema operativo especificado.|  
|**Computadores com um sistema operativo específico e o service pack**|Mostra os computadores com um sistema operativo e service pack especificados.|  
|**Contagem de versões do sistema operativo**|Mostra o número de computadores inventariados por sistema operativo.|  
|**Contagem de sistemas operativos e service packs**|Mostra o número de computadores inventariados por combinações de sistema operativo e service pack.|  
|**Serviços - computadores com um serviço específico**|Mostra uma lista de computadores a executar um serviço especificado.|  
|**Serviços - computadores com servidor de acesso remoto**|Mostra uma lista de computadores a executar o Servidor de Acesso Remoto.|  
|**Serviços - informações de serviços para um computador específico**|Mostra informações de resumo sobre os serviços num computador especificado.|  
|**Computadores Windows Server**|Mostra uma lista de computadores que executam os sistemas operativos Windows Server.|  

### <a name="out-of-band-management"></a>Gestão Fora de Banda  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores com controladores fora de banda gestão**|Mostra uma lista de computadores com controladores de gestão fora de banda.|  
|**Atividade fora de banda gestão consola**|Mostra uma lista de mensagens de estado a identificar a atividade da consola de gestão fora de banda.|  
|**Estado do cliente aprovisionamento fora de banda gestão**|Mostra uma lista de computadores aprovisionados para gestão fora de banda.|  

### <a name="power-management"></a>Gestão de Energia  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Gestão de energia - atividade do computador**|Mostra um gráfico com a atividade do monitor, computador e utilizador numa coleção especificada e num período de tempo especificado.|  
|**Gestão de energia - atividade do computador por computador**|Mostra um gráfico com a atividade do monitor, computador e utilizador, num computador especificado e numa data especificada.|  
|**Gestão de energia - detalhes de atividade do computador**|Mostra uma lista das funcionalidades de suspensão e reativação dos computadores na coleção especificada numa data e hora especificadas.|  
|**Gestão de energia - detalhes do computador**|Mostra informações detalhadas sobre as funcionalidades de energia, definições de energia e esquemas de energia aplicados a um computador especificado.|  
|**Gestão de energia - computador não transmite detalhes**|Mostra uma lista de computadores que não reportam atividade de energia numa data e hora especificadas.|  
|**Gestão de energia - computadores excluídos**|Mostra uma lista de computadores excluídos do esquema de energia.|  
|**Gestão de energia - computadores com vários esquemas de energia**|Mostra uma lista de computadores com múltiplas definições de energia em conflito aplicadas.|  
|**Gestão de energia - consumo de energia**|Mostra o consumo mensal total de energia (em kWh) de uma coleção especificada num período de tempo especificado.|  
|**Gestão de energia - consumo de energia por dia**|Mostra o consumo de energia total (em kWh) de uma coleção especificada nos últimos 31 dias.|  
|**Gestão de energia - custo de energia**|Mostra o custo do consumo mensal total de energia de uma coleção especificada num período de tempo especificado.|  
|**Gestão de energia - custo da energia por dia**|Mostra o custo do consumo de energia total de uma coleção especificada nos últimos 31 dias.|  
|**Gestão de energia - impacto ambiental**|Mostra um gráfico com as emissões de dióxido de carbono (CO2) geradas por uma coleção específica num dado período de tempo.|  
|**Gestão de energia - impacto ambiental por dia**|Mostra um gráfico com as emissões de CO2 geradas por uma coleção específica nos últimos 31 dias.|  
|**Gestão de energia - detalhes da insónia do computador**|Mostra informações detalhadas sobre computadores que não entraram em suspensão ou hibernação num período de tempo especificado.|  
|**Gestão de energia - relatório de insónia**|Mostra uma lista de causas comuns que impedem os computadores de suspender ou hibernar e o número de computadores que foram afetados por cada causa durante um período de tempo especificado.|  
|**Gestão de energia - capacidades de energia**|Mostra as funcionalidades de gestão de energia dos computadores na coleção especificada.|  
|**Gestão de energia - definições de energia**|Mostra uma lista agregada de definições de energia utilizadas pelos computadores numa coleção especificada.|  
|**Gestão de energia - detalhes de definições de energia**|Utilizado para apresentar mais informações sobre computadores que foram especificados no **gestão de energia - definições de energia** relatório.|  

### <a name="replication-traffic"></a>Tráfego de Replicação  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Global dados tráfego de replicação por ligação (gráfico de linhas)**|Mostra o tráfego total de replicação de dados globais numa ligação especificada para um número especificado de dias.|  
|**Global dados tráfego de replicação por ligação (gráfico circular)**|Mostra o tráfego total de replicação de dados globais numa ligação especificada para um número especificado de dias.|  
|**Tráfego de replicação de hierarquia por ligação**|Mostra o tráfego total de replicação para cada ligação na hierarquia para um número especificado de dias.|  
|**Hierarquia superior dez replicação grupos tráfego por ligação (gráfico circular)**|Mostra o tráfego de replicação dos dez principais grupos de replicação em toda a hierarquia identificada pela ligação.|  
|**Tráfego de replicação da ligação**|Mostra o tráfego total de replicação para todos os dados relativamente a um número especificado de dias.|  
|**Tráfego do grupo de replicação por ligação**|Mostra o tráfego de rede do grupo de replicação através de uma ligação de replicação da base de dados especificada para um número especificado de dias.|  
|**Site dados tráfego de replicação por ligação (gráfico de linhas)**|Mostra o tráfego de replicação total de dados do site numa ligação especificada para um número especificado de dias.|  
|**Site dados tráfego de replicação por ligação (gráfico circular)**|Mostra o tráfego de replicação total de dados do site numa ligação especificada para um número especificado de dias.|  
|**Tráfego de replicação da hierarquia total (gráfico de linhas)**|Mostra a replicação de dados do site e os dados globais agregados da hierarquia para cada direção de cada ligação relativamente a um número especificado de dias.|  
|**Tráfego de replicação da hierarquia total (gráfico circular)**|Mostra a replicação de dados do site e os dados globais agregados da hierarquia para cada direção de cada ligação relativamente a um número especificado de dias.|  

### <a name="site---client-information"></a>Site - informação de cliente  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório de estado detalhado sobre a atribuição de cliente**|Mostra informações detalhadas sobre o estado da atribuição do cliente.|  
|**Detalhes de falha de atribuição de cliente**|Mostra informações detalhadas sobre as falhas da atribuição do cliente.|  
|**Detalhes do Estado de atribuição de cliente**|Mostra informações gerais sobre o estado da atribuição do cliente.|  
|**Detalhes de êxito de atribuição de cliente**|Mostra informações detalhadas sobre os clientes cujas atribuições tiveram êxito.|  
|**Relatório de falhas de implementação do cliente**|Mostra informações detalhadas para clientes cujas implementações falharam.|  
|**Detalhes do Estado de implementação de cliente**|Mostra informações de resumo do estado das instalações do cliente.|  
|**Relatório de sucesso de implementação do cliente**|Mostra informações detalhadas de clientes cujas implementações tiveram êxito.|  
|**Clientes sem capacidade de comunicação HTTPS**|Mostra informações detalhadas sobre cada cliente no site que tenha executado a ferramenta HTTPS Communication Readiness e reportado incapacidade de comunicar por HTTPS.|  
|**Computadores atribuídos mas não instalados para um site específico**|Mostra uma lista de computadores que foram atribuídos a um site especificado, mas que não comunicam com esse site.|  
|**Computadores com uma versão de cliente específico do Configuration Manager**|Mostra uma lista de computadores com uma versão especificada do software de cliente do Configuration Manager.|  
|**Contagem de clientes e protocolo utilizado para comunicação**|Mostra um resumo dos métodos de comunicação utilizados pelos clientes (HTTP ou HTTPS).|  
|**Contagem de clientes atribuídos e instalados para cada site**|Mostra o número de computadores atribuídos e instalados em cada site. Os clientes com uma localização de rede associada a múltiplos sites só serão contados como instalados se estiverem a comunicar com esse site.|  
|**Contagem de clientes com capacidade de comunicação HTTPS**|Mostra informações detalhadas sobre cada cliente no site que tenha executado a ferramenta HTTPS Communication Readiness e reportado a sua capacidade ou incapacidade de comunicar por HTTPS.|  
|**Contagem de clientes para cada site**|Mostra o número de clientes do Configuration Manager instalados por código do site.|  
|**Clientes de contagem do Configuration Manager por versões de cliente**|Mostra o número de computadores detetados pela versão de cliente do Configuration Manager.|  
|**Detalhes de problemas relatados ao ponto de estado de contingência numa coleção especificada**|Mostra informações detalhadas sobre problemas reportados por clientes numa coleção especificada, se tiverem um ponto de estado de contingência atribuído.|  
|**Detalhes de problemas relatados ao ponto de estado de contingência para um site especificado**|Mostra informações detalhadas sobre os problemas reportados pelos clientes num site especificado, se tiverem um ponto de estado de contingência atribuído.|  
|**Resumo dos problemas reportados ao ponto de estado de contingência**|Mostra informações sobre todos os problemas reportados pelos clientes, se tiverem um ponto de estado de contingência atribuído.|  
|**Resumo dos problemas reportados ao ponto de estado de contingência numa coleção específica**|Mostra um resumo detalhado sobre os problemas reportados por clientes numa coleção especificada, se tiverem um ponto de estado de contingência atribuído.|  

### <a name="site---discovery-and-inventory-information"></a>Site - informações de inventário e de deteção  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Clientes que não relataram recentemente (num número especificado de dias)**|Mostra uma lista de clientes que não reportaram dados de deteção, inventário de hardware ou inventário de software num número especificado de dias.|  
|**Computadores detetados por um site específico**|Mostra uma lista de todos os computadores detetados por um site especificado e a data da deteção mais recente.|  
|**Computadores detetados recentemente por método de deteção**|Mostra uma lista de computadores detetados num número especificado de dias e os agentes que os detetaram. Um computador pode aparecer mais do que uma vez nesta lista se for detetado por múltiplos agentes.|  
|**Computadores não detetados recentemente (num número especificado de dias)**|Mostra uma lista de computadores que não foram detetados recentemente e o número de dias desde que foram detetados.|  
|**Computadores não inventariados recentemente (num número especificado de dias)**|Mostra uma lista de computadores que não foram inventariados recentemente e as últimas vezes em que foram inventariados.|  
|**Computadores que podem partilhar o mesmo identificador exclusivo do Configuration Manager**|Mostra uma lista de computadores cujos nomes foram alterados. Uma alteração no nome é um possível sintoma de que o computador partilha um identificador exclusivo do Configuration Manager com outro computador.|  
|**Computadores com endereços MAC duplicados**|Mostra os computadores que partilham o endereço MAC.|  
|**Contagem de computadores nos domínios de recurso ou grupos de trabalho**|Mostra o número de computadores em cada domínio de recurso ou grupo de trabalho.|  
|**Informações de deteção para um computador específico**|Mostra uma lista dos agentes e sites que detetaram um computador especificado.|  
|**Datas de inventário para um computador específico**|Mostra a data e hora da execução mais recente do inventário num computador especificado.|  

### <a name="site---general"></a>Site - geral  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores num site específico**|Mostra uma lista dos computadores cliente num site especificado.|  
|**Estado de site para a hierarquia**|Mostra a lista de sites na hierarquia com informações da versão do site e do estado do site.|  
|**Estado da atualização do Configuration Manager na hierarquia**|Mostra informações sobre atualizações de sites do Configuration Manager para a hierarquia.|  

### <a name="site---server-information"></a>Site - informações do servidor  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Funções de sistema de sites e servidores do sistema de sites para um site específico**|Mostra uma lista do servidor do sistema de sites e as respetivas funções do sistema de sites num site especificado.|  

### <a name="software---companies-and-products"></a>Software - empresas e produtos  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os produtos inventariados de uma empresa de software específica**|Mostra uma lista dos produtos e versões de software inventariados de uma empresa de software especificada.|  
|**Todas as empresas de software**|Mostra uma lista de todas as empresas que fabricam software inventariado.|  
|**Todas as aplicações do Windows**|Mostra um resumo das aplicações do Windows instaladas, ordenadas pelo número de instância com base nos critérios de pesquisa de nome, arquitetura ou publicador da aplicação.|  
|**Computadores com um produto específico**|Mostra uma lista de computadores nos quais um produto especificado está inventariado, bem como as versões desse produto.|  
|**Computadores com uma versão e nome de produto específico**|Mostra uma lista dos computadores nos quais uma versão especificada de um produto está inventariada.|  
|**Computadores com software específico registado em Adicionar/remover programas**|Mostra um resumo de todos os computadores com software especificado e registado em Adicionar/Remover Programas ou em Programas e Funcionalidades.|  
|**Contagem de todos os produtos inventariados e versões**|Mostra uma lista dos produtos e versões de software inventariados e o número de computadores nos quais estão instalados.|  
|**Contagem de produtos e versões inventariados para um produto específico**|Mostra uma lista das versões inventariadas de um produto especificado e o número de computadores nos quais estão instaladas.|  
|**Contagem de todas as instâncias de software registadas em Adicionar ou remover programas**|Mostra um resumo de todas as instâncias do software instalado e registado em Adicionar/Remover Programas ou em Programas e Funcionalidades nos computadores da coleção especificada.|  
|**Contagem de instâncias de software específico registado em Adicionar / remover programas**|Mostra uma contagem das instâncias dos pacotes de software especificados instalados e registados em Adicionar/Remover Programas ou em Programas e Funcionalidades.|  
|**Instalações de aplicações do Windows especificadas**|Este relatório mostra uma lista de todos os computadores com uma aplicação especificada do Windows|  
|**Produtos num computador específico**|Mostra um resumo dos produtos de software inventariados e os seus fabricantes num computador especificado.|  
|**Software registado em Adicionar/remover programas num computador específico**|Mostra um resumo do software instalado num computador especificado que esteja registado em Adicionar/Remover Programas ou em Programas e Funcionalidades.|  
|**Aplicações do Windows instaladas para o utilizador especificado**|Mostra todas as aplicações do Windows instaladas para o utilizador especificado|  

### <a name="software---files"></a>Software - Ficheiros  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os ficheiros inventariados para um produto específico**|Mostra um resumo dos ficheiros inventariados associados a um produto de software especificado.|  
|**Todos os ficheiros inventariados num computador específico**|Mostra um resumo de todos os ficheiros inventariados num computador especificado.|  
|**Comparar inventário de software em dois computadores**|Mostra as diferenças entre os inventários de software reportados em dois computadores especificados.|  
|**Computadores com um ficheiro específico**|Mostra uma lista de computadores que recolheram o inventário de software de um nome de ficheiro especificado. Um computador pode aparecer mais do que uma vez na lista se tiver várias cópias do ficheiro.|  
|**Contagem de computadores com um nome de ficheiro específico**|Mostra o número de computadores que recolheram o inventário de software de um ficheiro especificado.|  

### <a name="software-distribution---application-monitoring"></a>Distribuição de software - monitorização de aplicações  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as implementações de aplicações (avançadas)**|Mostra informações de resumo detalhadas de todas as implementações de aplicações.|  
|**Todas as implementações de aplicações (básico)**|Mostra as informações de resumo de todas as implementações de aplicações.|  
|**Compatibilidade de aplicações**|Mostra as informações de compatibilidade da aplicação especificada na coleção especificada.|  
|**Implementações de aplicações por ativo**|Mostra as aplicações implementadas num dispositivo ou utilizador especificado.|  
|**Erros de infra-estrutura de aplicações**|Mostra os erros da infraestrutura da aplicação.  Podem incluir erros da infraestrutura interna, assim como erros que resultem de regras de requisitos inválidas.|  
|**Estado detalhado da utilização de aplicações**|Mostra os detalhes de utilização das aplicações instaladas.|  
|**Estado de resumo de utilização de aplicação**|Mostra um resumo da utilização das aplicações instaladas.|  
|**Implementações de sequência de tarefas que contêm aplicação**|Mostra as implementações de sequência de tarefas que instalam uma aplicação especificada.|  
|**Pedidos de utilizador para uma aplicação Android**|Mostra os utilizadores que pediram para instalar uma aplicação Android.|  
|**aplicações iOS com implementações falhadas (aplicação já instalada)**|Mostra informações de compatibilidade para a aplicação iOS selecionada que implementou como "Pacote de aplicação para iOS da App Store" que estava associada a uma política de gestão de aplicações móveis. Este relatório é utilizado para apresentar os utilizadores e dispositivos em relação aos quais não foi possível instalar a aplicação, porque tinha já foi instalada manualmente pelo utilizador.|  

### <a name="software-distribution---collections"></a>Distribuição de Software - Coleções  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as coleções**|Mostra todas as coleções na hierarquia.|  
|**Todos os recursos numa coleção específica**|Mostra todos os recursos numa coleção especificada.|  
|**Janelas de manutenção disponíveis para um cliente especificado**|Mostra todas as janelas de manutenção aplicáveis ao cliente especificado.|  

### <a name="software-distribution---content"></a>Distribuição de Software - Conteúdos  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as distribuições de conteúdo ativas**|Mostra todos os pontos de distribuição nos quais estão a ser atualmente instalados ou removidos conteúdos.|  
|**Todo o conteúdo**|Mostra todas as aplicações e pacotes num site.|  
|**Todo o conteúdo no ponto de distribuição específico**|Mostra todos os conteúdos atualmente instalados no ponto de distribuição especificado.|  
|**Todos os pontos de distribuição**|Mostra informações sobre os pontos de distribuição de cada site.|  
|**Todas as mensagens de estado para um pacote específico num ponto de distribuição específico**|Mostra todas as mensagens de estado de um pacote especificado num ponto de distribuição especificado.|  
|**Estado de distribuição de conteúdo da aplicação**|Mostra informações sobre o estado de distribuição dos conteúdos da aplicação.|  
|**Aplicações direcionadas para o grupo de pontos de distribuição**|Mostra informações sobre os conteúdos da aplicação implementada num grupo de pontos de distribuição especificado.|  
|**Grupo de pontos de aplicações que são sincronizadas num distribuição especificado**|Mostra as aplicações nas quais os ficheiros de conteúdos associados não foram atualizados com a versão mais recente num grupo de pontos de distribuição específico.|  
|**Grupo de pontos de distribuição**|Mostra informações sobre um grupo de pontos de distribuição especificado.|  
|**Resumo de utilização de ponto de distribuição**|Mostra o resumo da utilização do ponto de distribuição para cada ponto de distribuição.|  
|**Estado de distribuição do pacote especificado**|Mostra o estado da distribuição dos conteúdos do pacote especificado em cada ponto de distribuição.|  
|**Pacotes direcionados para o grupo de pontos de distribuição**|Mostra informações sobre os pacotes que visam um grupo de pontos de distribuição especificado.|  
|**Grupo de pontos de pacotes que são sincronizadas num distribuição especificado**|Mostra os pacotes nos quais os ficheiros de conteúdos associados não foram atualizados com a versão mais recente num grupo de pontos de distribuição específico.|  

### <a name="software-distribution---package-and-program-deployment"></a>Distribuição de software - pacote de implementação e do programa  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as implementações de um pacote e programa especificados**|Mostra informações sobre todas as implementações de um pacote e programa especificados.|  
|**Todas as implementações de pacote e programa**|Mostra todas as implementações de pacotes e programas neste site.|  
|**Todas as implementações de pacotes e programas numa coleção especificada**|Mostra todas as implementações de pacotes e programas de uma coleção especificada.|  
|**Todas as implementações de pacote e programa num computador especificado**|Mostra todas as implementações de pacotes e programas aplicáveis a um computador especificado.|  
|**Todas as implementações de pacote e programa num utilizador especificado**|Mostra todas as implementações de pacotes e programas de um utilizador especificado.|  

### <a name="software-distribution---package-and-program-deployment-status"></a>Distribuição de software - estado de implementação de programa e pacote  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os recursos pacote e programa implementações do sistema com o Estado**|Mostra as implementações dos pacotes e programas no site com o estado de resumo de cada implementação.|  
|**Todos os recursos de sistema para uma implementação de pacote e programa especificada num estado especificado**|Mostra uma lista de recursos num estado especificado para uma implementação de pacote e programa especificada.|  
|**Gráfico - Estado horário pacote e programa conclusão da implementação**|Mostra a percentagem de computadores nos quais o pacote foi instalado com êxito, de hora em hora desde que a implementação do pacote e programa foi criada. Pode ser utilizado para monitorizar o tempo médio de implementação de um pacote e programa.|  
|**Estado de implementação de pacote e programa para um cliente e implementação especificados**|Mostra as mensagens de estado reportadas para um computador e implementação de pacote e programa especificados.|  
|**Estado de uma implementação de pacote e programa especificada**|Mostra o estado de resumo de uma implementação do pacote e programa especificada.|  

### <a name="software-metering"></a>Medição de Software  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as regras aplicadas a este site de medição de software**|Mostra uma lista de todas as regras de medição de software no site.|  
|**Computadores que têm um programa medido instalado mas que não o executaram desde uma data especificada**|Mostra todos os computadores que têm uma aplicação medida especificada instalada conforme reportados pelo inventário de software,  mas que não a executaram desde uma data especificada.|  
|**Computadores que executaram um programa de software medido específico**|Mostra uma lista de computadores que executaram programas correspondentes à regra de medição do software selecionada no mês e ano especificados.|  
|**Utilização em simultâneo de todos os programas de software medido**|Mostra o número máximo de utilizadores que executaram simultaneamente cada programa de software medido no mês e ano especificados.|  
|**Análise de tendências de utilização simultânea de um programa de software medido específico**|Mostra o número máximo de utilizadores que executaram simultaneamente o programa de software medido especificado durante cada mês do ano passado.|  
|**Base de instalação para todos os programas de software medido**|Mostra o número de computadores que têm programas de software medido instalados, como reportado pelo inventário de software. Este relatório precisa que o inventário de software seja recolhido nos computadores medidos.|  
|**Progresso de resumo de medição de software**|Mostra a hora do último processamento de dados de medição resumidos no servidor do site.  Só serão refletidos nos relatórios de medição de software os dados processados antes dessas datas.|  
|**Hora do dia este resumo de utilização de um programa de software medido específico**|Mostra o número médio de utilizações de um programa em particular nos últimos 90 dias apresentadas por hora e dia|  
|**Total de utilizações para todos os programas de software medido**|Mostra o número de utilizadores que executaram programas correspondentes a cada regra de medição do software, localmente ou através de Serviços de Terminal, no mês e ano especificados.|  
|**Total de utilizações para todos os programas de software medido em servidores de Terminal do Windows**|Mostra o número de utilizadores que executaram programas correspondentes a cada regra de medição do software com Serviços de Terminal no mês e ano especificados.|  
|**Análise de tendências de utilização total para um programa de software medido específico**|Mostra o número de utilizadores que executaram programas correspondentes a cada regra de medição do software, localmente ou através de Serviços de Terminal, durante cada mês do ano passado.|  
|**Análise de tendências de utilização total para um programa de software medido específico nos servidores de Terminal do Windows**|Mostra o número de utilizadores que executaram programas correspondentes a cada regra de medição do software com Serviços de Terminal durante cada mês do ano passado.|  
|**Utilizadores que executaram um programa de software medido específico**|Mostra uma lista de utilizadores que executaram programas correspondentes à regra de medição do software selecionada no mês e ano especificados.|  

### <a name="software-updates---a-compliance"></a>Atualizações de software - conformidade  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Conformidade 1 - conformidade geral**|Mostra os dados gerais de conformidade para um grupo de atualização de software.|  
|**Conformidade 2 - atualização de software específica**|Mostra os dados de conformidade de uma atualização de software especificada.|  
|**Conformidade 3 - grupo de atualização (por atualização)**|Mostra os dados de conformidade das atualizações de software definidas num grupo de atualização de software.|  
|**Conformidade 4 - atualizações por fabricante mês ano**|Mostra os dados de conformidade das atualizações de software disponibilizadas por um fornecedor durante um mês e ano especificados.|  
|**Conformidade 5 - computador específico**|Este relatório devolve os dados de conformidade da atualização de software de um computador especificado.  Para limitar a quantidade de informações devolvidas, pode especificar a classificação do fabricante e da atualização de software.|  
|**Conformidade 6 - Estados da atualização de software específica (secundário)**|Mostra a contagem e a percentagem de computadores em cada estado de conformidade para a atualização de software especificada.|  
|**Conformidade 7 - computadores num Estado de conformidade específico para um grupo de atualização (secundário)**|Mostra todos os computadores numa coleção com um estado de conformidade geral especificado relativamente a um grupo de atualização de software.|  
|**Conformidade 8 - computadores em conformidade específico estado para uma atualização (secundário)**|Mostra todos os computadores numa coleção com um estado de conformidade especificado de uma atualização de software.|  

### <a name="software-updates---b-deployment-management"></a>Atualizações de software - B gestão de implementação  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Gestão 1 - implementações de um grupo de atualização**|Mostra as implementações que contêm todas as atualizações de software definidas num grupo de atualização de software especificado.|  
|**Gestão 2 - atualizações necessárias mas não implementadas**|Mostra todas as atualizações de software de um fabricante específico que foram detetadas nos clientes, como necessário, mas que não foram implementadas numa coleção específica.|  
|**Gestão 3 - atualizações numa implementação**|Mostra as atualizações de software que estão contidas numa implementação especificada.|  
|**Gestão 4 - implementações direcionadas para uma coleção**|Mostra todas as implementações de atualização de software que visam uma coleção especificada.|  
|**Gestão 5 - implementações direcionadas para um computador**|Mostra todas as implementações de atualização de software que estão implementadas num computador especificado.|  
|**Gestão 6 - implementações que contêm uma atualização específica**|Mostra todas as implementações que contêm uma atualização de software especificada, assim como a coleção de destino associada à implementação.|  
|**Gestão 7 - atualizações numa implementação com conteúdos em falta**|Mostra as atualizações de software numa implementação especificada que não contêm todo o conteúdo associado obtido, impedindo os clientes de instalarem a atualização e de atingirem a total conformidade da implementação.|  
|**Gestão 8 - computadores com conteúdos em falta (secundário)**|Mostra todos os computadores que precisam de uma atualização de software especificada contida numa implementação especificada que não está aprovisionada num ponto de distribuição.|  

### <a name="software-updates---c-deployment-states"></a>Atualizações de software - C Estados de implementação  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Estados 1 - Estados de imposição para uma implementação**|Mostra os estados de imposição de uma implementações de atualização de software, que é tipicamente a segunda fase de uma avaliação da implementação.|  
|**Estados 2 - Estados de avaliação para uma implementação**|Mostra o estado de avaliação de uma implementação de atualização de software específica, que é tipicamente a primeira fase de uma avaliação da implementação.|  
|**Estados 3 - Estados para uma implementação e de computador**|Mostra os estados de todas as atualizações de software na implementação especificada de um computador especificado.|  
|**Estados 4 - computadores num estado específico de uma implementação (secundário)**|Mostra todos os computadores num estado especificado de uma implementação de atualização de software.|  
|**Estados 5 - Estados para uma atualização numa implementação (secundário)**|Mostra um resumo dos estados de uma atualização de software especificada visada por uma implementação especificada.|  
|**Estados 6 - computadores num Estado de imposição específico para uma atualização (secundário)**|Mostra todos os computadores num estado de imposição especificado de uma atualização de software especificada.|  

### <a name="software-updates---d-scan"></a>Atualizações de software - D análise  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Análise 1 - Estados da última análise por coleção**|Mostra a contagem de computadores numa coleção especificada em cada estado de análise de conformidade devolvido por clientes durante a última análise de conformidade.|  
|**Análise 2 - Estados da última análise por site**|Mostra a contagem de computadores num site especificado em cada estado de análise de conformidade devolvido por clientes durante a última análise de conformidade.|  
|**Análise 3 - clientes de uma coleção a relatar um estado específico (secundário)**|Mostra todos os computadores de uma coleção especificada e um estado de análise da conformidade especificado durante a última análise de compatibilidade.|  
|**Análise 4 - clientes de um site a relatar um estado específico (secundário)**|Mostra todos os computadores de um site especificado e um estado de análise da conformidade especificado durante a última análise de compatibilidade.|  

### <a name="software-updates---e-troubleshooting"></a>Atualizações de software - E resolução de problemas  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**1 de resolução de problemas - erros de análise**|Mostra os erros de análise no site e uma contagem dos computadores com cada erro.|  
|**2 de resolução de problemas - erros de implementação**|Mostra os erros de implementação no site e uma contagem dos computadores com cada erro.|  
|**Resolução de problemas 3 - computadores em falha com um erro de análise específico (secundário)**|Mostra uma lista dos computadores cuja análise falhou devido a um erro especificado.|  
|**Resolução de problemas 4 - computadores em falha com um erro de implementação específico (secundário)**|Mostra uma lista dos computadores nos quais a implementação da atualização está a falhar devido a um erro especificado.|  

### <a name="state-migration"></a>Migração de Estado  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Informações de migração de estado para um computador de origem específico**|Mostra informações de migração de estado de um computador de origem especificado.|  
|**Informações de migração de estado para um ponto de migração de estado específico**|Mostra informações de migração de estado de um ponto de migração de estado especificado.|  
|**Pontos de migração de estado para um site específico**|Mostra os pontos de migração de estado de um site específico|  

### <a name="status-messages"></a>Mensagens de Estado  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as mensagens para um ID de mensagem específico**|Mostra uma lista de mensagens de estado com um ID de mensagem especificado.|  
|**Clientes que relataram erros nas últimas 12 horas para um site específico**|Mostra uma lista de computadores e componentes que reportaram erros nas últimas 12 horas e o número de erros reportados.|  
|**Mensagens de componente durante as últimas 12 horas**|Mostra uma lista de mensagens de componente nas últimas 12 horas para um código de site, computador e componente específicos.|  
|**Mensagens de componente de última hora**|Mostra uma lista de mensagens de estado criadas na última hora por um componente especificado num computador especificado, num site do Configuration Manager especificado.|  
|**Contagem de mensagens de componente de última hora para um site específico**|Mostra o número de mensagens de estado por componente e gravidade reportadas na última hora num site especificado.|  
|**Contagem de erros nas últimas 12 horas**|Mostra o número de mensagens de estado de erro do componente de servidor nas últimas 12 horas.|  
|**Erros fatais (por componente)**|Mostra uma lista de computadores que reportaram erros fatais por componente.|  
|**Erros fatais (por nome de computador)**|Mostra uma lista de computadores que reportaram erros fatais por nome do computador.|  
|**1000 últimas mensagens para um computador específico (erros e avisos)**|Mostra um resumo das últimas 1 000 mensagens de estado de erro e aviso do componente num computador especificado.|  
|**1000 últimas mensagens para um computador específico (erros avisos e informação)**|Mostra um resumo das últimas 1 000 mensagens de estado de erro, aviso e informativas do componente num computador especificado.|  
|**1000 últimas mensagens para um computador específico (erros)**|Mostra um resumo das últimas 1 000 mensagens de estado de erro de servidor do componente num computador especificado.|  
|**1000 últimas mensagens para um componente de servidor específico**|Mostra um resumo das 1 000 mensagens de estado mais recentes de um componente de servidor especificado.|  

### <a name="status-messages---audit"></a>Mensagens de Estado - Auditoria  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todas as mensagens de auditoria para um utilizador específico**|Mostra um resumo de todas as mensagens de estado de auditoria para um utilizador especificado. Mensagens de auditoria descrevem ações tomadas na consola do Configuration Manager que adicionar, modificar ou eliminam objetos no Configuration Manager.|  
|**Controlo remoto - todos os computadores controlados remotamente por um utilizador específico**|Mostra um resumo das mensagens de estado a indicar o controlo remoto dos computadores cliente por um utilizador especificado.|  
|**Controlo remoto - todas as informações de controlo remoto**|Mostra um resumo das mensagens de estado relacionadas com o controlo remoto dos computadores cliente.|  

### <a name="task-sequence---deployment-status"></a>Sequência de tarefas - estado da implementação  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os recursos de sistema para uma implementação de sequência de tarefas num estado específico**|Mostra uma lista de computadores de destino para a implementação da sequência de tarefas especificada num estado de implementação especificado.|  
|**Todos os recursos de sistema para uma implementação de sequência de tarefas que se encontra num estado específico e que está disponível para computadores desconhecidos**|Mostra uma lista de computadores de destino para a implementação da sequência de tarefas especificada que está no estado de implementação especificado.|  
|**Contagem de recursos do sistema com implementações de sequência de tarefas atribuídas mas não executadas**|Mostra o número de computadores que aceitaram sequências de tarefas, mas que não executaram a sequência de tarefas.|  
|**Histórico de uma implementação de sequência de tarefas num computador**|Mostra o estado de cada passo da implementação da sequência de tarefas especificada no computador de destino especificado. Se não for devolvido nenhum valor, a sequência de tarefas não foi iniciada no computador.|  
|**Lista de computadores que excederam um limite de tempo para executar uma implementação de sequência de tarefas específico**|Mostra a lista de computadores de destino que excederam o limite de tempo especificado para a execução de uma sequência de tarefas.|  
|**Tempo de execução de uma implementação de sequência de tarefas específica num computador de destino específico**|Mostra o tempo total que uma sequência de tarefas especificada num computador especificado levou a ser concluída com êxito.|  
|**Tempo de execução de cada passo da implementação de sequência de tarefas num computador de destino específico**|Mostra o tempo que cada passo da implementação da sequência de tarefas especificada levou a ser concluído no computador de destino especificado.|  
|**Estado de uma implementação de sequência de tarefas específica para um computador específico**|Mostra o resumo do estado de uma implementação de sequência de tarefas especificada num computador especificado.|  
|**Estado de uma implementação de sequência de tarefas no computador de destino desconhecido**|Mostra o estado da implementação da sequência de tarefas especificada no computador de destino desconhecido especificado.|  
|**Resumo do Estado de uma implementação de sequência de tarefas específica**|Mostra um resumo do estado de todos os recursos que foram visados por uma implementação.|  
|**Resumo do Estado de uma implementação de sequência de tarefas disponível para computadores desconhecidos**|Mostra o resumo do estado de todos os recursos que foram visados por uma implementação especificada que está disponível numa coleção que contém computadores desconhecidos.|  

### <a name="task-sequence---deployments"></a>Sequência de Tarefas - Implementações  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os recursos do sistema num grupo ou fase específicos de uma implementação de sequência de tarefas específica**|Mostra uma lista de computadores que estão atualmente a ser executados num grupo ou fase especificado de uma implementação de sequência de tarefas especificada.|  
|**Todos os recursos de sistema onde uma implementação de sequência de tarefas falha dentro de um grupo ou fase específicos**|Mostra uma lista de computadores nos quais ocorreu um erro no grupo/fase especificada da implementação da sequência de tarefas especificada.|  
|**Todas as implementações de sequência de tarefas**|Mostra detalhes de todas as implementações de sequência de tarefas iniciadas a partir do site atual.|  
|**Todas as implementações disponíveis para computadores desconhecidos da sequência de tarefas**|Mostra detalhes de todas as implementações de sequência de tarefas iniciadas a partir do site e que estão implementadas em coleções de sites que contêm computadores desconhecidos.|  
|**Contagem de falhas em cada fase ou grupo da sequência de tarefas específica**|Mostra o número de falhas em cada fase ou grupo da sequência de tarefas especificada.|  
|**Contagem de falhas em cada fase ou grupo de uma implementação de sequência de tarefas específica**|Mostra o número de falhas em cada fase ou grupo da implementação de sequência de tarefas especificada.|  
|**Estado de implementação de todas as implementações de sequência de tarefas**|Mostra o progresso geral de todas as implementações de sequência de tarefas.|  
|**Progresso da sequência de tarefas em execução**|Mostra o progresso da sequência de tarefas especificada.|  
|**Progresso de uma implementação de sequência de tarefas em execução**|Mostra as informações de resumo da implementação da sequência de tarefas especificada.|  
|**Progresso de todas as implementações de sequência de tarefas específica**|Mostra o progresso de todas as implementações de sequência de tarefas especificada.|  
|**Relatório de resumo para uma implementação de sequência de tarefas**|Mostra as informações de resumo da implementação da sequência de tarefas especificada.|  

### <a name="task-sequence---progress"></a>Sequência de Tarefas - Progresso  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Gráfico - progresso semanal da sequência de tarefas**|Mostra o progresso semanal de uma sequência de tarefas iniciado na data de implementação.|  
|**Progresso de uma sequência de tarefas**|Mostra o progresso da sequência de tarefas especificada.|  
|**Progresso de todas as sequências de tarefas**|Mostra um resumo do progresso de todas as sequências de tarefas.|  
|**Progresso de sequências de tarefas para implementações do sistema operativo**|Mostra o progresso de todas as sequências de tarefas que implementam sistemas operativos.|  
|**Estado de todos os computadores desconhecidos**|Mostra uma lista de computadores desconhecidos no momento da execução de uma implementação de sequência de tarefas e se os computadores são conhecidos.|  

### <a name="task-sequences---references"></a>Sequências de Tarefas - Referências  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Conteúdo referenciado por uma sequência de tarefas específica**|Mostra os conteúdos referenciados por uma sequência de tarefas especificada.|  

### <a name="upgrade-assessment"></a>Avaliação da Atualização  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Estado da aplicação para um computador específico**|Mostra a compatibilidade das aplicações instaladas no sistema operativo específico de um computador.|  
|**Estado da aplicação para computadores numa coleção específica**|Mostra o estado geral dos computadores numa coleção para que os possa analisar para atualizar para um determinado sistema operativo com base nas aplicações de cada computador. Utilize este relatório para determinar quais os computadores que têm aplicações compatíveis antes de implementar um sistema operativo.|  
|**Resumo do Estado da aplicação**|Mostra um resumo do estado da aplicação num sistema operativo especificado. Utilize este relatório para determinar a compatibilidade das aplicações antes de implementar um sistema operativo.|  
|**Computadores com uma aplicação específica instalada**|Mostra os computadores com uma aplicação especificada instalada.|  
|**Computadores com um dispositivo de hardware específico**|Mostra os computadores que têm um dispositivo de hardware específico.|  
|**Estado do dispositivo de hardware para um computador específico**|Mostra o estado da compatibilidade dos dispositivos de hardware num sistema operativo especificado localizados num computador especificado.|  
|**Estado do dispositivo de hardware para computadores numa coleção específica**|Mostra o estado geral dos dispositivos de hardware de um sistema operativo específico em computadores de uma coleção específica. Utilize este relatório para determinar a compatibilidade do hardware antes de implementar um sistema operativo.|  
|**Estado do dispositivo de hardware resumo**|Mostra um resumo do estado do dispositivo de hardware num sistema operativo especificado. Pode utilizar este relatório para determinar a compatibilidade do dispositivo de hardware antes de implementar um sistema operativo.|  
|**Requisitos de hardware do sistema operativo**|Mostra os critérios de hardware mínimos e recomendados para os sistemas operativos.|  
|**Estado do requisito do sistema operativo para computadores numa coleção específica**|Mostra o estado dos requisitos do sistema operativo para o sistema operativo selecionado para computadores de uma coleção especificada. Utilize este relatório para determinar se um computador cumpre os requisitos especificados do sistema operativo relativamente à velocidade do processador da CPU, dimensão da memória e espaço no disco rígido.|  
|**Resumo da avaliação da atualização**|Mostra o resumo da avaliação da atualização. Pode utilizar este relatório para avaliar o estado geral da compatibilidade da atualização.|  

### <a name="user---device-affinity"></a>Utilizador - afinidade de dispositivo  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Associações de afinidade de dispositivo do utilizador pendentes por coleção**|Este relatório mostra todas as atribuições de afinidade dispositivo/utilizador pendentes, com base nos dados de utilização, para membros de uma coleção.|  
|**Associações de afinidade de dispositivo do utilizador por coleção**|Mostra todas as associações de afinidade dispositivo/utilizador da coleção especificada e agrupa os resultados por tipo de coleção (por exemplo, por utilizador ou dispositivo).|  

### <a name="user-data-and-profiles-health"></a>Dados do Utilizador e Estado de Funcionamento dos Perfis  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório de estado de funcionamento de redirecionamento de pasta - detalhes**|Mostra os detalhes do estado de funcionamento do redirecionamento da pasta por cada uma das pastas redirecionadas por determinado utilizador.|  
|**Roaming de relatório de estado de funcionamento de perfis de utilizador - detalhes**|Mostra os detalhes do estado de funcionamento do relatório de funcionamento de perfil de utilizador itinerante de um utilizador especificado.|  
|**Relatório de estado de funcionamento de perfis e dados do utilizador - detalhes**|Mostra os detalhes de erro ou de aviso para o redirecionamento de pastas ou o perfil de utilizador itinerante ao aprofundar o nível de detalhe na contagem do relatório de resumo.|  
|**Relatório de estado de funcionamento de perfis - resumo e os dados de utilizador**|Mostra o resumo dos estados de funcionamento do redirecionamento de pastas e perfis de utilizador itinerante.|  

### <a name="users"></a>Utilizadores  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Computadores para um nome de utilizador específico**|Mostra uma lista dos computadores que foram utilizados por um utilizador especificado.|  
|**Contagem de utilizadores por domínio**|Mostra o número de utilizadores em cada domínio.|  
|**Utilizadores num domínio específico**|Mostra uma lista de utilizadores e os respetivos computadores num domínio especificado.|  

### <a name="virtual-applications"></a>Aplicações Virtuais  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Resultados do ambiente Virtual de App-V**|Mostra informações sobre um ambiente virtual especificado que está num estado especificado para uma coleção especificada.|  
|**Resultados do ambiente Virtual App-V para ativo**|Mostra informações sobre um ambiente virtual especificado para um recurso especificado e qualquer tipo de implementação para o ambiente virtual especificado.|  
|**Estado do ambiente Virtual de App-V**|Mostra informações de compatibilidade num ambiente virtual especificado para uma coleção especificada.|  
|**Computadores com uma aplicação virtual específica**|Mostra um resumo dos computadores com o atalho da aplicação App-V especificada, criado com o Application Virtualization Management Sequencer.|  
|**Computadores com um pacote de aplicação virtual específica**|Mostra um resumo dos computadores com o pacote da aplicação App-V especificada.|  
|**Contagem de todas as instâncias de pacotes de aplicações virtuais**|Mostra uma contagem dos pacotes de aplicações App-V detetados.|  
|**Contagem de todas as instâncias de aplicações virtuais**|Mostra uma contagem das aplicações App-V detetadas.|  

### <a name="wake-on-lan"></a>Reativação Por LAN  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Todos os computadores visados para atividade de reativação por LAN**|Mostra uma lista dos computadores visados para atividade de Reativação por LAN durante uma implementação com tipo especificado por si.|  
|**Todos os objetos pendentes de atividade de reativação**|Mostra os objetos agendados para reativação.|  
|**Todos os sites com capacidade para reativação por LAN**|Mostra uma lista de todos os sites na hierarquia com capacidade para Reativação por LAN.|  
|**Erros recebidos durante o envio de pacotes de reativação durante um período de tempo definido**|Mostra os erros recebidos durante o envio de pacotes de reativação para computadores durante um período de tempo definido|  
|**Histórico da atividade de reativação por LAN**|Mostra um histórico da atividade de reativação ocorrida desde um determinado período.|  
|**Detalhes do Estado de implementação do Proxy de reativação**|Mostra informações sobre o estado de implementação do Proxy de Reativação de cada dispositivo de uma coleção especificada.|  
|**Resumo do Estado de implementação do Proxy de reativação**|Mostra um resumo do estado de implementação do Proxy de Reativação numa coleção especificada.|  
