---
title: Criar uma sequência de tarefas para instalar um sistema operativo
titleSuffix: Configuration Manager
description: Utilize sequências de tarefas no System Center Configuration Manager para instalar automaticamente uma imagem do sistema operativo e outros conteúdos num computador de destino.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 604cf10c660cd1f26513a6a34b370d380635504b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421081"
---
# <a name="create-a-task-sequence-to-install-an-operating-system-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para instalar um sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize sequências de tarefas no System Center Configuration Manager para instalar automaticamente uma imagem do sistema operativo num computador de destino. Terá de criar uma sequência de tarefas que faça referência a uma imagem de arranque utilizada para iniciar o computador de destino, à imagem do sistema operativo que pretende instalar no computador de destino e a eventuais conteúdos adicionais, tais como outras aplicações ou atualizações de software que pretenda instalar. Em seguida, tem de implementar a sequência de tarefas na coleção que contém o computador de destino.  

##  <a name="BKMK_InstallOS"></a> Criar uma sequência de tarefas para instalar um sistema operativo  
 Existem muitos cenários para implementar um sistema operativo em computadores no seu ambiente. Na maioria dos casos, irá criar uma sequência de tarefas e selecionar **Instalar um pacote de imagem existente** , no Assistente de Criação de Sequência de Tarefas, para instalar o sistema operativo, migrar as definições de utilizador, aplicar atualizações de software e instalar aplicações. Antes de criar uma sequência de tarefas para instalar um sistema operativo, é necessário o seguinte:   

-   **Necessário**  

    -   O [imagem de arranque](../get-started/manage-boot-images.md) tem de estar disponível na consola do Configuration Manager.  

    -   Uma [imagem do sistema operativo](../get-started/manage-operating-system-images.md) tem de estar disponível na consola do Configuration Manager.  

-   **Necessário (se utilizado)**  

    -   [Atualizações de software](../../sum/get-started/synchronize-software-updates.md) têm de ser sincronizadas na consola do Configuration Manager.  

    -   [Aplicativos](../../apps/deploy-use/create-applications.md) deve ser adicionado à consola do Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-installs-an-operating-system"></a>Para criar uma sequência de tarefas para instalar um sistema operativo  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3. No separador **Home Page**, no grupo **Criar**, clique em **Criar Sequência de Tarefas** para iniciar o Assistente de Criação de Sequência de Tarefas.  

4. Na página **Criar uma Nova Sequência de Tarefas** , clique em **Instalar um pacote de imagem existente**e clique em **Seguinte**.  

5. Na página **Informações da Sequência de Tarefas** , especifique as seguintes definições e clique em **Seguinte**.  

   -   **Nome da sequência de tarefas**: Especifique um nome que identifique a sequência de tarefas.  

   -   **Descrição**: Especifique uma descrição da tarefa que é executada pela sequência de tarefas.  

   -   **Imagem de arranque**: Especifique a imagem de arranque que instala o sistema operativo no computador de destino. A imagem de arranque contêm uma versão do Windows PE que é utilizada para instalar o sistema operativo, bem como os controladores de dispositivo adicionais que sejam necessários. Para obter informações, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

       > [!IMPORTANT]  
       >  A arquitetura da imagem de arranque deve ser compatível com a arquitetura de hardware do computador de destino.  

