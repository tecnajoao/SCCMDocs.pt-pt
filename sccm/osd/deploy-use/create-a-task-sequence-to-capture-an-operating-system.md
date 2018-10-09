---
title: Criar uma sequência de tarefas para capturar um sistema operativo
titleSuffix: Configuration Manager
description: Uma sequência de tarefas de compilação e captura baseia-se um computador de referência que pode incluir controladores específicos e atualizações de software, juntamente com o sistema operativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 34536114e6cb1be8f256da385b3d69d07c17f676
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862486"
---
# <a name="create-a-task-sequence-to-capture-an-operating-system-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para capturar um sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando utiliza uma sequência de tarefas para implementar um sistema operativo num computador no System Center Configuration Manager, o computador instala a imagem do sistema operativo que especificou na sequência de tarefas. Para personalizar a imagem do sistema operativo de modo a que inclua controladores, aplicações, atualizações de software específicos, etc., pode utilizar uma sequência de tarefas de compilação e captura para criar um computador de referência e, em seguida, capturar a imagem do sistema operativo a partir desse computador de referência. Se já tiver um computador de referência disponível para capturar, pode criar uma sequência de tarefas personalizada para capturar o sistema operativo. Utilize as secções seguintes para capturar um sistema operativo personalizado.  

##  <a name="BKMK_BuildCaptureTS"></a> Utilizar uma sequência de tarefas para compilar e capturar um computador de referência  
 A sequência de tarefas de compilação e captura cria partições e formata o computador de referência, instala o sistema operativo, bem como as atualizações de cliente, aplicativos e software do Configuration Manager e, em seguida, captura o sistema operativo do computador de referência . Os pacotes associados à sequência de tarefas, tais como aplicações, têm de estar disponíveis em pontos de distribuição antes de criar a sequência de tarefas de compilação e captura.  

###  <a name="BKMK_CreatePackages"></a> Preparar implementações de sistemas operativos  
 Existem muitos cenários para implementar um sistema operativo em computadores no seu ambiente. Na maioria dos casos, irá criar uma sequência de tarefas e selecionar **Instalar um pacote de imagem existente** , no Assistente de Criação de Sequência de Tarefas, para instalar o sistema operativo, migrar as definições de utilizador, aplicar atualizações de software e instalar aplicações. Antes de criar uma sequência de tarefas para instalar um sistema operativo, é necessário o seguinte:  

-   **Necessário**  

    -   O [imagem de arranque](../get-started/manage-boot-images.md) tem de estar disponível na consola do Configuration Manager.  

    -   Uma [imagem do sistema operativo](../get-started/manage-operating-system-images.md) tem de estar disponível na consola do Configuration Manager.  

