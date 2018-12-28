---
title: Funcionalidades no Technical Preview versão 1612
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão versão 1612.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 24f1d08fedfc09a190739182d7858772745fb3fe
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423376"
---
# <a name="capabilities-in-technical-preview-1612-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1612 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão versão 1612. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="the-data-warehouse-service-point"></a>O ponto de serviço de armazém de dados
A partir da versão do Technical Preview versão 1612, o ponto de serviço de armazém de dados permite-lhe armazenar e gerar relatórios sobre dados históricos de longo prazo para a sua implementação do Configuration Manager. Isto é conseguido ao sincronizações automáticas da base de dados do site do Configuration Manager para uma base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do ponto do Reporting services.

Por predefinição, ao instalar a nova função de sistema de sites, do Configuration Manager cria a base de dados do armazém de dados para numa instância do SQL Server que especificou. O armazém de dados suporta até 2 TB de dados, carimbos de data de registo de alterações.  Por predefinição, os dados que são sincronizados a partir da base de dados do site incluem os grupos de dados para dados globais, os dados do Site, Global_Proxy, dados na Cloud e vistas da base de dados. Também pode modificar o que é sincronizado para incluir tabelas adicionais, ou excluir tabelas específicas dos conjuntos de replicação predefinido.
Os dados de predefinição que são sincronizados incluem informações sobre:
- Estado de funcionamento da infraestrutura
- Segurança
- Conformidade
- Software maligno   
- Implementações de software
- Detalhes de inventário (no entanto, o histórico de inventário não está sincronizado)

Além de instalar e configurar a base de dados do armazém de dados, vários novos relatórios são instalados para que o utilizador pode procurar facilmente e gerar relatórios sobre estes dados.

### <a name="data-warehouse-dataflow"></a>Fluxo de dados de armazém de dados   
![Datawarehouse_flow](./media/datawarehouse.png)

| Passo         | Detalhes  |
|:------:|-----------|  
| **1**  |  O servidor do site transfere e armazena dados na base de dados do site.  |  
| **2** |   Com base na sua agenda e a configuração, o ponto de serviço de armazém de dados obtém os dados da base de dados do site.  |  
| **3** |  O ponto de serviço de armazém de dados transferidos e armazena uma cópia dos dados sincronizados na base de dados do armazém de dados. |  
| **A** |  Utilizar relatórios incorporados, para dados é feito um pedido que é passado para o Reporting Services apontar usando o SQL Server Reporting Services. |  
| **B** |   A maioria dos relatórios são para obter informações atuais, e estes pedidos são executados na base de dados do site. |  
| **C** | Quando um relatório solicita dados históricos, utilizando um dos relatórios com uma *categoria* dos **armazém de dados**, a solicitação será executada na base de dados do armazém de dados.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Pré-requisitos para o ponto de serviço de armazém de dados e a base de dados
- A hierarquia tem de ter do Reporting services, do ponto de função de sistema de sites instalada.
- O computador onde instalou a função de sistema de sites requer o .NET Framework 4.5.2 ou posterior.
- A conta de computador do computador onde instalou a função de sistema de sites tem de ter permissões de administrador local no computador que alojará a base de dados do armazém de dados.
- A conta administrativa que utilizar para instalar a função de sistema de sites tem de ser um DBO na instância do SQL Server que alojará a base de dados do armazém de dados.  
- A base de dados é suportada:
  - Com o SQL Server 2012 ou posterior, Enterprise ou Datacenter edition.
  - Numa instância predefinida ou nomeada
  - Num *Cluster do SQL Server*. Embora esta configuração funcione, ele não foi testado e o suporte é melhor esforço.
  - Quando localizado conjuntamente com ambos a base de dados do site ou a base de dados de ponto de serviços de relatório. No entanto, recomendamos que ele ser instalado num servidor separado.  
- A conta que é utilizada como o *conta do ponto de Reporting Services* tem de ter o **db_datareader** permissão para a base de dados do armazém de dados.  
- A base de dados não é suportado numa *grupo de Disponibilidade AlwaysOn do SQL Server*.

