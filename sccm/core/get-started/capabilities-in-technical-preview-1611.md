---
title: Funcionalidades no Technical Preview versão 1611
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão versão 1611.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 71ad5ae8ff823d03951d5f9ae1a13e8051cba23e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416576"
---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1611 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão versão 1611. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    

**Problemas conhecidos neste Technical Preview:**   
- ***Estado dos pré-requisitos***: Quando instalar a versão versão 1611, o estado geral da pré-requisitos poderá mostrar como passou com avisos, mas não a relaciona os pré-requisitos causado os avisos. Isto pode dever-se os seguintes dois pré-requisitos:
  - Opções de SQL Index Create Memory
  - Verifica a existência de uma versão suportada do SQL Server  

  Uma vez que estes são apenas avisos, que podem ser ignoradas.

- ***PowerShell***: Quando se liga ao Windows PowerShell a partir da consola do Configuration Manager, pode receber o erro seguinte: **Não está assinado digitalmente Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml**.  

   Pode resolver este problema ao substituir determinados arquivos assinadas versões da versão 1610. Copiar todos os ficheiros com as seguintes extensões do **&lt;diretório de instalação > \AdminConsole\bin\\** pasta na sua instalação da versão 1610: **. psd1**, **.ps1xml**, e **psm1**. Cole estes ficheiros para o **&lt;diretório de instalação > \AdminConsole\bin\\** pasta na sua instalação da versão 1611 de pré-visualização técnica, substituir a versão de versão 1611 dos ficheiros.


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Pré-armazenar conteúdo em cache para as implementações disponíveis e sequências de tarefas
Neste technical Preview, para as implementações disponíveis e sequências de tarefas, pode optar por utilizar a funcionalidade de pré-cache para que os clientes a transferir apenas o conteúdo relevante, antes de um usuário instala o conteúdo.

Por exemplo, digamos que pretende implementar uma sequência de tarefas de atualização in-loco do Windows 10, apenas pretende uma única sequência de tarefas para todos os utilizadores e tem várias arquiteturas de e/ou idiomas. No ramo atual, se criar uma implementação disponível e, em seguida, o usuário clica **instalar** no Centro de Software, o conteúdo downloads nesse momento. Esta ação adiciona mais tempo antes da instalação estiver pronta para começar. Em alternativa, no ramo atual se criar uma implementação de sequência de tarefas disponíveis, todo o conteúdo referenciado na sequência de tarefas é transferido. Isto inclui o pacote de atualização do sistema operativo para todos os idiomas e arquiteturas. Se cada um é aproximadamente 3 GB de tamanho, o pacote de download pode ser muito grande.

A funcionalidade de conteúdos da pré-cache de lhe dá a opção para permitir que o cliente transferir apenas o conteúdo aplicável assim que receber a implementação. Por conseguinte, quando o usuário clica **instalar** no Centro de Software, os conteúdos estiverem prontos e a instalação inicia rapidamente porque o conteúdo está no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Configurar a funcionalidade de pré-cache

1. Crie pacotes de atualização para arquiteturas específicas e de idiomas de sistema operativo. Especificar a arquitetura e o idioma no **origem de dados** Guia do pacote. Para o idioma, utilize a conversão em decimal (por exemplo, 1033 é decimal para inglês e 0x0409 é o equivalente hexadecimal). Para obter detalhes, consulte [criar uma sequência de tarefas para atualizar um sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Os valores de arquitetura e o idioma são utilizados para corresponder a condições de passo de sequência de tarefas irá criar no próximo passo para determinar se o pacote de atualização do sistema operativo deve ser previamente armazenados em cache.
2. Crie uma sequência de tarefas com passos condicionais a diferentes idiomas e arquiteturas. Por exemplo, para a versão em inglês pode criar um passo com o seguinte:

    ![Propriedades de pré-cache](media/precacheproperties2.png)

    ![Opções de pré-cache](media/precacheoptions2.png)  

3. Implemente a sequência de tarefas. Para a funcionalidade de pré-cache, configure o seguinte:
    - Sobre o **gerais** separador, selecione **pré-transferir conteúdos para esta sequência de tarefas**.
    - Sobre o **definições de implementação** separador, configure a sequência de tarefas com o **disponível** para **finalidade**. Se criar um **necessário** implementação, a funcionalidade de pré-cache não funcionará.
    - Na **agendamento** separador, para o **agendar quando esta implementação ficará disponível** definir, escolha uma hora no futuro que dá tempo suficiente para colocar em cache previamente o conteúdo antes da implementação é feita de clientes disponível para os utilizadores. Por exemplo, pode definir o tempo disponível para ser 3 horas no futuro para dar tempo suficiente para o conteúdo a ser previamente em cache.  
    - Sobre o **pontos de distribuição** separador, configure a **opções de implementação** definições. Se o conteúdo não é previamente em cache num cliente antes de um utilizador inicia a instalação, estas definições são utilizadas.


### <a name="user-experience"></a>Experiência de utilizador
- Quando o cliente recebe a política de implementação, ele iniciará o conteúdo de pré-cache. Isto inclui todos os conteúdos referenciados (quaisquer outros tipos de pacote) e apenas o pacote atualização do sistema operativo que corresponde ao cliente com base nas condições que defina na sequência de tarefas.
- Quando a implementação é disponibilizada para os utilizadores (definir a **agendamento** separador da implantação), é apresentada uma notificação a informar os utilizadores sobre a nova implementação e a implementação se torna visível no Centro de Software. O utilizador pode aceder ao centro de Software e clique em **instalar** para iniciar a instalação.
- Se o conteúdo não está totalmente previamente em cache, em seguida, irá utilizar as definições especificadas no **opção de implementação** separador da implementação. Recomendamos que existe tempo suficiente entre quando a implementação é criada e a hora em que a implementação fica disponível para utilizadores para permitir aos clientes tempo suficiente para o conteúdo de pré-cache.


## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)
