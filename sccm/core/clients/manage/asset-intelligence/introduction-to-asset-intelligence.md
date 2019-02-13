---
title: Introdução do Asset intelligence
titleSuffix: Configuration Manager
description: Utilize o asset intelligence no Configuration Manager para inventariar e gerir a utilização de licenças de software em toda a empresa.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17cdfdfa90dd53f516f0dde8cd3b1130f05b9a82
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137243"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Introdução ao asset intelligence no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Inventariar e gerir a utilização de licenças de software em toda a empresa ao utilizar o catálogo do asset intelligence. Do Asset intelligence adiciona as classes de inventário de hardware para melhorar a variedade das informações que recolhe do Configuration Manager. Estas informações incluem os títulos de hardware e software utilizados no seu ambiente. Mais de 60 relatórios apresentam estas informações num formato de fácil de usar. Muitos destes relatórios incluem uma ligação para relatórios mais específicos. Consultar informações gerais e desagregar para obter informações mais detalhadas. 

Adicione informações personalizadas ao catálogo do asset intelligence. Por exemplo, categorias de software personalizadas, famílias de software, etiquetas de software e requisitos de hardware. Para atualizar dinamicamente o catálogo do asset intelligence com as informações mais recentes disponíveis, ligue-o para a Cloud da Microsoft. 

Utilize o asset intelligence para o ajudar a reconciliar a utilização de licenças de software empresarial. Importar informações de licença de software para a base de dados do site do Configuration Manager para vê-lo contra a qual software está a ser utilizado.  



## <a name="BKMK_AssetIntelligenceCatalog"></a> Catálogo do Asset intelligence  

O catálogo do asset intelligence é um conjunto de tabelas de base de dados armazenados na base de dados do site. Estas tabelas incluem informações de categorização e identificação de mais de 300.000 versões e títulos de software. Também ajudam a gerir requisitos de hardware para títulos de software específico.  

O Asset intelligence inclui software informações de licença para títulos de software que estão sendo usados, da Microsoft e de software não Microsoft. Um conjunto predefinido de requisitos de hardware para títulos de software está disponível no catálogo do asset intelligence e pode criar novas informações de requisitos de hardware definidos pelo utilizador para satisfazer requisitos personalizados. Também pode personalizar informações no catálogo do asset intelligence e pode carregar informações de títulos de software para a cloud da Microsoft para categorização.  

Atualizações ao catálogo do Asset intelligence que incluem software recentemente publicadas estão disponíveis para transferência periodicamente para efetuar atualizações de catálogo em massa. Ele pode também ser atualizado dinamicamente utilizando o ponto de sincronização do asset intelligence.  


### <a name="BKMK_SoftwareCategories"></a> Categorias de software  

As categorias de software do Asset intelligence são utilizadas para categorizar amplamente títulos de software inventariado e, como agrupamentos de alto nível de famílias de software mais específicas. Por exemplo, uma categoria de software poderá ser empresas de energia e uma família de software dentro dessa categoria de software poderá ser petróleo e gás ou hidroelétrica. Muitas categorias de software estão predefinidas no catálogo do asset intelligence. Pode criar categorias definidas pelo utilizador para definir mais pormenorizadamente o software inventariado. O estado de validação para todas as categorias predefinidas de software é sempre **validado**. Informações de categorias personalizadas de software adicionadas ao catálogo do asset intelligence são **definido pelo utilizador**. 

