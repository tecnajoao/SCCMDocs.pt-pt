---
title: Criar suportes de dados
titleSuffix: Configuration Manager
description: "Crie suportes de dados no System Center Configuration Manager, para simplificar a implementação do Windows em vários cenários."
ms.custom: na
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
caps.latest.revision: "12"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: a26fc3daf17aefe24a46ece561fc2ceaf5284ffb
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/12/2017
---
# <a name="create-prestaged-media-with-system-center-configuration-manager"></a>Criar suportes de dados com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Suporte de dados pré-configurado no System Center Configuration Manager é um ficheiro de formato WIM (Windows Imaging) que pode ser instalado num computador bare-metal pelo fabricante ou num centro de transição empresarial que não está ligado ao ambiente do Configuration Manager.  
O suporte de dados pré-configurado contém a imagem de arranque utilizada para iniciar o computador de destino e a imagem de sistema operativo aplicada no computador de destino. Também pode especificar aplicações, pacotes e pacotes de controladores para incluir como parte do suporte de dados pré-configurado. A sequência de tarefas que implementa o sistema operativo não está incluída no suporte de dados. O suporte de dados pré-configurado é aplicado no disco rígido do computador novo antes do seu envio para o utilizador final. Utilize suportes de dados pré-configurados para os seguintes cenários de implementação do sistema operativo:  

-   [Criar uma imagem para um OEM de fábrica ou um depósito local](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Implementar o Windows to Go](deploy-windows-to-go.md)  

 Quando o computador é iniciado pela primeira vez após a aplicação do suporte de dados pré-configurado, o computador inicia o Windows PE e estabelece ligação a um ponto de gestão para localizar a sequência de tarefas que conclui o processo de implementação do sistema operativo. Pode especificar aplicações, pacotes e pacotes de controladores para incluir como parte do suporte de dados pré-configurado. Quando implementa uma sequência de tarefas que utiliza suportes de dados pré-configurados, o assistente verifica primeiro a presença de conteúdo válido na cache local da sequência de tarefas e, se o conteúdo não puder ser localizado ou tiver sido revisto, o assistente transfere-o a partir do ponto de distribuição.  

##  <a name="BKMK_CreatePrestagedMedia"></a> Como Criar Suportes de Dados Pré-configurados  
 Antes de criar suportes de dados pré-configurados através do Assistente de Criação de Suporte de Dados da Sequência de Tarefas, certifique-se de que todas as condições seguintes são preenchidas:  

|Tarefa|Descrição|  
|----------|-----------------|  
|Imagem de arranque|Considere o seguinte sobre a imagem de arranque que irá utilizar na sequência de tarefas para implementar o sistema operativo:<br /><br /> -A arquitetura da imagem de arranque tem de ser adequada à arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.<br />-Certifique-se de que a imagem de arranque contém os controladores de armazenamento em massa e de rede que são necessárias para aprovisionar o computador de destino.|  
|Criar uma sequência de tarefas para implementar um sistema operativo|Como parte do suporte de dados pré-configurado, tem de especificar a sequência de tarefas para implementar o sistema operativo.<br /><br /> -Para obter os passos criar uma nova sequência de tarefas, consulte [criar uma sequência de tarefas para instalar um sistema operativo](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md).<br />-Para mais informações sobre sequências de tarefas, consulte [gerir sequências de tarefas para automatizar tarefas](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).|  
|Distribuir todo o conteúdo associado à sequência de tarefas|Tem de distribuir todo o conteúdo exigido pela sequência de tarefas por, pelo menos, um ponto de distribuição. Isto inclui a imagem de arranque, a imagem do sistema operativo e outros ficheiros associados. O assistente recolhe as informações a partir do ponto de distribuição, ao criar o suporte de dados autónomo. Tem de ter direitos de acesso de **Leitura** à biblioteca de conteúdos desse ponto de distribuição.  Para obter mais informações, consulte [sobre a biblioteca de conteúdos](../../core/plan-design/hierarchy/the-content-library.md).|  
|Disco rígido no computador de destino|O disco rígido do computador de destino terá de ser formatado antes de o suporte de dados pré-configurado ser preparado no disco rígido do computador. Se o disco rígido não estiver formatado quando o suporte de dados for aplicado, a sequência de tarefas que implementa o sistema operativo falhará ao tentar iniciar o computador de destino.|  

