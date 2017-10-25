---
title: "Capacidades na pré-visualização técnica 1612 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1612."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bcb14a2be312d4d8a4a9c235652c7bf971a7a976
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1612-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1612 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*



Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1612. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="the-data-warehouse-service-point"></a>O ponto de serviço do armazém de dados
Começando com a versão de pré-visualização técnica 1612, o ponto de serviço do armazém de dados permite-lhe armazenar e elaborar relatórios sobre dados históricos a longo prazo para a sua implementação do Configuration Manager. Isto é conseguido ao sincronizações automáticas da base de dados do site do Configuration Manager para uma base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do ponto do Reporting services.

Por predefinição, quando instalar a nova função de sistema de sites, do Configuration Manager cria a base de dados do armazém de dados de uma instância do SQL Server que especificou. O armazém de dados suporta até 2 TB de dados, com carimbos de registo de alterações.  Por predefinição, os dados que são sincronizados a partir da base de dados do site incluem os grupos de dados para dados globais, dados do Site, Global_Proxy, dados em nuvem e vistas da base de dados. Também pode modificar o que está sincronizado para incluir tabelas adicionais, ou excluir tabelas específicas dos conjuntos de replicação de predefinição.
Os dados predefinidos que são sincronizados incluem informações sobre:
- Estado de funcionamento da infraestrutura
- Segurança
- Conformidade
- Software maligno   
- Implementações de software
- Detalhes de inventário (no entanto, o histórico de inventário não está sincronizado)

Para além de instalar e configurar a base de dados do armazém de dados, vários novos relatórios estão instalados para que possa facilmente procurar e relatórios sobre estes dados.

### <a name="data-warehouse-dataflow"></a>Fluxo de dados de armazém de dados   
![Datawarehouse_flow](./media/datawarehouse.png)

| Passo         | Detalhes  |
|:------:|-----------|  
| **1**  |  O servidor do site transfere e armazena dados na base de dados do site.  |  
| **2** |   Com base na respetiva agenda e a configuração, o ponto de serviço do armazém de dados obtém os dados da base de dados do site.  |  
| **3** |  O ponto de serviço do armazém de dados é transferida e armazena uma cópia dos dados sincronizados na base de dados do armazém de dados. |  
| **A** |  Utilizar relatórios incorporados, para dados é efetuado um pedido que é transferido para o Reporting Services ponto utilizando o SQL Server Reporting Services. |  
| **B** |   A maioria dos relatórios são para obter informações atuais e estes pedidos são executados na base de dados do site. |  
| **C** | Quando um relatório solicita dados históricos, utilizando um dos relatórios com um *categoria* de **do armazém de dados**, o pedido é executado na base de dados do armazém de dados.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Pré-requisitos para o ponto de serviço do armazém de dados e a base de dados
- A hierarquia tem de ter dos serviços de relatórios do ponto de função de sistema de sites instalada.
- O computador onde instalou a função de sistema de sites requer o .NET Framework 4.5.2 ou posterior.
- A conta de computador do computador onde instalou a função de sistema de sites tem de ter permissões de administrador local no computador que alojará a base de dados do armazém de dados.
- A conta administrativa utilizada para instalar a função de sistema de sites tem de ser um DBO na instância do SQL Server que alojará a base de dados do armazém de dados.  
-  A base de dados é suportada:
  - Com o SQL Server 2012 ou posterior, Enterprise ou Datacenter edition.
  - Numa instância predefinida ou nomeada
  - Num *Cluster do SQL Server*. Embora esta configuração deverão funcionar, não foram testado e suporte é melhor esforço.
  - Quando localizado conjuntamente com uma base de dados do site ou a base de dados de ponto de serviços de relatórios. No entanto, recomendamos que, de ser instalado num servidor separado.  
- A conta que é utilizada como o *conta de ponto do Reporting Services* tem de ter o **db_datareader** permissão para a base de dados do armazém de dados.  
- A base de dados não é suportado um *grupo de Disponibilidade AlwaysOn do SQL Server*.

