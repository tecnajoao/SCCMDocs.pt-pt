---
title: "Introdução do Asset Intelligence | Documentos do Microsoft"
description: "Obter uma introdução Asset intelligence no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
caps.latest.revision: 7
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: 879dc3f04f361af955afbc4db180d097073e8d41
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-asset-intelligence-in-system-center-configuration-manager"></a>Introdução Asset intelligence no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Asset Intelligence no System Center Configuration Manager permite-lhe inventariar e gerir a utilização de licenças de software em toda a empresa utilizando o catálogo de Asset Intelligence. Muitas classes do Windows Management Instrumentation (WMI) de inventário de hardware melhoram o volume de informações que são recolhidas sobre títulos de hardware e software que estão a ser utilizados. Mais de 60 relatórios apresentam estas informações num formato de fácil utilização. Muitos destes relatórios incluem uma ligação para relatórios mais específicos, nos quais pode consultar informações gerais e desagregar para obter informações mais detalhadas. No entanto, pode adicionar informações personalizadas ao catálogo do Asset Intelligence, tais como categorias de software personalizadas, famílias de software, etiquetas de software e requisitos de hardware. Também pode ligar ao System Center Online para atualizar dinamicamente o catálogo do Asset Intelligence com as informações mais recentes disponíveis. Os clientes Microsoft podem reconciliar a utilização de licenças de software empresarial com licenças de software adquiridas que estão a ser utilizada por importar informações de licença de software para a base de dados do site do Configuration Manager.  

##  <a name="BKMK_AssetIntelligenceCatalog"></a> Catálogo do Asset Intelligence  

 O catálogo do Configuration Manager Asset Intelligence é um conjunto de tabelas de base de dados armazenados na base de dados do site que contêm informações de categorização e identificação para versões e títulos de software 300,000 acima. Estas tabelas de base de dados também são utilizadas para gerir os requisitos de hardware para títulos de software específicos.  

 O catálogo do Asset Intelligence fornece informações de licenças de software para títulos de software que estão a ser utilizados, da Microsoft e de software que não seja da Microsoft. Um conjunto predefinido de requisitos de hardware para títulos de software está disponível no catálogo do Asset Intelligence e poderá criar novas informações de requisitos de hardware definidos pelo utilizador para satisfazer requisitos personalizados. Além disso, pode personalizar informações no catálogo do Asset Intelligence e pode carregar informações sobre títulos de software para o System Center Online para categorização.  

 Atualizações ao catálogo do Asset Intelligence, que contêm software recentemente publicado, estão disponíveis para transferência periodicamente para efetuar atualizações do catálogo em massa. Em alternativa, o catálogo pode ser atualizado dinamicamente utilizando a função de sistema de sites do ponto de sincronização do Asset Intelligence.  

