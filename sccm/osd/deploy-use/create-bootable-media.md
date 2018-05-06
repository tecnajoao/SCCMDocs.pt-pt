---
title: Criar suportes de dados
titleSuffix: Configuration Manager
description: Suportes de dados no Configuration Manager tornam mais fácil instalar uma nova versão do Windows ou substituir um computador e transferir definições.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3b2ce474488ebf02c3a3c4a82def91d706b6bfc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>Criar suportes de dados com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Suportes de dados no Configuration Manager contém a imagem de arranque, comandos de Pré-início opcionais e os ficheiros associados e ficheiros do Configuration Manager. Utilize suportes de dados pré-configurados para os seguintes cenários de implementação do sistema operativo:  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir definições](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> Criar suportes de dados de arranque  
 Quando inicia o sistema com o suporte de dados de arranque, o computador de destino é iniciado, estabelece ligação à rede e obtém a sequência de tarefas, a imagem do sistema operativo e qualquer outro conteúdo necessário a partir dessa rede. Dado que a sequência de tarefas não está no suporte de dados, pode alterar a sequência de tarefas ou o conteúdo sem ter de recriar o suporte de dados. Os pacotes dos suportes de dados de arranque não estão encriptados. É necessário tomar as medidas de segurança apropriadas, como adicionar uma palavra-passe ao suporte de dados, para garantir que o conteúdo do pacote está protegido contra utilizadores não autorizados.  

 Antes de criar suportes de dados de arranque através do Assistente de Criação de Suporte de Dados da Sequência de Tarefas, certifique-se de que todas as condições seguintes são preenchidas:  

|Tarefa|Descrição|  
|----------|-----------------|  
|Imagem de arranque|Considere o seguinte sobre a imagem de arranque que irá utilizar na sequência de tarefas para implementar o sistema operativo:<br /><br /> -A arquitetura da imagem de arranque tem de ser adequada à arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.<br />-Certifique-se de que a imagem de arranque contém os controladores de armazenamento em massa e de rede que são necessárias para aprovisionar o computador de destino.|  
|Criar uma sequência de tarefas para implementar um sistema operativo|Como parte do suporte de dados de arranque, tem de especificar a sequência de tarefas para implementar o sistema operativo. Para obter os passos criar uma nova sequência de tarefas, consulte [criar uma sequência de tarefas para instalar um sistema operativo](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).|  
|Distribuir todo o conteúdo associado à sequência de tarefas|Tem de distribuir todo o conteúdo exigido pela sequência de tarefas por, pelo menos, um ponto de distribuição. Isto inclui a imagem de arranque e outros ficheiros de pré-início associados. O assistente recolhe as informações a partir do ponto de distribuição ao criar o suporte de dados de arranque. Tem de ter direitos de acesso de **Leitura** à biblioteca de conteúdos desse ponto de distribuição.  Para obter mais informações, consulte [sobre a biblioteca de conteúdos](../../core/plan-design/hierarchy/the-content-library.md).|  
|Preparar a pen USB amovível|Para uma pen USB amovível:<br /><br /> Se planear utilizar uma pen USB amovível, a pen USB tem de estar ligada ao computador em que o assistente é executado e ser detetável pelo Windows como um dispositivo amovível. Quando cria o suporte de dados, o assistente escreve diretamente na pen USB. O suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar um suporte de dados autónomo numa pen USB cujo conteúdo inclua um ficheiro com tamanho superior a 4 GB.|  
|Criar uma pasta de saída|Para um conjunto de CD/DVD:<br /><br /> Antes de executar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas para criar suportes de dados para um conjunto de CDs ou DVDs, tem de criar uma pasta para os ficheiros de saída criados pelo assistente. O suporte de dados criado para um conjunto de CDs ou DVDs é escrito em formato de ficheiros .iso diretamente na pasta.|  

 Utilize o procedimento seguinte para criar suportes de dados de arranque.  

### <a name="to-create-bootable-media"></a>Para criar suportes de dados de arranque  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4.  Na página **Selecione o Tipo de Suporte de Dados** , especifique as opções seguintes e clique em **Seguinte**.  

    -   Selecione **Suporte de dados de arranque**.  

    -   Opcionalmente, se só pretender permitir a implementação do sistema operativo sem exigir a intervenção do utilizador, selecione **Permitir a implementação do sistema operativo autónoma**.  

        > [!IMPORTANT]  
        >  Ao selecionar esta opção, não serão solicitadas ao utilizador informações para a configuração de rede nem para sequências de tarefas opcionais. No entanto, continua a ser solicitada uma palavra-passe ao utilizador se o suporte de dados estiver configurado com proteção por palavra-passe.  

5.  Na página **Gestão de Suporte de Dados** , especifique uma das seguintes opções e clique em **Seguinte**.  

    -   Selecione **Suporte de dados dinâmico** se pretender permitir que um ponto de gestão redirecione o suporte de dados para outro ponto de gestão, com base na localização do cliente nos limites do site.  

    -   Selecione **Suporte de dados baseado no site** se pretender que o suporte de dados entre em contacto apenas com o ponto de gestão especificado.  

6.  Na página **Tipo de Suporte de Dados** , especifique se o suporte de dados é uma pen USB ou um conjunto de CD/DVD e, em seguida, clique para configurar o seguinte:  

    > [!IMPORTANT]  
    >  O suporte de dados autónomo utiliza um sistema de ficheiros FAT32. Não é possível criar um suporte de dados autónomo numa pen USB cujo conteúdo inclua um ficheiro com tamanho superior a 4 GB.  

    -   Se selecionar **Pen USB**, especifique a unidade onde pretende armazenar o conteúdo.  

    -   Se selecionar **Conjunto CD/DVD**, especifique a capacidade do suporte de dados e o nome e caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo:  **\\\servername\folder\outputfile.iso**  

         Se a capacidade do suporte de dados for demasiado pequena para armazenar todo o conteúdo, serão criados vários ficheiros e tem de armazenar o conteúdo em vários CDs ou DVDs. Quando vários suportes de dados é necessária, o Configuration Manager adiciona um número sequencial ao nome de cada ficheiro de saída criado. Além disso, se implementar uma aplicação juntamente com o sistema operativo e a aplicação não couber num único suporte de dados, o Configuration Manager armazenará a aplicação em vários suportes de dados. Quando o suporte de dados autónomo for executado, o Configuration Manager pede ao utilizador o suporte de dados seguinte em que a aplicação se encontra armazenada.  

        > [!IMPORTANT]  
        >  Se selecionar uma imagem .iso existente, o Assistente de Criação de Suporte de Dados da Sequência de Tarefas elimina essa imagem da unidade ou partilha logo que avança para a página seguinte do assistente. A imagem existente será eliminada, mesmo que em seguida cancele o assistente.  

     Clique em **Seguinte**.  

7.  Na página **Segurança** , especifique as seguintes opções e clique em **Seguinte**.  

    -   Selecione o **ativar suporte para computadores desconhecidos** caixa de verificação para permitir que o suporte de dados implementar um sistema operativo num computador que não seja gerido pelo Configuration Manager. Não há nenhum registo destes computadores na base de dados do Configuration Manager.  

         Os computadores desconhecidos incluem o seguinte:  

        -   Um computador em que o cliente do Configuration Manager não está instalado  

        -   Um computador que não é importado para o Configuration Manager  

        -   Um computador que não é detetado pelo Configuration Manager  

    -   Selecione a caixa de verificação **Proteger suporte de dados com uma palavra-passe** e introduza uma palavra-passe segura para ajudar a proteger o suporte de dados contra acesso não autorizado. Quando especificar uma palavra-passe, o utilizador terá de fornecer essa palavra-passe para utilizar o suporte de dados de arranque.  

        > [!IMPORTANT]  
        >  Como procedimento de segurança recomendado, atribua sempre uma palavra-passe para ajudar a proteger o suporte de dados de arranque.  

    -   Para comunicações HTTP, selecione **Criar um certificado de suporte de dados autoassinado**e especifique as datas de início e de expiração do certificado.  

    -   Para comunicações HTTPS, selecione **Importar certificado PKI**e especifique o certificado a importar e a respetiva palavra-passe.  

         Para mais informações sobre este certificado de cliente que é utilizado para imagens de arranque, consulte [requisitos dos certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Afinidade dispositivo / utilizador**: Para suportar a gestão centrada no utilizador no Configuration Manager, especifique como pretende que o suporte de dados associe utilizadores ao computador de destino. Para obter mais informações sobre como implementação de sistemas operativos suporta a afinidade dispositivo / utilizador, consulte [associar utilizadores um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

        -   Especifique **Permitir afinidade dispositivo/utilizador com aprovação automática** se pretender que o suporte de dados associe automaticamente utilizadores ao computador de destino. Esta funcionalidade baseia-se nas ações da sequência de tarefas que implementa o sistema operativo. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino quando implementa o sistema operativo no computador de destino.  

        -   Especifique **Permitir afinidade dispositivo/utilizador com aprovação pendente pelo administrador** se pretender que o suporte de dados associe utilizadores ao computador de destino após concessão da aprovação. Esta funcionalidade baseia-se no âmbito da sequência de tarefas que implementa o sistema operativo.  Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino, mas aguarda a aprovação de um utilizador administrativo antes da implementação do sistema operativo.  

        -   Especifique **Não permitir afinidade dispositivo/utilizador** se não pretender que o suporte de dados associe utilizadores ao computador de destino. Neste cenário, a sequência de tarefas não associa utilizadores ao computador de destino durante a implementação do sistema operativo.  

8.  Na página **Imagem de arranque** , especifique as seguintes opções e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de arranque que é distribuída deve ser adaptada à arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.  

    -   Na caixa **Imagem de arranque** , especifique a imagem de arranque que inicia o computador de destino.  

    -   Na caixa **Ponto de distribuição** , especifique o ponto de distribuição onde reside a imagem de arranque. O assistente obtém a imagem de arranque do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        >  Tem de ter direitos de acesso de **Leitura** à biblioteca de conteúdos no ponto de distribuição.  

    -   Se criar suportes de dados de arranque baseados no site na página **Gestão de Suporte de Dados** do assistente, especifique um ponto de gestão de um site primário na caixa **Ponto de gestão** .  

    -   Se criar suportes de dados de arranque dinâmicos na página **Gestão de Suporte de Dados** do assistente, especifique os pontos de gestão do site primário a utilizar e uma ordem de prioridade para as comunicações iniciais em **Pontos de gestão associados**.  

9. Na página **Personalização** , especifique as seguintes opções e clique em **Seguinte**.  

    -   Especifique as variáveis utilizadas pela sequência de tarefas para implementar o sistema operativo.  

    -   Especifique os comandos de pré-início que pretende executar antes da execução da sequência de tarefas. Os comandos de pré-início são um script ou um ficheiro executável que pode interagir com o utilizador no Windows PE antes da execução da sequência de tarefas para instalar o sistema operativo. Para obter mais informações, consulte [comandos para suporte de dados de sequência de tarefas de Pré-início](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Durante a criação de suportes de dados de sequência de tarefas, a sequência de tarefas escreve o ID de pacote e da linha de comandos, incluindo o valor das eventuais variáveis de sequência de tarefas, para o ficheiro de registo CreateTSMedia.log no computador que executa a consola do Configuration Manager de Pré-início. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

         Opcionalmente, selecione a caixa de verificação **Incluir ficheiros para o comando de pré-início** para incluir os ficheiros eventualmente necessários para o comando de pré-início.  

10. Conclua o assistente.  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>Criar suportes de dados numa unidade USB a partir de uma partilha de rede
As informações nesta secção ajudam-o a criar suportes de dados numa unidade flash USB, quando a unidade flash não está ligada ao computador que executa a consola do Configuration Manager. Para criar suportes de dados na unidade USB, pode criar suportes de dados de arranque de sequência de tarefas, montar o ficheiro ISO e transferir os ficheiros do ficheiro ISO na unidade USB.

1. [Criar o suporte de dados de arranque da sequência de tarefas](#to-create-task-boobable-media). No **tipo de suporte** página, selecione **conjunto CD/DVD**. O assistente escreve os ficheiros de saída para a localização que especificar. Por exemplo:  **\\\servername\folder\outputfile.iso**.  
2. Prepare a pen USB amovível. A unidade tem de ser formatado, vazio e arranque.
3. Montar o ficheiro ISO a partir da localização de partilha e transferir os ficheiros do ficheiro ISO na unidade USB.

## <a name="next-steps"></a>Passos seguintes  
[Utilizar suportes de dados de arranque para implementar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  
