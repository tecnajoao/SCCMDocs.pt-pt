---
title: Funcionalidades no Technical Preview 1611
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1611."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
caps.latest.revision: "2"
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: b56aee663319861427048fb722b1cdc0b5cc664d
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1611 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*



Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1611. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    

**Problemas conhecidos neste Technical Preview:**   
- ***Estado dos pré-requisitos***: Quando instalar a versão 1611, o estado geral dos pré-requisitos poderá mostrar, passou com avisos, mas não listar os pré-requisitos causado os avisos. Isto pode dever-se os seguintes pré-requisitos de duas:
  - Opções de memória de criar o índice de SQL
  - Verifica a existência de versão suportada do SQL Server  

 Uma vez que estes são apenas avisos, pode ser ignorados.

- ***PowerShell***: Quando se liga ao Windows PowerShell a partir da consola do Configuration Manager, poderá receber o erro seguinte: **Não está assinado digitalmente Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml**.  

   Pode resolver este problema, substituindo determinados ficheiros com versões assinadas da versão 1610. Copiar todos os ficheiros com as seguintes extensões da **&lt;diretório de instalação > \AdminConsole\bin\**  pasta na instalação versão 1610: **. psd1**, **.ps1xml**, e **. psm1**. Colar estes ficheiros para o **&lt;diretório de instalação > \AdminConsole\bin\**  pasta na instalação do Technical Preview 1611, substituindo a versão de 1611 dos ficheiros.


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Pré-armazenar conteúdo em cache para as implementações disponíveis e sequências de tarefas
Nesta pré-visualização técnica, para as implementações disponíveis e sequências de tarefas, pode optar por utilizar a funcionalidade de pré-cache para que os clientes transferir apenas o conteúdo relevante antes de um utilizador instala o conteúdo.

Por exemplo, digamos que pretende implementar uma sequência de tarefas de atualização no local do Windows 10, apenas pretende uma única sequência de tarefas para todos os utilizadores e ter várias arquiteturas de e/ou idiomas. No ramo atual, se criar uma implementação disponível e, em seguida, o utilizador clica em **instalar** no Centro de Software, as transferências de conteúdo nessa altura. Esta ação adiciona mais tempo antes da instalação estiver pronta para começar. Em alternativa, no ramo atual se criar uma implementação de sequência de tarefas disponível, todos os conteúdos referenciados na sequência de tarefas é transferido. Isto inclui o pacote de atualização do sistema operativo para todos os idiomas e arquiteturas. Se cada aproximadamente 3 GB de tamanho, o pacote de transferência pode ser bastante grande.

A funcionalidade de conteúdo pré-cache dá-lhe a opção para permitir que o cliente transferir apenas o conteúdo aplicável logo que recebe a implementação. Por conseguinte, quando o utilizador clica em **instalar** no Centro de Software, o conteúdo está pronto e a instalação inicia rapidamente porque o conteúdo no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Configurar a funcionalidade de pré-cache

1. Criação de pacotes de atualização para idiomas e arquiteturas específicas de sistema operativo. Especifique a arquitetura e idioma de **origem de dados** separador do pacote. Para o idioma, utilize a conversão decimal (por exemplo, 1033 é o valor decimal para inglês e 0x0409 é o equivalente hexadecimal). Para obter mais informações, consulte [criar uma sequência de tarefas para atualizar um sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Os valores de arquitetura e de idioma são utilizados para corresponder a condições de passo de sequência de tarefas irá criar o passo seguinte para determinar se o pacote de atualização do sistema operativo deve ser previamente colocadas em cache.
2. Crie uma sequência de tarefas com condicionais passos para os idiomas diferentes e arquiteturas. Por exemplo, para a versão inglesa pode criar um passo como o seguinte:

    ![Propriedades da pré-cache de](media/precacheproperties2.png)

    ![Opções de pré-cache](media/precacheoptions2.png)  

3. Implemente a sequência de tarefas. Para a funcionalidade de pré-cache, configure o seguinte:
    - No **geral** separador, selecione **previamente transferir conteúdo para esta sequência de tarefas**.
    - No **definições de implementação** separador, configure a sequência de tarefas com o **disponível** para **objetivo**. Se criar um **necessário** implementação, a funcionalidade de pré-cache não funcionará.
    - No **agendamento** separador, para o **agendar quando esta implementação ficará disponível** definição, escolha uma data futura que proporcione tempo suficiente para colocar em cache previamente o conteúdo antes da implementação é disponibilizada para os utilizadores de clientes. Por exemplo, pode definir o tempo disponível para ser 3 horas no futuro para permitir tempo suficiente para o conteúdo seja previamente em cache.  
    - No **pontos de distribuição** separador, configure o **opções de implementação** definições. Se o conteúdo não é previamente em cache no cliente antes de um utilizador inicia a instalação, estas definições são utilizadas.


### <a name="user-experience"></a>Experiência de utilizador
- Quando o cliente recebe a política de implementação, será iniciada colocar em cache o conteúdo previamente. Isto inclui todos os conteúdos referenciados (quaisquer outros tipos de pacote) e apenas o sistema operativo pacote de atualização que corresponda ao cliente com base nas condições que definiu na sequência de tarefas.
- Quando a implementação é disponibilizada para os utilizadores (definição de **agendamento** separador da implementação), apresenta uma notificação a informar os utilizadores sobre a nova implementação e a implementação fica visível no Centro de Software. O utilizador pode aceder ao centro de Software e clicar em **instalar** para iniciar a instalação.
- Se o conteúdo não está totalmente previamente em cache, em seguida, irá utilizar as definições especificadas no **a opção de implementação** separador da implementação. Recomendamos que não há tempo suficiente entre quando a implementação é criada e a hora em que a implementação fica disponível para os utilizadores para permitir que os clientes tempo suficiente para colocar em cache o conteúdo previamente.


## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)
