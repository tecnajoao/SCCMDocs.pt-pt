---
title: "Capacidades na pré-visualização técnica 1612 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1612."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: bcb14a2be312d4d8a4a9c235652c7bf971a7a976
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1612-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1612 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1612. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="the-data-warehouse-service-point"></a>O ponto de serviço do armazém de dados
Iniciar com a versão de pré-visualização técnica 1612, o ponto de serviço do armazém de dados permite-lhe armazenar e elaborar relatórios sobre dados históricos a longo prazo para a implementação do Configuration Manager. Isto é conseguido por sincronizações automáticas da base de dados do site do Configuration Manager para uma base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do seu ponto do Reporting services.

Por predefinição, quando instala a função de sistema de sites novo ou do Configuration Manager cria a base de dados do armazém de dados de uma instância do SQL Server que especificou. O armazém de dados suporta até 2 TB de dados, com carimbos de registo de alterações.  Por predefinição, os dados que são sincronizados a partir da base de dados do site incluem os grupos de dados para dados globais, dados do Site, Global_Proxy, dados de nuvem e vistas da base de dados. Também pode modificar o que é sincronizado para incluir tabelas adicionais, ou excluir a tabelas específicas a partir de conjuntos de replicação a predefinição.
Os dados predefinidos que são sincronizados incluem informações sobre:
- Estado de funcionamento da infraestrutura
- Segurança
- Conformidade
- Software maligno   
- Implementações de software
- Detalhes de inventário (no entanto, o histórico de inventário não está sincronizado)

Para além de instalar e configurar a base de dados do armazém de dados, várias novos relatórios são instalados para que possa procurar e comunicar facilmente sobre estes dados.

### <a name="data-warehouse-dataflow"></a>Fluxo de dados de armazém de dados   
![Datawarehouse_flow](./media/datawarehouse.png)

| Passo         | Detalhes  |
|:------:|-----------|  
| **1**  |     O servidor do site é transferida e armazena os dados na base de dados do site.  |  
| **2** |      Com base na sua agenda e a configuração, o ponto de serviço do armazém de dados obtém dados a partir da base de dados do site.  |  
| **3** |  O ponto de serviço do armazém de dados é transferida e armazena uma cópia dos dados sincronizados na base de dados do armazém de dados. |  
| **A** |  Utilizar relatórios incorporados, para dados é efetuado um pedido que é transmitido ao Reporting Services ponto através de SQL Server Reporting Services. |  
| **B** |      A maioria dos relatórios são para obter informações atuais e estes pedidos são executados na base de dados do site. |  
| **C** | Quando um relatório de pedidos de dados históricos, utilizando um dos relatórios com uma *categoria* de **do armazém de dados**, o pedido é executado na base de dados do armazém de dados.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Pré-requisitos para o ponto de serviço do armazém de dados e a base de dados
- A hierarquia tem de ter do Reporting services do ponto de função de sistema de sites instalada.
- O computador onde irá instalar a função de sistema de sites requer o .NET Framework 4.5.2 ou posterior.
- A conta de computador do computador onde instalou a função de sistema de sites tem de ter permissões de administrador local no computador que alojará a base de dados do armazém de dados.
- A conta administrativa utilizada para instalar a função de sistema de sites tem de ser um DBO na instância do SQL Server que alojará a base de dados do armazém de dados.  
-  A base de dados é suportada:
  - Com o SQL Server 2012 ou posterior, edição Enterprise ou Datacenter.
  - Num predefinido ou instância com nome
  - Num *Cluster do SQL Server*. Embora esta configuração deverá trabalhar, não foi testado e o suporte está melhor esforço.
  - Quando localizado conjuntamente com uma base de dados ou base de dados de ponto de serviços de relatórios. No entanto, recomendamos, de ser instalado num servidor separado.  
- A conta que é utilizada como o *conta ao ponto do Reporting Services* tem de ter o **db_datareader** permissão para a base de dados do armazém de dados.  
- A base de dados não é suportada num *grupo de Disponibilidade AlwaysOn do SQL Server*.

### <a name="install-the-data-warehouse"></a>Instalar o armazém de dados
Instalar a função de sistema de sites de armazém de dados num site de administração central ou site primário, utilizando o **Adicionar Assistente de funções de sistema de sites** ou **criar Assistente de servidor de sistema de sites**. Consulte o artigo [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles) para obter mais informações. Uma hierarquia suporta várias instâncias desta função, mas apenas uma instância é suportada em cada site.  

