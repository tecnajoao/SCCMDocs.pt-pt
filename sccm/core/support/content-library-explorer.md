---
title: Explorador da Biblioteca de Conteúdos
titleSuffix: Configuration Manager
description: Utilize o Explorador de biblioteca de conteúdo para ver e resolver problemas relacionados com a biblioteca de conteúdos num ponto de distribuição do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b9fb8c5c189407fdc6fc742ebcd0b7d9730d4289
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142209"
---
# <a name="content-library-explorer"></a>Explorador da Biblioteca de Conteúdos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Explorador de biblioteca de conteúdos é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). Utilize a ferramenta para as seguintes atividades:  

- Explore a biblioteca de conteúdos no ponto de distribuição específico  

- Resolver problemas com a biblioteca de conteúdos  

- Copiar pacotes, conteúdo, pastas e ficheiros fora da biblioteca de conteúdos  

- Redistribuir pacotes para o ponto de distribuição  

- Validar pacotes em pontos de distribuição remoto  



## <a name="requirements"></a>Requisitos

- Execute a ferramenta com uma conta que tenha acesso administrativo para:  

    - O ponto de distribuição de destino  

    - O fornecedor WMI no servidor do site  

    - O fornecedor do Configuration Manager  

- Apenas os **administrador total** e **analista só de leitura** funções tem direitos suficientes para ver todas as informações dessa ferramenta.  

    - Outras funções, como **administrador da aplicação**, pode ver informações parciais. Para obter mais informações, consulte [desativada pacotes](#bkmk_disabled-packages).  

    - O **analista só de leitura** não é possível redistribuir os pacotes a partir dessa ferramenta.  

- Execute a ferramenta em qualquer computador, desde que ele pode se conectar ao:  

    - O ponto de distribuição de destino  

    - Servidor do site primário  

    - O fornecedor do Configuration Manager  

- Se o ponto de distribuição colocalizado com o servidor do site, ainda é necessário ter acesso administrativo ao servidor do site.  



## <a name="usage"></a>Utilização 

Quando inicia **ContentLibraryExplorer.exe**, introduza o nome de domínio completamente qualificado (FQDN) do ponto de distribuição de destino. Em seguida, liga ao ponto de distribuição. Se o ponto de distribuição faz parte de um site secundário, ele pede para o FQDN do servidor do site primário e o código de site primário.

No painel esquerdo, ver os pacotes que são distribuídos para este ponto de distribuição. Expanda os pacotes e explore a estrutura de pasta. Esta estrutura corresponde a estrutura de pastas a partir do qual criou o pacote.

Quando seleciona uma pasta, ele exibe no painel da direita todos os ficheiros dentro da pasta. Esta vista inclui as seguintes informações: 
- Nome de ficheiro
- Tamanho do ficheiro
- Qual unidade está em
- Outros pacotes que utilizam o mesmo ficheiro na unidade
- Quando o ficheiro foi alterado pela última vez no ponto de distribuição

A ferramenta também se conecta ao fornecedor do Configuration Manager. Esta ligação é determinar quais os pacotes são distribuídos para o ponto de distribuição e se eles são, na verdade, na biblioteca de conteúdos do ponto de distribuição. Por exemplo, um pacote que está a aguardar a distribuição pode ainda não existir na biblioteca de conteúdos. Um pacote de tal aparece como "Pendente" na ferramenta e não existem ações estão ativadas para este pacote.


### <a name="bkmk_disabled-packages"></a> Pacotes desativados

Alguns pacotes estão presentes no ponto de distribuição, mas não visíveis na consola do Configuration Manager. Esses pacotes são marcados com um asterisco (\*). Não existem ações podem ser feitas nesses pacotes. Outros pacotes também podem estar marcados com um asterisco e têm ações desativada. 

Existem três principais motivos para pacotes desativados:  

- O pacote é a atualização de cliente do Configuration Manager. Este pacote inclui "ccmsetup.exe".  

- Sua conta de utilizador não é possível acessar o pacote, provavelmente devido a administração baseada em funções. Por exemplo, o **autor da aplicação** função não pode ver os pacotes de controladores no console, para que quaisquer pacotes de controladores no ponto de distribuição são marcados como desativados.  

- O pacote é órfã no ponto de distribuição.  


### <a name="validate-packages"></a>Validar pacotes

Validar pacotes utilizando **pacote** > **validar** na barra de ferramentas. Selecione um nó do pacote no painel esquerdo do primeiro não selecione um conteúdo ou uma pasta. A ferramenta se conectar ao Provedor de WMI no ponto de distribuição para esta ação. Quando a ferramenta é iniciada, os pacotes que estão em falta um ou mais conteúdo são marcados inválidos. A validar o pacote revela o conteúdo que está em falta. Se todo o conteúdo está presente, mas os dados estão danificados, validação Deteta a existência de danos.


### <a name="redistribute-packages"></a>Redistribuir pacotes

Redistribuir pacotes usando **pacote** > **redistribuir** na barra de ferramentas. Primeiro, selecione um nó do pacote no painel esquerdo. Esta ação requer permissões para redistribuir os pacotes.


### <a name="other-actions"></a>Outras ações

Uso **edite** > **cópia** para copiar pacotes, conteúdo, pastas e ficheiros fora da biblioteca de conteúdos para uma pasta especificada. Não é possível copiar a biblioteca de conteúdos em si. Selecionar mais de um ficheiro, mas não é possível selecionar várias pastas.

Procurar pacotes usando **edite** > **pacote encontrar**. Esta ação procura na sua consulta no nome do pacote e o ID do pacote.



## <a name="limitations"></a>Limitações

- A ferramenta não é possível manipular a biblioteca de conteúdos diretamente de qualquer forma. Alterações à biblioteca de conteúdos podem resultar em malfunctions.  

- A ferramenta pode redistribuir pacotes, mas apenas para a distribuição de destino do ponto.  

- Quando colocar o ponto de distribuição com o servidor do site, não é possível validar dados do pacote. Utilize a consola do Configuration Manager em vez disso. A ferramenta ainda inspeciona o pacote para se certificar de que todo o conteúdo estiver presente, mas não necessariamente intactos.  

- Não é possível eliminar o conteúdo com esta ferramenta.



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [A biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library)