### <a name="install-the-data-warehouse"></a>Instalar o armazém de dados
Instalar a função de sistema de sites do armazém de dados num site de administração central ou site primário, utilizando o **Adicionar Assistente de funções de sistema de Site** ou **criar Assistente de servidor de sistema de Site**. Consulte [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles) para obter mais informações. A hierarquia suporta várias instâncias desta função, mas é suportada apenas uma instância em cada site.  

Quando instalar a função, o Configuration Manager cria a base de dados do armazém de dados para si na instância do SQL Server que especificou. Se especificar o nome da base de dados existente (como iria fazer se a [mover a base de dados do armazém de dados para um novo SQL Server](#move-the-data-warehouse-database)), do Configuration Manager não criar uma nova base de dados, mas em vez disso, utiliza um que especificar.

#### <a name="configurations-used-during-installation"></a>Configurações utilizadas durante a instalação
Utilize as informações seguintes para concluir a instalação da função de sistema de sites:

**Seleção da função do sistema** página:  
Antes do assistente apresenta uma opção para selecionar e instalar o ponto de serviço do armazém de dados, tem de ter instalado um ponto do Reporting services.

**Geral** página: As seguintes informações gerais, é necessárias:
- **Definições de base de dados do Configuration Manager:**   
  - **Nome do servidor** -especifique o FQDN do servidor que aloja a base de dados do site. Se utilizar uma instância predefinida do SQL Server, tem de especificar a instância após o FQDN no seguinte formato: ***&lt;Sqlserver_FQDN >\&lt; Nome_Instância >***
  - **Nome da base de dados** -especifique o nome da base de dados do site.
  - **Certifique-se** -clique em **verifique** para se certificar de que a ligação para a base de dados do site é concluída com êxito.
</br></br>
- **Definições de base de dados do armazém de dados:**
  - **Nome do servidor** - especifique o FQDN do servidor que aloja o ponto de serviço do armazém de dados e da base de dados. Se utilizar uma instância predefinida do SQL Server, tem de especificar a instância após o FQDN no seguinte formato: ***&lt;Sqlserver_FQDN >\&lt; Nome_Instância >***
  - **Nome da base de dados** -especifique o FQDN para a base de dados do armazém de dados.  Configuration Manager irá criar a base de dados com este nome. Se especificar um nome de base de dados que já existe na instância do SQL server, o Configuration Manager irá utilizar a base de dados.
  - **Certifique-se** -clique em **verifique** para se certificar de que a ligação para a base de dados do site é concluída com êxito.

**As definições de sincronização** página:   
- **Definições de dados:**
  - **Grupos de replicação para sincronizar** – selecione os grupos de dados que pretende sincronizar. Para obter informações sobre os diferentes tipos de grupos de dados, consulte [replicação de base de dados](/sccm/core/servers/manage/data-transfers-between-sites#a-namebkmkdbrepa-database-replication) e **vistas distribuídas** no [transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites).
  - **As tabelas incluídas para sincronizar** – especifique o nome de cada tabela adicional que pretende sincronizar. Separe várias tabelas com uma vírgula. Estas tabelas vão ser sincronizadas a partir da base de dados do site, além de selecionar os grupos de replicação.
  - **As tabelas excluídas para sincronizar** -especifique o nome de tabelas individuais dos grupos de replicação sincronizar. As tabelas que especificar serão excluídas. Separe várias tabelas com uma vírgula.
- **Definições de sincronização:**
  - **Intervalo de sincronização (minutos)** -Especifique um valor em minutos. Após ter sido atingido o intervalo, inicia uma sincronização de novo. Isto suporta um intervalo entre 60 e 1440 minutos (24 horas).
  - **Agenda** -especifique os dias em que pretende que a sincronização para ser executada.

**Acesso de ponto de Reporting**:   
Após a função de armazém de dados está instalada, certifique-se a conta que é utilizada como o *conta de ponto do Reporting Services* tem o **db_datareader** permissão para a base de dados do armazém de dados.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Resolver problemas de instalação e os dados de sincronização
Utilize os seguintes registos para investigar problemas com a instalação do ponto de serviço do armazém de dados, ou uma sincronização de dados:
- **DWSSMSI.log** e **DWSSSetup.log** -utilizar estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
-   **Microsoft.ConfigMgrDataWarehouse.log** – utilizar este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.

### <a name="reporting"></a>Relatórios
Depois de instalar uma função de sistema de sites do armazém de dados, os seguintes relatórios estão disponíveis no seu ponto do Reporting services com um *categoria* de **do armazém de dados:**

|Relatório                   | Detalhes                                  |
|-------------------------|------------------------------------------|
| **Relatório de implementação de aplicação** | Ver os detalhes para a implementação de aplicação para uma aplicação específica e a máquina.|
| **Endpoint Protection e o relatório de conformidade de atualização de Software**   | Computadores de vista que estão em falta atualizações de software.|
| **Relatório de inventário de Hardware geral**  | Ver todo o inventário de hardware para um computador específico.|
| **Relatório de inventário de Software geral**  | Ver todo o inventário de software para uma máquina específica.|
| **Descrição geral do Estado de funcionamento de infraestrutura**  |Apresenta uma descrição geral do Estado de funcionamento da infraestrutura do Configuration Manager.|
| **Lista de Malware detetado**  |Software maligno de vista que foi detetado na organização.|
|* * Software distribuição resumo relatório * * | Um resumo de distribuição de software para um anúncio específico e a máquina.|

### <a name="move-the-data-warehouse-database"></a>Mover a base de dados do armazém de dados
Utilize os seguintes passos para mover a base de dados do armazém de dados para um novo SQL Server:

  1. Reveja a configuração de base de dados atual e registe os detalhes da configuração, incluindo:  
   - Os grupos de dados que sincronizar
   - Tabelas incluir ou excluir da sincronização       

   Irá reconfigurar estes grupos de dados e tabelas depois de restaurar a base de dados para um novo servidor e reinstalar a função de sistema de sites.  

  2. Utilize o SQL Server Management Studio para cópia de segurança de base de dados do armazém de dados e, em seguida, novamente para restaurar a base de dados para um SQL server no novo computador que irá alojar o armazém de dados.

  Depois de restaurar a base de dados para o novo servidor, certifique-se de que as permissões de acesso de base de dados são os mesmos na nova base de dados de armazém de dados idênticos na base de dados de armazém de dados original.

  3. Utilize a consola do Configuration Manager para remover a função de sistema de sites de ponto de serviço do armazém de dados do servidor atual.

  4. Instalar um novo ponto de serviço do armazém de dados e especifique o nome do novo SQL Server e instância que aloja a base de dados do armazém de dados que é restaurada.

  5. Após a instalação da função de sistema de sites, a mudança está concluída.

Pode rever os seguintes registos do Configuration Manager para confirmar que a função de sistema do site reinstalou com êxito:  
- **DWSSMSI.log** e **DWSSSetup.log** -utilizar estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
-   **Microsoft.ConfigMgrDataWarehouse.log** – utilizar este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.


## <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos
A partir da versão de pré-visualização técnica 1612, pode utilizar uma nova ferramenta de linha de comandos (**ContentLibraryCleanup.exe**) remover o conteúdo que é mais longo não associados a qualquer pacote ou aplicação a partir de um ponto de distribuição (órfão conteúdo). Esta ferramenta denomina-se a ferramenta de limpeza da biblioteca de conteúdos.

Esta ferramenta afeta apenas o conteúdo no ponto de distribuição que especificou quando executar a ferramenta e não é possível remover o conteúdo da biblioteca de conteúdos no servidor do site.

Depois de instalar 1612 de pré-visualização técnica, pode encontrar **ContentLibraryCleanup.exe** no *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* pasta no servidor do site de pré-visualização técnica.

A ferramenta lançada com este Technical Preview destina-se para substituir as versões anteriores das ferramentas semelhantes lançadas para produtos anteriores do Configuration Manager. Embora esta versão da ferramenta deixarão de funcionar após 1 de Março de 2017, novas versões vai lançar com pré-visualizações técnicas futuras até que esta ferramenta é lançada como parte do ramo atual, ou uma versão de fora de banda pronto de produção.

### <a name="requirements"></a>Requisitos  
 - A ferramenta pode ser executada diretamente no computador que aloja o ponto de distribuição ou remotamente a partir de outro servidor. A ferramenta só pode ser executada em relação a um único ponto de distribuição de cada vez.
 - A conta de utilizador que executa a ferramenta diretamente tem de ter permissões de administração baseada em funções que sejam iguais a um administrador total na hierarquia do Configuration Manager.  A ferramenta não funcionará quando a conta de utilizador é concedida permissões como um membro de um grupo de segurança do Windows que tem as permissões de administrador global.

### <a name="modes-of-operation"></a>Modos de funcionamento
A ferramenta pode ser executada em dois modos:
  1.    **Modo de investiguem**:   
      Quando não especificar o **/eliminar** comutador, a ferramenta é executado no modo de investiguem e identifica os conteúdos que serão eliminados do ponto de distribuição, mas não eliminar, na verdade, quaisquer dados.

      - Quando a ferramenta é executada neste modo, informações sobre o conteúdo que será eliminado automaticamente são escritas no ficheiro de registo de ferramentas. Não é pedido ao utilizador para confirmar eliminação cada potencial.
      - Por predefinição, o ficheiro de registo é escrito na pasta temporária de utilizadores no computador em que executa a ferramenta, no entanto, pode utilizar o comutador /log para redirecionar o ficheiro de registo para outra localização.  
      </br>

    Recomendamos que execute a ferramenta neste modo e rever o ficheiro de registo resultante antes de executar a ferramenta com o comutador /delete.  

  2. **Eliminar modo**: Quando executa a ferramenta com o **/eliminar** comutador, a ferramenta é executada no modo de eliminação.

     - Quando a ferramenta é executada neste modo, o conteúdo órfão que se encontra no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.
     -  Antes de eliminar cada ficheiro, é pedido ao utilizador para confirmar que o ficheiro deve ser eliminado.  Pode selecionar, **Y** para Sim, **N** para não, ou **Sim para todas as** para ignorar avisos adicionais e eliminar todos os órfão conteúdo.  
     </br>

     Recomendamos que execute a ferramenta no modo de investiguem e rever o ficheiro de registo resultante antes de executar a ferramenta com o comutador /delete.  

Quando a ferramenta de limpeza da biblioteca de conteúdos é executada em qualquer modo, cria automaticamente um registo com um nome que inclui o modo que é executada a ferramenta, o nome do ponto de distribuição, a data e a hora da operação. O ficheiro de registo abre automaticamente quando a ferramenta estiver concluída. Por predefinição, este registo é escrito para os utilizadores **temp** pasta no computador em que executa a ferramenta., no entanto, pode utilizar um comutador de linha de comandos para redirecionar o ficheiro de registo para outra localização, incluindo uma partilha de rede.   


### <a name="run-the-tool"></a>Execute a ferramenta
Para executar a ferramenta:
1. Abra uma linha de comandos administrativa para uma pasta que contém **ContentLibraryCleanup.exe**.  
2. Em seguida, introduza uma linha de comandos que inclui os comutadores de linha de comandos necessário e comutadores opcionais que pretende utilizar.

**Problema de conhecido** quando a ferramenta é executada, poderá ser devolvido um erro semelhante ao seguinte, quando qualquer pacote de implementação falhou ou está em curso:
-  *System.InvalidOperationException: Nesta biblioteca de conteúdos não é possível limpar neste momento porque o pacote <packageID> não é completamente instalado.*

**Solução:** Nenhuma. A ferramenta não é possível fiável identificar ficheiros órfãos quando o conteúdo está em curso ou falhou a implementação. Por conseguinte, a ferramenta não permitirá a limpar conteúdo até que este problema seja resolvido.



### <a name="command-line-switches"></a>Parâmetros da linha de comandos  
Os seguintes parâmetros de linha de comandos podem ser utilizados por qualquer ordem.   

|Parâmetro|Detalhes|
|---------|-------|
|**/DELETE**  |**Opcional** </br> Utilize este parâmetro se pretender eliminar o conteúdo do ponto de distribuição. Lhe for pedido antes do conteúdo é eliminado. </br></br> Quando este parâmetro não for utilizado, a ferramenta regista resultados sobre o conteúdo que será eliminado, mas não eliminar todos os conteúdos do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Execute a ferramenta no modo silencioso que suprime todos os avisos (como avisos aquando da eliminação de conteúdo) e não abra automaticamente o ficheiro de registo. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN do ponto de distribuição >**  | **Necessário** </br> Especifique o nome de domínio completamente qualificado (FQDN) do ponto de distribuição que pretende apagar. </br></br> Exemplo:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/PS &lt;site primário FQDN >**       | **Opcional** quando o conteúdo a partir de um ponto de distribuição num site primário de limpeza.</br>**Necessário** quando o conteúdo a partir de um ponto de distribuição num site secundário de limpeza. </br></br> Especifique o FQDN do ponto de distribuição do site primário pertence ao ou do elemento principal primário principal quando o ponto de distribuição num site secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código do site principal >**  | **Opcional** quando o conteúdo a partir de um ponto de distribuição num site primário de limpeza.</br>**Necessário** quando o conteúdo a partir de um ponto de distribuição num site secundário de limpeza. </br></br> Especifique o código do site do site primário que pertence o ponto de distribuição ou do site primário principal quando o ponto de distribuição num site secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log<log file directory>**       |**Opcional** </br> Especifique um diretório colocar ficheiros de registo na. Isto pode ser uma unidade local ou numa rede de partilha.</br></br> Quando este parâmetro não for utilizado, ficheiros de registo são automaticamente colocados na pasta temporária de utilizador.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de partilha de rede: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\ &lt;partilhar >\&lt; pasta >***|


## <a name="improvements-for-in-console-search"></a>Melhoramentos para pesquisa na consola
Com base nos comentários de voz do utilizador, iremos adicionou os seguintes melhoramentos para a pesquisa na consola:
 - **Caminho do objeto:**  
  Muitos objetos suportam agora uma nova coluna com o nome **caminho de objecto**.  Quando pesquisar e inclua esta coluna nos resultados a apresentar, pode ver o caminho para cada objeto. Por exemplo, se executar uma pesquisa de aplicações no nó de aplicações e também procura nodes secundárias, a *caminho de objecto* coluna no painel de resultados mostra o caminho para cada objeto devolvido.   

- **Preservação de texto de pesquisa:**  
  Quando introduzir o texto na caixa de texto de pesquisa e, em seguida, alternar entre a procurar nó secundárias e o nó atual, o texto que escreveu irá agora persistem e permanecem disponível para uma nova procura sem ter de introduzi-lo.

- **Preservação de sua decisão para procurar nodes secundárias:**  
 A opção que selecionar para a pesquisa a *nó atual* ou *todos os nós secundárias* agora persistir quando altera o nó que está a trabalhar.   Este novo comportamento significa que não é necessário repor constantemente a decisão como mover-se a consola.  Por predefinição, quando abrir a consola a opção é apenas pesquisar no nó atual.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Impedi a instalação de uma aplicação se estiver a executar um programa especificado.
Agora, pode configurar uma lista de ficheiros executáveis (com a extensão .exe) nas propriedades de tipo de implementação que, se em execução, irão bloquear a instalação de uma aplicação. Após a instalação for tentada, os utilizadores verão uma caixa de diálogo a perguntá-los para fechar os processos que estão a bloquear a instalação.

### <a name="try-it-out"></a>Experimente
Para configurar uma lista de ficheiros executáveis
1.  Na página de propriedades de qualquer tipo de implementação, escolha o **instalador processamento** separador.
2.  Clique em **adicionar**, para adicionar um mais ficheiros executáveis à lista (por exemplo **Edge.exe**)
3.  Clique em **OK** para fechar a caixa de diálogo de propriedades de tipo de implementação.

Agora, quando irá implementar esta aplicação para um utilizador ou um dispositivo e um dos executáveis que adicionou está em execução, o utilizador final verá uma caixa de diálogo de centro de Software informar de que a instalação falhou porque uma aplicação está em execução.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Novo do Windows Hello para notificação de negócio para os utilizadores finais

Uma nova notificação do Windows 10 informa os utilizadores finais que requerem ações adicionais para concluir Windows Hello para a configuração de negócio (por exemplo, definição de um PIN).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Loja Windows para o suporte de negócio no Configuration Manager

Pode agora implementar aplicações licenciadas online com um objetivo de implementação **disponível** da loja Windows para empresas para os computadores a executar o cliente do Configuration Manager.
Para obter mais detalhes, consulte [gerir aplicações da loja Windows para empresas com o System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

Suporte para esta funcionalidade está atualmente disponível apenas em PCs com a Windows 10 RS2 de pré-visualização.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior, quando ocorre uma falha de uma sequência de tarefas
Agora pode regressar a uma página anterior quando executa uma sequência de tarefas e não existe uma falha. Antes desta versão, era necessário reiniciar a sequência de tarefas quando ocorreu uma falha. Por exemplo, pode utilizar o **anterior** botão nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas é apresentada uma mensagem que existem não existem sequências de tarefas disponíveis. Agora, pode clicar em **anterior** para novamente procurar sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdos dependentes ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Pode agora distribuir o conteúdo em falta (se não foi distribuída ainda) ou aguardar que o conteúdo fique disponível nos pontos de distribuição e, em seguida, clique em **anterior** ter a pesquisa de sequência de tarefas novamente para o conteúdo.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Suporte para atualizações do Windows 10 de ficheiros de instalação rápida
Foi adicionado ficheiros de instalação rápida suportem no Configuration Manager para atualizações do Windows 10. Quando utiliza uma versão suportada do Windows 10, agora, pode utilizar definições de Configuration Manager para transferir apenas o delta entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior. Atualmente no ramo de atual do Configuration Manager, o Windows 10 cumulativa atualização completa (incluindo todas as atualizações de meses anteriores) são transferidos por mês. A utilização de ficheiros de instalação rápida fornece para transferências mais pequenas e tempos de instalação mais rápidos nos clientes.

> [!IMPORTANT]
> Enquanto as definições para suportar a utilização de ficheiros de instalação rápida está disponível no Configuration Manager, esta funcionalidade só é suportada no Windows 10 versão 1607 com uma atualização do Windows Update Agent incluída com as atualizações publicadas no 10 de Janeiro de 2017 (Patch Terça-feira). Para mais informações sobre estas atualizações, consulte [suporta artigo 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Pode tirar partido dos ficheiros de instalação rápida quando o seguinte conjunto de atualizações são lançadas a 14 de Fevereiro de 2017. Windows 10 versão 1607 sem a atualização e as versões anteriores não suportam a ficheiros de instalação rápida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Para permitir a transferência de ficheiros de instalação rápida para atualizações do Windows 10 no servidor
Para iniciar a sincronizar os metadados para ficheiros de instalação rápida do Windows 10, tem de ativá-la nas propriedades do ponto de atualização de Software.
1.  Na consola do Configuration Manager, navegue até à **administração** > **configuração do Site** > **Sites**.
2.  Selecione o site de administração central ou site primário autónomo.
3.  No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**. No **ficheiros de atualização** separador, selecione **transferir ficheiros completos de todas as atualizações aprovadas e ficheiros de instalação rápida para o Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para ativar o suporte para os clientes transferir e instalar ficheiros de instalação rápida
Para ativar o suporte de ficheiros de instalação rápida nos clientes, tem de ativar os ficheiros de instalação rápida nos clientes na secção de definições de cliente de atualizações de Software. Esta ação cria um serviço de escuta HTTP novo que escuta pedidos transferir ficheiros de instalação rápida na porta que especificar. Depois de implementar as definições de cliente para ativar esta funcionalidade no cliente, a tentativa de transferir as diferenças entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior (os clientes têm de executar uma versão do Windows 10 que suporta ficheiros de instalação rápida).
1.  Ative o suporte para ficheiros de instalação rápida nas propriedades do componente de ponto de atualização de Software (procedimento anterior).
2.  Na consola do Configuration Manager, navegue até à **administração** > **as definições de cliente**.
3.  Selecione as definições de cliente adequado, em seguida, no **home page** separador, clique em **propriedades**.
4.  Selecione o **atualizações de Software** página, configure **Sim** para o **ativar instalação de atualizações rápida nos clientes** definir e configurar a porta utilizada pelo serviço de escuta HTTP no cliente para o **porta utilizada para transferir conteúdo para atualizações de Express** definição.


## <a name="odata-endpoint-data-access"></a>Acesso de dados de ponto final de OData

 Configuration Manager fornece agora um ponto final de RESTful OData para aceder a dados do Configuration Manager. O ponto final é compatível com a versão 4, que ativa as ferramentas como o Excel e o Power BI para aceder facilmente aos dados do Configuration Manager através de um único ponto final de Odata. Technical Preview 1612 só suporta acesso de leitura para objetos no Configuration Manager.  

Dados que estão atualmente disponíveis no [fornecedor do Configuration Manager WMI](/sccm/develop/reference/configuration-manager-reference) também está agora acessível com o novo ponto de final de OData RESTful. Os conjuntos de entidade expostos pelo ponto final de OData permitem-lhe enumerar sobre os mesmos dados, pode consultar com o fornecedor WMI.

### <a name="try-it-out"></a>Experimente

Antes de poder utilizar o ponto final de OData, tem de ativá-la para o site.

1.  Aceda a **administração** > **configuração do Site** > **Sites**.
2.  Selecione o site primário e clique em **propriedades**.
3.  No separador Geral da folha de propriedades de site primário, clique em **REST de ativar o ponto final para todos os fornecedores neste site**e, em seguida, clique em **OK**.

No seu Visualizador de consulta de OData favorito, tente consultas semelhantes para os exemplos seguintes para devolver vários objetos no Configuration Manager:

| Objetivo | Consulta de OData |
|---|---|
| Obter todas as coleções | `http://localhost/CMRestProvider/Collection` |
| Obter uma coleção | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Obter superiores 100 dispositivos na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Obter um dispositivo com um ID de recurso na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Obter o sistema operativo do dispositivo na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Obter os utilizadores na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> As consultas de exemplo mostradas a utilização de tabela *localhost* como o anfitrião de nome no URL e pode ser utilizado no computador com o fornecedor de SMS. Se estiver a executar as suas consultas a partir de um computador diferente, substitua localhost o FQDN do servidor com o fornecedor de SMS instalado.

## <a name="azure-active-directory-onboarding"></a>Integração do Active Directory do Azure

A integração do Active Directory (AD) do Azure cria uma ligação entre o Configuration Manager e o Azure Active Directory para ser utilizado por outros serviços em nuvem. Atualmente pode ser utilizado para criar a ligação necessária para o Gateway de gestão de nuvem.

Execute esta tarefa com o administrador do Azure, pois terá as credenciais de administrador do Azure.

#### <a name="to-create-the-connection"></a>Para criar a ligação:

2. No **administração** área de trabalho, escolha **serviços em nuvem** > **do Azure Active Directory** > **adicionar do Azure Active Directory**.
2. Escolha **sessão** para criar a ligação com o Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Requisitos do cliente do Configuration Manager

Existem vários requisitos para ativar a criação da política de utilizador no Gateway de gestão de nuvem.

- O processo de integração do Azure AD tem de ser concluído e o cliente tem de ser inicialmente ligado à rede da empresa para obter as informações de ligação.
- Os clientes tem de ser ambos associados a um domínio (registado nos Active Directory) e na nuvem-associados a um domínio (registado no Azure AD).
- Tem de executar [deteção de utilizador do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#active-directory-user-discovery#active-directory-user-discovery).
- Tem de modificar o cliente do Configuration Manager para permitir pedidos de política de utilizador através da Internet e implementar a alteração ao cliente. Porque esta alteração para o cliente tem lugar *no dispositivo cliente*, podem ser implementada através do Gateway de gestão de nuvem, apesar de não concluídas as alterações de configuração necessárias para a política de utilizador.
- O ponto de gestão tem de ser configurado para utilizar HTTPS para proteger o token na rede e tem de ter o .net 4.5 instalados.

Depois de efetuar estas alterações de configuração, pode criar uma política de utilizador e mover clientes à Internet para testar a política. Pedidos de política de utilizador através do Gateway de gestão de nuvem serão autenticados com a autenticação baseada em tokens do AD do Azure.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Alterar para configurar a autenticação multifator para inscrição de dispositivos

Agora que pode configurar a autenticação multifator (MFA) para inscrição de dispositivos no portal do Azure, a opção de MFA foi removida na consola do Configuration Manager. Pode encontrar mais informações sobre como configurar a MFA para inscrição [neste tópico do Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/multi-factor-authentication-azure-active-directory).