Quando instala a função, o Configuration Manager cria a base de dados do armazém de dados por si na instância do SQL Server que especificou. Se especificar o nome da base de dados existente (como o faria se que [mover a base de dados do armazém de dados para um novo SQL Server](#move-the-data-warehouse-database)), o Configuration Manager não será criada uma nova base de dados, mas em vez disso, utilizará a especificar.

#### <a name="configurations-used-during-installation"></a>Configurações utilizadas durante a instalação
Utilize as informações seguintes para concluir a instalação da função de sistema de sites:

**Seleção da função do sistema** página:  
Antes do assistente apresenta uma opção para selecionar e instalar o ponto de serviço do armazém de dados, deverá ter sido instalado um ponto do Reporting services.

**Geral** página: As seguintes informações gerais, é necessárias:
- **Definições de base de dados do Configuration Manager:**   
  - **Nome do servidor** -especifique o FQDN do servidor que aloja a base de dados do site. Se não utilizar uma instância predefinida do SQL Server, tem de especificar a instância após o FQDN no seguinte formato: ***&lt;Sqlserver_FQDN >\&lt; Nome_Instância >***
  - **Nome da base de dados** -especifique o nome da base de dados do site.
  -    **Verifique se** -clique em **verificar** para se certificar de que a ligação à base de dados do site for concluída com êxito.
</br></br>
- **Definições de base de dados do armazém de dados:**
  -    **Nome do servidor** - especifique o FQDN do servidor que aloja o ponto de serviço do armazém de dados e da base de dados. Se não utilizar uma instância predefinida do SQL Server, tem de especificar a instância após o FQDN no seguinte formato: ***&lt;Sqlserver_FQDN >\&lt; Nome_Instância >***
  -    **Nome da base de dados** -especifique o FQDN para a base de dados do armazém de dados.  Configuration Manager irá criar a base de dados com este nome. Se especificar um nome de base de dados que já existe na instância do SQL server, o Configuration Manager irá utilizar essa base de dados.
  -    **Verifique se** -clique em **verificar** para se certificar de que a ligação à base de dados do site for concluída com êxito.

**As definições de sincronização** página:   
- **Definições de dados:**
  - **Grupos de replicação para sincronizar** – selecione os grupos de dados que pretende sincronizar. Para obter informações sobre os diferentes tipos de grupos de dados, consulte o artigo [replicação de base de dados](/sccm/core/servers/manage/data-transfers-between-sites#a-namebkmkdbrepa-database-replication) e **vistas distribuídas** no [transfere dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites).
  - **Tabelas incluídas para sincronizar** – especifique o nome de cada tabela adicional que pretende sincronizar. Utilize uma vírgula para separar várias tabelas. Estas tabelas serão sincronizadas a partir da base de dados do site para além de selecionar os grupos de replicação.
  - **Tabelas excluídas para sincronizar** -especifique o nome de tabelas individuais a partir de grupos de replicação sincronizar. Tabelas que especificar serão excluídas. Utilize uma vírgula para separar várias tabelas.
- **Definições de sincronização:**
  - **Intervalo de sincronização (minutos)** -especificar um valor em minutos. Depois do intervalo for atingido, inicia uma sincronização de novo. Isto suporta um intervalo entre 60 e 1440 minutos (24 horas).
  - **Agenda** -especifique os dias que pretende executar a sincronização.

**Acesso de ponto de Reporting**:   
Após a função de armazém de dados está instalada, certifique-se a conta que é utilizada como o *conta ao ponto do Reporting Services* tem o **db_datareader** permissão para a base de dados do armazém de dados.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Resolver problemas de sincronização de dados e de instalação
Utilize os seguintes registos para investigar problemas com a instalação do ponto de serviço do armazém de dados, ou uma sincronização de dados:
- **DWSSMSI.log** e **DWSSSetup.log** -utilizar estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
-     **Microsoft.ConfigMgrDataWarehouse.log** – utilizar este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.

### <a name="reporting"></a>Relatórios
Depois de instalar uma função de sistema de sites do armazém de dados, os relatórios seguintes estão disponíveis no seu ponto do Reporting services com um *categoria* de **armazém de dados:**

|Relatório                   | Detalhes                                  |
|-------------------------|------------------------------------------|
| **Relatório de implementação de aplicações** | Veja detalhes de implementação de aplicação para uma aplicação específica e a máquina.|
| **Relatório de conformidade de atualização de Software e do Endpoint Protection**   | Computadores de vista que estão em falta as atualizações de software.|
| **Relatório de inventário de Hardware gerais**  | Ver todo o inventário de hardware para uma máquina específica.|
| **Relatório de inventário de Software gerais**  | Ver todo o inventário de software para uma máquina específica.|
| **Descrição geral do Estado de funcionamento de infraestrutura**  |Apresenta uma descrição geral do Estado de funcionamento da infraestrutura do Configuration Manager.|
| **Lista de software maligno detetado**  |Vista contra software maligno que foi detetado na organização.|
|* * Software distribuição resumo relatório * * | Um resumo da distribuição de software para um anúncio específico e a máquina.|

### <a name="move-the-data-warehouse-database"></a>Mover a base de dados do armazém de dados
Utilize os seguintes passos para mover a base de dados do armazém de dados para um novo SQL Server:

  1. Reveja a configuração de base de dados atual e registar os detalhes de configuração, incluindo:  
   - Os grupos de dados que sincronizar
   - Tabelas incluir ou excluir da sincronização       

   Irá reconfigurar a estes grupos de dados e tabelas depois de restaurar a base de dados para um servidor novo e reinstale a função de sistema do site.  

  2. Utilize o SQL Server Management Studio para cópia de segurança de base de dados do armazém de dados e, em seguida, novamente para restaurar a base de dados para um SQL server no novo computador que irá alojar o armazém de dados.

  Depois de restaurar a base de dados para o novo servidor, certifique-se de que as permissões de acesso à base de dados são os mesmos na nova base de dados de armazém de dados que estavam na base de dados de armazém de dados original.

  3. Utilize a consola do Configuration Manager para remover a função de sistema de sites de ponto de serviço do armazém de dados do servidor atual.

  4. Instalar um novo ponto de serviço do armazém de dados e especifique o nome do novo SQL Server e instância que aloja a base de dados do armazém de dados que é restaurada.

  5. Após instala a função de sistema de sites, a mudança está concluída.

Pode rever os seguintes registos do Configuration Manager para confirmar que a função de sistema do site reinstalou com êxito:  
- **DWSSMSI.log** e **DWSSSetup.log** -utilizar estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
-     **Microsoft.ConfigMgrDataWarehouse.log** – utilizar este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.


## <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos
A partir da versão de pré-visualização técnica 1612, pode utilizar uma nova ferramenta de linha de comandos (**ContentLibraryCleanup.exe**) remover o conteúdo que é mais longa não associados a qualquer pacote ou aplicação a partir de um ponto de distribuição (órfãos conteúdo). Esta ferramenta chama-se a ferramenta de limpeza da biblioteca de conteúdos.

Esta ferramenta afeta apenas o conteúdo no ponto de distribuição que especificou quando executar a ferramenta e não é possível remover o conteúdo da biblioteca de conteúdos no servidor do site.

Depois de instalar 1612 de pré-visualização técnica, pode encontrar **ContentLibraryCleanup.exe** no *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* pasta no servidor do site de pré-visualização técnica.

A ferramenta lançada com este pré-visualização técnica destina-se para substituir as versões mais antigas do ferramentas semelhantes lançadas para produtos anteriores do Configuration Manager. Embora esta versão da ferramenta será cessar a funcionar depois de 1 de Março de 2017, novas versões serão versão com pré-visualizações técnica futuras até que esta ferramenta é disponibilizada como parte do ramo atual ou uma versão de fora de banda pronto de produção.

### <a name="requirements"></a>Requisitos  
 - A ferramenta pode ser executada diretamente no computador que aloja o ponto de distribuição ou remotamente a partir de outro servidor. A ferramenta apenas pode ser executada em relação a um único ponto de distribuição de cada vez.
 - A conta de utilizador que executa a ferramenta diretamente tem de ter permissões de administração baseada em funções que são iguais para um administrador total na hierarquia do Configuration Manager.  A ferramenta não funcionar quando a conta de utilizador é concedida permissões de membro de um grupo de segurança do Windows que tem as permissões de administrador global.

### <a name="modes-of-operation"></a>Modos de funcionamento
A ferramenta pode ser executada nos dois modos:
  1.    **Modo de hipóteses**:   
      Quando não especificar o **/eliminar** comutador, a ferramenta é executado em modo de hipóteses e identifica o conteúdo que seria eliminado do ponto de distribuição, mas não eliminar, na verdade, quaisquer dados.

      - Quando a ferramenta é executada neste modo, as informações sobre o conteúdo que seria eliminado automaticamente são escritas para o ficheiro de registo de ferramentas. O utilizador não será pedido para confirmar cada eliminação potencial.
      - Por predefinição, o ficheiro de registo é escrito para a pasta temporária de utilizadores no computador em que executou a ferramenta, no entanto, pode utilizar o comutador /log para redirecionar o ficheiro de registo para outra localização.  
      </br>

    Recomendamos que execute a ferramenta neste modo e rever o ficheiro de registo resultante antes de executar a ferramenta com o comutador /delete.  

  2. **Eliminar modo**: Quando executa a ferramenta com a **/eliminar** comutador, a ferramenta é executada no modo de eliminação.

     - Quando a ferramenta é executada neste modo, conteúdo órfão que se encontra no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.
     -     Antes de eliminar cada ficheiro, o utilizador é-lhe pedido para confirmar que o ficheiro deve ser eliminado.  Pode selecionar, **Y** para Sim, **N** para não, ou **Sim a todos os** para ignorar avisos adicionais e eliminar conteúdo órfão tudo.  
     </br>

     Recomendamos que execute a ferramenta no modo de hipóteses e rever o ficheiro de registo resultante antes de executar a ferramenta com o comutador /delete.  

Quando a ferramenta de limpeza da biblioteca de conteúdos é executado no modo de ambos, cria automaticamente um registo com um nome que inclui a ferramenta é executada no modo, o nome do ponto de distribuição, a data e a hora da operação. O ficheiro de registo aberto automaticamente quando a ferramenta de conclusão. Por predefinição, este registo é escrito para os utilizadores **temp** pasta no computador em que executou a ferramenta., no entanto, pode utilizar um parâmetro de linha de comandos para redirecionar o ficheiro de registo para outra localização, incluindo uma partilha de rede.   


### <a name="run-the-tool"></a>Execute a ferramenta
Para executar a ferramenta:
1. Abra uma linha de comandos administrativa para uma pasta que contém **ContentLibraryCleanup.exe**.  
2. Em seguida, introduza uma linha de comandos que inclui os parâmetros de linha de comandos necessário e parâmetros opcionais que pretende utilizar.

**Conhecido problema** quando a ferramenta é executada, poderá ser devolvido um erro semelhante ao seguinte quando qualquer pacote de implementação falhou ou está em curso:
-  *System.InvalidOperationException: Esta biblioteca de conteúdos não é possível limpar neste momento porque o pacote <packageID> não está completamente instalado.*

**Solução:** Nenhuma. A ferramenta não é possível fiável identificar ficheiros órfãos quando o conteúdo está em curso ou falhou implementar. Por conseguinte, a ferramenta não permitirá ao conteúdo de limpeza até que esse problema seja resolvido.



### <a name="command-line-switches"></a>Parâmetros de linha de comandos  
Os seguintes parâmetros de linha de comandos podem ser utilizados por qualquer ordem.   

|Parâmetro|Detalhes|
|---------|-------|
|**/DELETE**  |**Opcional** </br> Utilize este parâmetro quando pretender eliminar o conteúdo do ponto de distribuição. -Á antes do conteúdo é eliminado. </br></br> Quando este comutador não é utilizado, a ferramenta regista resultados sobre o conteúdo que seria eliminado, mas não eliminar o conteúdo do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /delete*** |
| **/q**       |**Opcional** </br> Execute a ferramenta no modo sossegado que suprime todos os avisos (como avisos quando está a eliminar o conteúdo) e não abrir automaticamente o ficheiro de registo. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp Server1. contoso.com*** |
| **/dp &lt;FQDN do ponto de distribuição >**  | **Necessário** </br> Especifique o nome de domínio completamente qualificado (FQDN) do ponto de distribuição que pretende limpar. </br></br> Exemplo:  ***/Dp de ContentLibraryCleanup.exe Server1. contoso.com***|
| **/PS &lt;FQDN de site principal >**       | **Opcional** quando limpar conteúdo a partir de um ponto de distribuição num site primário.</br>**Obrigatório** quando limpar conteúdo a partir de um ponto de distribuição num site secundário. </br></br> Especifique o FQDN do site primário, o ponto de distribuição pertence para ou do elemento principal primário principal, quando o ponto de distribuição estiver num site secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código do site principal >**  | **Opcional** quando limpar conteúdo a partir de um ponto de distribuição num site primário.</br>**Obrigatório** quando limpar conteúdo a partir de um ponto de distribuição num site secundário. </br></br> Especifique o código do site do site primário que o ponto de distribuição pertence a ou do site primário principal quando o ponto de distribuição estiver num site secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /sc ABC*** |
| **/log<log file directory>**       |**Opcional** </br> Especifique um diretório para colocar ficheiros de registo na. Isto pode ser numa unidade local ou numa rede de partilhar.</br></br> Quando este comutador não é utilizado, ficheiros de registo são automaticamente colocados na pasta temp utilizadores.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de partilha de rede: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /log \\ &lt;partilhar >\&lt; pasta >***|


## <a name="improvements-for-in-console-search"></a>Melhoramentos na cópia de pesquisa na consola
Com base em comentários de voz do utilizador, adicionámos os seguintes melhoramentos à pesquisa na consola:
 - **Caminho do objeto:**  
  Muitos objetos suportam agora uma nova coluna com o nome **caminho de objecto**.  Quando pesquisar e inclua esta coluna nos resultados da sua apresentação, pode ver o caminho para cada objeto. Por exemplo, se executar uma procura de aplicações no nó de aplicações e também estiver à procura nodes secundárias, a *caminho de objecto* coluna no painel de resultados irá mostrar o caminho para cada objeto devolvido.   

- **Preservação de texto de pesquisa:**  
  Quando introduzir texto na caixa de texto de pesquisa e, em seguida, alternar entre procurar um nó secundárias e o nó atual, o texto que introduzir agora irá manter e permanecem disponível para uma nova procura sem ter de reintroduzi-lo.

- **Preservação de sua decisão para pesquisar nodes secundárias:**  
 A opção que selecionar para qualquer um dos pesquisar o *nó atual* ou *todos os nós secundárias* agora persistir quando altera o nó onde está a trabalhar.   Este novo comportamento significa que não é necessário repor constantemente a decisão como mover-se a consola.  Por predefinição, ao abrir a consola a opção é procurar apenas o nó atual.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Evitar a instalação de uma aplicação se um programa especificado está em execução.
Agora pode configurar uma lista de ficheiros executáveis (com .exe extensão) nas propriedades de tipo de implementação que, se a ser executado, irão bloquear a instalação de uma aplicação. Após a instalação é tentada, os utilizadores irão ver uma caixa de diálogo a pedir-lhes para fecharem os processos que são bloquear a instalação.

### <a name="try-it-out"></a>Experimente
Para configurar uma lista de ficheiros executáveis
1.    Na página de propriedades de qualquer tipo de implementação, selecione o **instalador processamento** separador.
2.    Clique em **adicionar**, para adicionar um mais ficheiros executáveis à lista (por exemplo **Edge.exe**)
3.    Clique em **OK** para fechar a caixa de diálogo de propriedades de tipo de implementação.

Agora, quando implementar esta aplicação para um utilizador ou um dispositivo e um dos executáveis que adicionou está em execução, o utilizador final verá uma caixa de diálogo do Centro de Software informar de que a instalação falhou porque uma aplicação está em execução.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Novo Windows Hello para notificação de negócio para os utilizadores finais

Uma nova notificação do Windows 10 informa os utilizadores finais que o que tem de realizar ações adicionais para concluir Windows Hello para a configuração de negócio (por exemplo, definição de um PIN).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Loja Windows para o suporte de negócio no Configuration Manager

Agora pode implementar aplicações licenciadas online com um objetivo de implementação de **disponível** da loja Windows para empresas em PCs a executar o cliente do Configuration Manager.
Para obter mais detalhes, consulte o artigo [gerir aplicações na loja Windows para empresas com o System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

Suporte para esta funcionalidade só está atualmente disponível em PCs a executar a compilação de pré-visualização do Windows 10 RS2.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior, quando uma sequência de tarefas falhar
Agora, pode regressar à página anterior quando executa uma sequência de tarefas e existir uma falha. Esta versão, era necessário reiniciar a sequência de tarefas quando ocorreu uma falha. Por exemplo, pode utilizar o **anterior** botão nos seguintes cenários:

- Quando um computador arrancar no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas apresentada com uma mensagem que não existem não sequências de tarefas disponível. Agora, pode clicar em **anterior** para procurar novamente sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdos dependentes ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Pode agora distribuir o conteúdo em falta (se não foi distribuída ainda) ou aguardar que o conteúdo fique disponível nos pontos de distribuição e, em seguida, clique em **anterior** com a pesquisa de sequência de tarefas novamente para o conteúdo.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Suporte para atualizações do Windows 10 de ficheiros de instalação rápida
Adicionámos ficheiros de instalação rápida suportem no Configuration Manager para atualizações do Windows 10. Quando utiliza uma versão suportada do Windows 10, agora, pode utilizar definições do Configuration Manager para transferir apenas as diferenças entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior. Atualmente ramo de atual do Configuration Manager, o Windows 10 cumulativa atualização completa (incluindo todas as atualizações de meses anteriores) são transferidos por mês. Utilizar ficheiros de instalação rápida fornece para transferências mais pequenas e tempos mais rápidos de instalação em clientes.

> [!IMPORTANT]
> Enquanto as definições para suportar a utilização de ficheiros de instalação rápida está disponível no Configuration Manager, esta funcionalidade só é suportada no Windows 10 versão 1607 com uma atualização de agente do Windows Update incluído com as atualizações publicadas no 10 de Janeiro de 2017 (Patch Terça-feira). Para mais informações sobre estas atualizações, consulte o artigo [suporta artigo 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Pode tirar partido dos ficheiros de instalação rápida quando o próximo conjunto de atualizações são lançadas nos 14 de Fevereiro de 2017. Windows 10 versão 1607 sem a atualização e as versões anteriores não suportam ficheiros de instalação rápida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Para permitir a transferência de ficheiros de instalação rápida para atualizações do Windows 10 no servidor do
Para iniciar a sincronização dos metadados para ficheiros de instalação expressa do Windows 10, terá de a ativar nas propriedades do ponto de atualização de Software.
1.    Na consola do Configuration Manager, navegue para **administração** > **configuração do Site** > **Sites**.
2.    Selecione o site de administração central ou site primário autónomo.
3.    No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**. No **ficheiros de atualização** separador, selecione **transferir ficheiros completos de todas as atualizações aprovadas e rápida de ficheiros de instalação para o Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para ativar o suporte para os clientes transferir e instalar ficheiros de instalação rápida
Para ativar o suporte de ficheiros de instalação rápida nos clientes, tem de ativar os ficheiros de instalação rápida nos clientes na secção de atualizações de Software de definições de cliente. Isto cria um serviço de escuta HTTP novo que escuta pedidos transferir ficheiros de instalação rápida na porta que especificar. Depois de implementar as definições de cliente para ativar esta funcionalidade no cliente, irá tentar transferir as diferenças entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior (clientes tem de executar uma versão do Windows 10 que suporta express ficheiros de instalação).
1.    Ative o suporte para ficheiros de instalação rápida nas propriedades do componente de ponto de atualização de Software (procedimento anterior).
2.    Na consola do Configuration Manager, navegue para **administração** > **definições de cliente**.
3.    Selecione as definições de cliente apropriada, em seguida, no **base** separador, clique em **propriedades**.
4.    Selecione o **atualizações de Software** página, configure **Sim** para o **ativar a instalação das atualizações rápida nos clientes** definir e configurar a porta utilizada pelo serviço de escuta de HTTP no cliente para o **porta utilizada para transferir conteúdo para atualizações rápidas** definição.


## <a name="odata-endpoint-data-access"></a>Acesso de dados do ponto final de OData

 O Configuration Manager oferece agora um ponto final de OData REST para aceder a dados do Configuration Manager. O ponto final é compatível com a versão 4, Ativa as ferramentas como o Excel e Power BI para aceder facilmente a dados do Configuration Manager através de um único ponto de final de Odata. 1612 de pré-visualização técnica só suporta acesso de leitura a objetos no Configuration Manager.  

Dados que estão atualmente disponíveis no [fornecedor de WMI do Configuration Manager](/sccm/develop/reference/configuration-manager-reference) também está agora acessível com o novo ponto de final de OData REST. Os conjuntos de entidade expostos pelo ponto final de OData permitem-lhe enumerar relativamente aos mesmos dados, que pode consultar com o fornecedor WMI.

### <a name="try-it-out"></a>Experimente

Antes de poder utilizar o ponto final de OData, terá de a ativar para o site.

1.  Aceda a **administração** > **configuração do Site** > **Sites**.
2.  Selecione o site primário e clique em **propriedades**.
3.  No separador Geral da folha de propriedades de site primário, clique em **resto ativar o ponto final para todos os fornecedores neste site**e, em seguida, clique em **OK**.

No seu Visualizador de consulta de OData favorita, experimente consultas semelhantes para os exemplos seguintes para devolver vários objetos no Configuration Manager:

| Objetivo | Consulta de OData |
|---|---|
| Obter todas as coleções | `http://localhost/CMRestProvider/Collection` |
| Obter uma coleção | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Obter os dispositivos de 100 superior na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Obter um dispositivo com um ID de recurso na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Obter o sistema operativo do dispositivo da coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Obter os utilizadores na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> As consultas de exemplo apresentadas na tabela utilizam *localhost* como o anfitrião de nome no URL e pode ser utilizado no computador que executa o fornecedor de SMS. Se estiver a executar as consultas a partir de um computador diferente, substitua localhost o FQDN do servidor com o fornecedor de SMS instalado.

## <a name="azure-active-directory-onboarding"></a>Integração do Azure Active Directory

Integração do Azure Active Directory (AD) cria uma ligação entre o Configuration Manager e do Azure Active Directory para ser utilizado por outros serviços em nuvem. Atualmente pode ser utilizado para criar a ligação necessária para o Gateway de gestão da nuvem.

Execute esta tarefa com o administrador do Azure, como, terá de credenciais de administrador do Azure.

#### <a name="to-create-the-connection"></a>Para criar a ligação:

2. No **administração** área de trabalho, selecione **serviços em nuvem** > **do Azure Active Directory** > **adicionar do Azure Active Directory**.
2. Escolher **sessão** para criar a ligação com o Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Requisitos do cliente do Configuration Manager

Existem vários requisitos para ativar a criação da política de utilizador no Gateway de gestão na nuvem.

- O processo de integração do Azure AD tem de ser concluído e o cliente tiver inicialmente estar ligados à rede da empresa para obter as informações de ligação.
- Os clientes devem estar ambos associados a um domínio (registado nos Active Directory) e na nuvem-associados a um domínio (registado no Azure AD).
- Tem de executar [deteção de utilizador do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#active-directory-user-discovery#active-directory-user-discovery).
- Tem de modificar o cliente de Configuration Manager para permitir pedidos de política de utilizador através da Internet e implementar a alteração ao cliente. Uma vez que esta alteração ao cliente decorre *no dispositivo cliente*, podem ser implementada através do Gateway de gestão da nuvem, embora ainda não concluiu as alterações de configuração necessárias para a política de utilizador.
- O ponto de gestão tem de ser configurado para utilizar HTTPS para proteger o token na rede e deve ter o .net 4.5 instalados.

Depois de efetuar estas alterações de configuração, pode criar uma política de utilizador e deslocar-se os clientes na Internet para testar a política. Serão possível autenticar pedidos da política de utilizador através do Gateway de gestão da nuvem com a autenticação baseada em tokens do Azure AD.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Alterar para configurar a autenticação multifator para a inscrição de dispositivos

Agora que pode configurar a autenticação multifator (MFA) para a inscrição de dispositivos no portal do Azure, a opção de MFA foi removida na consola do Configuration Manager. Pode encontrar mais informações sobre como configurar a MFA para inscrição [neste tópico do Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/multi-factor-authentication-azure-active-directory).

