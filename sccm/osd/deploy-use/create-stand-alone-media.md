---
title: "Criar suporte de dados autónomo com o System Center Configuration Manager | Documentos do Microsoft"
description: "Utilize suportes de dados autónomos para implementar o sistema operativo num computador sem uma ligação a um site do Configuration Manager ou a rede."
ms.custom: na
ms.date: 03/24/2017
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
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: d4689545ce2be5c16a65b24489f30028a0f90f94
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Criar suportes de dados autónomos com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No Configuration Manager de suporte de dados autónomo contém tudo o que é necessário para implementar o sistema operativo num computador sem uma ligação para um site do Configuration Manager ou utilizando a rede. Utilize suportes de dados autónomos com os seguintes cenários de implementação do sistema operativo:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

 Suporte de dados autónomo inclui a sequência de tarefas que automatiza os passos para instalar o sistema operativo e todos os outros conteúdos necessários, incluindo a imagem de arranque, imagem do sistema operativo e controladores de dispositivo. Como tudo o que é necessário para implementar o sistema operativo está armazenado no suporte de dados autónomo, o espaço em disco necessário para o suporte de dados autónomo é significativamente maior do que o espaço em disco necessário para outros tipos de suportes de dados. Quando cria suportes de dados autónomo num site de administração central, o cliente irá obter o código de site atribuído do active directory. O suporte de dados autónomo criado em sites subordinados atribuirá automaticamente ao cliente o código do site para esse site.  

##  <a name="BKMK_CreateStandAloneMedia"></a>Criar suportes de dados autónomos  
 Antes de criar suportes de dados autónomos utilizando o Assistente Criar tarefa de sequência de suportes de dados, certifique-se de que são respeitadas as seguintes condições:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Criar uma sequência de tarefas para implementar um sistema operativo
