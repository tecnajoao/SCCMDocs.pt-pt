---
title: "A biblioteca de conteúdos"
titleSuffix: Configuration Manager
description: "Saiba mais sobre a biblioteca de conteúdos do System Center Configuration Manager utiliza para reduzir o tamanho geral do conteúdo distribuído."
ms.custom: na
ms.date: 2/14/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: "4"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 738f62747e755694cb508cd5b25caf83af300eb2
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="the-content-library-in-system-center-configuration-manager"></a>A biblioteca de conteúdos no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A biblioteca de conteúdos é um arquivo de instância única de conteúdo que o System Center Configuration Manager utiliza para reduzir o tamanho geral do corpo combinado de conteúdo que distribui. A biblioteca de conteúdos armazena todos os ficheiros de conteúdo para atualizações de software, aplicações, implementações do sistema operativo e assim sucessivamente.

 - Uma cópia da biblioteca de conteúdos é automaticamente criada e mantida em cada **servidor do site** e em cada **ponto de distribuição**.

 - Antes do Configuration Manager transfere ficheiros de conteúdo para o servidor do site ou copia os ficheiros para pontos de distribuição, o Configuration Manager verifica se cada ficheiro de conteúdo já se encontra na biblioteca de conteúdos.
 - Se o ficheiro de conteúdo estiver disponível, o Configuration Manager não copia o ficheiro e em vez disso, associa o ficheiro de conteúdo existente à aplicação ou pacote.

Em computadores onde instala um ponto de distribuição, pode configurar:

- Uma ou mais unidades de disco no qual pretende criar a biblioteca de conteúdos.
- Uma prioridade para cada unidade que utiliza.

Quando o Configuration Manager copia os ficheiros de conteúdo, copia-os para a unidade com a prioridade mais alta até essa unidade conter menos do que uma quantidade mínima de espaço livre que especificar.
- Configurar as definições de unidade durante a instalação do ponto de distribuição.
- Não é possível configurar as definições de unidade nas propriedades do ponto de distribuição após a conclusão da instalação.


Para obter mais informações sobre como configurar as definições de unidade para o ponto de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


>  [!IMPORTANT]  
>  Para mover a biblioteca de conteúdos para uma localização diferente num ponto de distribuição após a instalação, utilize o **ferramenta de transferência da biblioteca de conteúdos** no Toolkit do System Center 2012 R2 Configuration Manager. Pode transferir o toolkit a partir do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=279566).  

## <a name="about-the-content-library-on-the-central-administration-site"></a>Sobre a biblioteca de conteúdos no site de administração central  
 Por predefinição, o Configuration Manager cria uma biblioteca de conteúdos no site de administração central, quando a instalação do site. A biblioteca de conteúdos é colocada na unidade do servidor do site que tenha mais disco espaço livre. Uma vez que não é possível instalar um ponto de distribuição no site de administração central, não é possível atribuir prioridades aos processos unidades para utilização da biblioteca de conteúdos. Semelhante à biblioteca de conteúdos noutros servidores de site e pontos de distribuição, quando a unidade que contém a biblioteca de conteúdos fica sem espaço em disco disponível, a biblioteca de conteúdos aplica-se automaticamente para a unidade disponível seguinte.  

 O Configuration Manager utiliza a biblioteca de conteúdos no site de administração central, nos seguintes cenários:  

-   Quando cria conteúdo no site de administração central.  

-   Quando migra o conteúdo a partir de outro site do Configuration Manager e atribui o site de administração central como o site que gere esse conteúdo.  

> [!NOTE]  
>  Quando cria conteúdo num site primário e, em seguida, distribui-lo para outro site primário ou um site secundário abaixo de um site principal diferente, o site de administração central temporariamente armazena esse conteúdo na pasta a receber do Programador no site de administração central, mas não adiciona esse conteúdo à respetiva biblioteca de conteúdos.  

 Utilize as seguintes opções para gerir a biblioteca de conteúdos no site de administração central:  

-   Para impedir que a biblioteca de conteúdos que está a ser instalado numa unidade específica, crie um ficheiro vazio designado **no_sms_on_drive.sms**e, em seguida, copie-o para a pasta raiz da unidade antes da biblioteca de conteúdos é criada.  

-   Depois da biblioteca de conteúdos tiver sido criada, utilize **ferramenta de transferência da biblioteca de conteúdos** do Toolkit do System Center 2012 R2 Configuration Manager, para gerir a localização da biblioteca de conteúdos. Pode transferir o toolkit a partir do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=279566).  