6. Na página **Instalar o Windows** , especifique as seguintes definições e clique em **Seguinte**.  

   -   **Pacote de imagem**: Especifique o pacote que contém a imagem de sistema operativo a instalar. Para obter mais informações, consulte [gerir imagens de sistema operativo](../get-started/manage-operating-system-images.md).  

   -   **Imagem**: Se o pacote de imagem do sistema operativo tiver várias imagens, especifique o índice da imagem do sistema operativo a instalar.  

   -   **Particionar e formatar o computador de destino que instala o sistema operativo**: Especifique se pretende que a sequência de tarefas particione e formate o computador de destino antes do sistema operativo é instalado.  

   -   **Chave de produto**: Especifique a chave de produto para o sistema operativo do Windows instalar. Pode especificar chaves de licenciamento em volume codificadas e chaves de produto padrão. Se utilizar uma chave de produto não codificada, terá de separar cada grupo de 5 carateres por um hífen (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

   -   **Modo de licenciamento de servidor**: Especifique se a licença de servidor é **por posto de trabalho**, **por servidor**, ou não se é especificada nenhuma licença. Se a licença do servidor for **Por servidor**, especifique também o número máximo de ligações de servidor.  

   -   Especifique como lidar com a conta de administrador utilizada quando a imagem de sistema operativo é implementada.  

       -   **Desativar a conta de administrador local**: Especifique se a conta de administrador local é desativada quando a imagem de sistema operativo é implementada.  

       -   **Utilize sempre a mesma palavra-passe de administrador**: Especifique se a mesma palavra-passe é utilizada para a conta de administrador local em todos os computadores em que a imagem de sistema operativo é implementada.  

7. Na página **Configurar Rede** , especifique as seguintes definições e clique em **Seguinte**.  

   -   **Junte-se a um grupo de trabalho**: Especifique se pretende adicionar o computador de destino a um grupo de trabalho.  

   -   **Aderir a um domínio**: Especifique se pretende adicionar o computador de destino a um domínio. Em **Domínio**, especifique o nome do domínio.  

       > [!IMPORTANT]  
       >  Pode navegar para localizar domínios na floresta local, mas tem de especificar o nome de domínio de uma floresta remota.  

        Também pode especificar uma unidade organizacional (UO). Trata-se de uma definição opcional que especifica o nome único LDAP X.500 da UO em que deverá ser criada a conta de computador, caso ainda não exista.  

   -   **Conta**: Especifique o nome de utilizador e palavra-passe para a conta que tem permissões para aderir ao domínio especificado. Por exemplo: *domínio\utilizador* ou *%variable%*.  

       > [!IMPORTANT]  
       >  Se pretender migrar as definições de domínio ou as definições de grupo de trabalho, terá de introduzir as credenciais de domínio apropriadas.  

8. Sobre o **instalar o Configuration Manager** , especifique o pacote de cliente do Configuration Manager para instalar no computador de destino e, em seguida, clique em **próxima**.  

9. Na página **Migração de Estado** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Capturar definições do utilizador**: Especifique se a sequência de tarefas captura o estado do utilizador. Para obter mais informações sobre como capturar e restaurar o estado do utilizador, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

    -   **Capturar definições de rede**: Especifique se a sequência de tarefas captura definições de rede do computador de destino. Pode capturar a associação do domínio ou do grupo de trabalho, além das definições da placa de rede.  

    -   **Capturar definições do Microsoft Windows**:  Especifique se a sequência de tarefas captura definições do Windows do computador de destino antes da imagem do sistema operativo está instalada. Pode capturar o nome do computador, o nome do utilizador e da organização registados e as definições de fuso horário.  

10. Na página **Incluir Atualizações** , especifique se devem ser instaladas as atualizações de software necessárias, todas as atualizações de software ou nenhuma atualização de software e clique em **Seguinte**. Se especificar a instalação de atualizações de software, o Configuration Manager instala apenas as atualizações de software que são direcionadas para as coleções que o computador de destino é um membro do.  

11. Na página **Instalar Aplicações** , especifique as aplicações a instalar no computador de destino e clique em **Seguinte**. Se especificar várias aplicações, poderá também especificar que a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

12. Conclua o assistente.  

    Agora, pode implementar a sequência de tarefas numa coleção de computadores.  Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_InstallExistingOSImageTSExample"></a> Exemplo de sequência de tarefas para instalar uma imagem do sistema operativo existente  
 Utilize a tabela seguinte como guia para criar uma sequência de tarefas que implemente um sistema operativo utilizando uma imagem do sistema operativo existente. A tabela irá ajudá-lo a determinar a sequência geral para os passos da sequência de tarefas e como organizar e estruturar esses passos da sequência de tarefas em grupos lógicos. A sequência de tarefas que criar pode ser diferente da deste exemplo, podendo conter mais ou menos grupos e passos de sequência de tarefas.  

> [!IMPORTANT]  
>  Tem de utilizar sempre o Assistente de Criação de Sequência de Tarefas para criar esta sequência de tarefas.  

 Quando utiliza o Assistente de Criação de Sequência de Tarefas para criar esta nova sequência de tarefas, alguns dos nomes dos passos de sequência de tarefas são diferentes daquilo que seriam se adicionasse manualmente estes passos de sequência de tarefas a uma sequência de tarefas existente. A tabela seguinte apresenta as diferenças de nomenclatura:  

|Nome do Passo de Sequência de Tarefas do Assistente de Criação de Sequência de Tarefas|Nome do Passo Equivalente do Editor de Sequência de Tarefas|  
|---------------------------------------------------------|-----------------------------------------------|  
|Solicitar Armazenamento de Estados do Utilizador|Solicitar Armazenamento de Estados|  
|Capturar Definições e Ficheiros do Utilizador|Capturar Estado do Utilizador|  
|Libertar Armazenamento de Estados do Utilizador|Disponibilizar Armazenamento de Estados|  
|Reiniciar no Windows PE|Arrancar para o Windows PE ou disco rígido|  
|Criar Partições do Disco 0|Formatar e Particionar Disco|  
|Restaurar Definições e Ficheiros do Utilizador|Restaurar Estado do Utilizador|  

|Passo ou Grupo de Sequência de Tarefas|Descrição|  
|---------------------------------|-----------------|  
|Capturar ficheiros e definições - **(novo grupo de sequência de tarefas)**|Criar um grupo de sequência de tarefas. Os grupos de sequência de tarefas mantêm agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.<br /><br /> Este grupo contém os passos necessários para capturar ficheiros e definições do sistema operativo de um computador de referência.|  
|Capturar Definições do Windows|Utilize este passo de sequência de tarefas para identificar as definições do Microsoft Windows para capturar a partir do computador de referência. Pode capturar o nome do computador, informações do utilizador e da organização e as definições de fuso horário.|  
|Capturar definições de rede|Utilize este passo de sequência de tarefas para capturar definições de rede a partir do computador de referência. Pode capturar a associação a domínios ou grupos de trabalho do computador de referência e as informações de definições da placa de rede.|  
|Capturar definições e ficheiros de utilizador - **(nova tarefa subgrupo de sequência)**|Crie um grupo de sequência de tarefas dentro de um grupo de sequência de tarefas. Este subgrupo contém os passos necessários para capturar dados de estado do utilizador. De forma idêntica ao grupo inicial que adicionou, este subgrupo mantém agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.|  
|Solicitar Armazenamento de Estados do Utilizador|Utilize este passo de sequência de tarefas para pedir acesso a um ponto de migração de estado onde os dados de estado de utilizador estão armazenados. Pode configurar este passo de sequência de tarefas para capturar ou restaurar as informações de estado do utilizador.|  
|Capturar Definições e Ficheiros do Utilizador|Utilize este passo de sequência de tarefas para utilizar a ferramenta de migração de estado de utilizador (USMT) para capturar o estado do utilizador e as definições do computador de referência que irá receber a sequência de tarefas associada a este passo de tarefa. Pode capturar as opções padrão ou configurar as opções a capturar.|  
|Libertar Armazenamento de Estados do Utilizador|Utilize este passo de sequência de tarefas para notificar o ponto de migração de estado de que a ação de captura ou restauro está concluída.|  
|Instalar sistema operativo - **(novo grupo de sequência de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para instalar e configurar o ambiente Windows PE.|  
|Reiniciar no Windows PE|Utilize este passo de sequência de tarefas para especificar as opções de reinício para o computador de destino que recebe esta sequência de tarefas. Este passo apresentará uma mensagem ao utilizador a indicar que o computador será reiniciado para que a instalação possa continuar.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSInWinPE** . Se o valor associado for igual a **false** , o passo de sequência de tarefas continuará.|  
|Criar Partições do Disco 0|Este passo de sequência de tarefas especifica as ações necessárias para formatar o disco rígido no computador de destino. O número de disco predefinido é **0**.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSClientCache** . Este passo será executado se a cache do cliente do Configuration Manager não existe.|  
|Aplicar Sistema Operativo|Utilize este passo de sequência de tarefas para instalar a imagem do sistema operativo no computador de destino. Este passo aplica todas as imagens de volume contidas no ficheiro WIM ao volume de disco sequencial correspondente no computador de destino depois de eliminar primeiro todos os ficheiros nesse volume (à exceção dos arquivos de controle específico do Configuration Manager). Pode especificar um ficheiro de resposta **sysprep** , bem como configurar a partição de disco a utilizar para a instalação.|  
|Aplicar Definições do Windows|Utilize este passo de sequência de tarefas para configurar as informações de configuração das definições do Windows para o computador de destino. As definições do Windows que pode aplicar são informações da organização e do utilizador, informações da chave de licença ou produto, fuso horário e a palavra-passe de administrador local.|  
|Aplicar Definições de Rede|Utilize este passo de sequência de tarefas para especificar as informações de configuração da rede ou do grupo de trabalho para o computador de destino. Também pode especificar se o computador utiliza um servidor DHCP ou pode atribuir estaticamente as informações de endereço IP.|  
|Aplicar Controladores de Dispositivo|Utilize este passo de sequência de tarefas para instalar controladores como parte da implementação do sistema operativo. Pode permitir que a Configuração do Windows pesquise todas as categorias de controladores existentes ao selecionar **Considerar controladores de todas as categorias** ou limitar as categorias de controladores que a Configuração do Windows pode pesquisar ao selecionar **Limitar a correspondência de controladores para apenas considerar controladores nas categorias selecionadas**.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSMediaType** . Este passo de sequência de tarefas é executado apenas se o valor da variável não for igual a **FullMedia**.|  
|Aplicar Pacote de Controlador|Utilize este passo de sequência de tarefas para disponibilizar todos os controladores de dispositivo de um pacote de controladores para utilização pela configuração do Windows.|  
|Configurar sistema operativo - **(novo grupo de sequência de tarefas)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para configurar o sistema operativo instalado.|  
|Configurar Windows e ConfigMgr|Utilize este passo de sequência de tarefas para instalar o software de cliente do Configuration Manager. O Configuration Manager instala e regista o GUID do cliente do Configuration Manager. Pode atribuir os parâmetros de instalação necessários na janela **Propriedades de instalação** .|  
|Instalar Atualizações|Utilize este passo de sequência de tarefas para especificar a forma como as atualizações de software são instaladas no computador de destino. O computador de destino não é avaliado relativamente a atualizações de software aplicáveis até ser executado este passo de sequência de tarefas. Nesse ponto, o computador de destino é avaliado relativamente a atualizações de software semelhantes a qualquer outro cliente gerido pelo Configuration Manager.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSMediaType** . Este passo de sequência de tarefas é executado apenas se o valor da variável não for igual a **FullMedia**.|  
|Restaurar definições e ficheiros de utilizador - **(nova tarefa subgrupo de sequência)**|Crie outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para restaurar as definições e ficheiros do utilizador.|  
|Solicitar Armazenamento de Estados do Utilizador|Utilize este passo de sequência de tarefas para pedir acesso a um ponto de migração de estado onde os dados de estado de utilizador estão armazenados.|  
|Restaurar Definições e Ficheiros do Utilizador|Utilize este passo de sequência de tarefas para iniciar a ferramenta de migração de estado (USMT) do utilizador para restaurar o estado de utilizador e as definições para um computador de destino.|  
|Libertar Armazenamento de Estados do Utilizador|Utilize este passo de sequência de tarefas para notificar o ponto de migração de estado de que os dados de estado do utilizador já não são necessários.|  
