---
title: "Criar mídia autônoma com o System Center Configuration Manager | Microsoft Docs"
description: "Use mídia autônoma para implantar o sistema operacional em um computador sem uma conexão a um site do Configuration Manager ou a rede."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
caps.latest.revision: 21
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 98f902429ad1b9965a0dc4cc2e1bd071ad5c0779
ms.contentlocale: pt-pt
ms.lasthandoff: 06/08/2017


---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Criar suportes de dados autónomos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

No Gerenciador de configurações de mídia autônoma contém tudo o que é necessário para implantar o sistema operacional em um computador sem uma conexão a um site do Configuration Manager ou usando a rede. Use mídia autônoma nos seguintes cenários de implantação de sistema operacional:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Atualize o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

A mídia autônoma inclui a sequência de tarefas que automatiza as etapas para instalar o sistema operacional e qualquer outro conteúdo necessário, inclusive a imagem de inicialização, imagem do sistema operacional e drivers de dispositivo. Como tudo o que é necessário para implementar o sistema operativo está armazenado no suporte de dados autónomo, o espaço em disco necessário para o suporte de dados autónomo é significativamente maior do que o espaço em disco necessário para outros tipos de suportes de dados. Quando cria suportes de dados autónomo num site de administração central, o cliente irá obter o código de site atribuído do active directory. O suporte de dados autónomo criado em sites subordinados atribuirá automaticamente ao cliente o código do site para esse site.  

