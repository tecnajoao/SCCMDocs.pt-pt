---
title: "Capacidades na pré-visualização técnica 1611 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1611."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5d08d1f9ccd995d544c3c21c4af52ede73343077
ms.openlocfilehash: 5e77ebbfd3f3d573d903fe58024a22feb9884e4a
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1611 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1611. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    

**Problemas conhecidos neste pré-visualização técnica:**   
- ***Estado dos pré-requisitos***: Quando instalar a versão 1611, o estado geral dos pré-requisitos poderá mostrar como passou com avisos, mas não listar os pré-requisitos causado os avisos. Esta situação pode ocorrer os seguintes duas pré-requisitos:
  - Opções de memória de criar o índice de SQL
  - Verifica a existência de versão suportada do SQL Server  

 Uma vez que estes são apenas avisos, pode ser ignoradas.

- ***PowerShell***: Quando se liga ao Windows PowerShell a partir da consola do Configuration Manager, poderá receber o erro seguinte: **Não está assinado digitalmente Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml**.  

   Pode resolver este problema, substituindo determinados ficheiros com as versões com a sessão iniciada a partir da versão 1610. Copiar todos os ficheiros com as seguintes extensões a partir de **&lt;diretório de instalação > \AdminConsole\bin\**  pasta na instalação versão 1610: **. psd1**, **.ps1xml**, e **. psm1**. Colar estes ficheiros para o **&lt;diretório de instalação > \AdminConsole\bin\**  pasta na instalação 1611 de pré-visualização técnica, substituindo a versão de 1611 dos ficheiros.


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Conteúdo da cache de pré-lançamento para as implementações disponíveis e sequências de tarefas
Nesta pré-visualização técnico, para as implementações disponíveis e sequências de tarefas, pode optar por utilizar a funcionalidade de pré-cache ter clientes a transferir apenas lhe conteúdo relevante antes de um utilizador instala o conteúdo.

Por exemplo, digamos que pretende implementar uma sequência de tarefas de atualização no local do Windows 10, só pretende uma sequência de tarefas único para todos os utilizadores e vários arquiteturas de e/ou idiomas. Ramo atual, se criar uma implementação disponível e, em seguida, o utilizador clica **instalar** no Centro de Software, o conteúdo transfere nesse momento. Esta ação adiciona mais tempo antes da instalação estiver pronta para começar. Em alternativa, ramo atual se criar uma implementação de sequência de tarefas disponível, todo o conteúdo referenciado na sequência de tarefas é transferido. Isto inclui o pacote de atualização do sistema operativo para todos os idiomas e arquiteturas. Se cada seja aproximadamente 3 GB de tamanho, o pacote de transferência pode ser bastante grande.

A funcionalidade de conteúdo pré-cache fornece-lhe a opção para permitir que o cliente transferir apenas o conteúdo aplicável assim que receber a implementação. Por conseguinte, quando o utilizador clica **instalar** no Centro de Software, o conteúdo estiver disponível e a instalação for iniciada rapidamente porque o conteúdo está no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Para configurar a funcionalidade de pré-cache

1. Crie pacotes de atualização de arquiteturas específicas e idiomas de sistema operativo. Especifique a arquitetura e o idioma no **origem de dados** separador do pacote. Para o idioma, utilize a conversão decimal (por exemplo, 1033 é decimal para inglês e 0x0409 é equivalente a hexadecimal). Para obter mais detalhes, consulte o artigo [criar uma sequência de tarefas para atualizar um sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Os valores de arquitetura e de idioma são utilizados para correspondam às condições de passo de sequência de tarefas será criada no passo seguinte para determinar se o pacote de atualização do sistema operativo deve ser anterior à colocado em cache.
2. Crie uma sequência de tarefas com condicional passos para os idiomas diferentes e arquiteturas. Por exemplo, para a versão em inglês foi possível criar um passo como a seguinte:

    ![Propriedades de pré-cache](media/precacheproperties2.png)

    ![Opções de pré-cache de](media/precacheoptions2.png)  

3. Implemente a sequência de tarefas. Para a funcionalidade de pré-cache de configurado o seguinte:
    - No **geral** separador, selecione **previamente transferir conteúdo para esta sequência de tarefas**.
    - No **definições de implementação** separador, configure a sequência de tarefas com o **disponível** para **objetivo**. Se criar um **necessário** implementação, a funcionalidade de pré-cache não funcionará.
    - No **agendamento** separador, para o **agendar quando esta implementação ficará disponível** definição, escolher uma hora no futuro que proporcione tempo suficiente para o conteúdo em cache previamente antes da implementação é disponibilizada para os utilizadores de clientes. Por exemplo, pode definir o tempo disponível para ser 3 horas no futuro para dar tempo suficiente para o conteúdo seja previamente em cache.  
    - No **pontos de distribuição** separador, configure o **opções de implementação** definições. Se o conteúdo não é previamente em cache num cliente antes de um utilizador inicia a instalação, estas definições são utilizadas.


### <a name="user-experience"></a>Experiência de utilizador
- Quando o cliente recebe a política de implementação, iniciará para colocar em cache previamente o conteúdo. Isto inclui todo o conteúdo referenciado (quaisquer outros tipos de pacote) e apenas o pacote atualização do sistema operativo que corresponde ao cliente com base nas condições que configura na sequência de tarefas.
- Quando a implementação é disponibilizada para os utilizadores (a definição de **agendamento** separador da implementação), será apresentado uma notificação para informar os utilizadores sobre a nova implementação e a implementação torna-se visível no Centro de Software. O utilizador pode aceder ao centro de Software e clicar em **instalar** para iniciar a instalação.
- Se o conteúdo não está totalmente previamente colocadas em cache, em seguida, irá utilizar as definições especificadas no **opção de implementação** separador da implementação. Recomendamos que não existe tempo suficiente entre quando a implementação é criada e a hora em que a implementação torna-se disponíveis aos utilizadores para permitir que os clientes tempo suficiente para a pré-colocam o conteúdo em cache.


## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)