> [!NOTE]  
>  O assistente suporte de dados de criação de sequência de tarefas define a seguinte condição variável de sequência de tarefas no suporte de dados: **smstsmediatype = OEMMedia**. Pode utilizar esta condição na sua sequência de tarefas.  

 Utilize o procedimento seguinte para criar suportes de dados pré-configurados.  

#### <a name="to-create-prestaged-media"></a>Para criar um suporte de dados pré-configurado  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4.  Na página **Selecione o Tipo de Suporte de Dados** , especifique as informações seguintes e clique em **Seguinte**.  

    -   Selecione **Suporte de dados pré-configurado**.  

    -   Opcionalmente, se pretender permitir a implementação do sistema operativo sem exigir a intervenção do utilizador, selecione **Permitir a implementação do sistema operativo autónoma**. Ao selecionar esta opção, não serão solicitadas ao utilizador informações para a configuração de rede nem para sequências de tarefas opcionais. No entanto, continua a ser solicitada uma palavra-passe ao utilizador se o suporte de dados estiver configurado com proteção por palavra-passe.  

5.  Na página **Gestão de Suporte de Dados** , especifique as informações seguintes e clique em **Seguinte**.  

    -   Selecione **Suporte de dados dinâmico** se pretender permitir que um ponto de gestão redirecione o suporte de dados para outro ponto de gestão, com base na localização do cliente nos limites do site.  

    -   Selecione **Suporte de dados baseado no site** se pretender que o suporte de dados entre em contacto apenas com o ponto de gestão especificado.  

6.  Na página **Propriedades do Suporte de Dados**  , especifique as informações seguintes e, em seguida, clique em **Seguinte**.  

    -   **Criado pelo**: Especifique quem criou o suporte de dados.  

    -   **Versão**: Especifique o número de versão do suporte de dados.  

    -   **Comentário**: Especifique uma descrição exclusiva da que é utilizado o suporte de dados.  

    -   **Ficheiro de multimédia**: Especifique o nome e caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo:  **\\\servername\folder\outputfile.wim**  

