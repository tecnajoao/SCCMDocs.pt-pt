---
title: Criar suportes de dados autónomos
titleSuffix: Configuration Manager
description: Utilize suportes de dados autónomos para implementar o sistema operativo num computador sem uma ligação de rede.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cdf2c0e1501707e836c914265e0edf2d9c88521f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138074"
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Criar suportes de dados autónomos com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Suporte de dados autónomo no Configuration Manager contém tudo o que necessários para implementar o sistema operativo (SO) num computador sem uma ligação de rede. Utilize suportes de dados autónomos com os seguintes cenários de implementação do sistema operacional:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Atualize o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

Suporte de dados autónomo inclui a sequência de tarefas que automatiza os passos para instalar o sistema operacional e outro conteúdo necessário. Este conteúdo inclui a imagem de arranque, imagem do sistema operativo e controladores de dispositivo. Uma vez que o suporte de dados autónomo armazena tudo para implantar o sistema operacional, requer mais espaço em disco ao necessário para outros tipos de suportes de dados. Ao criar suporte de dados autónomo num site de administração central, o cliente obtém o código de site atribuído do Active Directory. Suporte de dados autónomo criado em sites subordinados automaticamente atribui ao cliente o código do site para esse site.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Criar suportes de dados autónomos  
Antes de criar suportes de dados autónomos, utilizando o assistente suporte de dados de criação de sequência de tarefas, certifique-se de que as seguintes condições são cumpridas:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Criar uma sequência de tarefas para implementar um sistema operativo
Como parte do suporte de dados autónomo, tem de especificar a sequência de tarefas para implementar um sistema operativo. Para obter os passos criar uma nova sequência de tarefas, consulte [criar uma sequência de tarefas para instalar um sistema operativo no System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

As seguintes ações não são suportadas para suportes de dados autónomos:
- O **aplicar controladores automaticamente** passo na sequência de tarefas. Suporte de dados autónomo não suporta a aplicação automática de controladores de dispositivo no catálogo de controladores. Utilize o **aplicar pacote de controlador** passo para disponibilizar um conjunto especificado de controladores à configuração do Windows.
- O **transferir conteúdo do pacote** passo na sequência de tarefas. As informações de ponto de gestão não estão disponíveis no suporte de dados autónomo, portanto o passo falhar tentar enumerar as localizações de conteúdo.
- Instalação de atualizações de software.
- A instalar o software antes de implementar o sistema operativo.
- Sequências de tarefas para implementações não pertencentes ao sistema operativo.
- Associação de utilizadores ao computador de destino para suportar a afinidade dispositivo/utilizador.
- O pacote dinâmico é instalado através da **instalar pacotes** tarefas.
- Aplicação dinâmica é instalada através da **instalar aplicação** tarefas.

> [!NOTE]    
> Poderá ocorrer um erro se a sequência de tarefas inclui o [Instalar pacote](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) passo e criar o suporte de dados autónomo num site de administração central. O site de administração central não tem as políticas de configuração de cliente necessário. Estas políticas são necessários para ativar o agente de distribuição de software durante a execução da sequência de tarefas. O erro seguinte pode ser apresentado no ficheiro CreateTsMedia.log:    
>     
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`    
> 
> Para suporte de dados autónomo, que inclui um **Instalar pacote** passo, criar suportes de dados autónomo num site primário que tenha o agente de distribuição de software ativado. 
>
> Em alternativa, adicione uma [executar linha de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) passo após a [configuração do Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) passo e antes do primeiro **Instalar pacote** passo na sequência de tarefas. O **executar linha de comandos** passo é executado o seguinte comando do WMIC para ativar o agente de distribuição de software antes do primeiro passo Instalar pacote:    
>    
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`


> [!IMPORTANT]    
> Não selecione a **utilizar o pacote de cliente de pré-produção quando disponível** definição **configuração do Windows e ConfigMgr** passo de sequência de tarefas para suporte de dados autónomo. Suporte de dados autónomo não suporta a utilização desta definição. Para obter mais informações sobre esta definição, consulte [configuração do Windows e ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas
Distribua todo o conteúdo necessário pela sequência de tarefas para, pelo menos, um ponto de distribuição. Este conteúdo inclui a imagem de arranque, imagem do sistema operativo e outros ficheiros associados. O assistente recolhe as informações a partir do ponto de distribuição, ao criar o suporte de dados autónomo. Tem de ter direitos de acesso de **Leitura** à biblioteca de conteúdos desse ponto de distribuição. Para obter mais informações, consulte [distribuir conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a pen USB amovível
*Para uma pen USB amovível:*

Se estiver a utilizar uma pen USB amovível, ligue-se a unidade USB ao computador em que o assistente é executado. A unidade USB tem de ser detetável pelo Windows como um dispositivo amovível. Quando cria o suporte de dados, o assistente escreve diretamente na pen USB. O suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar um suporte de dados autónomo numa pen USB cujo conteúdo inclua um ficheiro com tamanho superior a 4 GB.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída
*Para um conjunto de CD/DVD:*

Antes de executar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas para criar suportes de dados para um conjunto de CDs ou DVDs, tem de criar uma pasta para os ficheiros de saída criados pelo assistente. O suporte de dados criado para um conjunto de CDs ou DVDs é escrito em formato de ficheiros .iso diretamente na pasta.


 Utilize o procedimento seguinte para criar suportes de dados autónomos para uma pen USB amovível ou um conjunto de CD/DVD.  

## <a name="to-create-stand-alone-media"></a>Para criar suportes de dados autónomos  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3. No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4. Na página **Selecione o Tipo de Suporte de Dados** , especifique as opções seguintes e clique em **Seguinte**.  

   -   Selecione **suporte de dados autónomo**.  

   -   Opcionalmente, se pretender permitir a implementação do sistema operativo sem exigir a intervenção do utilizador, selecione **Permitir a implementação do sistema operativo autónoma**. Ao selecionar esta opção, não serão solicitadas ao utilizador informações para a configuração de rede nem para sequências de tarefas opcionais. Se o suporte de dados está configurada para proteção de palavra-passe, ainda é pedido ao utilizador uma palavra-passe.  

5. Sobre o **tipo de suporte** , especifique se o suporte de dados é uma pen USB amovível ou um conjunto de CD/DVD:  

   > [!IMPORTANT]  
   >  Por predefinição, o suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar o suporte de dados autónomo numa pen USB amovível cujo conteúdo inclua um ficheiro com mais de 4 GB de tamanho.  

   - Se selecionou **pen USB amovível**, especifique a unidade onde pretende armazenar o conteúdo.  

     - **Formatar pen USB amovível (FAT32) e tornar inicializável**: Por predefinição, permitem preparar a unidade USB do Configuration Manager. Muitos dispositivos mais recentes da UEFI requerem uma partição FAT32 inicializável. No entanto, esse formato também limita o tamanho dos ficheiros e a capacidade geral da unidade. Se já tiver formatado e configurado a unidade amovível, desative esta opção. 

   - Se selecionar **Conjunto CD/DVD**, especifique a capacidade do suporte de dados e o nome e caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo:  **\\\servername\folder\outputfile.iso**  

      Se a capacidade do suporte de dados for demasiado pequena para armazenar todo o conteúdo, serão criados vários ficheiros e tem de armazenar o conteúdo em vários CDs ou DVDs. Quando vários suportes de dados é necessária, o Configuration Manager adiciona um número sequencial ao nome de cada ficheiro de saída criado. Além disso, se implementar uma aplicação juntamente com o sistema operativo e a aplicação não couber num único suporte de dados, o Configuration Manager armazenará a aplicação em vários suportes de dados. Quando o suporte de dados autónomo for executado, o Configuration Manager solicita ao utilizador o suporte de dados seguinte onde a aplicação é armazenada.   

      > [!IMPORTANT]  
      >  Se selecionar uma imagem .iso existente, o Assistente de Criação de Suporte de Dados da Sequência de Tarefas elimina essa imagem da unidade ou partilha logo que avança para a página seguinte do assistente. A imagem existente será eliminada, mesmo que em seguida cancele o assistente.  

     Clique em **Seguinte**.  

6. Sobre o **Security** página, escolha entre as seguintes definições e, em seguida, clique em **próxima**:
   - **Proteger suporte de dados com uma palavra-passe**: Introduza uma palavra-passe segura para ajudar a proteger o suporte de dados. Se especificar uma palavra-passe, a palavra-passe é necessária para utilizar o suporte de dados.  

       > [!IMPORTANT]  
       >  No suporte de dados autónomo, apenas os passos de sequência de tarefas e as respetivas variáveis são encriptados. O restante conteúdo do suporte de dados não é encriptado, pelo que não deverá incluir quaisquer informações sensíveis nos scripts da sequência de tarefas. Store e na implementação de todas as informações sensíveis utilizando variáveis de sequência de tarefas.  

   - **Selecione o intervalo de datas para este suporte de dados autónomo seja válido** (a partir da versão 1702): Defina datas de início e de expiração opcionais no suporte de dados. Estas definições estão desativadas por predefinição. As datas são em comparação com a hora do sistema no computador antes do suporte de dados autónomo é executado. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, o suporte de dados autónomo não está iniciado. Estas opções também estão disponíveis ao utilizar o cmdlet New-CMStandaloneMedia PowerShell.
7. Sobre o **CD/DVD autónomo** página, especifique a sequência de tarefas que implementa o sistema operativo e, em seguida, clique em **próxima**. Para adicionar o conteúdo para o suporte de dados autónomo para as dependências da aplicação, escolha **detetar dependências da aplicação associada e adicioná-las a este suporte de dados**.
   > [!TIP]
   > Se não vir as dependências da aplicação esperado, desselecione e, em seguida, selecione novamente o **detetar dependências da aplicação associada e adicioná-las a este suporte de dados** definição para atualizar a lista.

   O assistente permite selecionar apenas as sequências de tarefas que estão associadas uma imagem de arranque.  

8. Sobre o **selecionar aplicação** página (disponível a partir da versão 1702), especifique o conteúdo da aplicação para incluir como parte do arquivo de multimédia e, em seguida, clique em **próxima**.
9. Sobre o **selecionar o pacote** página (disponível a partir da versão 1702), especifique o conteúdo do pacote para incluir como parte do arquivo de multimédia e, em seguida, clique em **próxima**.
10. Sobre o **selecionar pacote de controladores** página (disponível a partir da versão 1702), especifique o conteúdo do pacote de controladores para incluir como parte do arquivo de multimédia e, em seguida, clique em **próxima**.
11. Sobre o **pontos de distribuição** página, especifique os pontos de distribuição que contenham o conteúdo necessário e, em seguida, clique em **próxima**.  

    Configuration Manager apresenta apenas os pontos de distribuição que possuem o conteúdo. Distribua todo o conteúdo associado a sequência de tarefas, pelo menos, um ponto de distribuição antes de continuar. Após distribuir o conteúdo, atualize a lista de pontos de distribuição. Remover quaisquer pontos de distribuição que já selecionou nesta página, aceda à página anterior e, em seguida, voltar para o **pontos de distribuição** página. Em alternativa, reinicie o assistente. Para obter mais informações, consulte [distribuir conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) e [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  Tem de ter **leitura** direitos para a biblioteca de conteúdos nos pontos de distribuição de acesso.  

12. Na página **Personalização** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Especifique as variáveis utilizadas pela sequência de tarefas para implementar o sistema operativo.  

    -   Especifique os comandos de Pré-início que pretende executar antes da sequência de tarefas. Os comandos de Pré-início são um script ou um executável que é executado no Windows PE antes de inicia a sequência de tarefas. Para obter mais informações, consulte [comandos para suporte de dados de sequência de tarefas de Pré-início](../understand/prestart-commands-for-task-sequence-media.md).  

         Opcionalmente, selecione **ficheiros para o comando de Pré-início** para incluir qualquer ficheiros necessários para o comando de Pré-início.  

        > [!TIP]  
        >  Durante a criação de suportes de dados de sequência de tarefas, do Configuration Manager escreve o ID de pacote e a linha de comandos de Pré-início para o **Createtsmedia** ficheiro no computador que executa a consola do Configuration Manager. Este resultado inclui o valor das eventuais variáveis de sequência de tarefas. Consulte este ficheiro de registo para verificar o valor das variáveis de sequência de tarefas.  

13. Conclua o assistente.  

    Os ficheiros de suporte de dados autónomos (.iso) são criados na pasta de destino. Se tiver selecionado **CD/DVD Autónomo**, pode agora copiar os ficheiros de saída para um conjunto de CDs ou DVDs.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Sequência de tarefas de exemplo para suporte de dados autónomo  
 Para criar uma sequência de tarefas para implementar um sistema operativo utilizando suportes de dados autónomos, utilize a tabela seguinte como guia. A tabela ajuda-o a decidir a sequência geral para os passos de sequência de tarefas. Também ajuda a organizar e estruturar os passos de sequência de tarefas em grupos lógicos. A sequência de tarefas que criar pode ser diferente deste exemplo e pode conter mais ou menos grupos e passos de sequência de tarefas.  

> [!NOTE]  
>  Tem de utilizar sempre o Assistente de suporte de dados de sequência de tarefas para criar suportes de dados autónomos.  

|Passo ou Grupo de Sequência de Tarefas|Descrição|  
|---------------------------------|-----------------|  
|Capturar ficheiros e definições - **(novo grupo de sequência de tarefas)**|Criar um grupo de sequência de tarefas. Os grupos de sequência de tarefas mantêm agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.|  
|Capturar Definições do Windows|Utilize este passo de sequência de tarefas para capturar as definições do Windows do computador de destino antes da recriação da imagem. Capture o nome do computador, utilizador e informações organizacionais e as definições de fuso horário.|  
|Capturar definições de rede|Utilize este passo de sequência de tarefas para capturar definições de rede do computador que recebe a sequência de tarefas. Pode capturar a associação a domínios ou grupos de trabalho do computador e as informações de definições da placa de rede.|  
|Capturar definições e ficheiros de utilizador - **(novo subgrupo de sequência de tarefas)**|Crie um grupo de sequência de tarefas dentro de um grupo de sequência de tarefas. Este subgrupo contém os passos para capturar dados de estado de utilizador do computador de destino antes da recriação da imagem. De forma semelhante para o primeiro grupo que adicionou, este subgrupo mantém os passos de sequência de tarefas semelhantes em conjunto para uma melhor organização e o controlo de erros.|  
|Definir Localização de Estado Local|Utilize este passo de sequência de tarefas para especificar uma localização local utilizando a variável de sequência de tarefas de caminho protegido. O estado do utilizador é armazenado num diretório protegido no disco rígido.|  
|Capturar Estado do Utilizador|Utilize este passo de sequência de tarefas para capturar as definições e ficheiros do utilizador que pretende migrar para o novo sistema operativo.|  
|Instalar sistema operativo - **(novo grupo de sequência de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para instalar o sistema operativo.|  
|Arrancar para o Windows PE ou disco rígido|Utilize este passo de sequência de tarefas para especificar opções de reinício para o computador que recebe esta sequência de tarefas. Este passo exibe uma mensagem para o utilizador que está a reiniciar o computador para continuar a instalação.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSInWinPE** . Se o valor associado for igual a **false**, o passo de sequência de tarefas continuará.|  
|Aplicar Sistema Operativo|Utilize este passo de sequência de tarefas para instalar a imagem do sistema operativo no computador de destino. Este passo elimina todos os ficheiros nesse volume, exceto para os arquivos de controle específico do Configuration Manager. Em seguida, aplica-se todas as imagens de volume contidas no ficheiro WIM ao volume de disco sequencial correspondente. Também pode especificar um ficheiro de resposta **sysprep** para configurar a partição de disco a utilizar para a instalação.|  
|Aplicar Definições do Windows|Utilize este passo de sequência de tarefas para configurar as informações de configuração das definições do Windows para o computador de destino. Estas definições incluem o usuário e informações da empresa, informações da chave de licença ou produto, fuso horário e a palavra-passe de administrador local.|  
|Aplicar Definições de Rede|Utilize este passo de sequência de tarefas para especificar as informações de configuração da rede ou do grupo de trabalho para o computador de destino. Também pode especificar se o computador utiliza um servidor DHCP ou pode atribuir estaticamente as informações de endereço IP.|  
|Aplicar Pacote de Controlador|Utilize este passo de sequência de tarefas para disponibilizar todos os controladores de dispositivo de um pacote de controladores para utilização pela configuração do Windows. Todos os controladores de dispositivo necessários têm de estar contidos no suporte de dados autónomo.|  
|Configurar sistema operativo - **(novo grupo de sequência de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para instalar o cliente do Configuration Manager.|  
|Configurar Windows e ConfigMgr|Utilize este passo de sequência de tarefas para instalar o software de cliente do Configuration Manager. O Configuration Manager instala e regista o GUID do cliente do Configuration Manager. Pode atribuir os parâmetros de instalação necessários na janela **Propriedades de instalação** .|  
|Restaurar definições e ficheiros de utilizador - **(novo grupo de sequência de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para restaurar o estado do utilizador.|  
|Restaurar Estado do Utilizador|Utilize este passo de sequência de tarefas para iniciar a ferramenta de migração de estado de utilizador (USMT). USMT restaura o estado do utilizador e definições, capturadas anteriormente com o passo de capturar estado do utilizador, para o computador de destino.|  
