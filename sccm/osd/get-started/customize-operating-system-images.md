---
title: 'Personalizar imagens de sistema operativo '
titleSuffix: Configuration Manager
description: Utilize sequências de tarefas de captura e compilação, a configuração manual ou uma combinação de ambos para personalizar uma imagem do sistema operativo.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9a3f4583944f0818f74930753bad99e3408a928
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350022"
---
# <a name="customize-operating-system-images-with-system-center-configuration-manager"></a>Personalizar imagens de sistema operativo com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Imagens de sistema operativo no System Center Configuration Manager são ficheiros WIM e representam uma coleção comprimida de ficheiros de referência e pastas que são necessários para instalar e configurar um sistema operativo num computador com êxito. Uma imagem de sistema operativo personalizada é criada e capturada num computador de referência que é configurado com todos os ficheiros do sistema operativo, ficheiros de suporte, atualizações de software, ferramentas e outras aplicações de software necessários. Poderá decidir até que ponto configurar manualmente o computador de referência. Poderá automatizar completamente a configuração do computador de referência utilizando uma sequência de tarefas de criação e captura, configurar manualmente determinados aspetos do computador de referência e automatizar o resto utilizando sequências de tarefas ou configurar manualmente o computador de referência sem utilizar sequências de tarefas. Utilize as secções seguintes para personalizar um sistema operativo.

##  <a name="BKMK_PrepareReferenceComputer"></a> Preparar para o computador de referência  
 Existem vários aspetos a ter em conta antes de utilizar a captura de uma imagem de sistema operativo a partir de um computador de referência.  

###  <a name="BKMK_RefComputerDecide"></a> Decidir entre uma configuração automatizada ou manual  
 Os seguintes destaques descrevem as vantagens e desvantagens de configurações automatizadas e manuais do computador de referência.  

#### <a name="automated-configuration"></a>Configuração automatizada  
 **Vantagens**  

-   A configuração pode ser completamente autónoma, eliminando a necessidade da presença de um administrador ou utilizador.  

-   Poderá reutilizar a sequência de tarefas para repetir a configuração de computadores de referência adicionais com um elevado nível de confiança.  

-   Poderá modificar a sequência de tarefas para acomodar as diferenças dos computadores de referência, sem ter de recriar toda a sequência de tarefas.  

 **Desvantagens**  

-   A criação e teste da ação inicial para criar uma sequência de tarefas poderá demorar muito tempo.  

-   Se os requisitos do computador de referência foram alterados de forma significativa, a reconstrução e teste da sequência de tarefas poderá demorar muito tempo.  

#### <a name="manual-configuration"></a>Configuração manual  
 **Vantagens**  

-   Não é necessário criar uma sequência de tarefas ou perder tempo a testar e resolver problemas relacionados com a mesma.  

-   Poderá instalar diretamente a partir de CDs sem incluir todos os pacotes de software (incluindo o próprio Windows) para um pacote de Configuration Manager.  

 **Desvantagens**  

-   A exatidão da configuração do computador de referência depende do administrador ou utilizador que o configura.  

-   Continuará a ter de verificar e testar se o computador de referência se encontra corretamente configurado.  

-   Não é possível reutilizar o método de configuração.  

-   Isso requer o envolvimento ativo de uma pessoa ao longo do processo.  

###  <a name="BKMK_RefComputerConsiderations"></a> Considerações para o computador de referência  
 Segue-se uma listagem dos itens básicos a considerar ao configurar um computador de referência.  