7.  Na página **Segurança** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Selecione o **ativar suporte para computadores desconhecidos** caixa de verificação para permitir que o suporte de dados implementar um sistema operativo num computador que não seja gerido pelo Configuration Manager. Não há nenhum registo destes computadores na base de dados do Configuration Manager.  Para obter mais informações, consulte [preparar implementações de computadores desconhecidos](../get-started/prepare-for-unknown-computer-deployments.md).  

    -   Selecione a caixa de verificação **Proteger suporte de dados com uma palavra-passe** e introduza uma palavra-passe segura para ajudar a proteger o suporte de dados contra acesso não autorizado. Quando especificar uma palavra-passe, o utilizador terá de fornecer essa palavra-passe para utilizar o suporte de dados pré-configurado.  

        > [!IMPORTANT]  
        >  Como procedimento de segurança recomendado, atribua sempre uma palavra-passe para ajudar a proteger o suporte de dados pré-configurado.  

    -   Para comunicações HTTP, selecione **Criar um certificado de suporte de dados autoassinado**e especifique as datas de início e de expiração do certificado.  

    -   Para comunicações HTTPS, selecione **Importar certificado PKI**e especifique o certificado a importar e a respetiva palavra-passe.  

         Para mais informações sobre este certificado de cliente que é utilizado para imagens de arranque, consulte [requisitos dos certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Afinidade dispositivo / utilizador**: Para suportar a gestão centrada no utilizador no Configuration Manager, especifique como pretende que o suporte de dados associe utilizadores ao computador de destino. Para obter mais informações sobre como implementação de sistemas operativos suporta a afinidade dispositivo / utilizador, consulte [associar utilizadores um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

        -   Especifique **Permitir afinidade dispositivo/utilizador com aprovação automática** se pretender que o suporte de dados associe automaticamente utilizadores ao computador de destino. Esta funcionalidade baseia-se nas ações da sequência de tarefas que implementa o sistema operativo. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino quando implementa o sistema operativo no computador de destino.  

        -   Especifique **Permitir afinidade dispositivo/utilizador com aprovação pendente pelo administrador** se pretender que o suporte de dados associe utilizadores ao computador de destino após concessão da aprovação. Esta funcionalidade baseia-se no âmbito da sequência de tarefas que implementa o sistema operativo. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino, mas aguarda a aprovação de um utilizador administrativo antes da implementação do sistema operativo.  

        -   Especifique **Não permitir afinidade dispositivo/utilizador** se não pretender que o suporte de dados associe utilizadores ao computador de destino. Neste cenário, a sequência de tarefas não associa utilizadores ao computador de destino durante a implementação do sistema operativo.  

8.  Na página **Sequência de Tarefas** , especifique a sequência de tarefas que será executada no computador de destino. O conteúdo referenciado pela sequência de tarefas é apresentado em **Esta sequência de tarefas referencia o seguinte conteúdo**. Verifique o conteúdo e, em seguida, clique em **Seguinte**.  

9. Na página **Imagem de arranque** , especifique as seguintes informações e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de arranque que é distribuída deve ser adaptada à arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.  

    -   Na caixa **Imagem de arranque** , especifique a imagem de arranque que inicia o computador de destino. Para obter mais informações, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

    -   Na caixa **Ponto de distribuição** , especifique o ponto de distribuição onde reside a imagem de arranque. O assistente obtém a imagem de arranque do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        >  Tem de ter direitos de acesso de **Leitura** para a biblioteca de conteúdos do ponto de distribuição. Para obter mais informações, consulte [sobre a biblioteca de conteúdos](../../core/plan-design/hierarchy/the-content-library.md).  

    -   Se tiver selecionado **Suporte de dados baseado no site** na página **Gestão de Suporte de Dados** do assistente, na caixa **Ponto de gestão** , especifique um ponto de gestão de um site primário.  

    -   Se tiver selecionado **Suporte de dados dinâmico** na página **Gestão de Suporte de Dados** do assistente, na caixa **Pontos de gestão associados** , especifique os pontos de gestão do site primário a utilizar e uma ordem de prioridades para as comunicações iniciais.  

10. Na página **Imagens** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Na caixa **Pacote de imagem** , especifique a imagem do sistema operativo. Para obter mais informações, consulte [gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).  

    -   Se o pacote contiver várias imagens de sistema operativo, na caixa **Índice de imagens** especifique a imagem a implementar.  

    -   Na caixa **Ponto de distribuição** , especifique o ponto de distribuição onde reside o pacote da imagem do sistema operativo. O assistente obtém a imagem do sistema operativo a partir do ponto de distribuição e escreve-a no suporte de dados.  

11. Na página **Personalização** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Especifique as variáveis utilizadas pela sequência de tarefas para implementar o sistema operativo.  

    -   Especifique os comandos de pré-início que pretende executar antes da execução da sequência de tarefas. Os comandos de pré-início são um script ou um ficheiro executável que pode interagir com o utilizador no Windows PE antes da execução da sequência de tarefas para instalar o sistema operativo. Para obter mais informações sobre os comandos de Pré-início para suportes de dados, consulte o [comandos para suporte de dados de sequência de tarefas de Pré-início](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Durante a criação de suportes de dados de sequência de tarefas, a sequência de tarefas escreve o ID de pacote e da linha de comandos, incluindo o valor das eventuais variáveis de sequência de tarefas, para o ficheiro de registo CreateTSMedia.log no computador que executa a consola do Configuration Manager de Pré-início. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

12. Conclua o assistente.  

## <a name="next-steps"></a>Passos seguintes
[Cenários para implementar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md)
