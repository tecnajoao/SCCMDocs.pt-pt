---
title: "Criar suportes de dados de sequência de tarefas com o System Center Configuration Manager | Microsoft Docs"
description: "Crie suportes de dados da sequência tarefas, tais como um CD, para implementar um sistema operativo num computador de destino no seu ambiente do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: bd5448d70c2d465347de840cb197d4c33075c90a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="create-task-sequence-media-with-system-center-configuration-manager"></a>Criar um suporte de dados de sequência de tarefas com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar suportes de dados para capturar uma imagem de sistema operativo a partir de um computador de referência ou implementar um sistema operativo num computador de destino no seu ambiente do System Center Configuration Manager. O suporte de dados criado pode ser um conjunto de CD, DVD ou uma unidade flash USB.  

 Suporte de dados é essencialmente utilizado para implementar sistemas operativos em computadores de destino que não tenham uma ligação de rede ou que tenham uma ligação de largura de banda reduzida ao site do Configuration Manager. No entanto, o suporte de dados de implementação também é utilizado para iniciar a implementação de um sistema operativo fora de um sistema operativo Windows existente. Esta segunda utilização de suportes de dados de implementação é importante quando não existe um sistema operativo no computador de destino, quando o sistema operativo está num estado não operacional ou quando o utilizador administrativo pretende criar partições do disco rígido no computador de destino.  

 O suporte de dados de implementação inclui suportes de dados de arranque, suportes de dados autónomos e suportes de dados pré-configurados. O conteúdo do suporte de dados de implementação varia consoante o tipo de suporte de dados utilizado. Por exemplo, o suporte de dados autónomo contém a sequência de tarefas que implementa o sistema operativo, enquanto outros tipos de suportes de dados obtêm sequências de tarefas a partir do ponto de gestão.  

> [!IMPORTANT]  
>  Para criar suportes de dados de sequência de tarefas, tem de ser um administrador no computador em que executa a consola do Configuration Manager. Se não for um administrador, ser-lhe-ão pedidas as credenciais de administrador quando iniciar o assistente para Criar Suportes de Dados de Sequência de Tarefas.  

##  <a name="BKMK_PlanCaptureMedia"></a>Captura de suportes de dados para imagens de sistema operativo  
 O suporte de dados de captura permite capturar uma imagem do sistema operativo a partir de um computador de referência. O suporte de dados de captura contém a imagem de arranque que inicia o computador de referência e a sequência de tarefas que captura a imagem do sistema operativo. Para obter mais informações sobre como criar suportes de dados de captura, veja [Criar suportes de dados de captura com o System Center Configuration Manager](create-capture-media.md).  

##  <a name="BKMK_PlanBootableMedia"></a>Implementações do sistema operativo de suportes de dados  
 Suporte de dados de arranque contém apenas a imagem de arranque, opcional [comandos de Pré-início](../understand/prestart-commands-for-task-sequence-media.md) e os ficheiros necessários e os binários do Configuration Manager. Quando o computador de destino é iniciado, estabelece a ligação à rede e obtém a sequência de tarefas, a imagem do sistema operativo e qualquer outro conteúdo necessário a partir da rede. Dado que a sequência de tarefas não está no suporte de dados, pode alterar a sequência de tarefas ou o conteúdo sem ter de recriar o suporte de dados.  

> [!IMPORTANT]  
>  Os pacotes dos suportes de dados de arranque não estão encriptados. O utilizador administrativo deve tomar as medidas de segurança apropriadas, como adicionar uma palavra-passe ao suporte e dados, para garantir que o conteúdo do pacote está protegido contra utilizadores não autorizados.  

 Para obter informações sobre como criar suportes de dados [criar suportes de dados](create-bootable-media.md).  

##  <a name="BKMK_PlanPrestagedMedia"></a>Implementações de sistema operativo do suporte de dados pré-configurado  
 O suporte de dados pré-configurado permite-lhe pré-configurar o suporte de dados de arranque e uma imagem do sistema operativo num disco rígido antes do processo de aprovisionamento. O suporte de dados pré-configurado é um ficheiro de formato WIM (Windows Imaging) que pode ser instalado num computador bare-metal pelo fabricante ou num centro de transição empresarial que não está ligado ao ambiente do Configuration Manager.  

 O suporte de dados pré-configurado contém a imagem de arranque utilizada para iniciar o computador de destino e a imagem de sistema operativo aplicada no computador de destino. Também pode especificar aplicações, pacotes e pacotes de controladores para incluir como parte do suporte de dados pré-configurado. A sequência de tarefas que implementa o sistema operativo não está incluída no suporte de dados. Quando implementa uma sequência de tarefas que utiliza suportes de dados pré-configurados, o cliente verifica primeiro a presença de conteúdo válido na cache local da sequência de tarefas e, se o conteúdo não puder ser localizado ou tiver sido revisto, o cliente transfere-o a partir do ponto de distribuição.  

 O suporte de dados pré-configurado é aplicado no disco rígido do computador novo antes do seu envio para o utilizador final. Quando o computador é iniciado pela primeira vez após a aplicação do suporte de dados pré-configurado, o computador inicia o Windows PE e estabelece ligação a um ponto de gestão para localizar a sequência de tarefas que conclui o processo de implementação do sistema operativo.  

> [!IMPORTANT]  
>  Os pacotes dos suportes de dados pré-configurados não estão encriptados. O utilizador administrativo deve tomar as medidas de segurança apropriadas, como adicionar uma palavra-passe ao suporte e dados, para garantir que o conteúdo do pacote está protegido contra utilizadores não autorizados.  

 Para obter informações sobre como criar suportes de dados pré-configurados, consulte [criar suportes de dados pré-configurados](create-prestaged-media.md).  

##  <a name="BKMK_PlanStandaloneMedia"></a>Implementações de sistema operativo do suporte de dados autónomo  
 O suporte de dados autónomo contém tudo o que é necessário para implementar o sistema operativo. Isto inclui a sequência de tarefas e qualquer outro conteúdo necessário. Como tudo o que é necessário para implementar o sistema operativo está armazenado no suporte de dados autónomo, o espaço em disco necessário para o suporte de dados autónomo é significativamente maior do que o espaço em disco necessário para outros tipos de suportes de dados.  

 Para obter informações sobre como criar suportes de dados autónomos, consulte [criar suportes de dados autónomos](create-stand-alone-media.md).  

## <a name="media-considerations-when-using-site-systems-configured-for-https"></a>Considerações sobre o suporte de dados ao utilizar sistemas de sites configurados para HTTPS  
 Quando o ponto de gestão e os pontos de distribuição são configurados para utilizar comunicação HTTPS, deve criar os suportes de dados de arranque e os suportes de dados pré-configurados num site principal e não no site de administração central. Além disso, considere o seguinte para o ajudar a determinar se deve configurar o suporte de dados como dinâmico ou baseado no site:  

-   Para configurar o suporte de dados como suporte de dados dinâmico, todos os sites principais têm de ter a AC de raiz do site a partir do qual criou o suporte de dados. Pode importar a AC de raiz para todos os sites principais da hierarquia.  

-   Quando os sites primários na hierarquia do Configuration Manager utilizam várias AC de raiz, tem de utilizar suportes de dados baseados no site em cada site.  
