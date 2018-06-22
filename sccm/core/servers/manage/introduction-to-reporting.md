---
title: Introdução aos relatórios
titleSuffix: Configuration Manager
description: Saiba mais sobre o conjunto de ferramentas e recursos disponíveis para que possa gerir relatórios no Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 579e9494a4f44f41a411af88bf58df7dcc5e8075
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340475"
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>Introdução aos relatórios no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Relatórios no System Center Configuration Manager fornecem um conjunto de ferramentas e recursos que ajudam a utilizam as capacidades avançadas de relatórios do SQL Server Reporting Services (SSRS) e a experiência de que o Reporting Services Report Builder fornece de criação avançada. Relatórios ajudam a recolher, organizar e apresentar informações sobre utilizadores, hardware e inventário de software, atualizações de software, aplicações, estado do site e outras operações do Configuration Manager na sua organização. Os relatórios fornecem vários relatórios predefinidos que pode utilizar sem alterações ou modificar para corresponder aos seus requisitos, além de poder criar relatórios personalizados. Utilize as secções seguintes para ajudar a gerir relatórios no Configuration Manager.  

##  <a name="BKMK_SQLServerReportingServices"></a> Serviços de Relatórios do SQL Server  
 O SQL Server Reporting Services fornece um conjunto completo de ferramentas e serviços prontos a utilizar para o ajudar a criar, implementar e gerir relatórios para a sua organização e funcionalidades de programação que lhe permitem expandir e personalizar a funcionalidade dos relatórios. O Reporting Services é uma plataforma de relatórios baseada em servidor que fornece funcionalidade de relatórios completa para diversas origens de dados.  

 O Configuration Manager utiliza o SQL Server Reporting Services como a sua solução de relatórios. A integração com o Reporting Services proporciona as seguintes vantagens:  

-   Utiliza um sistema de relatórios padrão da indústria para consultar a base de dados do Configuration Manager.  

-   Apresenta relatórios utilizando o Visualizador de relatórios do Configuration Manager ou utilizando o Gestor de relatórios, que é uma ligação ao relatório baseada na web.  

-   Fornece desempenho, disponibilidade e escalabilidade elevados.  

-   Fornece subscrições de relatórios que os utilizadores podem subscrever; por exemplo, um gestor pode subscrever para receber automaticamente por correio eletrónico um relatório diário que detalhe o estado da implementação de uma atualização do software.  

-   Exporta relatórios que os utilizadores podem selecionar numa variedade de formatos populares.  

 Para obter mais informações sobre o Reporting Services, veja [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) no SQL Server 2008 Books Online.  

##  <a name="BKMK_ReportingServicesPoint"></a> Ponto do Reporting Services  
 O ponto do Reporting Services é uma função de sistema de sites que é instalada num servidor com o Microsoft SQL Server Reporting Services. O Gestor de configuração de cópias de ponto de relatório definições para o Reporting Services, cria pastas de relatórios com base em categorias de relatórios e define a política de segurança em pastas de relatórios e relatórios com base nas permissões baseadas em funções para os utilizadores administrativos do Configuration Manager do Reporting Services. Num intervalo de 10 minutos, o ponto do Reporting Services liga ao Reporting Services para reaplicar a política de segurança caso tenha sido alterada, por exemplo, utilizando o Gestor de Relatórios. Para mais informações sobre como planear e instalar um ponto do Reporting Services, consulte a seguinte documentação:  

-   [Planeamento de relatórios no System Center Configuration Manager](planning-for-reporting.md)  