-   **Implementar o sistema operativo**  

     O sistema operativo que pretende implementar nos computadores de destino tem de estar instalado no computador de referência. Para obter mais informações sobre os sistemas operativos que poderá implementar, consulte [requisitos de infraestrutura de implementação do sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Service pack adequado**  

     O sistema operativo que pretende implementar nos computadores de destino tem de estar instalado no computador de referência.  

-   **Atualizações de software apropriadas**  

     Instale todas as aplicações de software que pretende incluir na imagem do sistema operativo a capturar a partir do computador de referência. Também poderá instalar aplicações de software quando implementar a imagem do sistema operativo capturada nos computadores de destino.  

-   **Associação de grupo de trabalho**  

     O computador de referência tem de estar configurado como membro de um grupo de trabalho.  

-   **Sysprep**  

     A ferramenta de preparação do sistema (Sysprep) é uma tecnologia que pode utilizar com outras ferramentas de implementação para instalar sistemas operativos Windows em novo hardware. O Sysprep prepara o computador para criação de imagens do disco ou entrega ao cliente, configurando-o para criar um novo identificador de segurança (SID) do computador quando este é reiniciado. Além disso, o Sysprep limpa as definições específicas do utilizador e do computador e os dados que não deverão ser copiados para o computador de destino.  

     Poderá executar manualmente o Sysprep no computador de referência, através do seguinte comando:  

     `Sysprep /quiet /generalize /reboot`  

     A opção /generalize dá instruções ao Sysprep para remover dados específicos de sistema da instalação do Windows. As informações específicas do sistema incluem registos de eventos, IDs de segurança exclusiva (SIDs) e outras informações exclusivas. Depois de as informações exclusivas do sistema serem removidas, o computador é reiniciado.  

     Pode automatizar o Sysprep utilizando o suporte de dados de captura ou o passo da sequência de tarefas [Preparar Windows para Captura](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

    > [!IMPORTANT]  
    >  O passo da sequência de tarefas [Preparar Windows para Captura](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) tenta repor a palavra-passe do administrador local do computador de referência para um valor em branco antes da execução do Sysprep. Se a política de Segurança Local **A palavra-passe tem de satisfazer requisitos de complexidade** estiver ativa, este passo da sequência de tarefas não conseguirá repor a palavra-passe do administrador. Neste cenário, desative esta política antes de executar a sequência de tarefas.  

     Para mais informações sobre o Sysprep, veja [Referência Técnica sobre Preparação do Sistema (Sysprep)](http://go.microsoft.com/fwlink/?LinkId=280286).  

-   **As ferramentas apropriadas e os scripts necessários para atenuar os cenários de instalação**  

     Ferramentas e scripts adequados necessários para atenuar os cenários de instalação  

-   **Personalização de ambiente de trabalho adequada, tais como o padrão de fundo, imagem corporativa e perfil de utilizador predefinido**  

     Poderá configurar o computador de referência com as propriedades de personalização do ambiente de trabalho que pretender incluir ao capturar a imagem do sistema operativo do computador de referência. As propriedades de ambiente de trabalho incluem o padrão de fundo, imagem corporativa e um perfil de utilizador predefinido padrão.  

##  <a name="BKMK_ManuallyBuildReference"></a> Criar manualmente um computador de referência  
 Utilize o procedimento seguinte para criar manualmente um computador de referência.  

> [!NOTE]  
>  Ao criar manualmente o computador de referência, poderá capturar a imagem do sistema operativo utilizando um suporte de dados de captura. Para obter mais informações, consulte [criar suportes de dados de captura](../deploy-use/create-capture-media.md).  

#### <a name="to-manually-build-the-reference-computer"></a>Para criar manualmente o computador de referência  

1.  Identifique o computador a utilizar como computador de referência.  

2.  Configure o computador de referência com o sistema operativo adequado e o restante software necessário para criar a imagem do sistema operativo que pretende implementar.  

    > [!WARNING]  
    >  No mínimo, instale o sistema operativo e Service Pack adequados, os controladores de suporte as atualizações de software eventualmente necessárias.  

3.  Configure o computador de referência de modo a que seja membro de um grupo de trabalho.  

4.  Reponha a palavra-passe do Administrador local no computador de referência de modo a que o valor da palavra-passe esteja em branco.  

5.  Execute o Sysprep utilizando o comando: **sysprep /quiet /generalize /reboot**. A opção /generalize dá instruções ao Sysprep para remover dados específicos de sistema da instalação do Windows. As informações específicas do sistema incluem registos de eventos, IDs de segurança exclusiva (SIDs) e outras informações exclusivas. Depois de as informações exclusivas do sistema serem removidas, o computador é reiniciado.  

 Quando o computador de referência estiver pronto, utilize uma sequência de tarefas para capturar a imagem do sistema operativo a partir do computador de referência.  Para obter os passos detalhados, veja [Capturar uma imagem do sistema operativo a partir de um computador de referência existente](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer).  

##  <a name="BKMK_UseTSToBuildReference"></a> Utilizar uma sequência de tarefas para criar um computador de referência  
 Pode automatizar o processo de criação de um computador de referência utilizando uma sequência de tarefas para implementar o sistema operativo, controladores, aplicações, etc.  Utilize os passos seguintes para criar o computador de referência e, em seguida, capturar a imagem do sistema operativo a partir do computador de referência.  

-   Utilize uma sequência de tarefas para criar e capturar a imagem do sistema operativo a partir do computador de referência.  Para obter passos detalhados, veja [Utilizar uma sequência de tarefas para compilar e capturar um computador de referência](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).  
