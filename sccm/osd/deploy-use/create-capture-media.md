---
title: Criar suporte de dados de captura - Configuration Manager | Microsoft Docs
description: "Utilize o assistente suporte de dados de criação de sequência de tarefas para criar suportes de dados de captura no Configuration Manager para capturar uma imagem de sistema operativo a partir de um computador de referência."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5acf800ff5aebd849e294393337755145a60cca5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>Criar suportes de dados de captura com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Suporte de dados de captura no Configuration Manager permite-lhe capturar uma imagem de sistema operativo a partir de um computador de referência. Utilize suportes de dados de captura para o seguinte cenário:  

-   [Criar uma sequência de tarefas para capturar um sistemas operativos](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="BKMK_CreateCaptureMedia"></a> Como Criar Suportes de Dados de Captura  
 Utilize suportes de dados de captura para capturar uma imagem do sistema operativo a partir de um computador de referência. O suporte de dados de captura contém a imagem de arranque que inicia o computador de referência e a sequência de tarefas que captura a imagem do sistema operativo.

Os suportes de dados de captura são criados utilizando o Assistente de Criação de Suporte de Dados da Sequência de Tarefas. Antes de executar o assistente, certifique-se de que são respeitadas as seguintes condições:  

|Tarefa|Descrição|  
|----------|-----------------|  
|Imagem de arranque|Considere o seguinte sobre a imagem de arranque que irá utilizar na sequência de tarefas para capturar o sistema operativo:<br /><br /> -A arquitetura da imagem de arranque tem de ser adequada à arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.<br />-Certifique-se de que a imagem de arranque contém os controladores de armazenamento em massa e de rede que são necessárias para aprovisionar o computador de destino.|  
|Distribuir todo o conteúdo associado à sequência de tarefas|Tem de distribuir todo o conteúdo exigido pela sequência de tarefas por, pelo menos, um ponto de distribuição. Isto inclui a imagem de arranque, a imagem do sistema operativo e outros ficheiros associados. O assistente recolhe as informações a partir do ponto de distribuição, ao criar o suporte de dados autónomo. Tem de ter direitos de acesso de **Leitura** à biblioteca de conteúdos desse ponto de distribuição.  Para obter mais informações, consulte [distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).|  
|Preparar a pen USB amovível|Para uma pen USB amovível:<br /><br /> Se planear utilizar uma pen USB amovível, a pen USB tem de estar ligada ao computador em que o assistente é executado e ser detetável pelo Windows como um dispositivo amovível. Quando cria o suporte de dados, o assistente escreve diretamente na pen USB.|  
|Criar uma pasta de saída|Para um conjunto de CD/DVD:<br /><br /> Antes de executar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas para criar suportes de dados para um conjunto de CDs ou DVDs, tem de criar uma pasta para os ficheiros de saída criados pelo assistente. O suporte de dados criado para um conjunto de CDs ou DVDs é escrito em formato de ficheiros .iso diretamente na pasta.|  

 Utilize o procedimento seguinte para criar suportes de dados de captura.  

#### <a name="to-create-capture-media"></a>Para criar suportes de dados de captura  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4.  Na página **Selecione o Tipo de Suporte de Dados** , selecione **Suporte de dados de captura**e clique em **Seguinte**.  

5.  Na página **Tipo de Suporte de Dados** , especifique se o suporte de dados é uma pen USB ou um conjunto de CD/DVD e, em seguida, clique para configurar o seguinte:  

    -   Se selecionar **Pen USB**, especifique a unidade onde pretende armazenar o conteúdo.  

    -   Se selecionar **Conjunto CD/DVD**, especifique a capacidade do suporte de dados e o nome e caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo:  **\\\servername\folder\outputfile.iso**  

         Se a capacidade do suporte de dados for demasiado pequena para armazenar todo o conteúdo, serão criados vários ficheiros e tem de armazenar o conteúdo em vários CDs ou DVDs. Quando vários suportes de dados é necessária, o Configuration Manager adiciona um número sequencial ao nome de cada ficheiro de saída criado. Além disso, se implementar uma aplicação juntamente com o sistema operativo e a aplicação não couber num único suporte de dados, o Configuration Manager armazenará a aplicação em vários suportes de dados. Quando o suporte de dados autónomo for executado, o Configuration Manager pede ao utilizador o suporte de dados seguinte em que a aplicação se encontra armazenada.  

        > [!IMPORTANT]  
        >  Se selecionar uma imagem .iso existente, o Assistente de Criação de Suporte de Dados da Sequência de Tarefas elimina essa imagem da unidade ou partilha logo que avança para a página seguinte do assistente. A imagem existente será eliminada, mesmo que em seguida cancele o assistente.  

     Clique em **Seguinte**.  

6.  Na página **Imagem de arranque** , especifique as seguintes informações e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de arranque especificada tem de ser adequada à arquitetura do computador de referência. Por exemplo, um computador de referência x64 poderá efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. Mas um computador de referência x86 só poderá efetuar o arranque e a execução de uma imagem de arranque x86.  

    -   Na caixa **Imagem de arranque** , especifique a imagem de arranque que inicia o computador de referência.  

    -   Na caixa **Ponto de distribuição** , especifique o ponto de distribuição onde reside a imagem de arranque. O assistente obtém a imagem de arranque do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        >  Tem de ter direitos de acesso de Leitura para a biblioteca de conteúdos do ponto de distribuição.  

7.  Conclua o assistente.  
