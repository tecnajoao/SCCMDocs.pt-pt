---
title: "Passos de sequência de tarefas"
titleSuffix: Configuration Manager
description: "Saiba mais sobre os passos de sequência de tarefas que pode adicionar uma sequência de tarefas do Configuration Manager."
ms.custom: na
ms.date: 01/12/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: "26"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 695d21eb065f4d89143644dad28bfdb711392ab9
ms.sourcegitcommit: e121d8d3dd82b9f2dde2cb5206cbee602ab8e107
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/17/2018
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Variáveis de passos de tarefas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os seguintes passos de sequência de tarefas podem ser adicionados a uma sequência de tarefas do Configuration Manager. Para obter informações sobre a edição de uma sequência de tarefas, veja [Editar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

As seguintes definições são comuns a todos os passos de sequência de tarefas:

No **propriedades** separador:
 - **Nome**: O editor de sequência de tarefas requer que especifique um nome abreviado para descrever este passo. Quando adiciona um novo passo, o editor de sequência de tarefas define o nome para o tipo por predefinição. O **nome** não pode exceder 50 carateres.
 - **Descrição**: Opcionalmente, especifique as informações mais detalhadas sobre este passo. O **Descrição** comprimento não pode exceder os 256 carateres.
O resto deste artigo descreve as outras definições no **propriedades** separador para cada passo de sequência de tarefas.

No **opções** separador:  
-   **Desativar este passo**: A sequência de tarefas ignore este passo quando é executada num computador. O ícone para este passo é esbatido no editor de sequência de tarefas. 
-   **Continuar com o erro**: A sequência de tarefas continua se ocorrer um erro ao executar o passo.  
-   **Adicionar condição**: A sequência de tarefas avalia as declarações de condicionais para determinar se executa o passo.   
As secções abaixo para os passos de sequência de tarefas específica descrevem outras definições de possíveis no **opções** separador.



##  <a name="BKMK_ApplyDataImage"></a>Aplicar imagem de dados   
 Utilize este passo para copiar a imagem de dados para a partição de destino especificado.  

 Este passo é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas, consulte [variáveis de ação da sequência de tarefas](task-sequence-action-variables.md).  

No editor de sequência de tarefas, clique em **adicionar**, selecione **imagens**e selecione **aplicar imagem de dados** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Pacote de imagem**  
 Clique em **procurar** para especificar o **pacote de imagem** utilizado por esta sequência de tarefas. Selecione o pacote que pretende instalar na caixa de diálogo **Selecionar um Pacote**. As informações sobre propriedades associadas para cada pacote de imagem existente são apresentadas na parte inferior da caixa de diálogo **Selecionar um Pacote**. Utilize a lista pendente para selecionar a **Imagem** que pretende instalar a partir do **Pacote de Imagem** selecionado.  

> [!NOTE]  
>  Esta ação de sequência de tarefas processa a imagem como um ficheiro de dados. Esta ação não efetuar qualquer configuração para arrancar a imagem como um sistema operativo.  

 **Destino**  
 Configure uma das seguintes opções:

-   **Partição disponível seguinte**: Utilize a partição sequencial seguinte que um **aplicar sistema operativo** ou **aplicar imagem de dados** ação nesta sequência de tarefas não tem o destino já.  

-   **Partição e disco específico**: Selecione o **disco** número (começando com 0) e o **partição** número (começando com 1).  

-   **Letra de unidade lógica específica**: Especifique o **letra da unidade** atribuída à partição pelo Windows PE. Esta letra de unidade pode ser diferente da letra de unidade que atribui o sistema operativo recentemente implementado.  

-   **Letra de unidade lógica armazenada numa variável**: Especifique a variável de sequência de tarefas que contém a letra de unidade atribuída à partição pelo Windows PE. Esta variável é normalmente definida na secção avançada da **propriedades da partição** caixa de diálogo a **formatar e particionar disco** ação de sequência de tarefas.  

**Elimine todo o conteúdo na partição antes de aplicar a imagem**  
 Especifica que a sequência de tarefas Elimina todos os ficheiros na partição de destino antes de instalar a imagem. Ao não eliminar o conteúdo da partição, este passo pode ser utilizado para aplicar conteúdo adicional a uma partição direcionada anteriormente.  



##  <a name="BKMK_ApplyDriverPackage"></a>Aplicar pacote de controlador  
 Utilize este passo para transferir todos os controladores no pacote de controlador e instalá-los no sistema operativo Windows.

 O passo de sequência de tarefas **Aplicar Pacote de Controlador** torna todos os controladores de dispositivo num pacote de controlador disponíveis para serem utilizados pelo Windows. Adicionar este passo entre o **aplicar sistema operativo** e **configurar Windows e ConfigMgr** passos para disponibilizar os controladores no pacote do Windows. Normalmente, o passo **Aplicar Pacote de Controlador** é colocado depois do passo de sequência de tarefas **Aplicar Controladores Automaticamente**. O passo de sequência de tarefas **Aplicar Pacote de Controlador** também é útil em cenários de implementação de suportes de dados autónomos.  

 Certifique-se de que os controladores de dispositivo semelhantes são colocados num pacote de controlador e distribuídos para os pontos de distribuição adequados. Depois de serem distribuídos, computadores de cliente do Configuration Manager podem instalá-los. Por exemplo, colocar todos os controladores de um fabricante num pacote de controlador. Em seguida, distribua o pacote para pontos de distribuição em que os computadores associados podem aceder aos mesmos.

 O **aplicar pacote de controlador** passo é útil para suportes de dados autónomos. Este passo também é útil se pretender instalar um conjunto específico de controladores. Estes tipos de controladores incluem os dispositivos que uma análise plug and play, como impressoras de rede não serão detetados.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Pacote de Controlador](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

No editor de sequência de tarefas, clique em **adicionar**, selecione **controladores**e selecione **aplicar pacote de controlador** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Pacote de controladores**  
 Especifique o pacote de controlador que contém os controladores de dispositivo necessários, clicando em **Procurar** e iniciando a caixa de diálogo **Selecionar um Pacote**. Especifique um pacote existente para ser disponibilizado. As propriedades do pacote associado são apresentadas na parte inferior da caixa de diálogo.  

 **Selecione o controlador de armazenamento em massa no pacote que tem de ser instalado antes da configuração em sistemas de operativos anteriores ao Windows Vista**  
 Especifique quaisquer controladores de armazenamento em massa necessários para instalar um sistema operativo clássico.  

 **Controlador**  
 Selecione o ficheiro de controlador de armazenamento em massa a instalar antes da configuração de um sistema operativo clássico. Povoa na lista pendente do pacote especificado.  

 **Modelo**  
 Especifique o dispositivo crítico de arranque necessário para implementações de sistemas operativos anteriores ao Windows Vista.  

 **Efetuar a instalação autónoma de controladores não assinados numa versão do Windows em que tal é permitido**  
 Esta opção permite que o Windows instale controladores sem uma assinatura digital.  



##  <a name="BKMK_ApplyNetworkSettings"></a>Aplicar definições de rede   
 Utilize este passo para especificar as informações de configuração de rede ou o grupo de trabalho para o computador de destino. A sequência de tarefas armazena estes valores no ficheiro de resposta adequado. Este ficheiro de resposta durante a configuração do Windows utiliza o **configurar Windows e ConfigMgr** ação.  

 Este passo de sequência de tarefas é executado num sistema operativo padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Definições de Rede](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **definições**e selecione **aplicar definições de rede** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Aderir a um grupo de trabalho**  
 Selecione esta opção para associar o computador de destino ao grupo de trabalho especificado. Introduza o nome do grupo de trabalho na linha **Grupo de Trabalho**. Este valor pode ser substituído pelo valor capturado pelo passo de sequência de tarefas **Capturar Definições de Rede**.  

 **Aderir a um domínio**  
 Selecione esta opção para associar o computador de destino ao domínio especificado. Especifique ou navegue até ao domínio, tal como *fabricam.com*. Especifique ou navegue até um caminho de acesso protocolo LDAP (Lightweight Directory) para uma unidade organizacional. Por exemplo: *LDAP / / UO = computadores, DC = fabricam.com, C = com*  

 **Conta**  
 Clique em **Definir** para especificar uma conta com as permissões necessárias para associar o computador ao domínio. No **conta de utilizador do Windows** caixa de diálogo, pode introduzir o nome de utilizador usando o seguinte formato: **Domínio \ utilizador**.  

 **Definições do adaptador**  
 Especifique as configurações de rede para cada placa de rede no computador. Clique em **Novo** para abrir a caixa de diálogo **Definições de Rede** e, em seguida, especifique as definições de rede. Se também de utilizar o **capturar definições de rede** passo, a sequência de tarefas aplica as definições de capturados anteriormente para o adaptador de rede. A sequência de tarefas não aplicar as definições que especificar neste passo. Se a sequência de tarefas não anteriormente capturar definições de rede, aplica-se as definições especificadas no **aplicar definições de rede** passo. A sequência de tarefas aplica estas definições para os adaptadores de rede por ordem de enumeração de dispositivo do Windows.  



##  <a name="BKMK_ApplyOperatingSystemImage"></a>Aplicar imagem do sistema operativo  

> [!TIP]  
> Começando com o Windows 10, versão 1709, o suporte de dados inclui várias edições. Quando configura uma sequência de tarefas para utilizar um pacote de atualização do SO ou a imagem do SO, é necessário selecionar um [suportado edição](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Utilize este passo para instalar um sistema operativo no computador de destino. Este passo executa ações, dependendo se utiliza uma imagem do SO ou um pacote de atualização do SO.  

 O **aplicar imagem do sistema operativo** passo efetua as seguintes ações quando utilizar uma imagem do SO:  

1.  Elimine todo o conteúdo no volume de destino, exceto ficheiros na pasta o &#95; Especifica a variável de SMSTSUserStatePath.

2.  Extraia os conteúdos do ficheiro. wim especificado para a partição de destino especificado.  

3.  Prepare o ficheiro de resposta:  

    1.  Crie um nova configuração do Windows resposta ficheiro predefinido (sysprep.inf ou unattend.xml) para o sistema operativo que está a ser implementado.  

    2.  Intercala quaisquer valores do ficheiro de resposta fornecido pelo utilizador.  

4.  Copie carregadores de arranque do Windows para a partição ativa.  

5.  Defina o ficheiro boot.ini ou a base de dados de configuração de arranque (BCD) para referenciar o sistema operativo recentemente instalado.  

 O **aplicar imagem do sistema operativo** passo efetua as seguintes ações quando utilizar um pacote de atualização do SO:  

1.  Elimine todo o conteúdo no volume de destino, exceto ficheiros na pasta o &#95; Especifica a variável de SMSTSUserStatePath.  

2.  Prepare o ficheiro de resposta:  

    1.  Crie um ficheiro de resposta novo com valores padrão criados pelo Configuration Manager.  

    2.  Intercala quaisquer valores do ficheiro de resposta fornecido pelo utilizador.  

> [!NOTE]  
>  O **configurar Windows e ConfigMgr** passo inicia a instalação do Windows. 

 Depois do **aplicar sistema operativo** ação é executada, OSDTargetSystemDrive variável é definida para a letra de unidade da partição que contém os ficheiros de sistema operativo.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Imagem do Sistema Operativo](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **imagens**e selecione **aplicar imagem do sistema operativo** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Aplicar o sistema operativo a partir de uma imagem capturada**  
 Instala uma imagem do sistema operativo capturada anteriormente. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar um pacote** e selecione o pacote de imagem existente que pretende instalar. Se várias imagens associados especificado **pacote de imagem**, utilize a lista pendente para especificar a imagem associada a utilizar para esta implementação. Pode ver informações básicas sobre cada imagem existente clicando na imagem.  

 **Aplicar imagem do sistema operativo a partir de uma origem de instalação original**  
 Instala um sistema operativo utilizando uma origem de instalação original. Clique em **procurar** para abrir o **Select e pacote de instalação do sistema operativo** caixa de diálogo. Em seguida, selecione o pacote de atualização SO existente que pretende utilizar. Pode ver informações básicas sobre cada origem de imagem existente clicando na origem da imagem. As propriedades da origem da imagem associada são apresentadas no painel de resultados, na parte inferior da caixa de diálogo. Se existirem várias edições associadas ao pacote especificado, utilize a lista pendente para especificar a **Edição** associada que será utilizada.  

 **Utilizar um ficheiro de resposta sysprep ou autónomo para uma instalação personalizada**  
 Utilize esta opção para fornecer um ficheiro de resposta de configuração do Windows (**unattend.xml**, **unattend.txt** ou **sysprep.inf**), consoante a versão do sistema operativo e o método de instalação. O ficheiro que especificar pode incluir qualquer uma das opções de configuração padrão suportadas pelos ficheiros de resposta do Windows. Por exemplo, pode utilizá-lo para especificar a home page predefinida do Internet Explorer. Especifique o pacote que contém o ficheiro de resposta e o caminho associado para o ficheiro do pacote.  

> [!NOTE]  
>  O ficheiro de resposta de configuração que fornecer pode conter do Windows embedded variáveis de sequência de tarefas da % formulário*varname*%, onde *varname* é o nome da variável. O **configurar Windows e ConfigMgr** passo substitui o %*varname*cadeia % para os valores de variáveis reais. Estas variáveis de sequência de tarefas incorporadas não podem ser utilizados em campos apenas numéricos num ficheiro de resposta unattend.xml.  

 Se não fornecer um ficheiro de resposta de configuração do Windows, esta ação de sequência de tarefas gera automaticamente um ficheiro de resposta.  

 **Destino**  
 Configure uma das seguintes opções:  

-   **Partição disponível seguinte**: Utilize a partição sequencial seguinte que um **aplicar sistema operativo** ou **aplicar imagem de dados** ação nesta sequência de tarefas não tem o destino já. 

-   **Partição e disco específico**: Selecione o **disco** número (começando com 0) e o **partição** número (começando com 1).  

-   **Letra de unidade lógica específica**: Especifique o **letra da unidade** atribuída à partição pelo Windows PE. Esta letra de unidade pode ser diferente da letra de unidade que atribui o sistema operativo recentemente implementado.  

-   **Letra de unidade lógica armazenada numa variável**: Especifique a variável de sequência de tarefas que contém a letra de unidade atribuída à partição pelo Windows PE. Esta variável é normalmente definida na secção avançada da **propriedades da partição** caixa de diálogo a **formatar e particionar disco** ação de sequência de tarefas.  

### <a name="options"></a>Opções  
 Para além das opções predefinidas, configure as seguintes definições adicionais no **opções** separador deste passo de sequência de tarefas:  

-   **Aceder ao conteúdo diretamente a partir do ponto de distribuição**  
     Configure a sequência de tarefas para aceder à imagem do sistema operativo diretamente a partir do ponto de distribuição. Por exemplo, utilize esta opção quando implementar sistemas operativos em dispositivos embedded que tenham limitada a capacidade de armazenamento. Quando selecionar esta opção, também de configurar as definições de partilha de pacote no **acesso a dados** separador das propriedades do pacote.  

    > [!NOTE]  
    >  Esta definição substitui a opção de implementação que configurou no **pontos de distribuição** página no **Assistente de implementação de Software**. Esta substituição destina-se apenas a imagem do SO que especifique este passo, não para todos os conteúdos de sequência de tarefas.  



##  <a name="BKMK_ApplyWindowsSettings"></a>Aplicar definições do Windows  
 Utilize este passo para configurar as definições do Windows para o computador de destino. A sequência de tarefas armazena estes valores no ficheiro de resposta adequado. Este ficheiro de resposta durante a configuração do Windows utiliza o **configurar Windows e ConfigMgr** ação.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Definições do Windows](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **definições**e selecione **aplicar definições do Windows** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Nome de utilizador**  
 Especifique o nome de utilizador registado associado ao computador de destino. Este valor pode ser substituído pelo valor capturado pela ação de sequência de tarefas **Capturar Definições do Windows**.  

 **Nome da organização**  
 Especifique o nome da organização registado associado ao computador de destino. Este valor pode ser substituído pelo valor capturado pela ação de sequência de tarefas **Capturar Definições do Windows**.  

 **Chave de produto**  
 Especifique a chave de produto utilizada para a instalação do Windows no computador de destino.  

 **Licenciamento do servidor**  
 Especifique o modo de licenciamento do servidor. Pode selecionar **Por servidor** ou **Por utilizador** como modo de licenciamento. Se selecionar **por servidor**, também especificar o número máximo de ligações permitido por contrato de licença. Selecione **Não especificar** se o computador de destino não for um servidor ou o utilizador não pretender especificar o modo de licenciamento.  

 **Número máximo de ligações**  
 Especifique o número máximo de ligações disponíveis para este computador, conforme indicado no contrato de licença.  

 **Aleatoriamente gerar a palavra-passe de administrador local e desativar a conta nas plataformas suportadas (recomendado)**  
 Selecione esta opção para definir a palavra-passe de administrador local para uma cadeia gerado aleatoriamente. Esta opção também desativa a conta de administrador local em plataformas que suportam esta capacidade.  

 **Ativar a conta e especificar a palavra-passe de administrador local**  
 Selecione esta opção para ativar a conta de administrador local utilizando a palavra-passe especificada. Introduza a palavra-passe na linha **Palavra-passe** e confirme-a na linha **Confirmar palavra-passe**.  

 **Fuso horário**  
 Especifique o fuso horário a configurar no computador de destino. Este valor pode ser substituído pelo valor capturado pelo passo de sequência de tarefas **Capturar Definições do Windows**.  



##  <a name="BKMK_AutoApplyDrivers"></a>Aplicar controladores automaticamente  
 Utilize este passo para corresponder e instalar controladores como parte da implementação do sistema operativo.  

 O passo de sequência de tarefas **Aplicar Controladores Automaticamente** executa as seguintes ações:  

1.  Análise de hardware e localize os IDs plug and play para todos os dispositivos existentes no sistema.  

2.  Envie a lista de dispositivos e os respetivos IDs plug and play para o ponto de gestão. O ponto de gestão devolve uma lista de controladores compatíveis a partir do catálogo de controladores para cada dispositivo de hardware. A lista inclui todos os controladores independentemente de estarem no pacote de controlador, controladores marcados com a categoria de controladores especificados e os controladores não desativados.  

3.  Para cada dispositivo de hardware, a sequência de tarefas escolhe o melhor controlador. Este controlador é adequado para o sistema operativo implementado e no ponto de distribuição acessível.  

4.  A sequência de tarefas transfere os controladores selecionados a partir de um ponto de distribuição e prepara os controladores no sistema de operativo de destino.  

    1.  Para instalações baseadas em imagem, a sequência de tarefas coloca os controladores para o arquivo de controladores do sistema operativo.  

    2.  Para instalações baseadas em configurações, a sequência de tarefas configura a configuração do Windows com a localização dos controladores.  

5.  Durante a **configurar Windows e ConfigMgr** passo da sequência de tarefas, a configuração do Windows encontra os controladores pré-configurados por esta ação.  

> [!IMPORTANT]
>  Não é possível utilizar suportes de dados autónomos a **aplicar controladores automaticamente** passo. Configuração do Windows não tem uma ligação ao site do Configuration Manager neste cenário.

Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Controladores Automaticamente](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **controladores**e selecione **aplicar controladores automaticamente** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Instalar apenas o melhor correspondência de controladores compatíveis**  
 Especifica que o passo de sequência de tarefas instala apenas os controladores com melhor compatibilidade para cada dispositivo de hardware detetado.  

 **Instalar todos os controladores compatíveis**  
 A sequência de tarefas instale todos os controladores compatíveis para cada dispositivo de hardware detetado. Configuração do Windows, em seguida, escolhe o melhor controlador. Esta opção utiliza mais espaço de disco e largura de banda de rede. A sequência de tarefas transfere mais controladores, mas o Windows pode selecionar um controlador mais adequado.  

 **Considerar controladores de todas as categorias**  
 A sequência de tarefas procura todas as categorias de controladores disponíveis para os controladores de dispositivo adequados.  

 **Limitar a correspondência de controladores para apenas considerar controladores nas categorias selecionadas**  
 A sequência de tarefas procura nas categorias de controladores especificados para os controladores de dispositivo adequados.  

 **Efetuar a instalação autónoma de controladores não assinados nas versões do Windows em que tal é permitido**  
 Esta opção permite que o Windows instale controladores sem uma assinatura digital.   

  > [!IMPORTANT]  
  >  Esta opção não é aplicável a sistemas operativos onde não é possível configurar a política de assinatura de controladores.  



##  <a name="BKMK_CaptureNetworkSettings"></a>Capturar definições de rede  
 Utilize este passo para capturar definições de rede Microsoft do computador que executa a sequência de tarefas. A sequência de tarefas guarda estas definições em variáveis de sequência de tarefas. Estas definições substituem as predefinições configuradas no **aplicar definições de rede** passo.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Capturar Definições de Rede](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

No editor de sequência de tarefas, clique em **adicionar**, selecione **definições**e selecione **capturar definições de rede** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Migrar a associação ao domínio e grupo de trabalho**  
 Captura as informações de associação de domínios e grupos de trabalho do computador de destino.  

 **Migrar a configuração do adaptador de rede**  
 Captura a configuração da placa de rede do computador de destino. As informações capturadas incluem as definições de rede globais, o número de placas e as definições de rede associadas a cada placa. Estas definições incluem as definições associadas a DNS, WINS, IP e filtros de portas.  



##  <a name="BKMK_CaptureOperatingSystemImage"></a>Capturar imagem do sistema operativo  
 Este passo captura uma ou mais imagens a partir de um computador de referência. A sequência de tarefas cria um ficheiro de imagem do Windows (. wim) na partilha de rede especificado. Em seguida, utilize o **Adicionar pacote de imagem do sistema operativo** Assistente para importar esta imagem para o Configuration Manager para implementações do sistema de operativo baseada em imagem.  

 O Configuration Manager captura cada volume (unidade) do computador de referência para uma imagem separada no ficheiro. wim. Se o computador referenciado tiver vários volumes, o ficheiro. wim resultante contém uma imagem separada para cada volume. Apenas são capturados os volumes formatados como NTFS ou FAT32. Os volumes com outros formatos e os volumes USB são ignorados.  

 O sistema operativo instalado no computador de referência tem de ser uma versão do Windows que suporte do Configuration Manager. Utilize a ferramenta SysPrep para preparar o sistema de operativo de computador de referência. O volume do sistema operativo instalado e o volume de arranque têm de ser o mesmo volume.  

 Especifique uma conta com permissões de escrita para a partilha de rede selecionada.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Capturar Imagem do Sistema Operativo](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **imagens**e selecione **Capturar imagem do sistema operativo** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Destino**  
 Caminho de sistema de ficheiros para a localização que o Configuration Manager utiliza para armazenar a imagem do sistema operativo capturada.  

 **Descrição**  
 Descrição opcional definida pelo utilizador da imagem do sistema operativo capturada armazenada no ficheiro .WIM.  

 **Versão**  
 Número da versão opcional definido pelo utilizador para atribuir à imagem do sistema operativo capturada. Este valor pode ser qualquer combinação de letras e números, e está armazenado no ficheiro .WIM.  

 **Criado por**  
 Nome opcional do utilizador que criou a imagem do sistema operativo e está armazenado no ficheiro .WIM.  

 **Conta de imagem do sistema operativo para captura**  
 Tem de introduzir a conta do Windows com permissões para a partilha de rede especificada. Clique em **Definir** para especificar o nome dessa conta do Windows.  



##  <a name="BKMK_CaptureUserState"></a>Capturar estado do utilizador  
 Utilize este passo para utilizar a ferramenta de migração de estado de utilizador (USMT) para capturar o estado do utilizador e as definições do computador que executa a sequência de tarefas. Este passo de sequência de tarefas é utilizado em conjunto com o passo de sequência de tarefas **Restaurar Estado do Utilizador**. Com o USMT 3.0.1 e posterior, esta opção encripta sempre o armazenamento de Estados do USMT através de uma chave de encriptação gerada e gerida pelo Configuration Manager.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

 Se pretender guardar e restaurar as definições de estado do utilizador a partir de um ponto de migração de estado, utilize o **capturar estado do utilizador** passo com o **solicitar armazenamento de Estados** e **disponibilizar armazenamento de Estados** passos.  

 O passo de sequência de tarefas **Capturar Estado do Utilizador** fornece controlo sobre um subconjunto limitado das opções mais utilizadas pelo USMT. Podem ser especificadas opções da linha de comandos adicionais com a variável de sequência de tarefas OSDMigrateAdditionalCaptureOptions.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Capturar Estado do Utilizador](task-sequence-action-variables.md#BKMK_CaptureUserState).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **estado do utilizador**e selecione **capturar estado do utilizador** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Pacote de ferramenta de migração de estado de utilizador**  
 Especifique o pacote que contém a ferramenta de migração de estado de utilizador (USMT). A sequência de tarefas utiliza esta versão do USMT para capturar o estado do utilizador e as definições. Este pacote não requer um programa. Especifique um pacote com a versão de 32 bits ou 64 bits do USMT. A arquitetura do USMT depende da arquitetura do sistema operativo a partir da qual a sequência de tarefas é capturar o estado.  

 **Capturar todos os perfis de utilizador com opções padrão**  
 Migre todas as informações de perfil de utilizador. Esta é a opção predefinida.  

 Se selecionar esta opção, mas não selecionar **restaurar perfis de utilizador do computador local** no **restaurar estado do utilizador** passo, a sequência de tarefas falhará. O Configuration Manager não é possível migrar as novas contas sem lhes atribuir palavras-passe. 

 Quando utiliza o **instalar um pacote de imagem existente** opção o **nova sequência de tarefas** assistente, a sequência de tarefas resultante utilizará a predefinição **capturar todos os perfis de utilizador com opções padrão**. Esta sequência de tarefas predefinida não selecione a opção para **restaurar perfis de utilizador do computador local**, por outras palavras, contas de utilizador de domínio.  

 Selecione **Restaurar perfis de utilizador do computador local** e forneça uma palavra-passe para a conta a ser migrada. Numa sequência de tarefas criada manualmente, esta definição pode ser encontrada no passo Restaurar Estado do Utilizador. Numa sequência de tarefas criada pelo assistente **Nova Sequência de Tarefas**, esta definição pode ser encontrada na página do assistente no passo **Restaurar Definições e Ficheiros do Utilizador**.  

 Se tiver não existem contas de utilizador local, esta definição não se aplica.  

 **Personalizar como os perfis de utilizador são capturados**  
 Selecione esta opção para especificar uma migração de ficheiros de perfil personalizados. Clique em **Ficheiros** para selecionar os ficheiros de configuração para o USMT utilizar neste passo. Especifique um ficheiro. XML personalizado que contém as regras que definam os ficheiros de estado de utilizador a migrar.  

 **Clique aqui para selecionar os ficheiros de configuração:**  
 Selecione esta opção para selecionar os ficheiros de configuração no pacote do USMT que pretende utilizar para capturar os perfis de utilizador. Clique no botão **Ficheiros** para iniciar a caixa de diálogo **Ficheiros de Configuração**. Para especificar um ficheiro de configuração, introduza o nome do ficheiro na linha **Nome do ficheiro** e clique no botão **Adicionar**.  

 **Ativar o registo verboso**  
 Ative esta opção para gerar informações de ficheiros de registo mais detalhadas. Ao capturar o estado, a sequência de tarefas por predefinição gera ScanState.log na pasta de registo da sequência de tarefas, \windows\system32\ccm\logs.   

 **Ignorar ficheiros que utilizam o sistema de ficheiros encriptados**  
 Ative esta opção para ignorar a captura de ficheiros encriptado com o sistema de ficheiros encriptados (EFS). Estes ficheiros incluem ficheiros de perfil de utilizador. Consoante o sistema operativo e a versão do USMT, os ficheiros encriptados podem não ser legíveis após o restauro. Para mais informações, consulte a documentação do USMT.  

 **Copiar utilizando o acesso do sistema de ficheiros**  
 Ative esta opção para especificar qualquer uma das seguintes definições:  

-   **Continuar se não for possível capturar alguns ficheiros**: Ative esta definição continuar o processo de migração, mesmo se não for possível capturar alguns ficheiros. Se desativar esta opção se não for possível capturar um ficheiro, em seguida, este passo falhe. Por predefinição, esta opção encontra-se ativada.  

-   **Capturar localmente ao utilizar hiperligações em vez de copiar ficheiros**: Ative esta definição para utilizar ligações fixas NTFS para capturar ficheiros.  

     Para obter mais informações sobre a migração de dados com ligações fixas, veja [Hard-Link Migration Store](http://go.microsoft.com/fwlink/p/?LinkId=240222) (em inglês).  

-   **Capturar no modo offline (apenas Windows PE)**: Ative esta definição capturar o estado do utilizador no Windows PE em vez do sistema operativo completo.  
    
**Capturar utilizando o serviço de sombra de cópia de Volume (VSS)**  
 Esta opção permite-lhe capturar ficheiros mesmo que estejam bloqueados para edição por outra aplicação.  



##  <a name="BKMK_CaptureWindowsSettings"></a>Capturar definições do Windows  
 Utilize este passo para capturar as definições do Windows do computador que executa a sequência de tarefas. A sequência de tarefas guarda estas definições em variáveis de sequência de tarefas. Estas definições capturadas substituem as predefinições configuradas por si no **aplicar definições do Windows** passo.  

 Este passo de sequência de tarefas é executado no Windows PE ou num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Capturar Definições do Windows](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **definições**e selecione **capturar definições do Windows** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Migrar o nome do computador**  
 Capture o nome do computador NetBIOS do computador.  

 **Migrar nomes organizacionais e de utilizador registados**  
 Capture os nomes de utilizador e da organização registados do computador.  

 **Migrar fuso horário**  
 Capture a definição de fuso horário no computador.  



##  <a name="BKMK_CheckReadiness"></a>Verificar preparação  
 Utilize este passo para verificar se o computador de destino cumpre as condições de pré-requisitos de implementação especificado.  

No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **verificar disponibilidade** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Certifique-se a memória mínima (MB)**  
 Certifique-se de que a quantidade de memória, em megabytes (MB), cumpre ou excede o valor especificado. O passo ativa esta definição, por predefinição.  

 **Certifique-se a velocidade mínima do processador (MHz)**  
 Certifique-se de que a velocidade do processador, em megahertz (MHz), cumpre ou excede o valor especificado. O passo ativa esta definição, por predefinição.  

 **Certifique-se o espaço mínimo livre em disco (MB)**  
 Certifique-se de que a quantidade de espaço livre em disco, em megabytes (MB), cumpre ou excede o valor especificado.  

 **Certifique-se de SO atual atualizar**  
 Certifique-se de que o sistema operativo instalado no computador de destino cumpre o requisito especificado. O passo define este como **cliente** por predefinição.  

### <a name="options"></a>Opções
 > [!NOTE]  
 > Se ativar o **continuar com o erro** definição o **opções** separador deste passo apenas registará os resultados da verificação de preparação. Se uma verificação falhar, a sequência de tarefas não parou.



##  <a name="BKMK_ConnectToNetworkFolder"></a>Ligar à pasta de rede  
 Utilize este passo para criar uma ligação para uma pasta de rede partilhada.  

 Este passo de sequência de tarefas é executado num sistema operativo padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Ligar à Pasta de Rede](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **ligar à pasta de rede** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Caminho**  
 Clique em **procurar** para especificar o caminho da pasta de rede. Utilize o formato  *\\\server\share*.

 **Unidade**  
 Selecione a letra de unidade local para atribuir para esta ligação. 

 **Conta**  
 Clique em **definir** para especificar a conta de utilizador com permissões para ligar a esta pasta de rede.



##  <a name="BKMK_DisableBitLocker"></a>Desativar BitLocker  
 Utilize este passo para desativar a encriptação BitLocker na unidade do sistema operativo atual ou numa unidade específica. Esta ação deixa os protetores de chave visíveis em texto não encriptado no disco rígido, mas não desencripta o conteúdo da unidade. Por conseguinte, esta ação é concluída quase instantaneamente.  

> [!NOTE]  
>  A encriptação de unidade BitLocker fornece encriptação de baixo nível do conteúdo de um volume do disco.  

 Se tiver várias unidades encriptadas, tem de desativar o BitLocker em todas as unidades de dados antes de desativar o BitLocker na unidade do sistema operativo.  

 Este passo é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **discos**e selecione **desativar BitLocker** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Unidade de sistema operativo atual**  
 Desativa o BitLocker na unidade do sistema operativo atual.  

 **Unidade específica**  
 Desativa o BitLocker numa unidade específica. Utilize a lista pendente para especificar a unidade na qual o BitLocker está desativado.  



##  <a name="BKMK_DownloadPackageContent"></a>Transferir conteúdo do pacote  
 Utilize este passo para transferir qualquer um dos seguintes tipos de pacotes:  

-   Imagens de sistema operativo  

-   Pacotes de atualização do sistema operativo  

-   Pacotes de controladores  

-   Pacotes  
    
Este passo funciona bem numa sequência de tarefas para atualizar um sistema operativo nos seguintes cenários:  

-   Para utilizar uma única sequência de tarefas de atualização que funciona com plataformas x86 e x64. Inclua dois **transferir conteúdo do pacote** os passos no **preparar a atualização** grupo. Especificar as condições de **opções** separador para detetar a arquitetura do cliente e transferir apenas o adequado SO pacote de atualização. Configure cada **transferir conteúdo do pacote** passo para utilizar a mesma variável. Utilize a variável para o caminho de suporte de dados no **atualizar sistema operativo** passo.  

-   Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada **transferir conteúdo do pacote** passo para utilizar a mesma variável. Utilize a variável para o **conteúdo de teste** valor na secção controladores o **atualizar sistema operativo** passo.  

> [!NOTE]    
> Ao implementar uma sequência de tarefas que contém o passo transferir conteúdo do pacote, não selecione **transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas** ou **aceder ao conteúdo diretamente a partir de um ponto de distribuição** para **opções de implementação** no **pontos de distribuição** página do Assistente de implementação de Software.  

Este passo é executado num sistema operativo padrão ou no Windows PE. No entanto, a opção para guardar o pacote na cache do cliente do Configuration Manager não é suportada no WinPE.

 No editor de sequência de tarefas, clique em **adicionar**, selecione **Software**e selecione **transferir conteúdo do pacote** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 Ícone **Selecionar pacote**  
 Clique no ícone para selecionar o pacote a transferir. Depois de selecionar um pacote, pode clicar no ícone novamente para escolher outro.  

 **Colocar na seguinte localização**  
 Guarde o pacote numa das seguintes localizações:  

 -   **Diretório de trabalho de sequência de tarefas**  

 -   **Cache do cliente do Configuration Manager**: Utilize esta opção para armazenar o conteúdo na cache do cliente. O cliente funciona como uma origem de cache ponto a ponto para outros clientes de cache ponto a ponto. Para obter mais informações, consulte [cache ponto a ponto de preparar o Windows PE para reduzir o tráfego WAN](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -   **Caminho personalizado**  
   
**Guardar caminho como uma variável**  
 É possível guardar o caminho como uma variável que pode utilizar noutro passo de sequência de tarefas. Gestor de configuração adiciona um sufixo numérico ao nome da variável. Por exemplo, se especificar uma variável de %*omeuconteúdo*% como uma variável personalizada, esta é a raiz onde a sequência de tarefas armazena conteúdo referenciado todos os. Este conteúdo pode conter vários pacotes. Quando fizer referência à variável, adicione um sufixo numérico. Por exemplo, para o primeiro pacote, consulte %*osmeusconteúdos01*%. Quando fizer referência à variável em passos subsequentes, tais como **atualizar sistema operativo**, utilize %*osmeusconteúdos02*% ou %*mycontent03*%, onde o número corresponde do ordem pela qual o **transferir conteúdo do pacote** passo lista os pacotes.  

**Se a transferência de um pacote falhar, continue a transferir os outros pacotes na lista**  
 Se a sequência de tarefas não conseguir transferir um pacote, começa a transferir o pacote seguinte na lista.  



##  <a name="BKMK_EnableBitLocker"></a>Ativar o BitLocker  
Utilize este passo para ativar a encriptação BitLocker em, pelo menos, duas partições no disco rígido. A primeira partição ativa contém o código de arranque do sistema do Windows. Outra partição contém o sistema operativo. A partição de arranque do sistema tem de permanecer desencriptada.  

Utilize o passo de sequência de tarefas **Provisão prévia do BitLocker** para ativar o BitLocker numa unidade no Windows PE. Para obter mais informações, consulte o [provisão prévia do BitLocker](#BKMK_PreProvisionBitLocker) secção.  

> [!NOTE]  
>  A encriptação de unidade BitLocker fornece encriptação de baixo nível do conteúdo de um volume do disco.  

O passo **Ativar BitLocker** é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Ativar BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Quando especificar **apenas TPM**, **TPM e chave de arranque em USB**, ou **TPM e PIN**, o Trusted Platform Module (TPM) tem de ser no seguinte estado antes de poder executar o  **Ativar o BitLocker** passo:  

-   Ativado  
-   Ativado  
-   Propriedade Permitida  
   
Este passo conclui qualquer inicialização de TPM restante. Os passos restantes não requerem presença física ou reinícios. O **ativar BitLocker** passo transparente é concluído os passos de inicialização de TPM restantes, se necessário:  

-   Criar par de chaves de endossamento  
-   Criar valor de autorização do proprietário e efetuar caução para o Active Directory, expandido para suportar este valor  
-   Obter propriedade  
-   Criar SRK (Storage Root Key) ou repor se já existir mas for incompatível  
   
Se pretender que a sequência de tarefas deve aguardar para que o **ativar BitLocker** passo para concluir o processo de encriptação de unidade, em seguida, selecione o **aguarde** opção. Se não selecionar a **aguarde** opção, o processo de encriptação de unidade ocorre em segundo plano. A sequência de tarefas continua imediatamente para o passo seguinte.  

O BitLocker pode ser utilizado para encriptar várias unidades num sistema informático (sistema operativo e unidades de dados). Para encriptar uma unidade de dados, encriptar a unidade do sistema operativo e concluir o processo de encriptação. Este requisito é porque a unidade de sistema operativo armazena os protetores de chaves para as unidades de dados. Se a encriptar o sistema operativo e unidades de dados na mesma sequência de tarefas, selecione o **aguarde** opção o **ativar BitLocker** passo para a unidade de sistema operativo.  

Se o disco rígido já estiver encriptado, mas o BitLocker estiver desativado, o **ativar BitLocker** passo novamente permite que os protetores de chaves e concluído rapidamente. A reencriptação do disco rígido não é necessária neste caso.  

Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Ativar BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

No editor de sequência de tarefas, clique em **adicionar**, selecione **discos**e selecione **ativar BitLocker** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Selecione a unidade a encriptar**  
 Especifica a unidade a encriptar. Para encriptar a unidade do sistema operativo atual, selecione **Unidade do sistema operativo atual** e, em seguida, configure uma das seguintes opções para a gestão de chaves:  

-   **Apenas TPM**: Selecione esta opção para utilizar apenas Trusted Platform Module (TPM).  

-   **Chave de arranque em USB apenas**: Selecione esta opção para utilizar uma chave de arranque armazenada numa pen USB. Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até um dispositivo USB com uma chave de arranque BitLocker ser ligado ao computador.  

-   **TPM e chave de arranque em USB**: Selecione esta opção para utilizar o TPM e uma chave de arranque armazenada numa pen USB. Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até um dispositivo USB com uma chave de arranque BitLocker ser ligado ao computador.  

-   **TPM e PIN**:  Selecione esta opção para utilizar o TPM e um número de identificação pessoal (PIN). Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até o utilizador fornecer o PIN.  
   
Para encriptar uma unidade de dados específica, não pertencente ao sistema operativo, selecione **Unidade específica** e, em seguida, selecione a unidade a partir da lista.  

**Selecione onde criar a chave de recuperação**  
 Para especificar onde o BitLocker cria a palavra-passe de recuperação e caução-lo no Active Directory, selecione **no Active Directory**. Se selecionar esta opção, tem de expandir o Active Directory para o site. O BitLocker, em seguida, pode guardar as informações de recuperação associados no Active Directory. Selecione **não criar chave de recuperação** por não criar uma palavra-passe. Criar uma palavra-passe é uma melhor prática.  

**Aguarde que o BitLocker conclua o processo de encriptação de unidade em todas as unidades antes da execução de sequência de tarefas continuar**  
 Selecione esta opção para permitir a encriptação de unidade BitLocker concluir antes de executar o passo seguinte na sequência de tarefas. Se selecionar esta opção, o BitLocker encripta o volume de disco completo antes do utilizador é conseguirão iniciar sessão no computador.  

O processo de encriptação pode demorar horas a concluir quando encriptar uma unidade de disco rígida grande. Não selecionar esta opção permite que a sequência de tarefas prosseguir imediatamente.  



##  <a name="BKMK_FormatandPartitionDisk"></a>Formatar e particionar disco  
 Utilize este passo para formatar e particionar um disco especificado no computador de destino.  

> [!IMPORTANT]  
>  Cada definição que especificar para este passo de sequência de tarefas aplica-se a um único disco especificado. Para formatar e particionar outro disco no computador de destino, adicione mais **formatar e particionar disco** passo à sequência de tarefas.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Formatar e Particionar Disco](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **discos**e selecione **formatar e particionar disco** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Número do disco**  
 O número do disco físico do disco para formatar. O número é baseado na ordem de enumeração de discos do Windows.  

 **Tipo de disco**  
 O tipo do disco formatado. Existem duas opções disponíveis para seleção na lista pendente: 

-   Padrão (MBR) - registo de arranque principal
-   GPT - tabela de partições GUID  

> [!NOTE]  
>  Se alterar o tipo de disco **padrão (MBR)** para **GPT**e o esquema de partição contém uma partição expandida, a sequência de tarefas remove todas as partições expandidas e lógicas do esquema. O editor de sequência de tarefas pede-lhe para confirmar esta ação antes de alterar o tipo de disco.  
   
**Volume**  
 Informações específicas sobre a partição ou volume que cria a sequência de tarefas, incluindo os seguintes atributos:  

-   Nome  
-   Espaço em disco restante  
   
Para criar uma nova partição, clique em **Novo** para iniciar a caixa de diálogo **Propriedades de Partição**. Especifique o tipo de partição e o tamanho, e se se tratar de uma partição de arranque. Para modificar uma partição existente, clique na partição que pretende modificar e, em seguida, clique no botão de propriedades. Para obter mais informações sobre como configurar partições de disco rígido, consulte um dos seguintes artigos:  

-   [Como configurar partições de disco rígido baseadas em UEFI/GPT](http://go.microsoft.com/fwlink/?LinkID=272104)  
-   [Como configurar partições de disco rígido baseados em BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

Para eliminar uma partição, selecione a partição que pretende eliminar e clique em **Eliminar**.  



##  <a name="BKMK_InstallApplication"></a>Instalar a aplicação  
Este passo instala aplicações especificadas ou um conjunto de aplicações definidos por uma lista dinâmica de variáveis de sequência de tarefas. Quando este passo é executado, a instalação da aplicação começa de imediato, sem aguardar por um intervalo de consulta da política.  

A aplicação instalada tem de cumprir os seguintes critérios:  

-   Esta aplicação tem de ser um tipo de implementação do Windows Installer ou instalador de Script. Os tipos de implementação do pacote de aplicação do Windows (ficheiro .appx) não são suportados.  

-   Tem de ser executada na conta do sistema local e não na conta de utilizador.  

-   Não pode interagir com o ambiente de trabalho. O programa tem de ser executado no modo silencioso ou no modo automático.  

-   Não pode iniciar um reinício por si só. A aplicação tem de solicitar um reinício utilizando o código de reinício padrão, um código de saída 3010. Este comportamento assegura que o passo de sequência de tarefas processa corretamente o reinício. Se a aplicação devolver um código de saída 3010, o motor de sequência de tarefas subjacente executa o reinício. Após o reinício, a sequência de tarefas continua automaticamente.  

Quando o **instalar aplicação** passo é executado, a aplicação verifica a aplicabilidade das regras de requisitos e método de deteção nos respetivos tipos de implementação. Com base nos resultados desta verificação, a aplicação instala o tipo de implementação aplicável. Se um tipo de implementação tiver dependências, o tipo de implementação dependente é avaliado e instalado como parte do passo de instalação da aplicação. As dependências da aplicação não são suportadas no suporte de dados autónomo.  

> [!NOTE]  
>  Para instalar uma aplicação que substitui outra aplicação, os ficheiros de conteúdo da aplicação substituída devem estar disponíveis. Caso contrário, este passo de sequência de tarefas falhará. Por exemplo, o Microsoft Visio 2010 é instalado num cliente ou numa imagem capturada. Quando o **instalar aplicação** passo instala o Microsoft Visio 2013, os ficheiros de conteúdo para o Microsoft Visio 2010 (a aplicação substituída) tem de estar disponíveis num ponto de distribuição. Se o Microsoft Visio não está instalado em todos os num cliente ou capturado imagem, a sequência de tarefas instala o Microsoft Visio 2013 sem verificar para os ficheiros de conteúdo do Microsoft Visio 2010.  

> [!NOTE]
> Se o cliente não conseguir obter a lista de pontos de gestão dos serviços de localização, utilize as variáveis incorporadas SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout para especificar quantos milissegundos uma tarefa de sequência aguarda antes de repetir a instalar um aplicação ou atualização de software. Para obter mais informações, consulte [variáveis incorporadas de sequência de tarefas](task-sequence-built-in-variables.md).

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **Software**e selecione **instalar aplicação** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Instale as seguintes aplicações**  
 A sequência de tarefas instala estas aplicações, pela ordem especificada.  

 Filtros de Gestor de configuração fora de quaisquer aplicações desativadas, ou todas as aplicações com as seguintes definições:  

-   Apenas quando um utilizador tiver sessão iniciada  
-   Executar com direitos de utilizador  

Estas aplicações não aparecem no **selecionar a aplicação a instalar** caixa de diálogo.
  
**Instalar aplicações de acordo com a lista de variáveis dinâmicas**  
A sequência de tarefas instala aplicações com este nome de variável base. O nome de variável base é para um conjunto de variáveis de sequência de tarefas definidas para uma coleção ou computador. Estas variáveis especificam as aplicações que a sequência de tarefas instala para essa coleção ou computador. Cada nome de variável é constituído pelo nome base comum e um sufixo numérico a partir de 01. O valor de cada variável tem de conter o nome da aplicação e mais nada.  

Sequência de tarefas instalar aplicações, utilizando uma lista de variáveis dinâmicas, ative a definição seguinte no **geral** separador da aplicação **propriedades**: **Permitir que esta aplicação ser instalado a partir da ação de sequência de tarefas instalar aplicação, sem ser implementada**  

> [!NOTE]  
>  Não é possível instalar aplicações através de uma lista de variáveis dinâmicas em implementações de suportes de dados autónomos.  

Por exemplo, para instalar uma única aplicação através de uma variável de sequência de tarefas denominada AA01, tem de especificar a seguinte variável:  

|Nome da Variável|Valor da Variável|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Para instalar duas aplicações, tem de especificar as seguintes variáveis:  

|Nome da Variável|Valor da Variável|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

As seguintes condições afetam as aplicações instaladas pela sequência de tarefas:  

-   O valor de uma variável contém quaisquer informações além do nome da aplicação. A sequência de tarefas não instala a aplicação e a sequência de tarefas continua.  

-   Se a sequência de tarefas não encontrou uma variável com o nome base especificado e o sufixo "01", a sequência de tarefas não instalar quaisquer aplicações. 
   
**Se uma aplicação falhar, continue a instalar outras aplicações na lista**  
 Esta definição especifica que o passo continuará quando a instalação de uma aplicação individual falhar. Se especificar esta definição, a sequência de tarefas continuará independentemente de quaisquer erros de instalação. Se não especificar esta definição e a instalação falhar, o passo termina imediatamente.  

### <a name="options"></a>Opções
 > [!NOTE] 
 > Quando seleciona **continuar com o erro** no **opções** separador deste passo, a sequência de tarefas continua quando a instalação de uma aplicação falha. Quando não ativar esta opção, a sequência de tarefas falha e não instala as restantes aplicações.  
 
Para além das opções predefinidas, configure as seguintes definições adicionais no **opções** separador deste passo de sequência de tarefas:  

-   **Repita este passo se o computador reiniciar inesperadamente**  
    Se o computador de um das instalações de aplicações reiniciar inesperadamente, repita este passo. O passo ativa esta definição, por predefinição com duas tentativas. Pode especificar uma a cinco tentativas.  



##  <a name="BKMK_InstallPackage"></a>Instalar pacote
Utilize este passo para instalar um pacote de software como parte da sequência de tarefas. Quando este passo é executado, a instalação começa de imediato, sem aguardar por um intervalo de consulta de política.  

O pacote tem de cumprir os seguintes critérios:  

-   Tem de ser executada sob a conta de sistema local e não uma conta de utilizador.  

-   Não deve interagir com o ambiente de trabalho. O programa tem de ser executado no modo silencioso ou no modo automático.  

-   Não pode iniciar um reinício por si só. O software tem de solicitar um reinício utilizando o código de reinício padrão, um código de saída 3010. Este comportamento assegura que o passo de sequência de tarefas processa corretamente o reinício. Se o software devolver um código de saída 3010, o motor de sequência de tarefas subjacente reinicia o computador. Após o reinício, a sequência de tarefas continua automaticamente.  

Os programas que utilizam a opção **Executar outro programa primeiro** para instalar um programa dependente não são suportados quando implementar um sistema operativo. Se ativar a opção de pacote **executar outro programa primeiro**e o programa dependente já tiver executado no computador de destino, o programa dependente é executado e a sequência de tarefas continua. No entanto, se não o programa dependente já tiver executado no computador de destino, o passo de sequência de tarefas falhará.  

> [!NOTE]  
>  O site de administração central não tem as políticas de configuração de cliente necessárias para ativar o agente de distribuição de software durante a sequência de tarefas. Quando cria um suporte de dados autónomo para uma sequência de tarefas do site de administração central e a sequência de tarefas inclui um passo **Instalar Pacote**, pode aparecer o erro seguinte no ficheiro CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Para suporte de dados autónomo que inclua um **Instalar pacote** passo, criar suportes de dados autónomo num site primário que tenha o agente de distribuição de software ativado. Em alternativa, adicione um **executar linha de comandos** passo após o **configurar Windows e ConfigMgr** passo e antes do primeiro **Instalar pacote** passo. O **executar linha de comandos** passo é executado um comando WMIC para ativar o agente de distribuição de software antes do primeiro **Instalar pacote** passo. Utilize o seguinte comando no **executar linha de comandos** passo:  
>   
>  **Linha de comandos**:`WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>   
>  Para obter mais informações sobre como criar suportes de dados autónomos, consulte [criar suportes de dados autónomos](../deploy-use/create-stand-alone-media.md).  

Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

No editor de sequência de tarefas, clique em **adicionar**, selecione **Software**e selecione **Instalar pacote** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Instalar um único pacote de software**  
 Esta definição especifica um pacote de software do Configuration Manager. O passo aguarda até que a instalação estiver concluída.  

 **Instalar pacotes de software, de acordo com a lista de variável dinâmicas**  
 A sequência de tarefas instala os pacotes com este nome de variável base. O nome de variável base é para um conjunto de variáveis de sequência de tarefas definidas para uma coleção ou computador. Estas variáveis especificam os pacotes de que a sequência de tarefas instala para essa coleção ou computador. Cada nome de variável é constituído pelo nome base comum e um sufixo numérico a partir de 001. O valor de cada variável tem de conter um ID de pacote e o nome do software separados por dois pontos.  

 Sequência de tarefas instalar o software utilizando uma lista de variáveis dinâmicas, ative a definição seguinte no **avançadas** separador do pacote **propriedades**: **Permitir que este programa ser instalado a partir da sequência de tarefas Instalar pacote sem ser implementada**  

> [!NOTE]  
>  Não é possível instalar pacotes de software através de uma lista de variáveis dinâmicas em implementações de suportes de dados autónomos.  

 Por exemplo, para instalar um único pacote de software através de uma variável de sequência de tarefas denominada AA001, tem de especificar a seguinte variável:  

|Nome da Variável|Valor da Variável|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 Para instalar três pacotes de software, tem de especificar as seguintes variáveis:  

|Nome da Variável|Valor da Variável|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 As seguintes condições afetam os pacotes instalados pela sequência de tarefas:  

-   Se não criar o valor da variável no formato correto ou não especifique um ID de pacote válido e um nome, a instalação de software falha.  

-   Se o ID de pacote incluir carateres minúsculos, a instalação de software falha.  

-   Se a sequência de tarefas não encontrou uma variável com o nome base especificado e o sufixo "001", a sequência de tarefas instale quaisquer pacotes. A sequência de tarefas continua.  
   
**Se a instalação de um pacote de software falhar, continue a instalar outros pacotes na lista**  
 Esta definição especifica que o passo continuará se a instalação de um pacote de software individual falhar. Se especificar esta definição, a sequência de tarefas continuará independentemente de quaisquer erros de instalação. Se não especificar esta definição e a instalação falhar, o passo termina imediatamente.  



##  <a name="BKMK_InstallSoftwareUpdates"></a>Instalar atualizações de Software  
Utilize este passo para instalar atualizações de software no computador de destino. O computador de destino não é avaliado relativamente a atualizações de software aplicáveis até ser executado este passo de sequência de tarefas. Nessa altura, o computador de destino é avaliado relativamente a atualizações de software como qualquer outro cliente de Configuration Manager. Para este passo instalar atualizações de software, tem de implementar as atualizações para uma coleção de que o computador de destino é um membro.  
>  [!IMPORTANT]
> É uma prática de segurança para um desempenho ideal instalar a versão mais recente do agente do Windows Update. 
>* Para Windows 7, veja o [Artigo da Base de dados de conhecimento 3161647](https://support.microsoft.com/kb/3161647).
>* Para Windows 8, veja o [Artigo da Base de dados de conhecimento 3163023](https://support.microsoft.com/kb/3163023).

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Instalar Atualizações de Software](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Se o cliente não conseguir obter a lista de pontos de gestão dos serviços de localização, utilize as variáveis incorporadas SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout para especificar quantos milissegundos uma tarefa de sequência aguarda antes de repetir a instalar um aplicação ou atualização de software. Para obter mais informações, consulte [variáveis incorporadas de sequência de tarefas](task-sequence-built-in-variables.md).

 No editor de sequência de tarefas, clique em **adicionar**, selecione **Software**e selecione **instalar atualizações de Software** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Necessário para instalação - apenas atualizações de software obrigatórias**  
 Selecione esta opção para instalar todas as atualizações de software obrigatórias com prazos de instalação definidos pelo administrador.  

 **Disponível para instalação - todas as atualizações de software**  
 Selecione esta opção para instalar todas as atualizações de software disponível. Tem de implementar estas atualizações para uma coleção de que o computador é um membro. A sequência de tarefas instala todas as atualizações de software disponíveis nos computadores de destino.  

 **Avaliar atualizações de software a partir dos resultados de análise em cache**  
 Por predefinição, a sequência de tarefas utiliza os resultados da análise em cache do Windows Update Agent. Desmarque a caixa de verificação ao instruir o agente do Windows Update para transferir o catálogo mais recente a partir da atualização de software ponto. Escolha esta opção quando utilizar uma sequência de tarefas para [capturar e criar uma imagem do sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). Este cenário é provavelmente um grande número de atualizações de software. Muitas destas atualizações serão têm dependências, por exemplo, instalar X antes de Y aparece como aplicável. Ao desmarcar esta definição e implementar a sequência de tarefas para muitos clientes, todos eles estabelecer ligação ao ponto de atualização de software ao mesmo tempo. Este comportamento resulta em problemas de desempenho durante o processo e a transferência do catálogo. A melhor prática é a predefinição para utilizar os resultados da análise em cache. 

A variável de sequência de tarefas SMSTSSoftwareUpdateScanTimeout controla o tempo de limite de análise de atualizações de software, durante este passo. O valor predefinido é 30 minutos. Para obter mais informações, consulte [variáveis incorporadas de sequência de tarefas](task-sequence-built-in-variables.md).

### <a name="options"></a>Opções   
 Para além das opções predefinidas, configure as seguintes definições adicionais no **opções** separador deste passo de sequência de tarefas:  

-   **Repita este passo se o computador reiniciar inesperadamente**  
    Se uma das atualizações inesperadamente reinicia o computador, repita este passo. O passo ativa esta definição, por predefinição com duas tentativas. Pode especificar uma a cinco tentativas.  

    > [!NOTE]
    > Configure a variável de SMSTSWaitForSecondReboot para especificar quantos segundos a sequência de tarefas interrompe depois do computador for reiniciado neste cenário. Para obter mais informações, consulte [variáveis incorporadas de sequência de tarefas](task-sequence-built-in-variables.md).



##  <a name="BKMK_JoinDomainorWorkgroup"></a>Associar domínio ou grupo de trabalho  
 Utilize este passo para adicionar o computador de destino a um grupo de trabalho ou domínio.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Associar Domínio ou Grupo de Trabalho](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **associar domínio ou grupo de trabalho** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Aderir a um grupo de trabalho**  
 Selecione esta opção para associar o computador de destino ao grupo de trabalho especificado. Se o computador for atualmente membro de um domínio, se selecionar esta opção faz com que o reinício do computador.  

 **Aderir a um domínio**  
 Selecione esta opção para associar o computador de destino ao domínio especificado.  

 Opcionalmente, introduza ou procure uma unidade organizacional (UO) no domínio especificado para o computador ser associado. Se o computador for atualmente membro de outro domínio ou grupo de trabalho, esta opção faz com que o reinício do computador. Se o computador já for um membro de outra UO, uma vez que os serviços de domínio do Active Directory não permite a alteração da UO através deste método, o Windows configuração ignora esta definição.  

 **Introduza a conta que tenha permissão para aderir ao domínio**  
 Clique em **definir** para introduzir o nome de utilizador e palavra-passe para uma conta com permissões para aderir ao domínio. Introduza a conta no formato:  *Domínio \ conta*  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a>Preparar ConfigMgr Client para captura  
Utilize este passo para remover ou configurar o cliente do Configuration Manager no computador de referência. Esta ação prepara o computador para captura como parte do processamento de imagens.

A partir do Configuration Manager versão 1610, o **preparar ConfigMgr Client** passo remove completamente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas, implementa a imagem do sistema operativo capturada, instala um novo cliente de Configuration Manager cada vez.  

> [!Note]  
>  O motor de sequência de tarefas apenas remove o cliente durante o **compilar e capturar uma imagem de sistema operativo de referência** sequência de tarefas. O motor de sequência de tarefas não remover o cliente durante a outros métodos de captura, como suporte de dados de captura ou de uma sequência de tarefas personalizada.

Antes do Configuration Manager versão 1610, este passo efetua as seguintes tarefas:  

-   Remove a secção de propriedades de configuração do cliente do ficheiro smscfg.ini no diretório do Windows. Estas propriedades incluem informações específicas do cliente, incluindo o GUID de Configuration Manager e outros identificadores do cliente.  

-   Elimina todos os certificados SMS ou o Configuration Manager da máquina.  

-   Elimina a cache do cliente do Configuration Manager.  

-   Limpa a variável de site atribuído do cliente do Configuration Manager.  

-   Elimina todas as política local do Configuration Manager.  

-   Remove a chave de raiz fidedigna para o cliente do Configuration Manager.  

Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

No editor de sequência de tarefas, clique em **adicionar**, selecione **imagens**e selecione **preparar ConfigMgr Client para captura** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 Este passo não necessitam de quaisquer definições no **propriedades** separador.



##  <a name="BKMK_PrepareWindowsforCapture"></a>Preparar Windows para captura  
 Utilize este passo para especificar as opções do Sysprep ao capturar uma imagem de sistema operativo no computador de referência. Esta ação de sequência de tarefas executa o Sysprep e, em seguida, reinicia o computador na imagem de arranque do Windows PE especificada para a sequência de tarefas. Esta ação irá falhar se o computador de referência está associado a um domínio.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Preparar Windows para Captura](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **imagens**e selecione **preparar Windows para captura** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Compilar automaticamente a lista de controladores de armazenamento em massa**  
 Selecione esta opção para o Sysprep compilar automaticamente uma lista de controladores de armazenamento em massa a partir do computador de referência. Esta opção ativa a opção Compilar Controladores de Armazenamento em Massa no ficheiro sysprep.inf no computador de referência. Para obter mais informações sobre esta definição, consulte a documentação do Sysprep.  

 **Repor o sinalizador de ativação**  
 Selecione esta opção para impedir o Sysprep de repor o sinalizador de ativação do produto.  



##  <a name="BKMK_PreProvisionBitLocker"></a>Provisão prévia do BitLocker  
 Utilize este passo para ativar o BitLocker numa unidade no Windows PE. Apenas o espaço de disco utilizado é encriptado e, portanto, os tempos de encriptação são muito mais rápidos. Aplique as opções de gestão de chaves utilizando o passo de sequência de tarefas [Ativar BitLocker](#BKMK_EnableBitLocker) após a instalação do sistema operativo. Este passo é executado apenas no Windows PE. Não é executado num sistema operativo padrão.  

> [!IMPORTANT]  
>  Pré-aprovisionar o BitLocker requer, pelo menos, Windows 7. O computador também tem de conter um suportado e ativado Trusted Platform Module (TPM).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **discos**e selecione **provisão prévia do BitLocker** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Aplicar BitLocker ao drive especificado**  
 Especifique a unidade para a qual pretende ativar o BitLocker. Apenas o espaço utilizado na unidade é encriptado.  

 **Ignore este passo em computadores que não têm TPM ou quando o TPM não está ativado**  
 Selecione esta opção para ignorar a encriptação de unidade num computador que não contenha um TPM suportado ou ativado conforme necessário. Por exemplo, utilize esta opção quando implementar um sistema operativo para uma máquina virtual.  



##  <a name="BKMK_ReleaseStateStore"></a>Disponibilizar armazenamento de Estados  
 Utilize este passo para notificar o estado do ponto de migração de que a ação de captura ou restauro está concluída. Utilize este passo juntamente com o **solicitar armazenamento de Estados**, **capturar estado do utilizador**, e **restaurar estado do utilizador** passos. Utilize estes passos para migrar dados de estado de utilizador utilizando um ponto de migração de estado e a ferramenta de migração de estado de utilizador (USMT).  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

 Se utilizar o **solicitar armazenamento de Estados** passo para solicitar acesso a um ponto de migração de estado para *capturar* de estado do utilizador, este passo notifica o ponto de migração de estado a processar a captura está concluído. O ponto de migração de estado, em seguida, marca os dados de estado de utilizador como disponíveis para restauro. O ponto de migração de estado define o acesso de permissões de controlo para os dados de estado de utilizador para que apenas o computador de restauro tem acesso só de leitura.  

 Se utilizar o **solicitar armazenamento de Estados** passo para solicitar acesso a um ponto de migração de estado para *restaurar* de estado do utilizador, este passo notifica o ponto de migração de estado que o processo de restauro está concluído. A migração de estado do ponto de, em seguida, Ativa as definições de retenção de dados configurados.  

> [!IMPORTANT]  
>  Uma melhor prática é definir o **continuar com o erro** opção para quaisquer passos entre o **solicitar armazenamento de Estados** e **disponibilizar armazenamento de Estados** passos. Cada **solicitar armazenamento de Estados** passo tem de ter uma correspondência **disponibilizar armazenamento de Estados** passo.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência Disponibilizar Armazenamento de Estados](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **estado do utilizador**e selecione **disponibilizar armazenamento de Estados** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 Este passo não necessitam de quaisquer definições no **propriedades** separador.



##  <a name="BKMK_RequestStateStore"></a>Solicitar armazenamento de Estados  
 Utilize este passo para pedir acesso a um ponto de migração de estado ao capturar ou restaurar o estado.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

 Utilize este passo juntamente com o **disponibilizar armazenamento de Estados**, **capturar estado do utilizador**, e **restaurar estado do utilizador** passos. Utilize estes passos para migrar o estado do computador utilizando um ponto de migração de estado e a ferramenta de migração de estado de utilizador (USMT).  

> [!NOTE]  
>  Ao criar um novo ponto de migração de estado, o armazenamento de Estados do utilizador não está disponível para até uma hora. Para agilizar a disponibilidade, ajuste as definições de propriedade no ponto de migração de estado para acionar uma atualização de ficheiro de controlo do site.  

 Este passo de sequência de tarefas é executado num sistema operativo padrão e no Windows PE para o USMT offline. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Solicitar Armazenamento de Estados](task-sequence-action-variables.md#BKMK_RequestState).  

No editor de sequência de tarefas, clique em **adicionar**, selecione **estado do utilizador**e selecione **solicitar armazenamento de Estados** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Capturar estado do computador**  
 Localize um ponto de migração de estado que cumpre os requisitos mínimos, conforme configurado nas definições de ponto de migração de estado. Por exemplo, **número máximo de clientes** e **quantidade mínima de espaço livre em disco**. Esta opção não garante esteja disponível espaço suficiente no momento da migração de estado. Esta opção de solicita acesso ao ponto de migração de estado para capturar o estado do utilizador e as definições de um computador.  

 Se o site do Configuration Manager tiver vários pontos de migração de estado ativo, este passo localiza um ponto de migração de estado com espaço em disco disponível. A sequência de tarefas consulta o ponto de gestão para obter uma lista dos pontos de migração de estado e, em seguida, avalia cada um até encontrar um que cumpra os requisitos mínimos.  

 **Restaurar estado a partir de outro computador**  
 Pedir acesso a um ponto de migração de estado para restaurar o estado de utilizador capturados anteriormente e definições para um computador de destino.  

 Se existirem vários pontos de migração de estado, este passo localiza o ponto de migração de estado que possui o estado para o computador de destino.  

 **Número de tentativas**  
 O número de vezes que este passo tenta localizar um ponto de migração de estado adequado antes de falhar.  

 **Intervalo de repetição (em segundos)**  
 Período de tempo em segundos que o passo de sequência de tarefas aguarda entre as tentativas.  

 **Se a conta de computador falhar a ligação ao armazenamento de Estados, utilize a conta de acesso de rede.**  
 Se a sequência de tarefas não é possível aceder ao ponto de migração de estado utilizando a conta de computador, utiliza as credenciais de conta de acesso de rede para ligar. Esta opção é menos segura porque outros computadores poderia utilizar a conta de acesso de rede para o estado armazenado de acesso. Esta opção pode ser necessária se o computador de destino não está associado a um domínio.  



##  <a name="BKMK_RestartComputer"></a>Reiniciar computador  
 Utilize este passo para reiniciar o computador que executa a sequência de tarefas. Após o reinício, o computador continua automaticamente com o passo seguinte na sequência de tarefas.  

 Este passo pode ser executado num sistema operativo padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, consulte [reiniciar variáveis de ação de sequência de tarefas do computador](task-sequence-action-variables.md#BKMK_RestartComputer).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **reiniciar o computador** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **A imagem de arranque atribuída a esta sequência de tarefas**  
 Selecione esta opção para o computador de destino a utilizar a imagem de arranque atribuída à sequência de tarefas. A sequência de tarefas utiliza a imagem de arranque para executar os passos subsequentes no Windows PE.  

 **O sistema operativo predefinido atualmente instalado**  
 Selecione esta opção para o computador de destino ser reiniciado no sistema operativo instalado.  

 **Notificar o utilizador antes de reiniciar**  
 Selecione esta opção para apresentar uma notificação ao utilizador antes do reinício do computador de destino. O passo seleciona esta opção, por predefinição.  

 **Mensagem de notificação**  
 Introduza uma mensagem de notificação para apresentar ao utilizador antes do reinício do computador de destino.  

 **Tempo limite de visualização da mensagem**  
 Especifique a quantidade de tempo em segundos antes do reinício do computador de destino. A predefinição é 60 segundos.  



##  <a name="BKMK_RestoreUserState"></a>Restaurar estado do utilizador  
 Utilize este passo para iniciar o utilizador State Migration Tool (USMT) para restaurar o estado de utilizador e as definições para o computador de destino. Utilize este passo em conjunto com o **capturar estado do utilizador** passo.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

 Utilize este passo com o **solicitar armazenamento de Estados** e **disponibilizar armazenamento de Estados** passos para guardar ou restaurar as definições de estado com um ponto de migração de estado. Com o USMT 3.0 e superior, esta opção desencripta sempre o armazenamento de Estados do USMT através de uma chave de encriptação gerada e gerida pelo Configuration Manager.  

 O **restaurar estado do utilizador** passo fornece controlo sobre um subconjunto limitado das mais frequentemente opções utilizadas pelo USMT. Especifique as opções da linha de comandos adicionais com a variável de sequência de tarefas OSDMigrateAdditionalRestoreOptions.  

> [!IMPORTANT]  
>  Se estiver a utilizar este passo para um objetivo não relacionado com um cenário de implementação do sistema operativo, adicione o [reiniciar o computador](#BKMK_RestartComputer) passo imediatamente a seguir a **restaurar estado do utilizador** passo.  

 Este passo é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Restaurar Estado do Utilizador](task-sequence-action-variables.md#BKMK_RestoreUserState).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **estado do utilizador**e selecione **restaurar estado do utilizador** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Pacote de ferramenta de migração de estado de utilizador**  
 Especifique o pacote que contém a versão do USMT para este passo para utilizar. Este pacote não requer um programa. Quando o passo é executado, a sequência de tarefas utiliza a versão do USMT no pacote especificado. Especifique um pacote com a versão de 32 bits ou 64 bits do USMT. A arquitetura do USMT depende da arquitetura do sistema operativo para que a sequência de tarefas é de restaurar o estado. 

 **Restaurar todos os perfis de utilizador capturados com opções padrão**  
 Restaura todos os perfis de utilizador capturados com as opções padrão. Para personalizar as opções que restaura do USMT, selecione **personalizar captura de perfil de utilizador**.  

 **Personalizar como os perfis de utilizador são restaurados**  
 Permite personalizar os ficheiros que pretende restaurar para o computador de destino. Clique em **Ficheiros** para especificar os ficheiros de configuração no pacote do USMT que pretende utilizar para restaurar os perfis de utilizador. Para adicionar um ficheiro de configuração, introduza o nome do ficheiro na caixa **Nome do ficheiro** e clique em **Adicionar**. Painel ficheiros lista os ficheiros de configuração que utiliza a USMT. O ficheiro. XML especificado define o ficheiro de utilizador restaura USMT.  

 **Restaurar perfis de utilizador do computador local**  
 Restaura os perfis de utilizador do computador local. Estes perfis não são utilizadores do domínio. Tem de atribuir novas palavras-passe para as contas de utilizador locais restauradas. USMT não é possível migrar as palavras-passe original. Introduza a nova palavra-passe na caixa **Palavra-passe** e confirme-a na caixa **Confirmar Palavra-passe**.  

 **Continuar se não não possível restaurar alguns ficheiros**  
 Continua o restauro do Estado de utilizador e as definições, mesmo que esteja não é possível restaurar alguns ficheiros USMT. O passo ativa esta opção, por predefinição. Se desativar esta opção e USMT encontra erros ao restaurar os ficheiros, este passo falhe imediatamente. USMT não restaure todos os ficheiros.   

 **Ativar o registo verboso**  
 Ative esta opção para gerar informações de ficheiros de registo mais detalhadas. Ao restaurar o estado, a sequência de tarefas por predefinição gera Loadstate.log na pasta de registo da sequência de tarefas, \windows\system32\ccm\logs.  



##  <a name="BKMK_RunCommandLine"></a>Executar linha de comandos  
 Utilize este passo para executar a linha de comandos especificada.  

 Este passo pode ser executado num sistema operativo padrão ou no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Executar Linha de Comandos](task-sequence-action-variables.md#BKMK_RunCommand).  

 No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **executar linha de comandos** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Linha de comandos**  
 Especifica a linha de comandos que é executada. Este campo é obrigatório. As extensões de nome de ficheiro, incluindo são uma melhor prática, por exemplo,. vbs e .exe. Inclua todos os ficheiros de definições necessários, opções da linha de comandos ou parâmetros.  

 Se o nome de ficheiro não tiver uma extensão de nome de ficheiro especificado, o Configuration Manager tenta empresa>.com, .exe, e. bat. Se o nome do ficheiro tem uma extensão que não seja um executável, o Configuration Manager tenta aplicar uma associação local. Por exemplo, se a linha de comandos for readme.gif, o Configuration Manager inicia a aplicação especificada no computador de destino para abrir ficheiros GIF.  

 Exemplos:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
>  Para executar com êxito, preceder ações da linha de comandos com o **cmd.exe /c** comando. Exemplo destas ações incluem o redirecionamento de saída, encaminhando e copiar comandos.  

 **Desativar redirecionamento de sistema de ficheiros de 64 bits**  
 sistemas operativos de 64 bits utilizam o redirecionador de sistema de ficheiros WOW64 por predefinição para executar linhas de comandos. Este comportamento é corretamente encontrar versões de 32 bits dos executáveis de sistema operativo e bibliotecas. Selecione esta opção para desativar a utilização do redirecionador do sistema de ficheiros WOW64. Windows é executado o comando utilizando as versões de 64 bits nativas de executáveis de sistema operativo e bibliotecas. Esta opção não tem efeito numa execução num sistema operativo de 32 bits.  

 **Iniciar**  
 Especifica a pasta executável do programa, até 127 carateres. Esta pasta pode ser um caminho absoluto no computador de destino ou um caminho relativo para a pasta do ponto de distribuição que contém o pacote. Este campo é opcional.  

 Exemplos:  

 **c:\OfficeXP**  

 **i386**  

> [!NOTE]  
>  O **procurar** botão de procura no computador local para ficheiros e pastas. Tudo o que selecionar também têm de existir no computador de destino na mesma localização e com o mesmo ficheiro e os nomes de pastas.  

 **Pacote**  
 Ao especificar ficheiros ou programas na linha de comandos que já não estão presentes no computador de destino, selecione esta opção para especificar o pacote de Configuration Manager que contém os ficheiros adequados. O pacote não requer um programa. Esta opção não é necessária se os ficheiros especificados existirem no computador de destino.  

 **Tempo limite**  
 Especifica um valor que representa o período de tempo do Configuration Manager permite que a linha de comandos executar. Este valor pode ser de 1 minuto a 999 minutos. O valor predefinido é 15 minutos.  

 Esta opção está desativada por predefinição.  

> [!IMPORTANT]  
>  Se introduzir um valor que não permita tempo suficiente para o comando especificado concluir com êxito, este passo falhe. A sequência de tarefas completo foi falhar, consoante as restantes definições de controlo. Se o tempo limite expirar, o Configuration Manager termina o processo da linha de comandos.  

 **Executar este passo de como a seguinte conta**  
 Especifica que a linha de comandos é executada como uma conta de utilizador do Windows em vez da conta de sistema local.  

> [!NOTE]  
>  Para executar scripts simples ou comandos com outra conta depois de instalar o sistema operativo, tem de adicionar a conta de computador. Além disso, tem de restaurar o perfil de conta de utilizador do Windows para executar programas mais complexos, tais como um Windows Installer.  

 **Conta**  
 Especifica a conta de utilizador do Windows que neste passo utiliza para executar a linha de comandos. A linha de comandos é executada com as permissões da conta especificada. Clique em **Definir** para especificar a conta de utilizador local ou de domínio.  

> [!IMPORTANT]  
>  Se este passo Especifica uma conta de utilizador e é executado no Windows PE, a ação falhará. Não é possível associar o Windows PE para um domínio. O ficheiro smsts.log regista esta falha.  



##  <a name="BKMK_RunPowerShellScript"></a>Executar Script do PowerShell  
 Utilize este passo para executar o script do PowerShell especificado.  

 Este passo pode ser executado num sistema operativo padrão ou no Windows PE. Para executar este passo no Windows PE, o PowerShell tem de estar ativado na imagem de arranque. Pode ativar o Windows PowerShell (WinPE-PowerShell) a partir do separador **Componentes Opcionais** nas propriedades da imagem de arranque. Para obter mais informações sobre como modificar uma imagem de arranque, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  Por predefinição, o PowerShell não está ativado nos sistemas operativos Windows Embedded.  

No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **executar Script do PowerShell** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Pacote**  
 Especifique o pacote de Configuration Manager que contém o script do PowerShell. Um pacote pode conter vários scripts do PowerShell.  

 **Nome do script**  
 Especifica o nome do script do PowerShell a executar. Este campo é obrigatório.  

 **Parâmetros**  
 Especifica os parâmetros transmitidos para o script do Windows PowerShell. Estes parâmetros são os mesmos que os parâmetros do script do Windows PowerShell na linha de comandos.  

> [!IMPORTANT]  
>  Forneça parâmetros consumidos pelo script e não para a linha de comandos do Windows PowerShell.  
>   
>  O exemplo seguinte contém parâmetros válidos:  
>   
>  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
>   
>  O exemplo seguinte contém parâmetros inválidos. Os primeiros dois itens são parâmetros da linha de comandos do Windows PowerShell (**- NoLogo** e **- ExecutionPolicy Unrestricted**). O script não consumir estes parâmetros.  
>   
>  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

 **Política de execução do PowerShell**  
 Determinar quais os scripts do Windows PowerShell (se aplicável) permite a execução no computador. Escolha uma das seguintes políticas de execução:  

-   **AllSigned**: Executar apenas scripts assinados por um fabricante fidedigno  

-   **Indefinido**: Não defina qualquer política de execução  

-   **Ignorar**: Carregar todos os ficheiros de configuração e executar todos os scripts. Se transferir um script não assinado da Internet, do Windows PowerShell não pedir permissão antes de executar o script.  

> [!IMPORTANT]  
>  O PowerShell 1.0 não suporta as políticas de execução Indefinido e Ignorar.  



##  <a name="child-task-sequence"></a>Executar a sequência de tarefas

A partir do Configuration Manager versão 1710, pode adicionar um novo passo executa outra sequência de tarefas. Este passo cria uma relação principal-subordinado entre as sequências de tarefas. Com sequências de tarefas subordinadas, pode criar mais sequências de tarefas modulares e reutilizáveis.

Quando adicionar uma sequência de tarefas subordinados a uma sequência de tarefas, considere as seguintes instruções:
 - As sequências de tarefas principais e subordinados eficazmente são combinadas uma única política que executa o cliente.
 - O ambiente é global. Se a sequência de tarefas principal define uma variável e, em seguida, a sequência de tarefas subordinado alterará essa variável, retém o valor mais recente. Se a sequência de tarefas subordinado cria uma nova variável, está disponível para os restantes da sequência de tarefas principal.
 - Mensagens de estado são enviadas por normal para uma operação de sequência de tarefas único.
 - As sequências de tarefas escreverem entradas no ficheiro smsts.log, com o novo registo de entradas que desmarque quando uma sequência de tarefas subordinado é iniciado.

No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **executar a sequência de tarefas** para adicionar este passo. 

### <a name="properties"></a>Propriedades
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

**Selecione a sequência de tarefas para executar**  
 Clique em **procurar** para selecionar a sequência de tarefas subordinado. O **Selecione uma sequência de tarefas** caixa de diálogo não apresenta a sequência de tarefas do principal.



##  <a name="BKMK_SetDynamicVariables"></a>Definir variáveis dinâmicas  
 Utilize este passo para efetuar as seguintes ações:  

1.  Recolher informações do computador e do ambiente em que está e, em seguida, definir variáveis de sequência de tarefas especificadas com as informações.  

2.  Avaliar as regras definidas e definir variáveis de sequência de tarefas com base nas variáveis e nos valores configurados para as regras avaliadas como verdadeiras.  

A sequência de tarefas define automaticamente as seguintes variáveis de sequência de tarefas só de leitura:  
 -   &#95; SMSTSMake  
 -   &#95; SMSTSModel  
 -   &#95; SMSTSMacAddresses  
 -   &#95; SMSTSIPAddresses  
 -   &#95; SMSTSSerialNumber  
 -   &#95; SMSTSAssetTag  
 -   &#95; SMSTSUUID  

Este passo pode ser executado num sistema operativo padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas, consulte [variáveis de ação da sequência de tarefas](task-sequence-action-variables.md).  

No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **definir variáveis dinâmicas** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

**Regras e variáveis dinâmicas**  
 Para definir uma variável dinâmica para utilização na sequência de tarefas, adicione uma regra. Em seguida, defina um valor para cada variável especificada na regra. Além disso, adicione uma ou mais variáveis sem adicionar uma regra. Quando adicionar uma regra, escolha entre as seguintes categorias:  

 -   **Computador**: Avalie os valores de etiqueta de recursos de hardware, UUID, número de série ou endereço MAC. Defina vários valores conforme necessário. Se qualquer valor for VERDADEIRO, a regra avalia como verdadeiro. Por exemplo, a regra seguinte avalia como VERDADEIRO se o número de série do dispositivo for 5892087 e o endereço MAC é 22-A4-5A-13-78-26.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Localização**: Avaliar os valores para o gateway de rede predefinido  

-   **Marca e modelo**: Avalie os valores da marca e modelo de um computador. A marca e o modelo têm de avaliar como verdadeiro para a regra avaliar como verdadeiro.   

    <!-- for future edits: an escape code must be used for the bolded asterisk character, but may be removed somewhere along the way. Instead of five asterisk, should be bold tags with &#42; in-between -->

    A partir do Configuration Manager versão 1610, pode especificar um asterisco (**&#42;**) e o ponto de interrogação (**?**) como os carateres universais, onde **&#42;** corresponde a várias carateres e **?** corresponde a um único caráter. Por exemplo, a cadeia "DELL * 900?" corresponderá DELL-ABC-9001 e DELL9009. 

    Especifique um asterisco (**&#42;**) e o ponto de interrogação (**?**) como os carateres universais, onde **&#42;** corresponde a vários carateres e **?** corresponde a um único caráter. Por exemplo, a cadeia "DELL * 900?" corresponde a ABC-DELL-9001 e DELL9009.

-   **Variável de sequência de tarefas**: Adicione uma variável de sequência de tarefas, condição e valor a avaliar. A regra avalia como verdadeiro quando o conjunto de valores da variável cumpre a condição especificada.  

    Especifique um ou mais variáveis a definir para uma regra que avalia como VERDADEIRO ou definir variáveis sem utilizar uma regra. Selecione uma variável existente ou crie uma variável personalizada.  

     -   **Variáveis de sequência de tarefas existente**: Selecione uma ou mais variáveis a partir de uma lista de variáveis de sequência de tarefas existentes. As variáveis da matriz não estão disponíveis para seleção.  

     -   **As variáveis de sequência de tarefas personalizada**: Defina uma variável de sequência de tarefas personalizada. Também pode especificar uma variável de sequência de tarefas existente. Esta definição é útil para especificar uma matriz de variável existente, como OSDAdapter, uma vez que as matrizes de variáveis não estão na lista de variáveis de sequência de tarefas existente.  

Depois de selecionar as variáveis para uma regra, tem de fornecer um valor para cada variável. A variável é definida para o valor especificado quando a regra avalia como verdadeiro. Para cada variável, pode selecionar **Valor secreto** para ocultar o valor da variável. Por predefinição, algumas variáveis existentes ocultam valores, como a variável de sequência de tarefas OSDCaptureAccountPassword.  

> [!IMPORTANT]  
>  Gestor de configuração remove todos os valores das variáveis marcados como um **valor secreto** quando importar uma sequência de tarefas com o **definir variáveis dinâmicas** passo. Volte a introduzir o valor da variável dinâmica depois de importar a sequência de tarefas.  



##  <a name="BKMK_SetTaskSequenceVariable"></a>Definir variável da sequência de tarefas  
Utilize este passo para definir o valor de uma variável utilizada com a sequência de tarefas.  

Este passo pode ser executado num sistema operativo padrão ou no Windows PE. As variáveis de sequência de tarefas são lidas pelas ações de sequência de tarefas e especificam o comportamento dessas ações. Para mais informações sobre variáveis de ação de sequência de tarefas específicas, consulte [variáveis de ação da sequência de tarefas](task-sequence-action-variables.md). Para mais informações sobre variáveis incorporadas de sequência de tarefas específica, consulte [variáveis incorporadas de sequência de tarefas](/sccm/osd/understand/task-sequence-built-in-variables).

No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e selecione **Set Task Sequence Variable** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Variável de sequência de tarefas**  
 Especifique o nome de uma sequência de tarefas incorporada ou uma variável de ação ou especifique o seu próprio nome de variável definida pelo utilizador.  

 **Valor**  
 A sequência de tarefas define a variável para este valor. Defina esta variável de sequência de tarefas para o valor de outra variável de sequência de tarefas com a sintaxe % varname %.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a>Configurar Windows e ConfigMgr  
 Utilize este passo para efetuar a transição do Windows PE para o novo sistema operativo. Este passo da sequência de tarefas é uma parte necessária de qualquer implementação do sistema operativo. Instala o cliente do Configuration Manager para o novo sistema operativo e prepara a sequência de tarefas continuar a execução no novo sistema operativo.  

 Este passo é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para mais informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, consulte [variáveis de ação da sequência de tarefas configurar Windows e ConfigMgr](task-sequence-action-variables.md#BKMK_SetupWindows).  

 Este passo substitui as variáveis de diretório sysprep.inf ou unattend.xml, como % WINDIR % e % ProgramFiles %, com o diretório de instalação do Windows PE, X:\Windows. A sequência de tarefas ignora variáveis especificadas utilizando estas variáveis de ambiente.  

 Utilize este passo de sequência de tarefas para executar as seguintes ações:  

1.  Preliminares: Windows PE  

    1.  Substitua as variáveis de sequência de tarefas no ficheiro unattend.xml.  

    2.  Transferir o pacote que contém o cliente do Configuration Manager. Adicione o pacote na imagem implementada.  

2.  Configurar o Windows  

    1.  Instalação baseada em imagem  

        1.  Desative o cliente do Configuration Manager na imagem, se existir. Por outras palavras, desative o início automático para o serviço de cliente do Configuration Manager.  

        2.  Atualize o registo na imagem implementada para iniciar o sistema operativo implementado com a mesma letra de unidade que o computador de referência.  

        3.  Reiniciar para o sistema operativo implementado.  

        4.  A mini-configuração do Windows é executada através de especificado anteriormente ficheiro sysprep.inf ou unattend.xml resposta que tem todas as interações do utilizador final suprimidas. Se utilizar o **aplicar definições de rede** passo aderir a um domínio, em seguida, essas informações estão no ficheiro de resposta. A mini-configuração do Windows associa o computador ao domínio.  

    2.  Instalação baseada em Setup.exe.  Executa Setup.exe, que segue o processo de configuração normal do Windows:  

        1.  Pacote de atualização de SO de cópia, especificado no **aplicar sistema operativo** passo, a unidade de disco rígido.  

        2.  Reinicie o sistema operativo recentemente implementado.  

        3.  A mini-configuração do Windows é executada através de especificado anteriormente ficheiro sysprep.inf ou unattend.xml resposta que tem todas as definições de interface de utilizador suprimidas. Se utilizar o **aplicar definições de rede** passo aderir a um domínio, em seguida, essas informações estão no ficheiro de resposta. A mini-configuração do Windows associa o computador ao domínio.  

3.  Configurar o cliente do Configuration Manager  

    1.  Após a conclusão da miniconfiguração do Windows, a sequência de tarefas é retomada com o setupcomplete.cmd.  

    2.  Ativar ou desativar a conta de administrador local, com base na opção selecionada no **aplicar definições do Windows** passo.  

    3.  Instale o cliente do Configuration Manager utilizando o pacote transferido anteriormente e propriedades de instalação especificadas neste passo. A instalação do cliente no "modo de aprovisionamento" para impedi-lo de processar novos pedidos de política, até que conclua a sequência de tarefas.  

    4.  Aguarde que o cliente estar totalmente operacional.  

4.  A sequência de tarefas continua a executar o passo seguinte.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->

No editor de sequência de tarefas, clique em **adicionar**, selecione **imagens**e selecione **configurar Windows e ConfigMgr** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
 No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

 **Pacote de cliente**  
 Clique em **procurar**, em seguida, selecione o pacote de instalação de cliente do Configuration Manager para utilizar neste passo.  

 **Utilize o pacote de cliente de pré-produção quando disponível**  
 Se existir um pacote de cliente de pré-produção disponível, a sequência de tarefas utiliza este pacote em vez do pacote de cliente de produção. O cliente de pré-produção é uma versão mais recente para fins de teste no ambiente de produção. Clique em **procurar**, em seguida, selecione o pacote de instalação de cliente de pré-produção para utilizar com este passo.  

 **Propriedades de instalação**  
 A atribuição de sites e a configuração predefinida são especificadas automaticamente pela ação de sequência de tarefas. Pode utilizar este campo para especificar propriedades de instalação adicionais a utilizar quando instalar o cliente. Para introduzir várias propriedades de instalação, separe-as com um espaço.  

 Pode especificar opções da linha de comandos a utilizar durante a instalação do cliente. Por exemplo, pode introduzir **/skipprereq: silverlight.exe** para informar o ficheiro CCMSetup.exe para não instalar o pré-requisito Microsoft Silverlight. Para obter mais informações sobre as opções da linha de comandos disponíveis para CCMSetup.exe, consulte [acerca das propriedades de instalação de cliente](../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="options"></a>Opções
> [!NOTE]
> Não ative **continuar com o erro** no **opções** separador. Se ocorrer um erro durante este passo, a sequência de tarefas falhará se ou não ativar esta definição.



##  <a name="BKMK_UpgradeOS"></a>Atualizar sistema operativo  
 > [!TIP]  
 > Começando com o Windows 10, versão 1709, o suporte de dados inclui várias edições. Quando configura uma sequência de tarefas para utilizar um pacote de atualização do SO ou a imagem do SO, é necessário selecionar um [suportado edição](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Utilize este passo para atualizar uma versão mais antiga do Windows para uma versão mais recente do Windows 10.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

No editor de sequência de tarefas, clique em **adicionar**, selecione **imagens**e selecione **atualizar sistema operativo** para adicionar este passo. 

### <a name="properties"></a>Propriedades  
No **propriedades** separador para este passo, configure as definições descritas nesta secção.  

**Pacote de atualização**  
 Selecione esta opção para especificar o pacote de atualização do sistema operativo Windows 10 para utilizar na atualização.  

**Caminho de origem**  
 Especifica uma local ou o caminho para o suporte de dados do Windows 10 de rede que utiliza a configuração do Windows. Esta definição corresponde à opção da linha de comandos da configuração do Windows **/InstallFrom**. Também pode especificar uma variável, tal como %caminhodomeuconteúdo% ou %DPC01%. Quando utilizar uma variável para o caminho de origem, esta tem de ter sido especificada anteriormente na sequência de tarefas. Por exemplo, se utilizar o passo [Transferir Conteúdo do Pacote](#BKMK_DownloadPackageContent) na sequência de tarefas, pode especificar uma variável para a localização do pacote de atualização do sistema operativo. Em seguida, pode utilizar essa variável para o caminho de origem deste passo.  

**Edição**  
 Especifique a edição no suporte de dados do sistema operativo a utilizar para a atualização.  

**Chave de produto**  
 Especifique a chave de produto a aplicar ao processo de atualização  

**Fornecer o seguinte conteúdo de controladores à configuração do Windows durante a atualização**  
 Adicione controladores ao computador de destino durante o processo de atualização. Esta definição corresponde à opção da linha de comandos da configuração do Windows **/InstallDriver**. Os controladores têm de ser compatíveis com o Windows 10. Especifique uma das seguintes opções:  

-   **Pacote de controladores**: Clique em **procurar** e selecione um pacote de controladores existente na lista.  

-   **Conteúdo de teste**:  Selecione esta opção para especificar a localização para o pacote de controladores. Pode especificar uma pasta local, um caminho de rede ou uma variável de sequência de tarefas. Quando utilizar uma variável para o caminho de origem, esta tem de ter sido especificada anteriormente na sequência de tarefas. Por exemplo, utilizando o passo [Transferir Conteúdo do Pacote](task-sequence-steps.md#BKMK_DownloadPackageContent).  

**Tempo limite (minutos)**  
 Especifica o número de minutos antes do Gestor de configuração não consegue este passo. Esta opção é útil se a configuração do Windows para o processamento, mas não terminar.  

**Efetuar análise de compatibilidade de configuração do Windows sem iniciar a atualização**  
 Efetue a análise de compatibilidade de configuração do Windows sem iniciar o processo de atualização. Esta definição corresponde à opção da linha de comandos da configuração do Windows **/compat ScanOnly**. Tem de implementar a origem de instalação completa quando utilizar esta opção. A Configuração devolve um código de saída como resultado da análise. A tabela seguinte fornece alguns dos códigos de saída mais comuns.  

|Código de saída|Detalhes|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Não existem problemas de compatibilidade ("êxito").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0XC1900208)|Problemas de compatibilidade passíveis de ação.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0XC1900204)|A opção de migração selecionada não está disponível. Por exemplo, uma atualização do Empresarial para o Profissional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Não é elegível para Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0XC190020E)|Não existe espaço livre suficiente no disco.|  

Para obter mais informações sobre este parâmetro, veja [Windows Setup Command-Line Options](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx) (Opções da Linha de Comandos de Configuração do Windows)  

**Ignorar mensagens de compatibilidade dispensáveis**  
 Especifica que a configuração conclui a instalação, ignorando quaisquer mensagens de compatibilidade dispensáveis. Esta definição corresponde à opção da linha de comandos da configuração do Windows **/compat IgnoreWarning**.  

**Atualizar dinamicamente a configuração do Windows com o Windows Update**  
 Ativar a configuração para efetuar operações de atualização dinâmica, como pesquisa, transferir e instalar atualizações. Esta definição corresponde à opção da linha de comandos da configuração do Windows **/DynamicUpdate**. Esta definição não é compatível com atualizações de software do Configuration Manager. Ative esta opção quando gere as atualizações com autónomo Windows Server Update Services (WSUS) ou o Windows Update para empresas.  

**Ignorar política e utilizar o Microsoft Update por predefinição** substituir temporariamente a política local em tempo real para executar operações de atualização dinâmica e o computador obter as atualizações do Windows Update.