-   [Configurar relatórios no System Center Configuration Manager](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Relatórios do Configuration Manager  
 Configuration Manager fornece definições de relatórios para mais de 400 relatórios em mais de 50 pastas de relatórios, que são copiados para a pasta de relatórios raiz no SQL Server Reporting Services durante o processo de instalação de ponto do Reporting Services. Os relatórios são apresentados na consola do Configuration Manager e organizados em subpastas com base na categoria do relatório. Os relatórios não são propagados para cima ou para baixo de hierarquia do Configuration Manager; são executados apenas relativamente a base de dados do site em que são criados. No entanto, porque o Configuration Manager replica dados globais em toda a hierarquia, tem acesso a informações de toda a hierarquia. Quando um relatório obtém dados de uma base de dados de site, tem acesso a dados do site atual e dos sites subordinados e aos dados globais de todos os sites da hierarquia. Como outros objetos do Configuration Manager, um utilizador administrativo tem de ter as permissões adequadas para executar ou modificar relatórios. Para executar um relatório, um utilizador administrativo tem de ter a permissão **Executar Relatório** para o objeto. Para criar ou modificar um relatório, um utilizador administrativo tem de ter a permissão **Modificar Relatório** para o objeto.  

###  <a name="BKMK_CreatingReports"></a> Criar e modificar relatórios  
 O Configuration Manager utiliza o Microsoft SQL Server Report Builder como a exclusiva de criação e edição de ferramenta para relatórios baseados em modelos e baseados em SQL. Quando cria ou edita um relatório na consola do Configuration Manager, é aberto o Report Builder. Para obter mais informações sobre a gestão dos relatórios, veja [Operações e manutenção de relatórios no System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

###  <a name="BKMK_RunningReports"></a> Executar relatórios  
 Quando executar um relatório na consola do Configuration Manager, o Visualizador de relatórios é aberto e estabelece ligação ao Reporting Services. Depois de especificar os parâmetros de relatório necessários, o Reporting Services obtém os dados e apresenta os resultados no visualizador. Também pode ligar ao SQL Services Reporting Services, ligar à origem de dados para o site e executar relatórios.  

###  <a name="BKMK_ReportPrompts"></a> Pedidos de relatório  
 Um pedido de relatório ou parâmetro de relatório no Configuration Manager é uma propriedade de relatório que pode configurar quando um relatório é criado ou modificado. Os pedidos de relatório são criados para limitar ou direcionar os dados que um relatório obtém. Um relatório pode conter mais do que um pedido, desde que os respetivos nomes sejam exclusivos e contenham apenas carateres alfanuméricos em conformidade com as regras do SQL Server para identificadores.  

 Quando executa um relatório, o pedido solicita um valor para um parâmetro necessário e, com base no valor, obtém os dados do relatório. Por exemplo, o relatório **Informações sobre o computador para um computador específico** obtém as informações de um computador específico e solicita ao utilizador administrativo um nome de computador. O Reporting Services passa o valor especificado a uma variável que está definida na instrução SQL para o relatório.  

###  <a name="BKMK_ReportLinks"></a> Ligações de relatórios  
 Ligações de relatórios no Configuration Manager são utilizadas num relatório de origem para fornecer aos utilizadores administrativos acesso fácil a dados adicionais, tais como informações mais detalhadas sobre cada um dos itens no relatório de origem. Se o relatório de destino necessitar de um ou mais pedidos para a execução, o relatório de origem terá de conter uma coluna com os valores adequados para cada pedido. Tem de especificar o número da coluna que fornece o valor para o pedido. Por exemplo, poderá ligar um relatório que liste computadores que foram detetados recentemente a um relatório que liste as últimas mensagens recebidas relativas a um computador específico. Quando a ligação for criada, poderá especificar que a coluna 2 do relatório de origem contém nomes de computador, que é um pedido necessário para o relatório de destino. Quando o relatório de origem for executado, serão apresentados ícones de ligação à esquerda de cada linha de dados. Quando clicar no ícone de uma linha, o Visualizador de Relatórios passará o valor da coluna especificada para essa linha como valor do pedido necessário para apresentar o relatório de destino. É possível configurar um relatório apenas com uma ligação e essa ligação pode ligar apenas a um único recurso de destino.  

> [!WARNING]  
>  Se mover um relatório de destino para uma pasta de relatórios diferente, altera a localização do relatório de destino. A ligação do relatório no relatório de origem não é atualizada automaticamente com a nova localização e a ligação do relatório não funcionará no relatório de origem.  

##  <a name="BKMK_ReportFolders"></a> Pastas de relatórios  
 Pastas de relatórios no System Center Configuration Manager fornecem um método para ordenar e filtrar relatórios armazenados no Reporting Services. As pastas de relatórios são particularmente úteis quando tem muitos relatórios para gerir. Quando é instalado um ponto do Reporting Services, os relatórios são copiados para o Reporting Services e organizados em mais de 50 pastas de relatórios. As pastas de relatórios são só de leitura. Não é possível modificá-las na consola do Configuration Manager.  

##  <a name="BKMK_ReportSubscriptions"></a> Subscrições de relatórios  
 Uma subscrição de relatório no Reporting Services é um pedido recorrente de fornecimento de um relatório a uma hora específica ou em resposta a um evento, com um formato de ficheiro que é especificado na subscrição. As subscrições são uma alternativa à execução de um relatório a pedido. Os relatórios a pedido requerem que selecione ativamente o relatório de cada vez que pretender vê-lo. Em contraste, as subscrições podem ser utilizadas para agendar e automatizar a entrega de um relatório.  

 Pode gerir subscrições de relatórios na consola do Configuration Manager. As subscrições são processadas no servidor de relatórios. As subscrições são distribuídas utilizando extensões de entrega que são implementadas no servidor. Por predefinição, pode criar subscrições que enviem relatórios para uma pasta partilhada ou para um endereço de correio eletrónico. Para obter mais informações sobre a gestão das subscrições dos relatórios, veja [Operações e manutenção de relatórios no System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_ReportBuilder"></a> Report Builder  
 O Configuration Manager utiliza o Microsoft SQL Server Reporting Services o Services Report Builder como a exclusiva de criação e edição de ferramenta baseados no modelo e relatórios baseados em SQL. Quando inicia a ação para criar ou editar um relatório na consola do Configuration Manager, é aberto o Report Builder. Quando cria ou modifica um relatório pela primeira vez, o Report Builder é instalado automaticamente. A versão do Report Builder associada à versão instalada do SQL Server é aberta quando executa ou edita relatórios.  

 A instalação do Report Builder adiciona suporte para mais de 20 idiomas. Quando o Report Builder é executado, apresenta os dados no idioma do sistema operativo em execução no computador local. Se o Report Builder não suportar o idioma, os dados serão apresentados em inglês. O Report Builder suporta todas as capacidades do SQL Server 2008 Reporting Services, incluindo as seguintes:  

-   Fornece um ambiente de criação de relatórios intuitivo com um aspeto semelhante ao do Microsoft Office.  

-   Oferece o esquema de relatórios flexível da linguagem RDL (Report Definition Language) do SQL Server 2008.  

-   Fornece várias formas de visualização de dados, incluindo gráficos e medidores.  

-   Fornece caixas de texto com formatação.  

-   Exporta para o formato do Microsoft Word.  

 Também é possível abrir o Report Builder a partir do SQL Server Reporting Services.  

##  <a name="BKMK_ReportModels"></a> Modelos de relatórios no SQL Server Reporting Services  
 SQL Server Reporting Services no Configuration Manager utiliza modelos de relatórios para ajudar os utilizadores administrativos a selecionar itens da base de dados a incluir nos relatórios baseados em modelos. Para o utilizador administrativo que está a criar o relatório, os modelos de relatórios expõem apenas vistas especificadas e itens para escolha. Para criar relatórios baseados em modelos, tem de estar disponível pelo menos um modelo de relatório. Os modelos de relatórios têm as seguintes funcionalidades:  

-   Pode atribuir aos campos e às vistas da base de dados nomes comerciais lógicos para facilitar a produção de relatórios. Não é necessário conhecer a estrutura da base de dados para produzir relatórios.  

-   Pode agrupar itens de forma lógica.  

-   Pode definir relações entre os itens.  

-   Pode proteger elementos do modelo para que os utilizadores administrativos vejam apenas os dados que tenham permissão para ver.  

 Apesar do Configuration Manager fornece modelos de relatórios de exemplo, pode também definir modelos de relatórios que satisfaçam os seus requisitos de negócio. Para obter mais informações sobre como criar modelos de relatórios, veja [Criar modelos de relatórios personalizados para o System Center Configuration Manager no SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

## <a name="next-steps"></a>Passos seguintes
[Planeamento de relatórios](planning-for-reporting.md)