Para obter mais informações sobre como gerir categorias de software, consulte [configurar o asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

> [!NOTE]  
> Informações de categorias predefinidas de software armazenadas no catálogo do asset intelligence são só de leitura. Não é possível alterar ou eliminá-lo. Os utilizadores administrativos podem adicionar, modificar ou eliminar categorias de software definidas pelo utilizador.  


### <a name="BKMK_SoftwareFamilies"></a> Famílias de software  

As famílias de software do Asset intelligence são utilizadas para definir títulos de software inventariado dentro de categorias de software. Muitas famílias de software estão predefinidas no catálogo do asset intelligence. Pode criar categorias definidas pelo utilizador para definir mais pormenorizadamente o software inventariado. O estado de validação para todas as famílias predefinidas de software é sempre **validado**. Informações de famílias personalizadas de software adicionadas ao catálogo do asset intelligence é **definido pelo utilizador**. 

Para obter mais informações sobre como gerir famílias de software, consulte [configurar o asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

> [!NOTE]  
> Informações de famílias predefinidas de software é só de leitura e não podem ser alteradas. Os utilizadores administrativos podem adicionar, modificar ou eliminar famílias de software definidas pelo utilizador.  


### <a name="BKMK_CustomLabels"></a> Etiquetas de software  

As etiquetas personalizadas de software do Asset intelligence permitem criar filtros para agrupar títulos de software e visualizá-los em relatórios do asset intelligence. Utilize etiquetas de software para criar grupos definidos pelo utilizador de títulos de software que partilham um atributo comum. Por exemplo, poderia criar uma etiqueta de software denominada Shareware, associá-lo a títulos de shareware inventariados e executar um relatório para apresentar todos os títulos de software com essa etiqueta. Não existem não existem etiquetas predefinidas. O estado de validação para as etiquetas de software é sempre **Definido pelo Utilizador**. 

Para obter mais informações sobre como gerir etiquetas de software, consulte [configurar o asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  


### <a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  

Utilize as informações de requisitos de hardware para verificar se os computadores cumprem os requisitos de hardware para títulos de software antes de eles estão como destino para implementações de software. Gerir requisitos de hardware para títulos de software no **ativos e compatibilidade** área de trabalho a **os requisitos de Hardware** no nó os **do Asset Intelligence** nó. 

Muitos requisitos de hardware estão predefinidos no catálogo do asset intelligence. Crie novas informações de requisitos de hardware definidos pelo utilizador para satisfazer requisitos personalizados. O estado de validação para todos os requisitos de hardware predefinidos é sempre **validado**. Informações de requisitos de hardware definidos pelo utilizador adicionados ao catálogo do asset intelligence são **definido pelo utilizador**. 

Para obter mais informações sobre como gerir requisitos de hardware, consulte [configurar o asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

> [!NOTE]  
> Os requisitos de hardware apresentados na consola do Configuration Manager são obtidos a partir do catálogo do asset intelligence. Eles não são baseiam-se a informações de títulos de software inventariado de clientes. 
> 
> Informações de requisitos de hardware não são atualizadas como parte do processo de sincronização com a Microsoft. 
> 
> Pode criar requisitos de hardware definidos pelo utilizador para software inventariado que não tem requisitos de hardware associados.  

Por predefinição, as seguintes informações são apresentadas para cada requisito de hardware listado:  

- **Título de software**: O título de software associado ao requisito de hardware  

- **Velocidade mínima da CPU (MHz)**: A velocidade mínima do processador em megahertz (MHz), necessária para o título de software  

- **Quantidade mínima de RAM (KB)**: A quantidade mínima de RAM em quilobytes (KB), necessária para o título de software  

- **Espaço mínimo em disco (KB)**: O espaço livre mínimo do disco rígido em KB, necessário ao título de software  

- **Tamanho mínimo do disco (KB)**: O tamanho mínimo do disco rígido em KB, necessário ao título de software  

- **Estado de validação**: O estado de validação para o requisito de hardware  

Predefinidos hardware requisitos armazenados no catálogo do asset intelligence são só de leitura e não podem ser eliminados. Os utilizadores administrativos podem adicionar, modificar ou eliminar requisitos de hardware definidos pelo utilizador para títulos de software que não são armazenados no catálogo do asset intelligence.  



## <a name="BKMK_InventoriedSoftwareTitles"></a> Títulos de software inventariado  

Para ver informações de títulos de software inventariado na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho, expanda o **Asset Intelligence** nó e selecione o  **Inventariados Software** nó. O agente de inventário de hardware recolhe as informações de software inventariado de clientes do Configuration Manager com base nos títulos de software armazenados no catálogo do asset intelligence.  

> [!Note]  
> O agente de inventário de hardware recolhe inventário de acordo com o inventário de hardware do asset intelligence classes que permitem a de relatório. Para obter mais informações sobre como ativar o relatório de classes, consulte [configurar o asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

Por predefinição, as seguintes informações são apresentadas para cada título de software inventariado:  

- **Nome**: O nome do título de software inventariado  

- **Fornecedor**: O nome do fornecedor que desenvolveu o título de software inventariado  

- **Versão**: A versão de produto do título de software inventariado  

- **Categoria**: A categoria de software que está atualmente atribuída ao título de software inventariado  

- **Família**: A família de software que está atualmente atribuída ao título de software inventariado  

- **Etiqueta** [**1**, **2**, e **3**]: As etiquetas personalizadas associadas com o título de software. Os títulos de software inventariado podem ter até três etiquetas personalizadas associadas aos mesmos.  

- **Contagem de**: O número de clientes do Configuration Manager que inventariaram o título de software  

- **estado**: O estado de validação para o título de software inventariado  

> [!NOTE]  
> Pode alterar as informações de categorização para software inventariado apenas no site de nível superior na sua hierarquia. Estas informações incluem o nome do produto, fornecedor, categoria de software e família de software. Depois de modificar as informações de categorização para software predefinido, o estado de validação do software é alterado de **Validado** para **Definido pelo Utilizador**.  



## <a name="AssetIntelligenceSycnronizationPoint"></a> Ponto de sincronização do Asset intelligence  

O ponto de sincronização do asset intelligence é uma função de sistema de sites do Configuration Manager. É utilizado para ligar à nuvem da Microsoft na porta TCP 443 para gerir atualizações de informações do catálogo dinâmico. Instale esta função de site apenas no site de nível superior da hierarquia. Configure todos os personalização do catálogo asset intelligence, utilizando uma consola do Configuration Manager ligada ao site de nível superior. 

Embora configurar todas as atualizações no site de nível superior, informações do catálogo são replicadas para outros sites na hierarquia. A função de site permite-lhe pedir a sincronização do catálogo de demanda com a Microsoft, ou agendar sincronização automática do catálogo. Para além de transferir novas informações de catálogo, o ponto de sincronização do asset intelligence pode carregar informações de títulos de software personalizadas para a Microsoft para categorização. A Microsoft trata todos os títulos de software carregados como informações públicas. Certifique-se de que os títulos de software personalizados não incluem informações confidenciais ou proprietárias.  

Depois de submeter um título de software não categorizados, Microsoft não revisá-lo até que haja pelo menos, quatro pedidos de categorização de clientes para o mesmo título de software. Em seguida, os investigadores da Microsoft identificar, categorizarem e disponibilizam informações de categorização de títulos de software para todos os clientes que estão a utilizar o serviço online. Os títulos de software que representem o maior número de pedidos de categorização recebem prioridade máxima de categorização. Personalizadas de software e aplicações de linha de negócio são pouco provável que recebam uma categoria. Não envie estes títulos de software à Microsoft para categorização.  

Um ponto de sincronização do asset intelligence é necessário para ligar à nuvem da Microsoft. Para obter informações sobre como instalar a função, veja [configurar o asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  



## <a name="BKMK_AssetIntelligenceHomePage"></a> Home page do Asset intelligence  

O **Asset Intelligence** nó a **ativos e compatibilidade** área de trabalho é a home page do asset intelligence no Configuration Manager. Esta home page apresenta uma vista de dashboard de resumo para obter informações de catálogo do asset intelligence.  

> [!NOTE]  
> O **Asset Intelligence** home page do não ser atualizada automaticamente enquanto estiver a ver.  

O **Asset Intelligence** página inicial inclui as secções seguintes:  

- **Sincronização do catálogo**: Informações sobre se o asset intelligence está ativado e o estado atual do ponto de sincronização do asset intelligence.  

    > [!NOTE]  
    > A home page apresenta apenas esta secção quando instala um ponto de sincronização do asset intelligence.  

    A secção também fornece as seguintes informações:  

    - Agenda de sincronização  

    - Se importar uma declaração de licença de cliente   

    - Última atualização de estado  

    - O tempo para a próxima atualização agendada  

    - Aponte o número de alterações após a instalação da sincronização do asset intelligence   

- **Estado de Software inventariado**: A contagem e a percentagem de software inventariado, categorias de software e famílias de software que são identificadas pela Microsoft, identificada por um administrador, com identificação online pendente ou não identificadas e não pendentes. As informações apresentadas em formato de tabela mostram a contagem de cada uma e as informações apresentadas no gráfico mostram a percentagem de cada uma.  



## <a name="BKMK_AssetIntelligenceReports"></a> Relatórios do Asset intelligence  

Os relatórios do asset intelligence estão localizados na consola do Configuration Manager, na **monitorização** área de trabalho, na **do Asset intelligence** pasta sob o **relatórios**nó. Os relatórios fornecem informações sobre hardware, gestão de licenças e software. Para obter mais informações sobre os relatórios no Configuration Manager, consulte [relatórios](/sccm/core/servers/manage/reporting).  

> [!NOTE]  
> A precisão da quantidade de títulos de software instalado e informações de licença apresentadas do asset intelligence relatórios podem variar em relação ao número real de títulos de software instalados ou de licenças que são utilizadas no ambiente. Esta variação deve-se às complexas dependências e limitações envolvidas no inventário de informações de licenças de software para títulos de software que estão instalados em ambientes empresariais. Não utilize relatórios do asset intelligence como única fonte para determinar o cumprimento da licença de software adquiridas.  


### <a name="BKMK_HardwareReports"></a> Relatórios de hardware  

Relatórios de hardware do Asset intelligence fornecem informações sobre os recursos de hardware na organização. Ao utilizar as informações de inventário de hardware, tais como velocidade, memória e dispositivos periféricos, relatórios de hardware do asset intelligence podem apresentar informações sobre dispositivos USB, sobre o hardware que tem de ser atualizado e até sobre computadores que não estão preparadas para um específico atualização de software.  

> [!NOTE]  
> Alguns dados de utilizador nos relatórios de hardware do asset intelligence são recolhidos a partir do registo de eventos de segurança do Windows. Para uma melhor exatidão do relatório, desmarque este registo ao reatribuir um computador a um novo utilizador.  


### <a name="BKMK_LicenseManagementReports"></a> Relatórios de gestão de licenças  

Relatórios de gestão de licenças do Asset intelligence fornecem dados sobre as licenças que estão a ser utilizados. O **Ledger de licenciamento** reportar listas instaladas aplicações da Microsoft num formato Congruente com uma declaração de licença da Microsoft (MLS). Este formato fornece um método prático de correspondência de licenças adquirida com licenças utilizadas. Outros relatórios de gestão de licenças fornecem informações sobre computadores que funcionam como servidores que executam o serviço de gestão de chaves (KMS) para estatísticas de ativação do Windows.  

> [!IMPORTANT]  
> Vários dos relatórios de gestão de licenças do asset intelligence apresentam informações sobre a função de KMS, um método de administração do licenciamento por volume. Se ainda não tiver implementado um servidor KMS, alguns relatórios podem não devolver quaisquer dados.  


### <a name="BKMK_SoftwareReports"></a> Relatórios de software  

Relatórios de software do Asset intelligence fornecem informações sobre famílias de software, categorias e títulos de software específicos que estão instalados nos computadores da organização. Os relatórios de software apresentam informações como objetos auxiliares de navegador e de software que inicia automaticamente. Estes relatórios podem ser utilizados para identificar adware, spyware e outro software maligno. Também pode usá-los para identificar a redundância de software para ajudar a simplificar a aquisição de software e suporte.  


### <a name="BKMK_SoftwareIdTagReports"></a> Relatórios de etiquetas de identificação de software  

Relatórios de etiquetas de identificação de software do Asset intelligence fornecem informações sobre software que inclua uma etiqueta de identificação de software em conformidade com ISO/IEC 19770-2. As etiquetas de identificação de software fornecem informações autoritativas utilizadas para identificar o software instalado. Quando ativa a **SMS_SoftwareTag** classe de relatório de inventário de hardware, o Configuration Manager recolhe informações sobre o software com etiquetas de identificação de software. 

Os relatórios seguintes fornecem informações sobre o software:  

- **Software 14A - procurar etiqueta de identificação de software de software ativado**: A contagem do software instalado com uma etiqueta de identificação de software ativada  

- **Software 14B - computadores com etiqueta de identificação de software específico ativada software instalado**: Todos os computadores que têm software instalado com uma etiqueta de identificação de software específico ativada  

- **Software 14C - instalado identificação etiqueta ativada de software num computador específico**: Todo o software instalado com uma etiqueta de identificação de software específico ativada num computador específico  


### <a name="BKMK_ReportingLImitations"></a> Limitações de relatórios  

Relatórios do Asset intelligence podem fornecer grandes quantidades de informações sobre títulos de software instalado e tiver adquirido licenças de software que estão sendo usadas. Não utilize estas informações como a única origem para determinar o cumprimento da licença de software adquirida.  

#### <a name="BKMK_ExampleDependencies"></a> Exemplos de dependências  
A precisão da quantidade apresentada nos relatórios do asset intelligence para instalado títulos de software e informações de licença podem variar de às quantidades reais que atualmente a ser utilizadas. Esta variação é causada pelas complexas dependências envolvidas no inventário de informações de licenças de software para títulos de software em utilização em ambientes empresariais. Os exemplos seguintes mostram as dependências envolvidas no inventário de software instalado na empresa utilizando o asset intelligence, que pode afetar a precisão dos relatórios do asset intelligence:  

- **Dependências de inventário de hardware do cliente**: Relatórios de software do Asset intelligence instalado baseiam-se nos dados recolhidos a partir de clientes do Configuration Manager ao expandir o inventário de hardware para ativar os relatórios do asset intelligence. Devido a esta dependência nos relatórios de inventário de hardware, os relatórios do asset intelligence refletem dados apenas a partir de clientes que concluir com êxito os processos de inventário de hardware com as necessário WMI reporting classes do asset intelligence ativadas. Uma vez que os clientes do Configuration Manager executam processos de inventário de hardware, com base numa agenda definida pelo utilizador administrativo, pode ocorrer um atraso na comunicação que afeta a precisão dos relatórios do asset intelligence de dados. 

    Por exemplo, um título de software licenciado inventariado poderá ser desinstalado após o cliente concluir um ciclo de inventário de hardware com êxito. Relatórios do Asset intelligence apresentam o título de software, como instalado até seguinte inventário de hardware agendado ciclo de comunicação o cliente.  

- **Dependências de empacotamento de software**: Relatórios do Asset intelligence baseiam-se a dados de títulos de software instalado recolhidos através de processos do inventário de hardware de cliente do padrão do Configuration Manager. Alguns dados de títulos de software podem não ser recolhidos corretamente. Exemplos que podem causar relatórios do incorreta asset intelligence:  

    - Instalações de software que não estejam em conformidade com processos de instalação padrão  

    - Instalações de software que foram alteradas antes da instalação   

#### <a name="BKMK_LegalLimitations"></a> Limitações legais  
As informações apresentadas nos relatórios do asset intelligence estão sujeitas a muitas limitações. As informações apresentadas nos mesmos não representam jurídico, contabilístico ou outro aconselhamento profissional. As informações fornecidas pelo relatórios do asset intelligence são apenas para informação. Não utilize como a única fonte de informações para determinar o cumprimento de utilização de licença de software.  

As seguintes limitações são exemplos de como utilizar o asset intelligence, que pode afetar a precisão dos relatórios:  

- **Limitações de quantidade de utilização de licenças Microsoft**:  

    - A quantidade de licenças de software Microsoft adquiridas baseia-se nas informações fornecidas pelos administradores. Reveja atentamente-lo para se certificar de que o número correto de licenças de software é fornecido.  

    - A quantidade comunicada de licenças de software da Microsoft inclui informações apenas sobre licenças de software Microsoft adquiridas por meio de programas de licenciamento em volume. Ele não reflete as informações de licenças de software adquiridas através de revenda, OEM ou outros canais de vendas de licença de software.  

    - As licenças de software adquiridas nos últimos 45 dias podem não ser incluídas na quantidade de licenças de software Microsoft comunicada devido a prazos e requisitos de comunicação de revendedores de software.  

    - As transferências de licenças de software resultantes de fusões ou aquisições da empresa podem não ser refletidas nas quantidades de licenças de software Microsoft.  

    - Nestandardní termos e condições num contrato de licenciamento de Volume da Microsoft (MVLS) podem afetar o número de licenças de software comunicados. Eles podem exigir revisão adicional por um representante da Microsoft.  

- **Limitações de quantidade de títulos de software instalado**: Clientes do Configuration Manager tem de concluir com êxito o inventário de hardware ciclos para os relatórios do asset intelligence comuniquem com precisão a quantidade de títulos de software instalado. Pode haver um atraso entre a instalação ou desinstalação de um título de software licenciado após um ciclo de relatório de inventário de hardware com êxito. Esta ação não pode ser refletida no relatórios do asset intelligence executados antes do cliente comunicar o seu próximo inventário de hardware agendado.  

- **Limitações de reconciliação de licenças**: A reconciliação da quantidade de títulos de software instalado para a quantidade de licenças de software adquirida é calculada mediante a utilização de uma comparação de quantidade de licenças especificada pelo administrador e a quantidade de títulos de software instalado recolhidos a partir de Inventários de hardware do cliente de Configuration Manager com base num agendamento definido pelo administrador. Esta comparação não representa uma conclusão final da Microsoft, Estados de licenciamento. O estado de licenciamento real depende dos direitos de utilização e das licenças de títulos de software específicos concedidos pelos termos de licenciamento.  



## <a name="BKMK_ValidationStates"></a> Estados de validação do Asset intelligence  

Estados de validação do Asset intelligence representam a origem e o estado de validação atual das informações de catálogo do asset intelligence. A tabela seguinte mostra os Estados de validação possíveis do asset intelligence e as ações de administrador que podem causá-los.  

| Estado | Definição | Ação do administrador | Comentário |  
|---------------|--------------------|------------------------------|-----------------|  
|**Validado**|Os investigadores da Microsoft definido o item de catálogo|Nenhum|Melhor estado|  
|**Definido pelo Utilizador**|Os investigadores da Microsoft ainda não tiverem definido o item de catálogo|Personalizar as informações do catálogo local|Este estado é apresentado em relatórios do asset intelligence|  
|**Pendente**|Os investigadores da Microsoft ainda não tiverem definido o item de catálogo, mas tiver submetido o item à Microsoft para categorização|Nenhuma ação adicional depois de pedir a categorização|O item de catálogo permanece neste estado até os investigadores da Microsoft categorizarem o item e sincronizar o catálogo do asset intelligence|  
|**Atualizável**|Um item de catálogo definido pelo utilizador foi categorizado de forma diferente pelo Microsoft durante a sincronização do catálogo.|Utilizar o **resolver conflito** ação para decidir se deve utilizar as novas informações de categorização ou o valor definido pelo utilizador anterior. Para obter mais informações sobre como resolver conflitos, consulte [operações do asset intelligence](/sccm/core/clients/manage/asset-intelligence/operations-for-asset-intelligence).|Depois de resolver um conflito de categorização, o item não é validado como estando em conflito novamente, a menos que atualizações posteriores de categorização introduzam novas informações sobre o item.|  
|**Não categorizado**|O item de catálogo ainda não foi definido pelos investigadores da Microsoft, o item não foi enviado para a Microsoft para categorização e o administrador não tenha atribuído um valor de categorização definidas pelo utilizador.|Peça a categorização ou personalize suas informações do catálogo local. Para obter mais informações, consulte [operações do asset intelligence](/sccm/core/clients/manage/asset-intelligence/operations-for-asset-intelligence).|Nenhum|  

> [!NOTE]  
> Itens de catálogo que enviar à Microsoft para categorização têm o estado de validação **pendente** num site de administração central, mas continuam a ser apresentados com o estado de validação **não categorizado**em sites primários subordinados.  

Para obter exemplos de quando um Estado de validação poderá transitar de um Estado para outro, consulte [transições de estado de validação de exemplo para o asset intelligence](/sccm/core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence).  