###  <a name="BKMK_SoftwareCategories"></a> Categorias de software  
 As categorias de software do Asset Intelligence são utilizadas para categorizar amplamente títulos de software inventariado e são também utilizadas como agrupamentos de alto nível de famílias de software mais específicas. Por exemplo, uma categoria de software poderá ser empresas de energia e uma família de software dentro dessa categoria de software poderá ser petróleo e gás ou hidroelétrica. Muitas categorias de software estão predefinidas no catálogo do Asset Intelligence e é possível criar categorias definidas pelo utilizador para definir mais pormenorizadamente o software inventariado. O estado de validação para todas as categorias predefinidas de software é sempre **Validado**, ao passo que o estado das informações de categorias personalizadas de software adicionadas ao catálogo do Asset Intelligence é **Definido pelo Utilizador**. Para obter mais informações sobre como gerir categorias de software, consulte o artigo [configuração de Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  As informações de categorias predefinidas de software que estão armazenadas no catálogo do Asset Intelligence são só de leitura e não podem ser alteradas nem eliminadas. Os utilizadores administrativos podem adicionar, modificar ou eliminar categorias de software definidas pelo utilizador.  

###  <a name="BKMK_SoftwareFamilies"></a> Famílias de software  
 As famílias de software do Asset Intelligence são utilizadas para definir títulos de software inventariado dentro de categorias de software. Muitas famílias de software estão predefinidas no catálogo do Asset Intelligence e é possível criar categorias definidas pelo utilizador para definir mais pormenorizadamente o software inventariado. O estado de validação para todas as famílias predefinidas de software é sempre **Validado**, enquanto que o estado das informações de famílias personalizadas de software adicionadas ao catálogo do Asset Intelligence é **Definido pelo Utilizador**. Para obter mais informações sobre como gerir famílias de software, consulte o artigo [configuração de Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  As informações de famílias de software predefinidas são só de leitura e não podem ser alteradas. Os utilizadores administrativos podem adicionar, modificar ou eliminar famílias de software definidas pelo utilizador.  

###  <a name="BKMK_CustomLabels"></a> Etiquetas de software  
 As etiquetas personalizadas de software do Asset Intelligence permitem criar filtros que poderá utilizar para agrupar títulos de software e visualizá-los através de relatórios do Asset Intelligence. Pode utilizar etiquetas de software para criar grupos definidos pelo utilizador de títulos de software que partilham um atributo comum. Por exemplo, poderia criar uma etiqueta de software denominada Shareware, associar essa etiqueta de software a títulos de shareware inventariados e executar um relatório para apresentar todos os títulos de software com a etiqueta de software Shareware associada. As etiquetas de software não estão predefinidas. O estado de validação para as etiquetas de software é sempre **Definido pelo Utilizador**. Para obter mais informações sobre como gerir etiquetas de software, consulte o artigo [configuração de Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

###  <a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  
 Pode utilizar as informações de requisitos de hardware para verificar se os computadores cumprem os requisitos de hardware para títulos de software antes de terem como destino implementações de software. Pode gerir requisitos de hardware para títulos de software na área de trabalho **Ativos e Compatibilidade** , no nó **Requisitos de Hardware** sob o nó **Asset Intelligence** . Muitos requisitos de hardware estão predefinidos no catálogo do Asset Intelligence e poderá criar novas informações de requisitos de hardware definidos pelo utilizador para satisfazer requisitos personalizados. O estado de validação para todos os requisitos de hardware predefinidos é sempre **Validado**, enquanto que o estado das informações de requisitos de hardware definidos pelo utilizador adicionados ao catálogo do Asset Intelligence é **Definido pelo Utilizador**. Para obter mais informações sobre como gerir os requisitos de hardware, consulte o artigo [configuração de Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Os requisitos de hardware apresentados na consola do Configuration Manager são obtidos a partir do catálogo do Asset Intelligence e não são baseados nas informações de título de software inventariado dos clientes do System Center 2012 Configuration Manager. As informações de requisitos de hardware não são atualizadas como parte do processo de sincronização com o System Center Online. Pode criar requisitos de hardware definidos pelo utilizador para software inventariado, que não tenham requisitos de hardware associados.  

 Por predefinição, as seguintes informações são apresentadas para cada requisito de hardware listado:  

-   **Título de software**: Especifica o título de software associado com os requisitos de hardware.  

-   **Mínimo CPU (MHz)**: Especifica a velocidade mínima do processador, em megahertz (MHz), necessária para o título de software.  

-   **RAM mínima (KB)**: Especifica a RAM mínima, em quilobytes (KB) necessários para o título de software.  

-   **Espaço mínimo em disco (KB)**: Especifica o espaço de disco rígido livre mínimo no artigo BDC, necessária para o título de software.  

-   **Tamanho de disco mínimo (KB)**: Especifica o tamanho mínimo do disco rígido, no artigo BDC, necessária para o título de software.  

-   **Estado de validação**: Especifica o estado de validação para o requisito de hardware.  

 Os requisitos de hardware predefinidos armazenados no catálogo do Asset Intelligence são só de leitura e não podem ser eliminados.  Os utilizadores administrativos podem adicionar, modificar ou eliminar requisitos de hardware definidos pelo utilizador para títulos de software que não estão armazenados no catálogo do Asset Intelligence.  

##  <a name="BKMK_InventoriedSoftwareTitles"></a> Títulos de software inventariado  
 Pode ver informações de títulos de software inventariado na área de trabalho **Ativos e Compatibilidade** , no nó **Software inventariado** , sob o nó **Asset Intelligence** . O agente de cliente de inventário de Hardware recolhe as informações do software inventariado clientes do Configuration Manager com base nos títulos de software que estão armazenados no catálogo do Asset Intelligence.  

> [!WARNING]  
>  O Agente do Cliente de Inventário de Hardware recolhe inventário com base nas classes de relatório de inventário de hardware do Asset Intelligence que ativar. Para obter mais informações sobre como ativar os relatórios de classes, consulte o artigo [configuração de Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Por predefinição, as seguintes informações são apresentadas para cada título de software inventariado:  

-   **Nome**: Especifica o nome do título de software inventariado.  

-   **Fornecedor**: Especifica o nome do fornecedor que desenvolvidos no título de software inventariado.  

-   **Versão**: Especifica a versão de produto do título de software inventariado.  

-   **Categoria**: Especifica a categoria de software que está atualmente atribuída para o título de software inventariado.  

-   **Família**: Especifica a família de software que está atualmente atribuída para o título de software inventariado.  

-   **Label** [**1**, **2**, and **3**]: Especifica as etiquetas personalizadas que estão associadas ao título de software. Os títulos de software inventariado podem ter até três etiquetas personalizadas associadas aos mesmos.  

-   **Contagem**: Especifica o número de clientes do Configuration Manager inventariado têm o título de software.  

-   **Estado**: Especifica o estado de validação para o título de software inventariado.  

> [!NOTE]  
>  Pode alterar as informações de categorização (nome de produto, fornecedor, categoria de software e família de software) para software inventariado apenas no site de nível superior na sua hierarquia. Depois de modificar as informações de categorização para software predefinido, o estado de validação do software é alterado de **Validado** para **Definido pelo Utilizador**.  

##  <a name="AssetIntelligenceSycnronizationPoint"></a> Ponto de Sincronização do Asset Intelligence  
 O ponto de sincronização do Asset Intelligence é uma função de sistema de sites do Configuration Manager utilizada para estabelecer ligação ao System Center Online (utilizando a porta TCP 443) para gerir informações de catálogo do Asset Intelligence dinâmicas atualizações. Esta função de site só pode ser instalada no site de nível superior da hierarquia. É necessário configurar todos os personalização de catálogo do Asset Intelligence utilizando uma consola do Configuration Manager ligada ao site de nível superior. Apesar de todas as atualizações terem de ser configuradas no site de nível superior, as informações do catálogo do Asset Intelligence são replicadas para outros sites na hierarquia. A função de site do ponto de sincronização do Asset Intelligence permite-lhe pedir a sincronização do catálogo a pedido com o System Center Online ou agendar a sincronização automática do catálogo. Para além de transferir novas informações do catálogo do Asset Intelligence, o ponto de sincronização do Asset Intelligence pode carregar informações personalizadas de títulos de software para o System Center Online para categorização. A Microsoft trata todos os títulos de software carregados para o System Center Online para categorização como informações públicas. Por conseguinte, deverá certificar-se de que os títulos de software personalizados não contêm informações confidenciais ou de propriedade.  

> [!NOTE]  
>  Depois de um título de software não categorizado ser submetido, e caso existam, pelo menos, 4 pedidos de categorização de clientes para o mesmo título de software, os investigadores do System Center Online identificam, categorizam e disponibilizam as informações de categorização do título de software para todos os clientes que estejam a utilizar o serviço online. Os títulos de software que representem o maior número de pedidos de categorização recebem prioridade máxima de categorização. É improvável que as aplicações personalizadas de linha de negócio e de software recebam uma categoria e, como melhor prática, o utilizador não deve enviar estes títulos de software à Microsoft para categorização.  

> [!NOTE]  
>  Uma função de sistema de sites do ponto de sincronização do Asset Intelligence é necessário para ligar ao System Center Online. Para obter informações sobre como instalar um ponto de sincronização do Asset Intelligence, consulte o artigo [configuração de Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

##  <a name="BKMK_AssetIntelligenceHomePage"></a> Home page do Asset Intelligence  
 O **Asset Intelligence** nó o **ativos e compatibilidade** área de trabalho é a home page do Asset Intelligence no Configuration Manager. A home page do **Asset Intelligence** apresenta uma vista de dashboard de resumo de informações do catálogo do Asset Intelligence.  

> [!NOTE]  
>  A home page do **Asset Intelligence** não é atualizada automaticamente enquanto está a ser visualizada.  

 A home page do **Asset Intelligence** contém as secções seguintes:  

-   **Sincronização do catálogo**: Fornece informações sobre se o Asset Intelligence está ativado e o estado atual do ponto de sincronização do Asset Intelligence. A secção também fornece o agendamento da sincronização, se a declaração de licença de cliente é importada, quando o estado foi atualizado pela última vez e a hora da próxima atualização agendada, bem como o número de alterações que ocorreram após a instalação do sistema de sites do ponto de sincronização do Asset Intelligence.  

    > [!NOTE]  
    >  A secção de sincronização do catálogo do Asset Intelligence da home page do **Asset Intelligence** só é apresentada se tiver sido instalada uma função de sistema de sites do ponto de sincronização do Asset Intelligence.  

-   **Estado do Software inventariado, localizado**: Fornece a contagem e a percentagem de software inventariado, categorias de software e famílias de software que são identificadas pela Microsoft, identificado por um administrador, pendentes identificação online, ou não identificado e não pendente. As informações apresentadas em formato de tabela mostram a contagem de cada uma e as informações apresentadas no gráfico mostram a percentagem de cada uma.  

##  <a name="BKMK_AssetIntelligenceReports"></a> Relatórios do Asset Intelligence  
 Os relatórios de Asset Intelligence estão localizados na consola do Configuration Manager, no **monitorização** área de trabalho, na pasta do Asset Intelligence no **relatórios** nó. Os relatórios fornecem informações sobre hardware, gestão de licenças e software. Para obter mais informações sobre os relatórios no Configuration Manager, consulte o artigo [Reporting no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  A precisão da quantidade de títulos de software instalados e as informações de licenças apresentadas nos relatórios do Asset Intelligence podem variar em relação ao número real de títulos de software instalados ou de licenças utilizadas no ambiente. Esta variação deve-se às complexas dependências e limitações envolvidas no inventário de informações de licenças de software para títulos de software que estão instalados em ambientes empresariais. Não utilize os relatórios do Asset Intelligence como única fonte para determinar o cumprimento das licenças de software adquiridas.  

###  <a name="BKMK_HardwareReports"></a> Relatórios de hardware do Asset Intelligence  
 Os relatórios de hardware do Asset Intelligence fornecem informações sobre recursos de hardware na organização. Através da utilização de informações de inventário de hardware, tais como velocidade, memória, dispositivos periféricos, entre outras, os relatórios de hardware do Asset Intelligence podem apresentar informações sobre dispositivos USB, sobre o hardware que tem de ser atualizado e até sobre computadores que não estão prontos para uma atualização específica de software.  

> [!NOTE]  
>  Alguns dados de utilizador nos relatórios de hardware do Asset Intelligence são recolhidos a partir do Registo de Eventos de Segurança do Sistema. Para uma melhor exatidão do relatório, recomendamos que desmarque este registo ao reatribuir um computador a um novo utilizador.  

###  <a name="BKMK_LicenseManagementReports"></a> Relatórios de gestão de licenças do Asset Intelligence  
 Os relatórios de gestão de licenças do Asset Intelligence fornecem dados sobre as licenças que estão a ser utilizadas. O relatório de Razão de Licenciamento apresenta uma lista de aplicações Microsoft instaladas num formato congruente com uma Declaração de Licença Microsoft (MLS). Isto proporciona um método prático de correspondência de licenças adquiridas com licenças utilizadas. Outros relatórios de Gestão de Licenças fornecem informações sobre computadores que funcionam como servidores que executam o Key Management Service (KMS) para estatísticas de ativação do sistema operativo.  

> [!IMPORTANT]  
>  Muitos dos relatórios de Gestão de Licenças do Asset Intelligence apresentam informações sobre a função de KMS, um método de administração de licenciamento em volume. Se não tiver sido implementado um servidor KMS, alguns relatórios podem não devolver dados. Para obter mais informações sobre KMS, procure KMS no [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225).  

###  <a name="BKMK_SoftwareReports"></a> Relatórios de software do Asset Intelligence  
 Os relatórios de software do Asset Intelligence fornecem informações sobre famílias de software, categorias e títulos de software específicos que são instalados em computadores na organização. Os relatórios de software apresentam informações sobre objetos de programa auxiliar de browser, software que inicia automaticamente e muito mais. Estes relatórios podem ser utilizados para identificar adware, spyware e outro software maligno, e identificam redundância de software para ajudar a otimizar a compra de software e o suporte.  

###  <a name="BKMK_SoftwareIdTagReports"></a> Relatórios de etiquetas de identificação de software do Asset Intelligence  
 Os relatórios de etiquetas de identificação de software do Asset Intelligence fornecem informações sobre software que contém uma etiqueta de identificação de software compatível com a norma ISO/IEC 19770-2. As etiquetas de identificação de software fornecem informações autoritativas que são utilizadas para identificar o software instalado. Quando ativar o inventário de hardware SMS_SoftwareTag classe, o Configuration Manager recolhe informações sobre o software utilizando os códigos de identificação de software. Os relatórios seguintes fornecem informações sobre o software:  

-   **Software 14A - procurar etiqueta de identificação de software ativado software**: Este relatório fornece a contagem de software instalado com uma etiqueta de identificação de software ativada.  

-   **Software 14B - computadores com etiqueta de identificação de software específica ativada software instalado**: Este relatório lista todos os computadores que têm instalado software com uma etiqueta de identificação de software específica ativada.  

-   **Instalado software 14C - software identificação software ativado por etiqueta num computador específico**: Este relatório lista todos os instalado software com uma etiqueta de identificação de software específica ativada num computador específico.  

###  <a name="BKMK_ReportingLImitations"></a> Limitações de relatórios do Asset Intelligence  
 Os relatórios do Asset Intelligence podem fornecer grandes quantidades de informação sobre títulos de software instalado e licenças de software compradas que estão a ser utilizadas. No entanto, deve não utilizar estas informações como a única origem para determinar o cumprimento das licenças de software compradas.  

####  <a name="BKMK_ExampleDependencies"></a> Exemplos de dependências  
 A exatidão da quantidade apresentada nos relatórios do Asset Intelligence de títulos de software instalado e informações de licenças pode variar em relação às quantidades reais que estão a ser utilizadas. Esta variação é causada pelas complexas dependências envolvidas no inventário de informações de licenças de software para títulos de software em utilização em ambientes empresariais. Os exemplos seguintes mostram as dependências envolvidas no inventário de software instalado na empresa, utilizando o Asset Intelligence, que podem afetar a precisão dos relatórios do Asset Intelligence:  

 **Dependências de inventário de hardware do cliente**  
 Relatórios de software do Asset Intelligence instalado se baseiem em dados que são recolhidos a partir de clientes do Configuration Manager com a extensão de inventário de hardware para ativar a denúncia de Asset Intelligence. Devido a esta dependência de relatórios de inventário de hardware, os relatórios do Asset Intelligence refletirem dados apenas clientes do Configuration Manager que concluir com êxito a processos de inventário de hardware com as classes de relatório WMI do Asset Intelligence necessárias ativadas. Além disso, uma vez que os clientes do Configuration Manager efetuam processos de inventário de hardware, com base numa agenda definida pelo utilizador administrativo, pode ocorrer um atraso nos dados de relatórios que afeta a precisão dos relatórios do Asset Intelligence. Por exemplo, um título de software licenciado inventariado poderá ser desinstalado após o cliente concluir um ciclo de inventário de hardware com êxito. No entanto, o título de software é apresentado como instalado nos relatórios de Asset Intelligence até que seguinte agendada inventário de hardware o cliente ciclo de comunicação.  

 **Dependências de empacotamento de software**  
 Uma vez que os relatórios de Asset Intelligence baseiam-se a dados do título de software instalado que são recolhidos através de processos do inventário de hardware de cliente do padrão do Configuration Manager, alguns dados de título de software podem não ser recolhidos corretamente. Por exemplo, as instalações de software que não estão em conformidade com os processos de instalação padrão ou as instalações de software que foram alteradas antes da instalação podem causar relatórios do Asset Intelligence incorretos.  

####  <a name="BKMK_LegalLimitations"></a> Limitações legais  
 As informações apresentadas nos relatórios do Asset Intelligence estão sujeitas a muitas limitações e as informações apresentadas nos mesmos não representam aconselhamento jurídico, contabilístico ou outro aconselhamento profissional. As informações fornecidas pelos relatórios do Asset Intelligence destinam-se apenas a fins informativos e não devem ser utilizadas como a única fonte de informação para determinar o cumprimento da utilização de licenças de software.  

 Os exemplos seguintes são exemplos de limitações envolvidas no inventário de software instalado e utilização de licenças na empresa, utilizando o Asset Intelligence, que podem afetar a precisão dos relatórios do Asset Intelligence:  

 **Limitações de quantidade de utilização de licenças Microsoft**  
 -   A quantidade de licenças de software Microsoft adquiridas baseia-se nas informações fornecidas pelos administradores e devem ser revistas com muita atenção para garantir que é fornecido o número correto de licenças de software.  

-   A quantidade comunicada de licenças de software Microsoft contém apenas informações sobre licenças de software Microsoft adquiridas através de programas de licenciamento em volume e não reflete as informações relativas a licenças de software adquiridas através de revenda, OEM ou outros canais de venda de licenças de software.  

-   As licenças de software adquiridas nos últimos 45 dias podem não ser incluídas na quantidade de licenças de software Microsoft comunicada devido a prazos e requisitos de comunicação de revendedores de software.  

-   As transferências de licenças de software resultantes de fusões ou aquisições da empresa podem não ser refletidas nas quantidades de licenças de software Microsoft.  

-   Os termos e condições não padrão num contrato de Licenciamento em Volume da Microsoft (MVLS) podem afetar o número de licenças de software comunicadas e, por conseguinte, poderão exigir revisão adicional por um representante da Microsoft.  

 **Limitações de quantidade de títulos de software instalado**  
 Clientes do Configuration Manager deve concluir com êxito o inventário de hardware ciclos para que os relatórios de Asset Intelligence comunicar com precisão a quantidade de títulos de software instalado. Além disso, poderá haver um atraso entre a instalação ou a desinstalação de um título de software licenciado após um ciclo de comunicação de inventário de hardware com êxito, que não se refletirá nos relatórios do Asset Intelligence executados antes de o cliente comunicar o seu próximo inventário de hardware agendado.  

 **Limitações de reconciliação de licenças**  
 As versões a quantidade de títulos de software instalado para a quantidade de licenças de software adquiridas são calculada utilizando uma comparação do número de licenças especificado pelo administrador e a quantidade de instalado títulos de software recolhidos do inventários de hardware do cliente do Configuration Manager com base numa agenda definida pelo administrador. Esta comparação não representa uma conclusão final da Microsoft dos estados de licenciamento. O estado de licenciamento real depende dos direitos de utilização e das licenças de títulos de software específicos concedidos pelos termos de licenciamento.  

##  <a name="BKMK_ValidationStates"></a> Estados de validação do Asset Intelligence  
 Os estados de validação do Asset Intelligence representam a origem e o estado de validação atual das informações do catálogo do Asset Intelligence. A tabela seguinte mostra os estados de validação possíveis do Asset Intelligence e as ações de administrador que podem causá-los.  

|**Estado**|**Definição**|**Ação do administrador**|**Comentário**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Validado**|O item do catálogo foi definido pelos investigadores do System Center Online.|Nenhuma.|O melhor estado.|  
|**Definido pelo Utilizador**|O item do catálogo não foi definido pelos investigadores do System Center Online.|Personalizou as informações do catálogo local.|Este estado é apresentado nos relatórios do Asset Intelligence.|  
|**Pendente**|O item do catálogo não foi definido pelos investigadores do System Center Online, mas o item foi submetido para o System Center Online para categorização.|Pediu a categorização a partir do System Center Online.|O item do catálogo permanece neste estado até os investigadores do System Center Online categorizarem o item e o catálogo do Asset Intelligence ser sincronizado.|  
|**Atualizável**|Um item de catálogo definido pelo utilizador foi categorizado de forma diferente pelo System Center Online durante a sincronização do catálogo subsequente.|Personalizou o catálogo do Asset Intelligence local para categorizar um item como definido pelo utilizador.|Pode utilizar a ação Resolver Conflito para decidir se deve utilizar as novas informações de categorização ou o valor definido pelo utilizador anterior. Para mais informações sobre como resolver conflitos, consulte o artigo [operações para o Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  
|**Não categorizado**|O item do catálogo não foi definido pelos investigadores do System Center Online, o item não foi submetido para o System Center Online para categorização e o administrador não atribuiu um valor de categorização definido pelo utilizador.|Nenhuma.|Peça a categorização ou personalize as informações do catálogo local.<br /><br /> Para mais informações sobre categorização requerente, consulte o artigo [operações para o Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).<br /><br /> Para obter mais informações sobre como alterar a categoria para o título de software, consulte o artigo [operações para o Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  

> [!NOTE]  
>  Os itens do catálogo submetidos para o System Center Online para categorização têm o estado de validação **Pendente** num site de administração central, mas continuam a ser apresentados com o estado de validação **Não Categorizado** nos sites primários subordinados.  

> [!NOTE]  
>  Após a resolução de um conflito de categorização, o item não é validado como estando em conflito novamente, a menos que as atualizações posteriores de categorização introduzam novas informações sobre o item.  

 Para obter exemplos de quando um Estado de validação poderá transição do Estado de um para outro, consulte o artigo [transições de estado de validação de exemplo para o Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md).  