### <a name="install-the-data-warehouse"></a>Instalar o armazém de dados
Instalar a função de sistema de sites do armazém de dados num site de administração central ou site primário utilizando o **Adicionar Assistente de funções de sistema de sites** ou o **criar Assistente de servidor de sistema de sites**. Ver [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles) para obter mais informações. A hierarquia suporta várias instâncias desta função, mas apenas uma instância é suportada em cada site.  

Quando instalar a função, o Configuration Manager cria a base de dados do armazém de dados para na instância do SQL Server que especificou. Se especificar o nome da base de dados existente (como faria se [mover a base de dados do armazém de dados para um novo servidor SQL](#move-the-data-warehouse-database)), o Configuration Manager não cria uma nova base de dados, mas usa aquele que especificar.

#### <a name="configurations-used-during-installation"></a>Configurações utilizadas durante a instalação
Utilize as seguintes informações para concluir a instalação da função de sistema do site:

**Seleção da função do sistema** página:  
Antes do assistente apresenta uma opção para selecionar e instalar o ponto de serviço de armazém de dados, deve ter instalado um ponto do Reporting services.

**Geral** página: As seguintes informações gerais, é necessárias:
- **Definições de base de dados do Configuration Manager:**   
  - **Nome do servidor** -especifique o FQDN do servidor que aloja a base de dados do site. Se não utilizar uma instância predefinida do SQL Server, tem de especificar a instância depois do FQDN no seguinte formato: ***&lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **Nome da base de dados** -especifique o nome da base de dados do site.
  - **Certifique-se** -clique em **verificar** para se certificar de que a ligação à base de dados do site é efetuada com êxito.
</br></br>
- **Definições de base de dados do armazém de dados:**
  - **Nome do servidor** - especifique o FQDN do servidor que aloja o ponto de serviço de armazém de dados e de base de dados. Se não utilizar uma instância predefinida do SQL Server, tem de especificar a instância depois do FQDN no seguinte formato: ***&lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **Nome da base de dados** -especifique o FQDN para a base de dados do armazém de dados.  Configuration Manager irá criar a base de dados com este nome. Se especificar um nome de base de dados que já existe na instância do SQL server, o Configuration Manager irá utilizar essa base de dados.
  - **Certifique-se** -clique em **verificar** para se certificar de que a ligação à base de dados do site é efetuada com êxito.

**As definições de sincronização** página:   
- **Definições de dados:**
  - **Grupos de replicação para sincronizar** – selecione os grupos de dados que pretende sincronizar. Para obter informações sobre os diferentes tipos de grupos de dados, consulte [replicação de base de dados](/sccm/core/servers/manage/data-transfers-between-sites#a-namebkmkdbrepa-database-replication) e **vistas distribuídas** na [transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites).
  - **Tabelas incluídas para sincronizar** – especifique o nome de cada tabela adicional que pretende sincronizar. Separe várias tabelas com uma vírgula. Estas tabelas irão ser sincronizadas a partir da base de dados do site, além de selecionar os grupos de replicação.
  - **Tabelas excluídos para sincronizar** -especifique o nome de tabelas individuais a partir de grupos de replicação sincronizar. Tabelas que especificar serão excluídas. Separe várias tabelas com uma vírgula.
- **Definições de sincronização:**
  - **Intervalo de sincronização (minutos)** -Especifique um valor em minutos. Quando o intervalo é alcançado, inicia uma sincronização de novo. Isso oferece suporte a um intervalo de 60 a 1440 minutos (24 horas).
  - **Agenda** -especifique os dias em que pretende que a sincronização para ser executada.

**Acesso de ponto de Reporting**:   
Após a função de armazém de dados está instalada, certifique-se a conta que é utilizada como o *conta do ponto de Reporting Services* tem o **db_datareader** permissão para a base de dados do armazém de dados.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Resolver problemas de sincronização de dados e de instalação
Utilize os seguintes registos para investigar problemas com a instalação do ponto de serviço de armazém de dados, ou a sincronização de dados:
- **DWSSMSI.log** e **DWSSSetup.log** -utilizar estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
-   **Microsoft.ConfigMgrDataWarehouse.log** – Utilize este registo para investigar a sincronização de dados entre a base de dados na base de dados do armazém de dados.

### <a name="reporting"></a>Relatórios
Depois de instalar uma função de sistema de sites do armazém de dados, os seguintes relatórios estão disponíveis no seu ponto do Reporting services com uma *categoria* de **armazém de dados:**

|Relatório                   | Detalhes                                  |
|-------------------------|------------------------------------------|
| **Relatório de implantação de aplicativos** | Ver os detalhes para a implementação de aplicação para uma aplicação específica e a máquina.|
| **Endpoint Protection e o relatório de conformidade de atualização de Software**   | Ver os computadores que estão em falta atualizações de software.|
| **Relatório de inventário de Hardware geral**  | Ver todo o inventário de hardware de uma máquina específica.|
| **Relatório de inventário de Software geral**  | Ver todo o inventário de software para uma máquina específica.|
| **Descrição geral do Estado de funcionamento de infraestrutura**  |Apresenta uma visão geral do Estado de funcionamento da sua infraestrutura do Configuration Manager.|
| **Lista de software maligno detetado**  |Software maligno do modo de exibição que foi detetado na organização.|
| **Relatório de resumo de distribuição de software** | Um resumo da distribuição de software para um anúncio específico e a máquina.|

### <a name="move-the-data-warehouse-database"></a>Mover a base de dados do armazém de dados
Utilize os seguintes passos para mover a base de dados do armazém de dados para um novo servidor SQL:

1. Reveja a configuração de base de dados atual e registe os detalhes de configuração, incluindo:  
   - Os grupos de dados que sincronizar
   - Tabelas incluir ou excluir da sincronização       

   Irá reconfigurar a estes grupos de dados e tabelas depois de restaurar a base de dados para um novo servidor e reinstalar a função de sistema de sites.  

2. Utilizar o SQL Server Management Studio para a base de dados do armazém de dados, de cópia de segurança e, em seguida, novamente para restaurar a base de dados para um SQL server no novo computador que irá alojar o armazém de dados.

   Depois de restaurar a base de dados para o novo servidor, certifique-se de que as permissões de acesso de base de dados são os mesmos sobre a nova base de dados de armazém de dados tal como estavam na base de dados de armazém de dados original.

3. Utilize a consola do Configuration Manager para remover a função de sistema de sites de ponto de serviço de armazém de dados do servidor atual.

4. Instalar um novo ponto de serviço de armazém de dados e especifique o nome do novo SQL Server e instância que aloja a base de dados do armazém de dados que é restaurada.

5. Depois de instala a função de sistema de sites, a migração está concluída.

Pode rever os seguintes registos do Configuration Manager para confirmar que a função de sistema do site reinstalou com êxito:  
- **DWSSMSI.log** e **DWSSSetup.log** -utilizar estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
-   **Microsoft.ConfigMgrDataWarehouse.log** – Utilize este registo para investigar a sincronização de dados entre a base de dados na base de dados do armazém de dados.


## <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos
A partir da versão de Technical Preview versão 1612, pode usar uma nova ferramenta de linha de comandos (**ContentLibraryCleanup.exe**) remover o conteúdo que é mais longo para não associado a nenhum pacote ou aplicação a partir de um ponto de distribuição (órfão conteúdo). Essa ferramenta denomina-se a ferramenta de limpeza da biblioteca de conteúdos.

Essa ferramenta só afeta o conteúdo no ponto de distribuição que especificou quando executa a ferramenta e não é possível remover o conteúdo da biblioteca de conteúdos no servidor do site.

Depois de instalar 1612 de pré-visualização técnica, pode encontrar **ContentLibraryCleanup.exe** no \*%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* pasta no servidor do site de pré-visualização técnica.

A ferramenta lançada com este Technical Preview destina-se para substituir as versões mais antigas ferramentas semelhantes foram lançadas nos últimos produtos do Configuration Manager. Embora esta versão da ferramenta deixará de funcionar após 1 de Março de 2017, as novas versões vão lançar com futuras Technical Previews até ao momento em que esta ferramenta é lançada como parte do ramo atual, ou uma versão fora de banda pronto para produção.

### <a name="requirements"></a>Requisitos  
 - A ferramenta pode ser executada diretamente no computador que aloja o ponto de distribuição, ou remotamente a partir de outro servidor. A ferramenta só pode ser executada num único ponto de distribuição de cada vez.
 - A conta de utilizador que executa a ferramenta diretamente tem de ter permissões de administração baseada em funções que sejam iguais a um administrador total na hierarquia do Configuration Manager.  A ferramenta não funciona quando é concedidas permissões de conta de utilizador como membro de um grupo de segurança do Windows que tem as permissões de administrador completo.

### <a name="modes-of-operation"></a>Modos de funcionamento
A ferramenta pode ser executada em dois modos:
1. **Modo de hipóteses**:   
   Se não especificar a **/eliminar** comutador, a ferramenta é executado no modo de hipóteses e identifica os conteúdos que serão eliminados do ponto de distribuição, mas não eliminar, na verdade, todos os dados.

   - Quando a ferramenta é executada neste modo, as informações sobre o conteúdo que será eliminado automaticamente são escritas para o ficheiro de registo de ferramentas. Não é pedido ao utilizador para confirmar a cada eliminação potencial.
   - Por predefinição, o ficheiro de registo é escrito para a pasta temp do utilizador no computador em que executou a ferramenta, no entanto, pode utilizar o comutador de /log para redirecionar o ficheiro de registo para outra localização.  
   </br>

   Recomendamos que execute a ferramenta neste modo e rever o ficheiro de registo resultante antes de executar a ferramenta com a opção /delete.  

2. **Eliminar modo**: Quando executa a ferramenta com o **/eliminar** comutador, a ferramenta é executada no modo de eliminação.

   - Quando a ferramenta é executada neste modo, o conteúdo órfão que se encontra no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.
   -  Antes de excluir cada arquivo, é pedido ao utilizador para confirmar que o ficheiro deve ser eliminado.  Pode selecionar, **Y** para Sim, **N** para não, ou **Sim para todos os** para ignorar a outros prompts e eliminar conteúdo órfão tudo.  
   </br>

   Recomendamos que execute a ferramenta no modo de hipóteses e rever o ficheiro de registo resultante antes de executar a ferramenta com a opção /delete.  

Quando a ferramenta de limpeza da biblioteca de conteúdos é executado no modo de ambos, este cria automaticamente um registo com um nome que inclui o modo da que ferramenta é executada, o nome do ponto de distribuição, a data e a hora da operação. O ficheiro de registo abre-se automaticamente quando a ferramenta é concluída. Por predefinição, este registo é escrito para os usuários **temp** pasta no computador em que executou a ferramenta., no entanto, pode utilizar um comutador de linha de comandos para redirecionar o ficheiro de registo para outro local, incluindo um compartilhamento de rede.   


### <a name="run-the-tool"></a>Execute a ferramenta
Para executar a ferramenta:
1. Abra uma linha de comandos administrativa para uma pasta que contém **ContentLibraryCleanup.exe**.  
2. Em seguida, introduza uma linha de comando que inclui as opções de linha de comandos necessários e opcionais comutadores que pretende utilizar.

**Problema conhecido** quando a ferramenta é executada, pode ser devolvido um erro semelhante ao seguinte, quando nenhum pacote ou implementação falhou ou está em curso:
-  *System.InvalidOperationException: Nesta biblioteca de conteúdos não é possível limpar neste momento porque o pacote <packageID> não está totalmente instalado.*

**Solução:** Nenhuma. A ferramenta não é confiável identificar arquivos órfãos quando o conteúdo está em curso ou falhou a implementação. Por conseguinte, a ferramenta não permitirá que para limpar o conteúdo até que esse problema foi resolvido.



### <a name="command-line-switches"></a>Opções de linha de comandos  
Os seguintes parâmetros de linha de comandos podem ser utilizados por qualquer ordem.   

|Parâmetro|Detalhes|
|---------|-------|
|**/delete**  |**Opcional** </br> Use esta opção quando pretender eliminar o conteúdo do ponto de distribuição. É pedido antes do conteúdo é eliminado. </br></br> Quando este comutador não for utilizado, a ferramenta regista resultados sobre o conteúdo que será eliminado, mas não eliminar a qualquer conteúdo a partir do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Execute a ferramenta no modo silencioso, que suprime todas as instruções (assim como nos prompts quando exclui conteúdo) e não abrir automaticamente o ficheiro de registo. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN do ponto de distribuição >**  | **Necessário** </br> Especifique o nome de domínio completamente qualificado (FQDN) do ponto de distribuição que pretende limpar. </br></br> Exemplo:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/PS &lt;site primário de FQDN >**       | **Opcional** quando limpar o conteúdo de um ponto de distribuição num site primário.</br>**Necessário** quando limpar o conteúdo de um ponto de distribuição num site secundário. </br></br> Especifique o FQDN do ponto de distribuição do site primário pertence para ou do principal primário principal, quando o ponto de distribuição estiver num site secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código do site primário >**  | **Opcional** quando limpar o conteúdo de um ponto de distribuição num site primário.</br>**Necessário** quando limpar o conteúdo de um ponto de distribuição num site secundário. </br></br> Especifique o código do site do site primário que pertence o ponto de distribuição ou de site primário principal, quando o ponto de distribuição estiver num site secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Opcional** </br> Especifique um diretório para colocar os arquivos de log. Isso pode ser uma unidade local ou numa rede de partilhar.</br></br> Quando este comutador não for utilizado, ficheiros de registo são automaticamente colocados na pasta temp do utilizador.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de compartilhamento de rede: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\ &lt;partilhar >\&lt; pasta >***|


## <a name="improvements-for-in-console-search"></a>Aprimoramentos de pesquisa na consola
Com base nos comentários do Uservoice, adicionámos as seguintes melhorias à pesquisa na consola:
 - **Caminho do objeto:**  
  Muitos objetos suportam agora uma nova coluna chamada **caminho do objeto**.  Ao pesquisar e inclua esta coluna nos resultados de sua apresentação, pode ver o caminho para cada objeto. Por exemplo, se executar uma pesquisa para as aplicações no nó Applications e também é pesquisar sub-nós, o *caminho do objeto* coluna no painel de resultados mostram-lhe o caminho para cada objeto retornado.   

- **Preservação do texto de pesquisa:**  
  Quando inserir texto na caixa de texto de pesquisa e, em seguida, alternar entre pesquisando um nó secundário e o nó atual, o texto digitado será manter e permanecem disponível para uma nova pesquisa sem ter de redigitá-lo.

- **Preservação da sua decisão de pesquisar sub-nós:**  
 A opção que selecionar para a pesquisa a *nó atual* ou *todos os nós secundários* agora persistir quando altera o nó que está a trabalhar.   Esse novo comportamento significa que não é necessário repor constantemente a decisão medida que navega da consola.  Por predefinição, quando abrir a consola, a opção é pesquisar apenas o nó atual.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Impedi a instalação de um aplicativo se estiver a executar um programa especificado.
Agora pode configurar uma lista de ficheiros executáveis (com a extensão .exe) nas propriedades de tipo de implementação que, se executar, irão bloquear a instalação de um aplicativo. Após a instalação for tentada, os utilizadores verão uma caixa de diálogo solicitando-los para fechar os processos que estão a bloquear instalação.

### <a name="try-it-out"></a>Experimentar
Para configurar uma lista de ficheiros executáveis
1.  Na página de propriedades de qualquer tipo de implementação, selecione o **manipulação do instalador** separador.
2.  Clique em **Add**, para adicionar um dos mais ficheiros executáveis para a lista (por exemplo **Edge.exe**)
3.  Clique em **OK** para fechar a caixa de diálogo de propriedades de tipo de implementação.

Agora, quando implementar esta aplicação para um utilizador ou um dispositivo e um dos executáveis que adicionou está em execução, o utilizador final verá uma caixa de diálogo do Centro de Software informando-o de que a instalação falhou porque um aplicativo está em execução.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Novo Windows Hello para notificação de negócios para os utilizadores finais

Uma nova notificação do Windows 10 informa os utilizadores finais que têm de realizar ações adicionais para concluir Windows Hello para a configuração de negócio (por exemplo, configuração de um PIN).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Windows Store para suporte de negócio no Configuration Manager

Agora, pode implementar aplicações licenciadas online com um objetivo de implementação **disponível** partir da Windows Store para empresas para PCs a executar o cliente do Configuration Manager.
Para obter mais detalhes, consulte [gerir aplicações a partir da Windows Store para empresas com o System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

Suporte para esta funcionalidade só está atualmente disponível para PCs que executam a versão de pré-visualização do Windows 10 RS2.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior quando ocorre uma falha de uma sequência de tarefas
Agora pode retornar a uma página anterior quando executa uma sequência de tarefas e de falha. Antes desta versão, tinha que reinicie a sequência de tarefas quando ocorreu uma falha. Por exemplo, pode utilizar o **Previous** botão nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar-se antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas é apresentada uma mensagem que não há nenhum sequências de tarefas disponíveis. Agora, pode clicar **Previous** para procurar novamente sequências de tarefas disponíveis. Pode repetir esse processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdo dependentes ainda não estão disponíveis em pontos de distribuição, a sequência de tarefas falhará. Pode agora distribuir o conteúdo em falta (se não foi distribuída ainda) ou aguardar que o conteúdo fique disponível nos pontos de distribuição e, em seguida, clique em **Previous** para que a pesquisa de sequência de tarefas novamente para o conteúdo.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Suporte para atualizações do Windows 10 de ficheiros de instalação rápida
Adicionámos no Configuration Manager de suporte de ficheiros de instalação rápida para atualizações do Windows 10. Quando utiliza uma versão suportada do Windows 10, agora, pode utilizar as definições do Gestor de configuração para transferir apenas o delta entre Windows 10 Cumulative Update o mês atual e atualização deste mês anterior. Atualmente no Configuration Manager Current Branch, o total Windows 10 Cumulative Update (incluindo todas as atualizações dos meses anteriores) são transferidos por mês. A utilização de ficheiros de instalação rápida fornece para transferências mais pequenas e tempos de instalação mais rápidos nos clientes.

> [!IMPORTANT]
> Enquanto as definições para suportar a utilização de ficheiros de instalação rápida está disponível no Configuration Manager, esta funcionalidade só é suportada no Windows 10 versão 1607 com uma atualização do Windows Update Agent incluído com as atualizações publicadas no dia 10 de Janeiro de 2017 ( Patch Terça-feira). Para obter mais informações sobre estas atualizações, consulte [3213986 do artigo de suporte](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Pode tirar partido dos ficheiros de instalação rápida quando o próximo conjunto de atualizações são lançadas a 14 de Fevereiro de 2017. Windows 10 versão 1607 sem a atualização e as versões anteriores não suportam ficheiros de instalação rápida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Para ativar a transferência de ficheiros de instalação rápida para atualizações do Windows 10 no servidor
Para começar a sincronizar os metadados para ficheiros de instalação rápida do Windows 10, tem de ativá-la nas propriedades do ponto de atualização de Software.
1.  Na consola do Configuration Manager, navegue até **Administration** > **configuração do Site** > **Sites**.
2.  Selecione o site de administração central ou site primário autónomo.
3.  No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**. Sobre o **ficheiros de atualização** separador, selecione **transfira ficheiros completos de todas as atualizações aprovadas e ficheiros de instalação rápida para o Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para ativar o suporte para clientes transferir e instalar ficheiros de instalação rápida
Para ativar o suporte de ficheiros de instalação rápida nos clientes, tem de ativar os ficheiros de instalação rápida nos clientes, na secção de definições de cliente de atualizações de Software. Esta ação cria um novo ouvinte HTTP que escuta pedidos transferir ficheiros de instalação rápida na porta que especificar. Depois de implementar as definições de cliente para ativar esta funcionalidade no cliente, ele irá tentar transferir o delta entre Windows 10 Cumulative Update o mês atual e atualização deste mês anterior (os clientes têm de executar uma versão do Windows 10, que oferece suporte a express ficheiros de instalação).
1.  Ative o suporte para ficheiros de instalação rápida nas propriedades do componente de ponto de atualização de Software (procedimento anterior).
2.  Na consola do Configuration Manager, navegue até **Administration** > **definições de cliente**.
3.  Selecione as definições de cliente adequado, em seguida, no **home page** separador, clique em **propriedades**.
4.  Selecione o **atualizações de Software** página, configure **Sim** para o **ativar a instalação de atualizações de Express em clientes** definir e configurar a porta utilizada pelo serviço de escuta HTTP no cliente para o **porta utilizada para transferir conteúdo para atualizações de Express** definição.


## <a name="odata-endpoint-data-access"></a>Acesso de dados do ponto final de OData

 Agora o Configuration Manager fornece um ponto de extremidade RESTful OData para aceder a dados do Configuration Manager. O ponto final é compatível com a versão 4, que permite que ferramentas como o Excel e o Power BI para aceder facilmente a dados do Configuration Manager por meio de um único ponto final do Odata. Versão 1612 de pré-visualização técnica só suporta acesso de leitura a objetos no Configuration Manager.  

Dados que estão atualmente disponíveis na [fornecedor de WMI do Configuration Manager](/sccm/develop/reference/configuration-manager-reference) também está agora acessível com o novo ponto de final RESTful do OData. Os conjuntos de entidades expostos pelo ponto de extremidade OData permitem-lhe enumerar os mesmos dados que pode consultar com o fornecedor WMI.

### <a name="try-it-out"></a>Experimentar

Antes de poder utilizar o ponto final OData, tem de ativá-la para o site.

1.  Aceda a **Administration** > **configuração do Site** > **Sites**.
2.  Selecione o site primário e clique em **propriedades**.
3.  Na guia Geral da folha de propriedades do site primário, clique em **ponto final de ativar o REST para todos os fornecedores neste site**e, em seguida, clique em **OK**.

Em seu Visualizador de consulta de OData favorito, tente consultas semelhantes para os exemplos seguintes para retornar vários objetos no Configuration Manager:

| Objetivo | Consulta de OData |
|---|---|
| Obter todas as coleções | `http://localhost/CMRestProvider/Collection` |
| Obter uma coleção | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Obter os dispositivos de 100 principais na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Obter um dispositivo com um ID de recurso da coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Obter o sistema operativo do dispositivo da coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Obter os utilizadores na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> As consultas de exemplo mostradas a utilização de tabela *localhost* como host dê um nome no URL e pode ser utilizado no computador com o fornecedor de SMS. Se estiver a executar as suas consultas num computador diferente, substitua localhost o FQDN do servidor com o fornecedor de SMS instalado.

## <a name="azure-active-directory-onboarding"></a>Integração do Active Directory do Azure

Integração do Active Directory (AD) do Azure cria uma ligação entre o Configuration Manager e o Azure Active Directory para ser utilizado por outros serviços em nuvem. Atualmente pode ser utilizado para criar a ligação necessária para o Gateway de gestão na Cloud.

Execute esta tarefa com o administrador do Azure, pois irá precisar do credenciais de administrador do Azure.

#### <a name="to-create-the-connection"></a>Para criar a ligação:

2. Na **administração** área de trabalho, escolha **serviços Cloud** > **do Azure Active Directory** > **adicionar Azure Active Directory Diretório**.
2. Escolher **sessão** para criar a ligação com o Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Requisitos do cliente do Configuration Manager

Existem vários requisitos para ativar a criação de política de utilizador no Gateway de gestão na Cloud.

- O processo de integração do Azure AD tem de ser concluído e o cliente tem de ser inicialmente ligado à rede da empresa para obter as informações de ligação.
- Os clientes devem ser ambos associados a um domínio (registado no Active Directory) e na cloud-associados a um domínio (registado no Azure AD).
- Tem de executar [deteção de utilizador do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#active-directory-user-discovery#active-directory-user-discovery).
- Tem de modificar o cliente do Configuration Manager para permitir pedidos de política de utilizador através da Internet e implementar a alteração para o cliente. Uma vez que esta alteração para o cliente é efetuada *no dispositivo cliente*, pode ser implementado através do Gateway de gestão na Cloud, embora ainda não concluiu as alterações de configuração necessárias para a política de utilizador.
- O ponto de gestão tem de ser configurado para utilizar HTTPS para proteger o token na rede e tem de ter o .net 4.5 instalado.

Depois de efetuar estas alterações de configuração, pode criar uma política de utilizador e mover os clientes para a Internet para testar a política. Pedidos de política de utilizador através do Gateway de gestão na Cloud serão autenticados com autenticação baseada em tokens do AD do Azure.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Alterar a configuração da autenticação multifator para inscrição de dispositivos

Agora que pode configurar a autenticação multifator (MFA) para inscrição de dispositivos no portal do Azure, a opção de MFA foi removida na consola do Configuration Manager. Pode encontrar mais informações sobre como configurar a MFA para inscrição [neste tópico do Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/multi-factor-authentication-azure-active-directory).