-   **Necessário (se utilizado)**  

    -   [Pacotes de controladores](../get-started/manage-drivers.md) que contêm as informações necessárias drivers do Windows para suportar hardware no computador de referência tem de estar disponíveis na consola do Configuration Manager. Para obter mais informações sobre os passos de sequência de tarefas para gerir controladores, consulte [utilizar sequências de tarefas para instalar controladores de dispositivo](../get-started/manage-drivers.md#BKMK_TSDrivers).  

    -   [Atualizações de software](../../sum/get-started/synchronize-software-updates.md) têm de ser sincronizadas na consola do Configuration Manager.  

    -   [Aplicativos](../../apps/deploy-use/create-applications.md) deve ser adicionado à consola do Configuration Manager.  

###  <a name="BKMK_CreateBuildCaptureTS"></a> Criar uma sequência de tarefas de compilação e captura  
 Utilize o procedimento seguinte para utilizar uma sequência de tarefas para compilar um computador de referência e capturar o sistema operativo.  

#### <a name="to-create-a-task-sequence-that-builds-and-captures-an-operating-system-image"></a>Para criar uma sequência de tarefas que crie e capture uma imagem de sistema operativo  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente de Criação de Sequência de Tarefas.  

4.  Na página **Criar uma Nova Sequência de Tarefas** , selecione **Construir e capturar uma imagem do sistema operativo de referência**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Nome da sequência de tarefas**: Especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: Especifique uma descrição da tarefa que é executada pela sequência de tarefas, como uma descrição do sistema operativo que é criado pela sequência de tarefas.  

    -   **Imagem de arranque**: Especifique a imagem de arranque que instala a imagem de sistema operativo.  

        > [!IMPORTANT]  
        >  A arquitetura da imagem de arranque deve ser compatível com a arquitetura de hardware do computador de destino.  

6.  Na página **Instalar o Windows** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Pacote de imagem**: Especifique o pacote de imagem do sistema operativo, que contém os ficheiros que são necessárias para instalar o sistema operativo.  

    -   **Índice de imagens**: Especifique o sistema operativo a instalar. Se a imagem do sistema operativo tiver várias versões, selecione a versão que pretende instalar.  

    -   **Chave de produto**: Especifique a chave de produto para o sistema operativo do Windows instalar. Pode especificar chaves de licenciamento em volume codificadas e chaves de produto padrão. Se utilizar uma chave de produto não codificada, terá de separar cada grupo de 5 carateres por um hífen (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modo de licenciamento de servidor**: Especifique se a licença de servidor é **por posto de trabalho**, **por servidor**, ou não se é especificada nenhuma licença. Se a licença do servidor for **Por servidor**, especifique também o número máximo de ligações de servidor.  

    -   Especifique como lidar com a conta de administrador utilizada quando o sistema operativo é implementado.  

        -   **Aleatoriamente gerar a palavra-passe de administrador local e desativar a conta nas plataformas suportadas**: Especifique se pretende que o Configuration Manager, crie uma palavra-passe aleatória para a conta de administrador local e desative a conta quando o sistema operativo é implementado.  

        -   **Ativar a conta e especificar a palavra-passe de administrador local**: Especifique se a mesma palavra-passe é utilizada para a conta de administrador local em todos os computadores em que o sistema operativo é implementado.  

7.  Na página **Configurar Rede** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Junte-se a um grupo de trabalho**: Especifique se pretende adicionar o computador de destino a um grupo de trabalho quando o sistema operativo é implementado.  

    -   **Aderir a um domínio**: Especifique se pretende adicionar o computador de destino a um domínio quando o sistema operativo é implementado. Em **Domínio**, especifique o nome do domínio.  

        > [!IMPORTANT]  
        >  Pode navegar para localizar domínios na floresta local, mas tem de especificar o nome de domínio de uma floresta remota.  

         Também pode especificar uma unidade organizacional (UO). Trata-se de uma definição opcional que especifica o nome único LDAP X.500 da UO em que deverá ser criada a conta de computador, caso ainda não exista.  

    -   **Conta**: Especifique o nome de utilizador e palavra-passe para a conta que tem permissões para aderir ao domínio especificado. Por exemplo: *domínio\utilizador* ou *%variable%*.  

        > [!IMPORTANT]  
        >  Se pretender migrar as definições de domínio ou as definições de grupo de trabalho, terá de introduzir as credenciais de domínio apropriadas.  

8.  Sobre o **instalar o Configuration Manager** , especifique o pacote de cliente do Configuration Manager que contém os ficheiros de origem para instalar o cliente do Configuration Manager, adicione as propriedades adicionais necessárias para instalar o cliente, e, em seguida, clique em **seguinte**.  

     Para obter mais informações sobre as propriedades que podem ser utilizados para instalar um cliente, consulte [acerca das propriedades de instalação de cliente](../../core/clients/deploy/about-client-installation-properties.md).  

9. Na página **Incluir Atualizações** , especifique se devem ser instaladas as atualizações de software necessárias, todas as atualizações de software ou nenhuma atualização de software e clique em **Seguinte**. Se especificar a instalação de atualizações de software, o Configuration Manager instala apenas as atualizações de software que são direcionadas para as coleções que o computador de destino é um membro do.  

10. Na página **Instalar Aplicações** , especifique as aplicações a instalar no computador de destino e clique em **Seguinte**. Se especificar várias aplicações, poderá também especificar que a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

11. Na página **Preparação do Sistema** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Pacote**: Especifique o pacote do Configuration Manager que contém a versão adequada de Sysprep a utilizar para capturar as definições de computador de referência.  

         Se a versão do sistema operativo em execução for Windows Vista ou posterior, o Sysprep será automaticamente instalado no computador, sem necessidade de especificar um pacote.  

12. Na página **Propriedades da Imagem** , especifique as seguintes definições para a imagem de sistema operativo e clique em **Seguinte**.  

    -   **Criado por**: Especifique o nome do utilizador que criou a imagem de sistema operativo.  

    -   **Versão**: Especifique um número de versão definido pelo utilizador que está associado a imagem do sistema operativo.  

    -   **Descrição**: Especifique uma descrição definida pelo utilizador da imagem de computador do sistema operativo.  

13. Na página **Capturar Imagem** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Caminho**: Especifique uma pasta de rede partilhada onde a saída. Ficheiro WIM resultante. Este ficheiro contém a imagem de sistema operativo baseada nas definições especificadas utilizando este assistente. Se especificar uma pasta que já contenha um ficheiro .WIM, o ficheiro existente está substituído.  

    -   **Conta**: Especifique a conta do Windows que tem permissões para a partilha de rede onde está armazenada a imagem.  

14. Conclua o assistente.  

15. Para adicionar mais passos à sequência de tarefas, selecione a sequência de tarefas que criou e clique em **Editar**. Para obter informações sobre como editar uma sequência de tarefas, consulte [editar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Implemente a sequência de tarefas num computador de referência de uma das seguintes formas:  

-   Se o computador de referência for um cliente do Configuration Manager, pode implementar a compilação e captura de sequência de tarefas na coleção que contenha o computador de referência. Para obter informações sobre como implementar a imagem do sistema operativo, consulte [criar uma sequência de tarefas para instalar um sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).  

    > [!NOTE]  
    >  Se a sequência de tarefas possuir um passo da sequência de tarefas de criação de partições no disco, não selecione a opção **Transferir Programa** ao implementar a sequência de tarefas.  

-   Se o computador de referência não for um cliente do Configuration Manager ou se pretender executar manualmente a sequência de tarefas no computador de referência, execute o **criar Assistente de suporte de dados de sequência de tarefas** para criar suportes de dados. Para obter informações sobre como criar suportes de dados, consulte [criar suportes de dados](create-bootable-media.md).  

##  <a name="BKMK_CaptureExistingRefComputer"></a> Capturar uma imagem do sistema operativo a partir de um computador de referência existente  
 Quando já tiver um computador de referência preparado para capturar, pode criar uma sequência de tarefas que capture o sistema operativo a partir do computador de referência. Utilizará o passo de sequência de tarefas **Capturar Imagem do Sistema Operativo** para capturar uma ou mais imagens de um computador de referência e armazená-las num ficheiro de imagem (.wim) na partilha de rede especificada. O computador de referência é iniciado no Windows PE através de uma imagem de arranque e cada disco rígido no computador de referência é capturado como uma imagem separada no ficheiro .wim. Se o computador referenciado tiver várias unidades, o ficheiro .wim resultante irá conter uma imagem separada para cada volume. Apenas são capturados os volumes formatados como NTFS ou FAT32. Os volumes com outros formatos e os volumes USB são ignorados.  

 Utilize o procedimento seguinte para capturar uma imagem do sistema operativo a partir de um computador de referência existente.  

#### <a name="to-capture-an-operating-system-from-an-existing-reference-computer"></a>Para capturar um sistema operativo a partir de um computador de referência existente  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente de Criação de Sequência de Tarefas.  

4.  Na página **Criar uma Nova Sequência de Tarefas** , selecione **Criar uma nova sequência de tarefas personalizada**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique um nome e uma descrição para a sequência de tarefas.  

6.  Especifique uma imagem de arranque para a sequência de tarefas. Esta imagem de arranque é utilizada para iniciar o computador de referência com o Windows PE.  Para obter mais informações, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

7.  Conclua o assistente.  

8.  Em **Sequências de Tarefas**, selecione a sequência de tarefas personalizada e, em seguida, no separador **Base** , no grupo **Sequência de Tarefas** , clique em **Editar** , para abrir o editor de sequência de tarefas.  

9. Utilize este passo apenas se o cliente do Configuration Manager está instalado no computador de referência.  

     Clique em **Add**, clique em **imagens**e, em seguida, clique em [preparar ConfigMgr Client para captura](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Este passo de sequência de tarefas usa o cliente do Configuration Manager no computador de referência e prepara-o para captura como parte do processo de geração de imagens.  

    > [!Note]  
    >  A sequência de tarefas não suporta a desinstalar o cliente do Configuration Manager.

10. Clique em **Add**, clique em **imagens**e, em seguida, clique em [preparar Windows para captura](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Esta ação de sequência de tarefas executa o Sysprep e, em seguida, reinicia o computador na imagem de arranque do Windows PE especificada para a sequência de tarefas. O computador de referência não deve ser associado a um domínio para que esta ação seja concluída com êxito.  

11. Clique em **Add**, clique em **imagens**e, em seguida, clique em [Capture Operating System Image](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  Este passo da sequência de tarefas só será executado a partir do Windows PE para capturar os discos rígidos no computador de referência. Configure as definições seguintes para o passo de sequência de tarefas.  

    -   **Nome** e **Descrição**: Opcionalmente, pode alterar o nome do passo de sequência de tarefas e forneça uma descrição.  

    -   **Destino**: Especifique uma pasta de rede partilhada onde a saída. Ficheiro WIM resultante. Este ficheiro contém a imagem de sistema operativo baseada nas definições especificadas utilizando este assistente. Se especificar uma pasta que já contenha um ficheiro .WIM, o ficheiro existente está substituído.  

    -   **Descrição**, **versão**, e **criados por**: Opcionalmente, indique detalhes sobre a imagem que vai capturar.  

    -   **Conta de imagem do sistema operativo para captura**: Especifique a conta do Windows que tem permissões para a rede partilhar que especificou. Clique em **Definir** para especificar o nome dessa conta do Windows.  

     Clique em **OK** para fechar o editor de sequência de tarefas.  

 Implemente a sequência de tarefas num computador de referência de uma das seguintes formas:  

-   Se o computador de referência for um cliente do Configuration Manager, pode implementar a sequência de tarefas na coleção que contenha o computador de referência. Para obter informações sobre como implementar a imagem do sistema operativo, consulte [criar uma sequência de tarefas para instalar um sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).  

-   Se o computador de referência não for um cliente do Configuration Manager ou se pretender executar manualmente a sequência de tarefas no computador de referência, execute o **criar Assistente de suporte de dados de sequência de tarefas** para criar suportes de dados. Para obter informações sobre como criar suportes de dados, consulte [criar suportes de dados](create-bootable-media.md).  

##  <a name="BKMK_BuildandCaptureTSExample"></a> Exemplo de sequência de tarefas para compilar e capturar uma imagem do sistema operativo  
 Utilize a tabela seguinte como guia para criar uma sequência de tarefas que compile e capture uma imagem do sistema operativo. A tabela irá ajudá-lo a decidir a sequência geral para os passos da sequência de tarefas e como organizar e estruturar esses passos da sequência de tarefas em grupos lógicos. A sequência de tarefas que criar pode ser diferente da deste exemplo, podendo conter mais ou menos passos de sequência de tarefas e grupos.  

> [!IMPORTANT]  
>  Utilize sempre o Assistente de Criação de Sequência de Tarefas para criar este tipo de sequência de tarefas.  

 Quando utiliza a opção **Nova Sequência de Tarefas** para criar esta nova sequência de tarefas, alguns dos nomes dos passos de sequência de tarefas são diferentes do que seriam se adicionasse manualmente esses passos a uma sequência já existente. A tabela seguinte apresenta as diferenças de nomenclatura:  

|Nome do Novo Passo de Sequência de Tarefas do Assistente de Sequência de Tarefas|Nome do Passo Equivalente do Editor de Sequência de Tarefas|  
|------------------------------------------------------|-----------------------------------------------|  
|Reiniciar no Windows PE|Arrancar para o Windows PE ou disco rígido|  
|Criar Partições do Disco 0|Formatar e Particionar Disco|  
|Aplicar Controladores de Dispositivo|Aplicar Controladores Automaticamente|  
|Instalar Atualizações|Instalar Atualizações de Software|  
|Aderir ao Grupo de Trabalho|Associar Domínio ou Grupo de Trabalho|  
|Preparar ConfigMgr Client|Prepare ConfigMgr Client for Capture|  
|Preparar Sistema Operativo|Prepare Windows for Capture|  
|Capturar o Computador de Referência|Capturar Imagem do Sistema Operativo|  

|Grupo/Passo de Sequência de Tarefas|Referência|  
|-------------------------------|---------------|  
|Compilar Computador de Referência - **(Novo Grupo de Sequência de Tarefas)**|Criar um grupo de sequência de tarefas. Os grupos de sequência de tarefas mantêm agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.<br /><br /> Este grupo contém as ações necessárias para compilar um computador de referência.|  
|Reiniciar no Windows PE|Utilize este passo de sequência de tarefas para especificar as opções de reinício do computador de destino. Este passo apresentará uma mensagem ao utilizador a indicar que o computador será reiniciado para que a instalação possa continuar.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSInWinPE** . Se o valor associado for igual a **false** , o passo de sequência de tarefas continuará.|  
|Criar Partições do Disco 0|Utilize este passo de sequência de tarefas para especificar as ações necessárias para formatar o disco rígido no computador de destino. O número de disco predefinido é **0**.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSClientCache** . Este passo será executado se a cache do cliente do Configuration Manager não existe.|  
|Aplicar Sistema Operativo|Utilize este passo de sequência de tarefas para instalar uma imagem do sistema operativo especificada no computador de destino. Este passo aplica todas as imagens de volume contidas no ficheiro WIM ao volume de disco sequencial correspondente no computador de destino depois de eliminar primeiro todos os ficheiros nesse volume (à exceção dos arquivos de controle específico do Configuration Manager).|  
|Aplicar Definições do Windows|Utilize este passo de sequência de tarefas para configurar as informações de configuração das definições do Windows para o computador de destino.|  
|Aplicar Definições de Rede|Utilize este passo de sequência de tarefas para especificar as informações de configuração da rede ou do grupo de trabalho para o computador de destino.|  
|Aplicar Controladores de Dispositivo|Utilize este passo de sequência de tarefas para corresponder e instalar controladores como parte da implementação do sistema operativo. Pode permitir que a Configuração do Windows pesquise todas as categorias de controladores existentes ao selecionar **Considerar controladores de todas as categorias** ou limitar as categorias de controladores que a Configuração do Windows pode pesquisar ao selecionar **Limitar a correspondência de controladores para apenas considerar controladores nas categorias selecionadas**.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSMediaType** . Se o valor associado não for igual a **FullMedia** , será executado este passo de sequência de tarefas.|  
|Configurar Windows e ConfigMgr|Utilize este passo de sequência de tarefas para instalar o software de cliente do Configuration Manager. O Configuration Manager instala e regista o GUID do cliente do Configuration Manager. Pode atribuir os parâmetros de instalação necessários na janela **Propriedades de instalação** .|  
|Instalar Atualizações|Utilize este passo de sequência de tarefas para especificar a forma como as atualizações de software são instaladas no computador de destino. O computador de destino não é avaliado relativamente a atualizações de software aplicáveis até ser executado este passo de sequência de tarefas. Nesse ponto, o computador de destino é avaliado relativamente a atualizações de software semelhantes a qualquer outro cliente gerido pelo Configuration Manager.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSMediaType** . Se o valor associado não for igual a **FullMedia** , será executado este passo de sequência de tarefas.|  
|Capturar Computador de Referência - **(Novo Grupo de Sequência de Tarefas)**|Criar outro grupo de sequência de tarefas. Este grupo contém os passos necessários para preparar e capturar um computador de referência.|  
|Aderir ao Grupo de Trabalho|Utilize este passo de sequência de tarefas para especificar as informações necessárias para associar o computador de destino a um grupo de trabalho.|  
|Prepare ConfigMgr Client for Capture|Utilize este passo para tirar o cliente do Configuration Manager no computador de referência e prepara-o para captura como parte do processo de geração de imagens|  
|Preparar Sistema Operativo|Utilize este passo de sequência de tarefas para especificar as opções de Sysprep a utilizar quando capturar as definições do Windows a partir do computador de referência. Este passo de sequência de tarefas executa o Sysprep e, em seguida, reinicia o computador na imagem de arranque do Windows PE especificada para a sequência de tarefas.|  
|Capturar Imagem do Sistema Operativo|Utilize este passo de sequência de tarefas para introduzir uma partilha de rede existente e um ficheiro .WIM específicos a utilizar quando guardar a imagem. Esta localização é utilizada como a localização de origem do pacote quando adicionar um pacote de imagem do sistema operativo com o **Assistente para Adicionar Pacote de Imagem do Sistema Operativo**.|  

 Após ter capturado uma imagem de um computador de referência, não capture outra imagem do sistema operativo do computador de referência, porque as entradas do registo são criadas durante a configuração inicial. Crie um novo computador de referência sempre que capturar a imagem do sistema operativo. Se planear utilizar o mesmo computador de referência para criar imagens de sistema de operativo futuras, desinstale primeiro o cliente do Configuration Manager e, em seguida, reinstalar o cliente de Configuration Manager.  

## <a name="next-steps"></a>Passos seguintes  
[Métodos para implementar sistemas operativos empresariais](methods-to-deploy-enterprise-operating-systems.md)