Como parte do suporte de dados autónomo, tem de especificar a sequência de tarefas para implementar um sistema operativo. Para obter os passos criar uma nova sequência de tarefas, consulte o artigo [criar uma sequência de tarefas para instalar um sistema operativo no System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Não são suportadas as seguintes ações para suportes de dados autónomos:
- O passo Aplicar Controladores Automaticamente na sequência de tarefas. A aplicação automática de controladores de dispositivo a partir do catálogo de controladores não é suportada, mas pode escolher o passo Aplicar Pacote de Controlador para disponibilizar um conjunto especificado de controladores à Configuração do Windows.
- A transferir conteúdo de pacotes passo na sequência de tarefas. A informação do ponto de gestão não está disponível no suporte de dados autónomo, por conseguinte, que o passo não será bem sucedida tentar enumerar localizações de conteúdo.
- Instalação de atualizações de software.
- Instalação do software antes de implementar o sistema operativo.
- Sequências de tarefas para implementações do sistema de operativo.
- Associação de utilizadores ao computador de destino para suportar a afinidade dispositivo/utilizador.
- O pacote dinâmico é instalado através da tarefa Instalar Pacotes.
- A aplicação dinâmica é instalada através da tarefa Instalar Aplicação.

Se a sequência de tarefas para implementar um sistema operativo inclui o [Instalar pacote](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) passo e criar o suporte de dados autónomo num site de administração central, poderá ocorrer um erro. O site de administração central não possui as políticas de configuração de cliente necessárias para ativar o agente de distribuição de software durante a execução da sequência de tarefas. O erro seguinte pode ser apresentado no ficheiro CreateTsMedia.log:<br /><br /> "Falha no método de WMI SMS_TaskSequencePackage.GetClientConfigPolicies (0x80041001)"<br /><br /> Para suportes de dados autónomos, que inclui um **Instalar pacote** passo, tem de criar o suporte de dados autónomo num site primário que tenha o agente de distribuição de software ativado ou adicionar um [executar linha de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) passo após o [configurar Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) passo e antes do primeiro **Instalar pacote** passo na sequência de tarefas. O passo **Executar Linha de Comandos** executa um comando WMIC para ativar o agente de distribuição de software antes da execução do primeiro passo Instalar Pacote. Pode utilizar o seguinte no passo da sequência de tarefas **Executar Linha de Comandos** :<br /><br />
```
WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
```

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas
Tem de distribuir todo o conteúdo exigido pela sequência de tarefas por, pelo menos, um ponto de distribuição. Isto inclui a imagem de arranque, a imagem do sistema operativo e outros ficheiros associados. O assistente recolhe as informações a partir do ponto de distribuição, ao criar o suporte de dados autónomo. Tem de ter direitos de acesso de **Leitura** à biblioteca de conteúdos desse ponto de distribuição.  Para obter detalhes, veja [Distribuir conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a pen USB amovível
*Para uma pen USB amovível:*

Se planear utilizar uma pen USB amovível, a pen USB tem de estar ligada ao computador em que o assistente é executado e ser detetável pelo Windows como um dispositivo amovível. Quando cria o suporte de dados, o assistente escreve diretamente na pen USB. O suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar um suporte de dados autónomo numa pen USB cujo conteúdo inclua um ficheiro com tamanho superior a 4 GB.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída
*Para um conjunto de CD/DVD:*

Antes de executar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas para criar suportes de dados para um conjunto de CDs ou DVDs, tem de criar uma pasta para os ficheiros de saída criados pelo assistente. O suporte de dados criado para um conjunto de CDs ou DVDs é escrito em formato de ficheiros .iso diretamente na pasta.


 Utilize o procedimento seguinte para criar suportes de dados autónomos para uma pen USB amovível ou um conjunto de CD/DVD.  

## <a name="to-create-stand-alone-media"></a>Para criar suportes de dados autónomos  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4.  Na página **Selecione o Tipo de Suporte de Dados** , especifique as opções seguintes e clique em **Seguinte**.  

    -   Selecione **suportes de dados autónomos**.  

    -   Opcionalmente, se pretender permitir a implementação do sistema operativo sem exigir a intervenção do utilizador, selecione **Permitir a implementação do sistema operativo autónoma**. Ao selecionar esta opção, não serão solicitadas ao utilizador informações para a configuração de rede nem para sequências de tarefas opcionais. No entanto, continua a ser solicitada uma palavra-passe ao utilizador se o suporte de dados estiver configurado com proteção por palavra-passe.  

5.  Na página **Tipo de Suporte de Dados** , especifique se o suporte de dados é uma pen USB ou um conjunto de CD/DVD e, em seguida, clique para configurar o seguinte:  

    > [!IMPORTANT]  
    >  O suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar um suporte de dados autónomo numa pen USB cujo conteúdo inclua um ficheiro com tamanho superior a 4 GB.  

    -   Se selecionar **Pen USB**, especifique a unidade onde pretende armazenar o conteúdo.  

    -   Se selecionar **Conjunto CD/DVD**, especifique a capacidade do suporte de dados e o nome e caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo:  **\\\servername\folder\outputfile.iso**  

         Se a capacidade do suporte de dados for demasiado pequena para armazenar todo o conteúdo, serão criados vários ficheiros e tem de armazenar o conteúdo em vários CDs ou DVDs. Se forem necessários vários suportes de dados, o Configuration Manager adiciona um número sequencial ao nome de cada ficheiro de saída criado. Além disso, se implementar uma aplicação juntamente com o sistema operativo e a aplicação não couber num único suporte de dados, o Configuration Manager armazenará a aplicação em vários suportes de dados. Quando o suporte de dados autónomo for executado, o Configuration Manager solicita ao utilizador o suporte de dados seguinte em que a aplicação está armazenada.   

         > [!IMPORTANT]  
         >  Se selecionar uma imagem .iso existente, o Assistente de Criação de Suporte de Dados da Sequência de Tarefas elimina essa imagem da unidade ou partilha logo que avança para a página seguinte do assistente. A imagem existente será eliminada, mesmo que em seguida cancele o assistente.  

     Clique em **Seguinte**.  

6.  No **segurança** página, escolha entre as seguintes definições e, em seguida, clique em **seguinte**:
    - **Proteger suporte de dados com uma palavra-passe**: Introduza uma palavra-passe segura para ajudar a proteger o suporte de dados. Se especificar uma palavra-passe, a palavra-passe é necessário para utilizar o suporte de dados.  

        > [!IMPORTANT]  
        >  Em suportes de dados autónomos, apenas os passos de sequência de tarefas e as respetivas variáveis são encriptados. O restante conteúdo do suporte de dados não é encriptado, pelo que não deverá incluir quaisquer informações sensíveis nos scripts da sequência de tarefas. Armazene e implemente todas as informações sensíveis utilizando variáveis de sequência de tarefas.  

    - **Selecione o intervalo de datas para este suportes de dados autónomos ser válida** (começando na versão 1702): Defina opcionais datas de início e de expiração no suporte de dados. Estas definições estão desativadas por predefinição. As datas são comparados com a hora do sistema no computador antes da execução do suporte de dados autónomo. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, o suporte de dados autónomo não está iniciado. Estas opções também estão disponíveis ao utilizar o cmdlet New-CMStandaloneMedia do PowerShell.
7.  No **CD/DVD autónomo** página, especifique a sequência de tarefas que implementa o sistema operativo e, em seguida, clique em **seguinte**. Escolher **detetar dependências de aplicação associado e adicioná-las a este suporte** para adicionar conteúdo ao suporte de dados autónomo para as dependências da aplicação.
    > [!TIP]
    > Se não conseguir ver as dependências da aplicação esperado, desmarque a opção e, em seguida, selecione novamente o **detetar dependências de aplicação associado e adicioná-las a este suporte** definição para atualizar a lista.

    O assistente permite-lhe selecionar apenas as sequências de tarefas que estão associadas uma imagem de arranque.  

8. No **selecionar aplicação** página (disponível a partir na versão 1702), especifique o conteúdo da aplicação para incluir como parte do ficheiro de suporte de dados e, em seguida, clique em **seguinte**.
9. No **selecionar pacote** página (disponível a partir na versão 1702), especifique o conteúdo do pacote incluir como parte do ficheiro de suporte de dados e, em seguida, clique em **seguinte**.
10. No **selecionar pacote de controlador** página (disponível a partir na versão 1702), especifique o conteúdo do pacote de controladores para incluir como parte do ficheiro de suporte de dados e, em seguida, clique em **seguinte**.
11.  No **pontos de distribuição** página, especifique os pontos de distribuição que contenham o conteúdo exigido pela sequência de tarefas e, em seguida, clique em **seguinte**.  

     O Configuration Manager mostrará apenas a pontos de distribuição que possuem o conteúdo. Tem de distribuir todo o conteúdo associado à sequência de tarefas (imagem de arranque, imagem do sistema operativo, etc.) por, pelo menos, um ponto de distribuição para poder continuar. Após distribuir o conteúdo, pode ou reinicie o assistente ou remover quaisquer pontos de distribuição que já selecionada nesta página, aceda à página anterior e, em seguida, novamente o **pontos de distribuição** página para atualizar a lista de pontos de distribuição. Para obter mais informações sobre a distribuição de conteúdo, veja [Distribuir conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS). Para mais informações sobre pontos de distribuição e gestão de conteúdo, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  Tem de ter **leitura** direitos para a biblioteca de conteúdos nos pontos de distribuição de acesso.  

12. Na página **Personalização** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Especifique as variáveis utilizadas pela sequência de tarefas para implementar o sistema operativo.  

    -   Especifique os comandos de Pré-início que pretende executar antes da sequência de tarefas. Os comandos de pré-início são um script ou um ficheiro executável que pode interagir com o utilizador no Windows PE antes da execução da sequência de tarefas para instalar o sistema operativo. Para mais informações sobre os comandos de Pré-início para suportes de dados, consulte o artigo [comandos para dados de sequência de tarefas no System Center Configuration Manager de Pré-início](../understand/prestart-commands-for-task-sequence-media.md).  

         Opcionalmente, selecione **ficheiros para o comando de Pré-início** para incluir quaisquer ficheiros necessários para o comando de Pré-início.  

        > [!TIP]  
        >  Durante a criação de suportes de dados da sequência de tarefas, a sequência de tarefas escreve o ID de pacote e um comando de Pré-início da linha de comandos, incluindo o valor das eventuais variáveis de sequência de tarefas, para o ficheiro de registo Createtsmedia no computador que executa a consola do Configuration Manager. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

13. Conclua o assistente.  

 Os ficheiros de suporte de dados autónomos (.iso) são criados na pasta de destino. Se tiver selecionado **CD/DVD Autónomo**, pode agora copiar os ficheiros de saída para um conjunto de CDs ou DVDs.  

##  <a name="BKMK_StandAloneMediaTSExample"></a>Exemplo de sequência de tarefas para suportes de dados autónomos  
 Utilize a tabela seguinte como um guia como criar uma sequência de tarefas para implementar um sistema operativo utilizando suportes de dados autónomos. A tabela irá ajudá-lo a decidir a sequência geral para os passos da sequência de tarefas e como organizar e estruturar esses passos da sequência de tarefas em grupos lógicos. A sequência de tarefas que criar pode variar deste exemplo e pode incluir mais ou menos passos de sequência de tarefas e grupos.  

> [!NOTE]  
>  Tem de utilizar sempre o Assistente de suporte de dados de sequência de tarefas para criar suportes de dados autónomos.  

|Passo ou Grupo de Sequência de Tarefas|Descrição|  
|---------------------------------|-----------------|  
|Capturar ficheiros e definições - **(novo grupo de sequência de tarefas)**|Criar um grupo de sequência de tarefas. Os grupos de sequência de tarefas mantêm agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.|  
|Capturar Definições do Windows|Utilize este passo de sequência de tarefas para identificar as definições do Microsoft Windows que são capturadas a partir do sistema operativo existente no computador de destino antes da recriação da imagem. Pode capturar o nome do computador, informações do utilizador e da organização e as definições de fuso horário.|  
|Capturar Definições de Rede|Utilize este passo de sequência de tarefas para capturar definições de rede do computador que recebe a sequência de tarefas. Pode capturar a associação a domínios ou grupos de trabalho do computador e as informações de definições da placa de rede.|  
|Capturar ficheiros do utilizador e definições - **(novo grupo sequência de tarefas secundárias)**|Crie um grupo de sequência de tarefas dentro de um grupo de sequência de tarefas. Este subgrupo contém os passos necessários para capturar os dados de estado de utilizador do sistema operativo existente no computador de destino antes da recriação da imagem. De forma idêntica ao grupo inicial que adicionou, este subgrupo mantém agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.|  
|Definir Localização de Estado Local|Utilize este passo de sequência de tarefas para especificar uma localização local utilizando a variável de sequência de tarefas de caminho protegido. O estado do utilizador é armazenado num diretório protegido no disco rígido.|  
|Capturar Estado do Utilizador|Utilize este passo de sequência de tarefas para capturar as definições e ficheiros do utilizador que pretende migrar para o novo sistema operativo.|  
|Instalar o sistema operativo - **(novo grupo de sequência de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para instalar o sistema operativo.|  
|Reiniciar para o Windows PE ou disco rígido|Utilize este passo de sequência de tarefas para especificar opções de reinício para o computador que recebe esta sequência de tarefas. Este passo apresentará uma mensagem ao utilizador a indicar que o computador será reiniciado para que a instalação possa continuar.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSInWinPE** . Se o valor associado for igual a **false** , o passo de sequência de tarefas continuará.|  
|Aplicar Sistema Operativo|Utilize este passo de sequência de tarefas para instalar a imagem do sistema operativo no computador de destino. Este passo elimina todos os ficheiros nesse volume (à exceção dos ficheiros de controlo do específico do Configuration Manager) e, em seguida, aplica-se todas as imagens de volume contidas no ficheiro WIM para o volume do disco sequenciais correspondente. Também pode especificar um ficheiro de resposta **sysprep** para configurar a partição de disco a utilizar para a instalação.|  
|Aplicar Definições do Windows|Utilize este passo de sequência de tarefas para configurar as informações de configuração das definições do Windows para o computador de destino. As definições do Windows que pode aplicar são informações da organização e do utilizador, informações da chave de licença ou produto, fuso horário e a palavra-passe de administrador local.|  
|Aplicar Definições de Rede|Utilize este passo de sequência de tarefas para especificar as informações de configuração da rede ou do grupo de trabalho para o computador de destino. Também pode especificar se o computador utiliza um servidor DHCP ou pode atribuir estaticamente as informações de endereço IP.|  
|Aplicar Pacote de Controlador|Utilize este passo de sequência de tarefas para disponibilizar todos os controladores de dispositivo de um pacote de controladores para utilização pela configuração do Windows. Todos os controladores de dispositivo necessários têm de estar contidos no suporte de dados autónomo.|  
|Configurar o sistema operativo - **(novo grupo de sequência de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este grupo secundárias contém os passos necessários para instalar o cliente do Configuration Manager.|  
|Configurar Windows e ConfigMgr|Utilize este passo de sequência de tarefas para instalar o software de cliente do Configuration Manager. O Configuration Manager instala e regista o GUID do cliente do Configuration Manager. Pode atribuir os parâmetros de instalação necessários na janela **Propriedades de instalação** .|  
|Restaurar os ficheiros de utilizador e definições - **(novo grupo de sequência de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para restaurar o estado do utilizador.|  
|Restaurar Estado do Utilizador|Utilize este passo de sequência de tarefas para iniciar a User State Migration Tool (USMT) para restaurar as definições e o estado do utilizador que foram capturados a partir da ação Capturar Estado do Utilizador para o computador de destino.|  