##  <a name="BKMK_CreateStandAloneMedia"></a>Criar mídia autônoma  
Antes de criar mídia autônoma usando o Assistente para criar de mídia de sequência de tarefas, certifique-se de que as seguintes condições forem atendidas:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Criar uma sequência de tarefas para implementar um sistema operativo
Como parte do suporte de dados autónomo, tem de especificar a sequência de tarefas para implementar um sistema operativo. Para obter as etapas criar uma nova sequência de tarefas, consulte [criar uma sequência de tarefas para instalar um sistema operacional no System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Não há suporte para as seguintes ações para mídia autônoma:
- O passo Aplicar Controladores Automaticamente na sequência de tarefas. A aplicação automática de controladores de dispositivo a partir do catálogo de controladores não é suportada, mas pode escolher o passo Aplicar Pacote de Controlador para disponibilizar um conjunto especificado de controladores à Configuração do Windows.
- Etapa de baixar conteúdo do pacote na sequência de tarefas. As informações de ponto de gerenciamento não estão disponíveis na mídia autônoma, portanto, que a etapa falhará ao tentar enumerar locais de conteúdo.
- Instalação de atualizações de software.
- Instalação do software antes de implantar o sistema operacional.
- Sequências de tarefas para implantações de sistema de operacional.
- Associação de utilizadores ao computador de destino para suportar a afinidade dispositivo/utilizador.
- O pacote dinâmico é instalado através da tarefa Instalar Pacotes.
- A aplicação dinâmica é instalada através da tarefa Instalar Aplicação.

> [!NOTE]    
> Se a sequência de tarefas para implantar um sistema operacional incluir a [instalar pacote](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) etapa e criar a mídia autônoma em um site de administração central, pode ocorrer um erro. O site de administração central não possui as políticas de configuração de cliente necessárias para ativar o agente de distribuição de software durante a execução da sequência de tarefas. O erro seguinte pode ser apresentado no ficheiro CreateTsMedia.log:    
>     
> "Falha do método WMI SMS_TaskSequencePackage.GetClientConfigPolicies (0x80041001)"    
> 
> Para mídia autônoma que inclui um **instalar pacote** etapa, você deve criar a mídia autônoma em um site primário que tem o agente de distribuição de software habilitado ou adicionar um [executar linha de comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) etapa após o [instalação do Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) etapa e antes da primeira **instalar pacote** etapa na sequência de tarefas. O passo **Executar Linha de Comandos** executa um comando WMIC para ativar o agente de distribuição de software antes da execução do primeiro passo Instalar Pacote. Pode utilizar o seguinte no passo da sequência de tarefas **Executar Linha de Comandos** :    
>    
> *WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName = "Enable SWDist", Enabled = "true", LockSettings = "TRUE", PolicySource = "local", PolicyVersion = "1.0", SiteSettingsKey = "1" /NOINTERACTIVE*


> [!IMPORTANT]    
> Quando você usa o **instalação do Windows e ConfigMgr** sequência de tarefas na sequência de tarefas de sistema operacional, não selecione a **usar pacote de cliente de pré-produção quando disponível** configuração para mídia autônoma. Se essa configuração está selecionada e o pacote de cliente de pré-produção estiver disponível, ele será usado na mídia autônoma. Não há suporte para isso. Para obter detalhes sobre essa configuração, consulte [instalação do Windows e ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas
Tem de distribuir todo o conteúdo exigido pela sequência de tarefas por, pelo menos, um ponto de distribuição. Isto inclui a imagem de arranque, a imagem do sistema operativo e outros ficheiros associados. O assistente recolhe as informações a partir do ponto de distribuição, ao criar o suporte de dados autónomo. Tem de ter direitos de acesso de **Leitura** à biblioteca de conteúdos desse ponto de distribuição.  Para obter detalhes, veja [Distribuir conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a pen USB amovível
*Para uma unidade USB removível:*

Se planear utilizar uma pen USB amovível, a pen USB tem de estar ligada ao computador em que o assistente é executado e ser detetável pelo Windows como um dispositivo amovível. Quando cria o suporte de dados, o assistente escreve diretamente na pen USB. O suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar um suporte de dados autónomo numa pen USB cujo conteúdo inclua um ficheiro com tamanho superior a 4 GB.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída
*Para um conjunto de CD/DVD:*

Antes de executar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas para criar suportes de dados para um conjunto de CDs ou DVDs, tem de criar uma pasta para os ficheiros de saída criados pelo assistente. O suporte de dados criado para um conjunto de CDs ou DVDs é escrito em formato de ficheiros .iso diretamente na pasta.


 Use o procedimento a seguir para criar mídia autônoma para uma unidade USB removível ou um conjunto de CD/DVD.  

## <a name="to-create-stand-alone-media"></a>Para criar mídia autônoma  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4.  Na página **Selecione o Tipo de Suporte de Dados** , especifique as opções seguintes e clique em **Seguinte**.  

    -   Selecione **mídia autônoma**.  

    -   Opcionalmente, se pretender permitir a implementação do sistema operativo sem exigir a intervenção do utilizador, selecione **Permitir a implementação do sistema operativo autónoma**. Ao selecionar esta opção, não serão solicitadas ao utilizador informações para a configuração de rede nem para sequências de tarefas opcionais. No entanto, continua a ser solicitada uma palavra-passe ao utilizador se o suporte de dados estiver configurado com proteção por palavra-passe.  

5.  Na página **Tipo de Suporte de Dados** , especifique se o suporte de dados é uma pen USB ou um conjunto de CD/DVD e, em seguida, clique para configurar o seguinte:  

    > [!IMPORTANT]  
    >  O suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar um suporte de dados autónomo numa pen USB cujo conteúdo inclua um ficheiro com tamanho superior a 4 GB.  

    -   Se selecionar **Pen USB**, especifique a unidade onde pretende armazenar o conteúdo.  

    -   Se selecionar **Conjunto CD/DVD**, especifique a capacidade do suporte de dados e o nome e caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo:  **\\\servername\folder\outputfile.iso**  

         Se a capacidade do suporte de dados for demasiado pequena para armazenar todo o conteúdo, serão criados vários ficheiros e tem de armazenar o conteúdo em vários CDs ou DVDs. Se várias mídias forem necessárias, o Configuration Manager adiciona um número de sequência ao nome de cada arquivo de saída que ele cria. Além disso, se você implantar um aplicativo juntamente com o sistema operacional e o aplicativo não couber em uma única mídia, o Configuration Manager armazena o aplicativo em várias mídias. Quando a mídia autônoma é executada, o Configuration Manager solicita ao usuário a próxima mídia em que o aplicativo está armazenado.   

         > [!IMPORTANT]  
         >  Se selecionar uma imagem .iso existente, o Assistente de Criação de Suporte de Dados da Sequência de Tarefas elimina essa imagem da unidade ou partilha logo que avança para a página seguinte do assistente. A imagem existente será eliminada, mesmo que em seguida cancele o assistente.  

     Clique em **Seguinte**.  

6.  Sobre o **segurança** página, escolha entre as seguintes configurações e, em seguida, clique em **próximo**:
    - **Proteger mídia com senha**: Insira uma senha forte para ajudar a proteger a mídia. Se você especificar uma senha, a senha é necessária para usar a mídia.  

        > [!IMPORTANT]  
        >  Na mídia autônoma, somente as etapas da sequência de tarefas e suas variáveis são criptografadas. O restante conteúdo do suporte de dados não é encriptado, pelo que não deverá incluir quaisquer informações sensíveis nos scripts da sequência de tarefas. Armazene e implemente todas as informações confidenciais usando variáveis de sequência de tarefas.  

    - **Selecione o intervalo de datas para esta mídia autônoma válido** (começando na versão 1702): Definir datas de início e vencimento opcionais na mídia. Essas configurações são desabilitadas por padrão. As datas são comparadas com a hora do sistema no computador antes de executa a mídia autônoma. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, a mídia autônoma não foi iniciada. Essas opções também estão disponíveis usando o cmdlet New-CMStandaloneMedia do PowerShell.
7.  Sobre o **CD/DVD autônomo** página, especifique a sequência de tarefas que implanta o sistema operacional e, em seguida, clique em **próximo**. Escolha **detectar dependências de aplicativos associados e adicioná-las a esta mídia** para adicionar conteúdo a mídia autônoma para dependências de aplicativos.
    > [!TIP]
    > Se você não vir as dependências de aplicativo esperado, cancele a seleção e, em seguida, selecione novamente o **detectar dependências de aplicativos associados e adicioná-las a esta mídia** configuração para atualizar a lista.

    O assistente permite que você selecione apenas as sequências de tarefas que estão associadas uma imagem de inicialização.  

8. Sobre o **Selecionar aplicativo** página (disponível a partir do versão 1702), especifique o conteúdo do aplicativo para incluir como parte do arquivo de mídia e, em seguida, clique em **próximo**.
9. Sobre o **selecionar pacote** página (disponível a partir do versão 1702), especifique o conteúdo do pacote para incluir como parte do arquivo de mídia e, em seguida, clique em **próximo**.
10. Sobre o **selecionar pacote de Driver** página (disponível a partir do versão 1702), especifique o conteúdo do pacote de driver para incluir como parte do arquivo de mídia e, em seguida, clique em **próximo**.
11.  Sobre o **pontos de distribuição** página, especifique os pontos de distribuição que contêm o conteúdo exigido pela sequência de tarefas e, em seguida, clique em **próximo**.  

     Gerenciador de configuração só exibirá os pontos de distribuição que têm o conteúdo. Tem de distribuir todo o conteúdo associado à sequência de tarefas (imagem de arranque, imagem do sistema operativo, etc.) por, pelo menos, um ponto de distribuição para poder continuar. Após distribuir o conteúdo, você pode reiniciar o assistente ou remover os pontos de distribuição que já selecionou nessa página, ir para a página anterior e, em seguida, de volta para o **pontos de distribuição** página para atualizar a lista de pontos de distribuição. Para obter mais informações sobre a distribuição de conteúdo, veja [Distribuir conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS). Para obter mais informações sobre pontos de distribuição e gerenciamento de conteúdo, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  Você deve ter **leitura** direitos de acesso para a biblioteca de conteúdo nos pontos de distribuição.  

12. Na página **Personalização** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Especifique as variáveis utilizadas pela sequência de tarefas para implementar o sistema operativo.  

    -   Especifique quaisquer comandos prestart que deseja executar antes da sequência de tarefas. Os comandos de pré-início são um script ou um ficheiro executável que pode interagir com o utilizador no Windows PE antes da execução da sequência de tarefas para instalar o sistema operativo. Para obter mais informações sobre comandos prestart para mídia, consulte [comandos para mídia de sequência de tarefas no System Center Configuration Manager Prestart](../understand/prestart-commands-for-task-sequence-media.md).  

         Opcionalmente, selecione **arquivos para o comando de pré-inicialização** para incluir quaisquer arquivos necessários para o comando de pré-inicialização.  

        > [!TIP]  
        >  Durante a criação de mídia de sequência de tarefas, a sequência de tarefas grava a ID do pacote e pré-inicia a linha de comando, incluindo o valor para quaisquer variáveis de sequência de tarefas, no arquivo de log CreateTSMedia.log no computador que executa o console do Configuration Manager. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

13. Conclua o assistente.  

 Os ficheiros de suporte de dados autónomos (.iso) são criados na pasta de destino. Se tiver selecionado **CD/DVD Autónomo**, pode agora copiar os ficheiros de saída para um conjunto de CDs ou DVDs.  

##  <a name="BKMK_StandAloneMediaTSExample"></a>Exemplo de sequência de tarefas para mídia autônoma  
 Use a tabela a seguir como um guia que você crie uma sequência de tarefas para implantar um sistema operacional usando mídia autônoma. A tabela irá ajudá-lo a decidir a sequência geral para os passos da sequência de tarefas e como organizar e estruturar esses passos da sequência de tarefas em grupos lógicos. A sequência de tarefas que você criar pode variar do que esse exemplo e pode conter mais ou menos etapas da sequência de tarefas e grupos.  

> [!NOTE]  
>  Você sempre deve usar o Assistente de mídia de sequência de tarefas para criar mídia autônoma.  

|Passo ou Grupo de Sequência de Tarefas|Descrição|  
|---------------------------------|-----------------|  
|Capturar arquivos e configurações - **(novo grupo de sequências de tarefas)**|Criar um grupo de sequência de tarefas. Os grupos de sequência de tarefas mantêm agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.|  
|Capturar Definições do Windows|Utilize este passo de sequência de tarefas para identificar as definições do Microsoft Windows que são capturadas a partir do sistema operativo existente no computador de destino antes da recriação da imagem. Pode capturar o nome do computador, informações do utilizador e da organização e as definições de fuso horário.|  
|Capturar Definições de Rede|Utilize este passo de sequência de tarefas para capturar definições de rede do computador que recebe a sequência de tarefas. Pode capturar a associação a domínios ou grupos de trabalho do computador e as informações de definições da placa de rede.|  
|Capturar arquivos e configurações - **(nova tarefa sequência subgrupo)**|Crie um grupo de sequência de tarefas dentro de um grupo de sequência de tarefas. Este subgrupo contém os passos necessários para capturar os dados de estado de utilizador do sistema operativo existente no computador de destino antes da recriação da imagem. De forma idêntica ao grupo inicial que adicionou, este subgrupo mantém agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.|  
|Definir Localização de Estado Local|Utilize este passo de sequência de tarefas para especificar uma localização local utilizando a variável de sequência de tarefas de caminho protegido. O estado do utilizador é armazenado num diretório protegido no disco rígido.|  
|Capturar Estado do Utilizador|Utilize este passo de sequência de tarefas para capturar as definições e ficheiros do utilizador que pretende migrar para o novo sistema operativo.|  
|Instalar o sistema operacional - **(novo grupo de sequências de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para instalar o sistema operativo.|  
|Reiniciar para o Windows PE ou disco rígido|Utilize este passo de sequência de tarefas para especificar opções de reinício para o computador que recebe esta sequência de tarefas. Este passo apresentará uma mensagem ao utilizador a indicar que o computador será reiniciado para que a instalação possa continuar.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSInWinPE** . Se o valor associado for igual a **false** , o passo de sequência de tarefas continuará.|  
|Aplicar Sistema Operativo|Utilize este passo de sequência de tarefas para instalar a imagem do sistema operativo no computador de destino. Esta etapa exclui todos os arquivos nesse volume (com exceção dos arquivos de controle específicos do Configuration Manager) e, em seguida, aplica todas as imagens de volume contidas no arquivo WIM para o volume de disco sequencial correspondente. Também pode especificar um ficheiro de resposta **sysprep** para configurar a partição de disco a utilizar para a instalação.|  
|Aplicar Definições do Windows|Utilize este passo de sequência de tarefas para configurar as informações de configuração das definições do Windows para o computador de destino. As definições do Windows que pode aplicar são informações da organização e do utilizador, informações da chave de licença ou produto, fuso horário e a palavra-passe de administrador local.|  
|Aplicar Definições de Rede|Utilize este passo de sequência de tarefas para especificar as informações de configuração da rede ou do grupo de trabalho para o computador de destino. Também pode especificar se o computador utiliza um servidor DHCP ou pode atribuir estaticamente as informações de endereço IP.|  
|Aplicar Pacote de Controlador|Utilize este passo de sequência de tarefas para disponibilizar todos os controladores de dispositivo de um pacote de controladores para utilização pela configuração do Windows. Todos os controladores de dispositivo necessários têm de estar contidos no suporte de dados autónomo.|  
|Configurar o sistema operacional - **(novo grupo de sequências de tarefas)**|Crie outro subgrupo de sequência de tarefas. Esse subgrupo contém as etapas necessárias para instalar o cliente do Configuration Manager.|  
|Configurar Windows e ConfigMgr|Use essa etapa de sequência de tarefas para instalar o software cliente do Configuration Manager. Configuration Manager instala e registra o GUID do cliente do Configuration Manager. Pode atribuir os parâmetros de instalação necessários na janela **Propriedades de instalação** .|  
|Restaurar arquivos e configurações - **(novo grupo de sequências de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para restaurar o estado do utilizador.|  
|Restaurar Estado do Utilizador|Utilize este passo de sequência de tarefas para iniciar a User State Migration Tool (USMT) para restaurar as definições e o estado do utilizador que foram capturados a partir da ação Capturar Estado do Utilizador para o computador de destino.|  

