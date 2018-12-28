---
title: Passos de sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba mais sobre os passos que pode adicionar a uma sequência de tarefas do Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e62983f76b0f2a4277edfab08d4321da5d4a258
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416491"
---
# <a name="task-sequence-steps-in-configuration-manager"></a>Passos de sequência de tarefas no Configuration Manager

 *Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Os seguintes passos de sequência de tarefas podem ser adicionados a uma sequência de tarefas do Configuration Manager. Para obter informações sobre a edição de uma sequência de tarefas, veja [Editar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  

 As definições seguintes são comuns a todos os passos de sequência de tarefas:

#### <a name="properties-tab"></a>Separador Propriedades
 - **Nome**: O editor de sequência de tarefas requer que especifique um nome abreviado para descrever este passo. Quando adiciona um novo passo, o editor de sequência de tarefas define o nome para o tipo por predefinição. O **nome** não pode ter mais de 50 caracteres.  

 - **Descrição**: Opcionalmente, especifique as informações mais detalhadas sobre este passo. O **Descrição** comprimento não pode exceder os 256 carateres.  


 O resto deste artigo descreve as outras definições no **propriedades** separador para cada passo de sequência de tarefas.

#### <a name="options-tab"></a>Separador Opções  

 - **Desativar este passo**: A sequência de tarefas ignore este passo quando é executada num computador. O ícone para este passo está esbatido no editor de sequência de tarefas.  

 - **Continuar com o erro**: Se ocorrer um erro ao executar o passo, a sequência de tarefas continua. Para obter mais informações, consulte [considerações sobre planeamento para automatizar tarefas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSGroups).   

 - **Adicionar condição**: A sequência de tarefas avalia estas instruções condicionais para determinar se ele é executado o passo. Para obter um exemplo da utilização de uma variável de sequência de tarefas como uma condição, consulte [como utilizar variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables#bkmk_access-condition).   


 As secções abaixo para passos de sequência de tarefas específica descrevem outras configurações possíveis a **opções** separador.



##  <a name="BKMK_ApplyDataImage"></a> Aplicar imagem de dados   

 Utilize este passo para copiar a imagem de dados para a partição de destino especificado.  

 Este passo é executado apenas no Windows PE. Não é executado no SO completo. 

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDDataImageIndex](/sccm/osd/understand/task-sequence-variables#OSDDataImageIndex)  
 - [OSDWipeDestinationPartition](/sccm/osd/understand/task-sequence-variables#OSDWipeDestinationPartition)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **imagens**e selecione **aplicar imagem de dados**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="image-package"></a>Pacote de Imagem  
 Clique em **navegue** para especificar a **pacote de imagem** utilizado por esta sequência de tarefas. Selecione o pacote que pretende instalar na caixa de diálogo **Selecionar um Pacote**. Na parte inferior da caixa de diálogo apresenta as informações de propriedade associada para cada pacote de imagem existente. Utilize a lista pendente para selecionar a **Imagem** que pretende instalar a partir do **Pacote de Imagem** selecionado.  

 > [!NOTE]  
 >  Esta ação de sequência de tarefas processa a imagem como um ficheiro de dados. Esta ação não faz qualquer programa de configuração para arrancar a imagem como um sistema operacional.  

#### <a name="destination"></a>Destino  
 Configure uma das seguintes opções:

 - **Partição disponível seguinte**: Utilize a partição sequencial seguinte que um **aplicar sistema operativo** ou **aplicar imagem de dados** passo para esta sequência de tarefas não tiver já visados.  

 - **Partição e disco específico**: Selecione o **disco** número (começando com 0) e o **partição** número (começando com 1).  

 - **Letra de unidade lógica específica**: Especifique a **letra de unidade** que atribui do Windows PE na partição. Esta letra de unidade pode ser diferente da letra de unidade atribuída pelo sistema operativo recentemente implementado.  

 - **Letra de unidade lógica armazenada numa variável**: Especifique a variável de sequência de tarefas que contém a letra de unidade atribuída à partição pelo Windows PE. Esta variável normalmente é definida na secção avançada a **propriedades de partição** caixa de diálogo para o **formatar e particionar disco** passo de sequência de tarefas.  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Elimine todo o conteúdo na partição antes de aplicar a imagem  
 Especifica que a sequência de tarefas Elimina todos os ficheiros na partição de destino antes de instalar a imagem. Ao não eliminar o conteúdo da partição, esta ação pode ser utilizada para aplicar conteúdo adicional a uma partição direcionada anteriormente.  



##  <a name="BKMK_ApplyDriverPackage"></a> Aplicar pacote de controlador  

 Utilize este passo para transferir todos os controladores no pacote de controlador e instalá-los no SO Windows.

 O passo de sequência de tarefas **Aplicar Pacote de Controlador** torna todos os controladores de dispositivo num pacote de controlador disponíveis para serem utilizados pelo Windows. Adicionar este passo entre o **aplicar sistema operativo** e **configuração do Windows e ConfigMgr** passos para tornar os controladores no pacote disponível para Windows. Normalmente, o passo **Aplicar Pacote de Controlador** é colocado depois do passo de sequência de tarefas **Aplicar Controladores Automaticamente**. O passo de sequência de tarefas **Aplicar Pacote de Controlador** também é útil em cenários de implementação de suportes de dados autónomos.  

 Colocar os controladores de dispositivo semelhantes num pacote de controladores e distribuí-los para os pontos de distribuição apropriados. Por exemplo, coloque todos os controladores de um fabricante num pacote de controlador. Em seguida, distribua o pacote para pontos de distribuição em que os computadores associados podem aceder aos mesmos.

 O **aplicar pacote de controlador** passo é útil para suportes de dados autónomos. Este passo também é útil para instalar um conjunto específico de controladores. Esses tipos de controladores incluem os dispositivos Windows plug and play não Deteta, tais como impressoras de rede.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado no SO completo. 

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDApplyDriverBootCriticalContentUniqueID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalContentUniqueID)  
 - [OSDApplyDriverBootCriticalHardwareComponent](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalHardwareComponent)  
 - [OSDApplyDriverBootCriticalID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalID)  
 - [OSDApplyDriverBootCriticalINFFile](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalINFFile)  
 - [OSDInstallDriversAdditionalOptions](/sccm/osd/understand/task-sequence-variables#OSDInstallDriversAdditionalOptions) <!--516679/2840016--> (a partir da versão 1806)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **controladores**e selecione **aplicar pacote de controlador**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="driver-package"></a>Pacote de controladores
 Especifique o pacote de controladores que contém os controladores de dispositivo necessários. Clique em **navegue** para iniciar o **selecionar um pacote** caixa de diálogo. Selecione um pacote de controladores existente para aplicar. Na parte inferior da caixa de diálogo apresenta as propriedades do pacote associado.  

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Selecionar o controlador de armazenamento em massa no pacote que tem de ser instalado antes da configuração em sistemas operativos anteriores ao Windows Vista
 Especifique quaisquer controladores de armazenamento em massa necessários para instalar um sistema operacional clássico.  

#### <a name="driver"></a>Controlador
 Selecione o ficheiro de controlador de armazenamento em massa a instalar antes da configuração de um sistema operacional clássico. Preenche a lista pendente do pacote especificado.  

#### <a name="model"></a>Modelo  
 Especifique o dispositivo crítico de arranque que é necessária para Implantações de SO de Vista de anteriores ao Windows.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Efetuar a instalação autónoma de controladores não assinados nas versões do Windows em que tal é permitido
 Esta opção permite que o Windows instalar controladores sem uma assinatura digital.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Aplicar definições de rede   

 Utilize este passo para especificar as informações de configuração de rede ou o grupo de trabalho para o computador de destino. A sequência de tarefas armazena estes valores no ficheiro de resposta adequado. Este ficheiro de resposta durante a configuração do Windows utiliza a **configuração do Windows e ConfigMgr** ação.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado no SO completo. 

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDAdapter](/sccm/osd/understand/task-sequence-variables#OSDAdapter)  
 - [OSDAdapterCount](/sccm/osd/understand/task-sequence-variables#OSDAdapterCount)  
 - [OSDDNSDomain](/sccm/osd/understand/task-sequence-variables#OSDDNSDomain)  
 - [OSDDNSSuffixSearchOrder](/sccm/osd/understand/task-sequence-variables#OSDDNSSuffixSearchOrder)  
 - [OSDDomainName](/sccm/osd/understand/task-sequence-variables#OSDDomainName)  
 - [OSDDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDDomainOUName)  
 - [OSDEnableTCPIPFiltering](/sccm/osd/understand/task-sequence-variables#OSDEnableTCPIPFiltering)  
 - [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
 - [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
 - [OSDWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDWorkgroupName)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **definições**e selecione **aplicar definições de rede**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="join-a-workgroup"></a>Aderir a um grupo de trabalho
 Selecione esta opção para associar o computador de destino ao grupo de trabalho especificado. Introduza o nome do grupo de trabalho na linha **Grupo de Trabalho**. O valor que o **capturar definições de rede** capturas de passo de sequência de tarefas podem substituir este valor. 

#### <a name="join-a-domain"></a>Aderir a um domínio
 Selecione esta opção para associar o computador de destino ao domínio especificado. Especifique ou navegue até ao domínio, tal como `fabricam.com`. Especifique ou navegue até um caminho de Lightweight Directory Access Protocol (LDAP) para uma unidade organizacional. Por exemplo: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

#### <a name="account"></a>Conta
 Clique em **Definir** para especificar uma conta com as permissões necessárias para associar o computador ao domínio. Na **conta de utilizador do Windows** caixa de diálogo, introduza o nome de utilizador no seguinte formato: `Domain\User`. Para obter mais informações, consulte [domínio de conta de adesão ao](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account). 

#### <a name="adapter-settings"></a>Definições da placa  
 Especifique as configurações de rede para cada placa de rede no computador. Clique em **Novo** para abrir a caixa de diálogo **Definições de Rede** e, em seguida, especifique as definições de rede. 
 - Se também de utilizar o **capturar definições de rede** passo, a sequência de tarefas aplica as definições de capturados anteriormente para o adaptador de rede. 
 - Se a sequência de tarefas anteriormente não capturar definições de rede, aplica-se as definições que especificar neste passo. 
 - A sequência de tarefas aplica-se estas definições a adaptadores de rede na ordem de enumeração de dispositivos do Windows.  
 - A sequência de tarefas imediatamente não se aplica as definições que especificar neste passo para o computador. 



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Aplicar imagem do sistema operativo  

 > [!TIP]  
 > A partir do Windows 10, versão 1709, o suporte de dados inclui várias edições. Ao configurar uma sequência de tarefas para utilizar um pacote de atualização de SO ou a imagem do SO, certifique-se de que selecione um [suportado edition](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

 Utilize este passo para instalar um sistema operacional no computador de destino. 

 > [!NOTE]  
 >  O **configuração do Windows e ConfigMgr** passo inicia a instalação do Windows. 

 Depois do **aplicar sistema operativo** execuções de ação, ele define a **OSDTargetSystemDrive** variável para a letra de unidade da partição que contém os ficheiros de sistema operacional.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado no SO completo. 

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDConfigFileName](/sccm/osd/understand/task-sequence-variables#OSDConfigFileName)  
 - [OSDImageIndex](/sccm/osd/understand/task-sequence-variables#OSDImageIndex)  
 - [OSDTargetSystemDrive](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemDrive)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **imagens**e selecione **Apply Operating System Image**. 

 Este passo executa ações consoante se utiliza uma imagem de sistema operacional ou um pacote de atualização de SO.  

#### <a name="os-image-actions"></a>Ações de imagem do SO
 O **Apply Operating System Image** passo executa as ações seguintes quando utilizar uma imagem de SO:  

1. Elimine todo o conteúdo no volume de destino, exceto os ficheiros na pasta especificada pelos  **\_SMSTSUserStatePath** variável.  

2. Extraia os conteúdos do ficheiro. wim especificado para a partição de destino especificado.  

3. Prepare o arquivo de resposta:  

   1.  Crie um novo programa de configuração do Windows resposta ficheiro predefinido (Sysprep. inf ou Unattend. xml) para o sistema operativo implementado.  

   2.  Intercale quaisquer valores do arquivo de resposta fornecido pelo usuário.  

4. Copie carregadores de inicialização do Windows para a partição ativa.  

5. Defina o Boot. ini ou a base de dados de configuração de arranque (BCD) para referenciar o sistema operativo recentemente instalado.  

#### <a name="os-upgrade-package-actions"></a>Ações de pacote de atualização de SO
 O **Apply Operating System Image** passo executa as ações seguintes quando utilizar um pacote de atualização de SO:  

1. Elimine todo o conteúdo no volume de destino, exceto os ficheiros na pasta especificada pelos  **\_SMSTSUserStatePath** variável.  

2. Prepare o arquivo de resposta:  

   1.  Crie um ficheiro de resposta novo com valores padrão criados pelo Configuration Manager.  

   2.  Intercale quaisquer valores do arquivo de resposta fornecido pelo usuário.  


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Aplicar o sistema operativo a partir de uma imagem capturada
 Instala uma imagem de SO que capturou. Clique em **navegue** para abrir o **selecionar um pacote** caixa de diálogo. Em seguida, selecione o pacote de imagem existente que pretende instalar. Se várias imagens estão associadas a especificado **pacote de imagem**, selecione na lista pendente a imagem associada a utilizar para esta implementação. Pode ver informações básicas sobre cada imagem existente clicando na mesma.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Aplicar o sistema operativo a partir de uma origem de instalação original
 Instala um sistema operacional com um pacote de atualização de SO, que também é uma origem de instalação original. Clique em **navegue** para abrir o **Select e o pacote de instalação do sistema operativo** caixa de diálogo. Em seguida, selecione o pacote de atualização SO existente que pretende utilizar. Pode ver informações básicas sobre cada origem de imagem existente clicando na mesma. O painel de resultados na parte inferior da caixa de diálogo apresenta as propriedades da origem de imagem associado. Se existirem várias edições associadas ao pacote especificado, utilize a lista pendente para selecionar o **Edition** que pretende utilizar.  

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Utilize um ficheiro de resposta Sysprep ou autónomo para uma instalação personalizada
 Utilize esta opção para fornecer um ficheiro de resposta de configuração do Windows (**Unattend. XML**, **Unattend. txt**, ou **Sysprep. inf**) dependendo do método de instalação e a versão do SO. O ficheiro que especificar pode incluir qualquer uma das opções de configuração padrão suportadas pelos ficheiros de resposta do Windows. Por exemplo, pode utilizá-lo para especificar a home page predefinida do Internet Explorer. Especifique o pacote que contém o arquivo de resposta e o caminho associado para o ficheiro do pacote.  

 > [!NOTE]  
 >  O Windows pode conter o ficheiro de resposta de configuração que fornecer incorporado variáveis de sequência de tarefas do formulário `%varname%`, onde *varname* é o nome da variável. O **configuração do Windows e ConfigMgr** passo substitui a cadeia de carateres variável para o valor real da variável. Não é possível utilizar estas variáveis de sequência de tarefas incorporadas em campos apenas numéricos num ficheiro de resposta Unattend. XML.  

 Se não fornecer um arquivo de resposta de instalação do Windows, a sequência de tarefas gera automaticamente um arquivo de resposta.  

#### <a name="destination"></a>Destino  
 Configure uma das seguintes opções:  

 - **Partição disponível seguinte**: Utilize a partição sequencial seguinte que ainda não estiver direcionada por uma **aplicar sistema operativo** ou **aplicar imagem de dados** passo nesta sequência de tarefas.  

 - **Partição e disco específico**: Selecione o **disco** número (começando com 0) e o **partição** número (começando com 1).  

 - **Letra de unidade lógica específica**: Especifique a **letra de unidade** atribuída à partição pelo Windows PE. Esta letra de unidade pode ser diferente da letra de unidade atribuída pelo sistema operativo recentemente implementado.  

 - **Letra de unidade lógica armazenada numa variável**: Especifique a variável de sequência de tarefas que contém a letra de unidade atribuída à partição pelo Windows PE. Esta variável normalmente é definida na secção avançada a **propriedades de partição** caixa de diálogo para o **formatar e particionar disco** passo de sequência de tarefas.  


### <a name="options"></a>Opções  

 Além das opções predefinidas, configure as seguintes definições adicionais no **opções** separador deste passo de sequência de tarefas:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Acesso a conteúdo diretamente a partir do ponto de distribuição
 Configure a sequência de tarefas para acessar a imagem do SO diretamente a partir do ponto de distribuição. Por exemplo, utilize esta opção quando implementar sistemas operativos em dispositivos embedded que tenham a limitava a capacidade de armazenamento. Quando selecionar esta opção, também de configurar as definições de partilha de pacote no **acesso a dados** separador de propriedades da imagem de sistema operacional.  

 > [!NOTE]  
 >  Esta definição substitui a opção de implementação que configurou no **pontos de distribuição** página no **Assistente de implementação de Software**. Esta substituição é apenas para a imagem do SO que especifica este passo, não para todos os conteúdos de sequência de tarefas.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar definições do Windows  

 Utilize este passo para configurar as definições do Windows para o computador de destino. A sequência de tarefas armazena estes valores no ficheiro de resposta adequado. Este ficheiro de resposta durante a configuração do Windows utiliza a **configuração do Windows e ConfigMgr** passo.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado no SO completo.  

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-input)  
 - [OSDLocalAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDLocalAdminPassword)  
 - [OSDProductKey](/sccm/osd/understand/task-sequence-variables#OSDProductKey)  
 - [OSDRandomAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDRandomAdminPassword)  
 - [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-input)  
 - [OSDRegisteredUserName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredUserName)  
 - [OSDServerLicenseConnectionLimit](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseConnectionLimit)  
 - [OSDServerLicenseMode](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseMode)  
 - [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-input)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **definições**e selecione **aplicar definições do Windows**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="user-name"></a>Nome de utilizador
 Especifique o nome de utilizador registado para associar o computador de destino. O valor que o **capturar definições do Windows** capturas de passo de sequência de tarefas podem substituir este valor.  

#### <a name="organization-name"></a>Nome da organização
 Especifique o nome da organização registado para associar o computador de destino. O valor que o **capturar definições do Windows** capturas de passo de sequência de tarefas podem substituir este valor.  

#### <a name="product-key"></a>Chave de produto  
 Especifique a chave de produto a utilizar para a instalação do Windows no computador de destino.  

#### <a name="server-licensing"></a>Licenciamento do servidor  
 Especifique o modo de licenciamento do servidor. 
 - Selecione **por servidor** ou **por utilizador** como modo de licenciamento.  
 - Se selecionou **por servidor**, também especificar o número máximo de ligações permitido por contrato de licença.  
 - Se o computador de destino não é um servidor ou não pretender especificar o modo de licenciamento, selecione **não especificar**.   

#### <a name="maximum-connections"></a>Máximo de ligações
 Especifique o número máximo de ligações disponíveis para este computador, conforme indicado no contrato de licença.  

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Gerar aleatoriamente a palavra-passe do administrador local e desativar a conta nas plataformas suportadas (recomendado)  
 Selecione esta opção para definir a palavra-passe de administrador local para uma cadeia de caracteres gerada aleatoriamente. Esta opção também desativa a conta de administrador local nas plataformas que suportam esta capacidade.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Ativar a conta e especificar a palavra-passe do administrador local  
 Selecione esta opção para ativar a conta de administrador local usando a palavra-passe especificada. Introduza a palavra-passe na linha **Palavra-passe** e confirme-a na linha **Confirmar palavra-passe**.  

#### <a name="time-zone"></a>Fuso Horário
 Especifique o fuso horário a configurar no computador de destino. O valor que o **capturar definições do Windows** capturas de passo de sequência de tarefas podem substituir este valor.  



##  <a name="BKMK_AutoApplyDrivers"></a> Aplicar controladores automaticamente  

 Utilize este passo para fazer corresponder e instalar controladores como parte da implementação do sistema operacional.  

 O passo de sequência de tarefas **Aplicar Controladores Automaticamente** executa as seguintes ações:  

 1. Verificar o hardware e encontre os IDs de plug-and-play para todos os dispositivos existentes no sistema.  

 2. Envie a lista de dispositivos e os respetivos IDs de plug-and-play para o ponto de gestão. O ponto de gestão devolve uma lista de controladores compatíveis a partir do catálogo de controladores para cada dispositivo de hardware. A lista inclui ativados todos os controladores independentemente do pacote de controlador estão em e controladores marcados com a categoria de controlador especificado.  

 3. Para cada dispositivo de hardware, a sequência de tarefas escolhe o melhor controlador. Esse driver é adequado para o sistema operativo implementado e é no ponto de distribuição acessível.  

 4. A sequência de tarefas transfere os controladores selecionados a partir de um ponto de distribuição e prepara os controladores no sistema operacional de destino.  

    1. Quando utilizar uma imagem de sistema operacional, a sequência de tarefas coloca os controladores para o arquivo de driver de sistema operacional.  

    2. Quando utiliza um pacote de atualização do sistema operacional como uma origem de instalação original, a sequência de tarefas configura a configuração do Windows com a localização dos controladores.  

 5.  Durante a **configuração do Windows e ConfigMgr** passo na sequência de tarefas, o programa de configuração do Windows encontra os controladores pré-configurados por este passo.  


 > [!IMPORTANT]  
 >  Suporte de dados autónomo não é possível utilizar o **aplicar controladores automaticamente** passo. A sequência de tarefas não tenha nenhuma ligação ao site do Configuration Manager neste cenário.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado no SO completo.

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDAutoApplyDriverBestMatch](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverBestMatch)  
 - [OSDAutoApplyDriverCategoryList](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverCategoryList)  
 - [SMSTSDriverRequestConnectTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestConnectTimeOut)  
 - [SMSTSDriverRequestReceiveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestReceiveTimeOut)  
 - [SMSTSDriverRequestResolveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestResolveTimeOut)  
 - [SMSTSDriverRequestSendTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestSendTimeOut)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **controladores**e selecione **aplicar controladores automaticamente**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Instalar apenas os controladores com melhor compatibilidade
 Especifica que o passo de sequência de tarefas instala apenas os controladores com melhor compatibilidade para cada dispositivo de hardware detetado.  

#### <a name="install-all-compatible-drivers"></a>Instalar todos os controladores compatíveis
 A sequência de tarefas instala todos os controladores compatíveis para cada dispositivo de hardware detetado. Configuração do Windows, em seguida, escolhe o melhor controlador. Esta opção utiliza mais espaço de disco e de largura de banda de rede. A sequência de tarefas transfere mais controladores, mas o Windows podem selecionar um controlador mais adequado.  

#### <a name="consider-drivers-from-all-categories"></a>Considerar controladores de todas as categorias
 A sequência de tarefas procura todas as categorias de controladores disponíveis para os controladores de dispositivo adequados.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Limitar a correspondência de controladores para apenas considerar controladores nas categorias selecionadas
 A sequência de tarefas procura nas categorias de controladores especificados para os controladores de dispositivo adequados.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Efetuar a instalação autónoma de controladores não assinados nas versões do Windows em que tal é permitido
 Esta opção permite que o Windows instalar controladores sem uma assinatura digital.   

 > [!IMPORTANT]  
 >  Esta opção não se aplica a sistemas operativos em que não é possível configurar a política de assinatura de controladores.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Capturar definições de rede  

 Utilize este passo para capturar as definições de rede do Microsoft do computador que executa a sequência de tarefas. A sequência de tarefas salva essas configurações em variáveis de sequência de tarefas. Estas definições substituem as predefinições configuradas no **aplicar definições de rede** passo.  

 Este passo de sequência de tarefas é executado apenas no SO completo. Não é executado no Windows PE.  

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDMigrateAdapterSettings](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdapterSettings)  
 - [OSDMigrateNetworkMembership](/sccm/osd/understand/task-sequence-variables#OSDMigrateNetworkMembership)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **definições**e selecione **capturar definições de rede**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Migrar associações de domínio e de grupo de trabalho 
 Captura as informações de associação de domínios e grupos de trabalho do computador de destino.  

#### <a name="migrate-network-adapter-configuration"></a>Migrar configuração da placa de rede
 Captura a configuração da placa de rede do computador de destino. Captura as seguintes informações: 
 - Definições de rede global  
 - Número de adaptadores  
 - As seguintes definições de rede associadas a cada adaptador: DNS, WINS, IP e filtros de portas



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagem do sistema operativo  

 Este passo captura uma ou mais imagens de um computador de referência. A sequência de tarefas cria um ficheiro de imagem (. wim) do Windows na partilha de rede especificado. Em seguida, utilize o **Adicionar pacote de imagem de sistema operativo** Assistente para importar esta imagem para o Configuration Manager para implementações de sistema operacional baseada em imagem.  

 O Configuration Manager captura cada volume (unidade) do computador de referência para uma imagem separada no ficheiro. wim. Se o computador referenciado tiver vários volumes, o ficheiro. wim resultante contém uma imagem separada para cada volume. Este passo captura apenas volumes formatados como NTFS ou FAT32. Ele ignora os volumes com outros formatos e os USB volumes.  

 O sistema operacional instalado no computador de referência tem de ser uma versão do Windows suportado pelo Configuration Manager. Utilize a ferramenta SysPrep para preparar o sistema operacional no computador de referência. O volume do sistema operacional instalado e o volume de arranque tem de ser o mesmo volume.  

 Especifique uma conta com permissões de escrita para a partilha de rede selecionada. Para obter mais informações sobre a conta de imagem do sistema operacional de captura, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account).

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado no SO completo. 

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDCaptureAccount](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccount)  
 - [OSDCaptureAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccountPassword)  
 - [OSDCaptureDestination](/sccm/osd/understand/task-sequence-variables#OSDCaptureDestination)  
 - [OSDImageCreator](/sccm/osd/understand/task-sequence-variables#OSDImageCreator)  
 - [OSDImageDescription](/sccm/osd/understand/task-sequence-variables#OSDImageDescription)  
 - [OSDImageVersion](/sccm/osd/understand/task-sequence-variables#OSDImageVersion)  
 - [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-input)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **imagens**e selecione **Capture Operating System Image**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="target"></a>Destino  
 Caminho do sistema de ficheiros para a localização que o Configuration Manager utiliza ao armazenar a imagem capturada do sistema operacional.  

#### <a name="description"></a>Descrição  
 Uma utilizador-Descrição opcional definida da imagem capturada do sistema operacional que está armazenada no arquivo de imagem.  

#### <a name="version"></a>Versão  
 Um número de versão opcional definido pelo utilizador para atribuir à imagem capturada do sistema operacional. Este valor pode ser qualquer combinação de letras e números. Ele é armazenado no arquivo de imagem.  

#### <a name="created-by"></a>Criado por  
 O nome opcional do utilizador que criou a imagem do sistema operacional. Ele é armazenado no arquivo de imagem.  

#### <a name="capture-operating-system-image-account"></a>Conta para captura da imagem do sistema operativo  
 Introduza a conta do Windows que tem permissões para a partilha de rede especificada. Clique em **definir** para especificar o nome da conta do Windows.  



##  <a name="BKMK_CaptureUserState"></a> Capturar estado do utilizador  

 Este passo utiliza a ferramenta de migração de estado de utilizador (USMT) para capturar o estado de utilizador e as definições do computador que executa a sequência de tarefas. Este passo de sequência de tarefas é utilizado em conjunto com o passo de sequência de tarefas **Restaurar Estado do Utilizador**. Este passo encripta sempre o armazenamento de Estados do USMT através de uma chave de encriptação que o Configuration Manager gera e gere.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](/sccm/osd/get-started/manage-user-state).  

 Se quiser salvar e restaurar as definições de estado do utilizador a partir de um ponto de migração de estado, utilize este passo com o **Store de estado do pedido** e **Store de estado da versão** passos.  

 Este passo fornece controlo sobre um subconjunto limitado das mais opções utilizadas pelo USMT. Especificar as opções da linha de comandos adicionais com o **OSDMigrateAdditionalCaptureOptions** variável de sequência de tarefas.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado no SO completo.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [_OSDMigrateUsmtPackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtPackageID)  
 - [OSDMigrateAdditionalCaptureOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalCaptureOptions)  
 - [OSDMigrateConfigFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateConfigFiles)  
 - [OSDMigrateContinueOnLockedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnLockedFiles)  
 - [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
 - [OSDMigrateMode](/sccm/osd/understand/task-sequence-variables#OSDMigrateMode)  
 - [OSDMigrateSkipEncryptedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateSkipEncryptedFiles)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **estado do utilizador**e selecione **capturar estado do utilizador**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="user-state-migration-tool-package"></a>Pacote do User State Migration Tool
 Especifique o pacote que contém a ferramenta de migração de estado de utilizador (USMT). A sequência de tarefas utiliza esta versão do USMT para capturar o estado do utilizador e as definições. Este pacote não requer um programa. Especifique um pacote com a versão de 32 bits ou 64 bits do USMT. A arquitetura do USMT depende da arquitetura do sistema operacional de que a sequência de tarefas é capturar o estado.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Capturar todos os perfis de utilizador com opções padrão
 Migre todas as informações de perfil do usuário. Esta opção é a predefinição.  

 Se selecionar esta opção, mas não as selecione **restaurar perfis de utilizador do computador local** no **restaurar estado do utilizador** passo, a sequência de tarefas falha. O Configuration Manager não é possível migrar as novas contas sem lhes atribuir palavras-passe. 

 Quando utiliza a **instalar um pacote de imagem existente** opção da **nova sequência de tarefas** predefinições do assistente, a sequência de tarefas resultante para **capturar todos os perfis de utilizador com opções padrão**. Esta sequência de tarefas padrão, não selecione a opção para **restaurar perfis de utilizador do computador local**, ou contas de utilizador de domínio.  

 Selecione **restaurar perfis de utilizador do computador local** e fornecer uma palavra-passe para a conta a migrar. Numa seqüência de tarefas criada manualmente, esta definição pode é encontrada no **restaurar estado do utilizador** passo. Numa sequência de tarefas criada pelo assistente **Nova Sequência de Tarefas**, esta definição pode ser encontrada na página do assistente no passo **Restaurar Definições e Ficheiros do Utilizador**.  

 Se tiver não existem contas de utilizador local, esta definição não se aplica.  

#### <a name="customize-how-user-profiles-are-captured"></a>Personalizar como os perfis de utilizador são capturados
 Selecione esta opção para especificar um ficheiro de perfil personalizado para a migração. Clique em **Ficheiros** para selecionar os ficheiros de configuração para o USMT utilizar neste passo. Especifique um ficheiro. XML personalizado que contém as regras que definem os ficheiros de estado do utilizador a migrar.  

#### <a name="click-here-to-select-configuration-files"></a>Clique aqui para selecionar ficheiros de configuração
 Selecione esta opção para selecionar os ficheiros de configuração no pacote do USMT que pretende utilizar para capturar os perfis de utilizador. Clique no botão **Ficheiros** para iniciar a caixa de diálogo **Ficheiros de Configuração**. Para especificar um ficheiro de configuração, introduza o nome do ficheiro na linha **Nome do ficheiro** e clique no botão **Adicionar**.  

#### <a name="enable-verbose-logging"></a>Ativar registo verboso
 Ative esta opção para gerar informações de ficheiros de registo mais detalhadas. Ao capturar o estado, a sequência de tarefas por predefinição gera **Scanstate** na pasta de registo da sequência de tarefas, `%WinDir%\ccm\logs`.   

#### <a name="skip-files-using-encrypted-file-system"></a>Ignorar ficheiros que utilizam o sistema de encriptação de ficheiros
 Ative esta opção para ignorar a captura de ficheiros encriptado com o sistema de ficheiros encriptados (EFS). Esses arquivos incluem ficheiros de perfil do utilizador. Consoante as versões de SO e o USMT, ficheiros encriptados podem não ser legíveis após o restauro. Para mais informações, consulte a documentação do USMT.  

#### <a name="copy-by-using-file-system-access"></a>Copiar utilizando o acesso do sistema de ficheiros
 Ative esta opção para especificar qualquer uma das seguintes definições:  

 - **Continuar se não for possível capturar alguns ficheiros**: Ative esta definição continuar o processo de migração mesmo que ele não é possível capturar alguns ficheiros. Se desativar esta opção, e não for possível capturar um ficheiro, este passo falhe. Por predefinição, esta opção encontra-se ativada.  

 - **Capturar localmente ao utilizar ligações em vez de copiar ficheiros**: Ative esta definição para utilizar ligações fixas NTFS para capturar ficheiros.  

     Para obter mais informações sobre como migrar dados com ligações fixas, veja [Store de migração de Link físico](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store).  

 - **Capturar no modo offline (apenas no Windows PE)**: Ative esta definição capturar o estado do utilizador no Windows PE em vez de todo o sistema operacional.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Capturar utilizando o Serviço Sombra de Cópia de Volume (VSS)
 Esta opção permite-lhe capturar ficheiros mesmo que estão bloqueados para edição por outra aplicação.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Capturar definições do Windows  

 Utilize este passo para capturar as definições do Windows do computador que executa a sequência de tarefas. A sequência de tarefas salva essas configurações em variáveis de sequência de tarefas. Estas definições capturadas substituem as predefinições que configura na **aplicar definições do Windows** passo.  

 Este passo de sequência de tarefas é executado no Windows PE ou o SO completo.  

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-output)  
 - [OSDMigrateComputerName](/sccm/osd/understand/task-sequence-variables#OSDMigrateComputerName)  
 - [OSDMigrateRegistrationInfo](/sccm/osd/understand/task-sequence-variables#OSDMigrateRegistrationInfo)  
 - [OSDMigrateTimeZone](/sccm/osd/understand/task-sequence-variables#OSDMigrateTimeZone)  
 - [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-output)  
 - [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-output)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **definições**e selecione **capturar definições do Windows**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="migrate-computer-name"></a>Migrar nome do computador
 Capture o nome do computador NetBIOS do computador.  

#### <a name="migrate-registered-user-and-organization-names"></a>Migrar nomes organizacionais e de utilizador registados
 Capture os nomes de utilizador e da organização registados do computador.  

#### <a name="migrate-time-zone"></a>Migrar fuso horário
 Capture a definição de fuso horário no computador.  



##  <a name="BKMK_CheckReadiness"></a> Verificar estado de preparação  

 Utilize este passo para verificar se o computador de destino cumpre as condições de pré-requisitos de implementação especificado.  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **verificar disponibilidade**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="ensure-minimum-memory-mb"></a>Assegurar memória mínima (MB)
 Certifique-se de que a quantidade de memória, em megabytes (MB), cumpre ou excede o valor especificado. O passo ativa esta definição, por predefinição.  

#### <a name="ensure-minimum-processor-speed-mhz"></a>Assegurar velocidade mínima do processador (MHz)  
 Certifique-se de que a velocidade do processador, em megahertz (MHz), cumpre ou excede o valor especificado. O passo ativa esta definição, por predefinição.  

#### <a name="ensure-minimum-free-disk-space-mb"></a>Assegurar espaço mínimo livre em disco (MB)
 Certifique-se de que a quantidade de espaço livre em disco, em megabytes (MB), cumpre ou excede o valor especificado.  

#### <a name="ensure-current-os-to-be-refreshed-is"></a>Assegurar atualização do SO atual
 Certifique-se de que o sistema operacional instalado no computador de destino cumpre o requisito especificado. O passo define esta definição para **cliente** por predefinição.  


### <a name="options"></a>Opções

 > [!NOTE]  
 > Se ativar a **continuar com o erro** definir o **opções** separador deste passo, regista apenas os resultados da verificação de preparação. Se uma verificação falhar, não para a sequência de tarefas.  



##  <a name="BKMK_ConnectToNetworkFolder"></a> Ligar à pasta de rede  

 Utilize este passo para criar uma ligação para uma pasta de rede partilhada.  

 Este passo de sequência de tarefas é executado no SO completo ou no Windows PE.  

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [SMSConnectNetworkFolderAccount](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderAccount)  
 - [SMSConnectNetworkFolderDriveLetter](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderDriveLetter)  
 - [SMSConnectNetworkFolderPassword](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPassword)  
 - [SMSConnectNetworkFolderPath](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPath)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **Connect To Network Folder**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="path"></a>Caminho  
 Clique em **procurar** para especificar o caminho da pasta de rede. Utilize o formato `\\server\share`.

#### <a name="drive"></a>Unidade  
 Selecione a letra de unidade local para atribuir para esta ligação. 

#### <a name="account"></a>Conta 
 Clique em **definir** para especificar a conta de utilizador com permissões para ligar a esta pasta de rede. Para obter mais informações sobre a conta de ligação de pasta de rede de sequência de tarefas, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account).



##  <a name="BKMK_DisableBitLocker"></a> Desativar BitLocker  

 Utilize este passo para desativar a encriptação BitLocker na unidade do sistema operacional atual ou numa unidade específica. Esta ação deixa os protetores de chave visíveis em texto não criptografado no disco rígido. Ele não desencripta o conteúdo da unidade. Esta ação é concluída quase instantaneamente.  

 > [!NOTE]  
 >  A encriptação de unidade BitLocker fornece encriptação de baixo nível do conteúdo de um volume do disco.  

 Se tiver várias unidades encriptadas, desative o BitLocker em quaisquer unidades de dados antes de desativar o BitLocker na unidade do sistema operacional.  

 Este passo é executado apenas em todo o sistema operacional. Não é executado no Windows PE.  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **discos**e selecione **desativar BitLocker**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="current-operating-system-drive"></a>Unidade do sistema operativo atual
 Desativa o BitLocker na unidade do sistema operacional atual.  

#### <a name="specific-drive"></a>Unidade específica  
 Desativa o BitLocker numa unidade específica. Utilize a lista pendente para especificar a unidade na qual o BitLocker está desativado.  



##  <a name="BKMK_DownloadPackageContent"></a> Transferir conteúdo do pacote  

 Utilize este passo para transferir qualquer um dos seguintes tipos de pacotes:  

 - Imagens do sistema operacional  
 - Pacotes de atualização do SO  
 - Pacotes de controladores  
 - Pacotes  
 - Imagens de arranque  


 Este passo funciona bem numa sequência de tarefas para atualizar um sistema operacional nos seguintes cenários:  

 - Para utilizar uma única sequência de tarefas de atualização que funciona com plataformas x86 e x64. Inclua dois **transferir conteúdo do pacote** etapas na **preparar para a atualização** grupo. Especificar condições no **opções** separador para detetar a arquitetura do cliente e transferir apenas o sistema operacional atualização pacote adequado. Configure cada **transferir conteúdo do pacote** passo para utilizar a mesma variável. Utilize a variável para o caminho de suporte de dados no **atualizar sistema operativo** passo.  

 - Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada **transferir conteúdo do pacote** passo para utilizar a mesma variável. Utilize a variável para o **conteúdo de teste** valor na secção controladores a **atualizar sistema operativo** passo.  


 > [!NOTE]    
 > Quando implementa uma sequência de tarefas que contém este passo, não selecione **transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas** ou **aceder ao conteúdo diretamente a partir de um ponto de distribuição** para **Opções de implementação** sobre os **pontos de distribuição** página do Assistente de implementação de Software.  

 Este passo é executado no SO completo ou o Windows PE. A opção de guardar o pacote na cache do cliente do Configuration Manager não é suportada no Windows PE.

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **Software**e selecione **transferir conteúdo do pacote**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="select-package"></a>Selecionar pacote  
 Clique no ícone para selecionar o pacote a transferir. Depois de selecionar um pacote, clique no ícone novamente para escolher outro.  

#### <a name="place-into-the-following-location"></a>Coloque na seguinte localização
 Opte por guardar o pacote das seguintes localizações:  

 - **Diretório de trabalho de sequência de tarefas**: Esta localização é também referida como o cache da sequência de tarefas.  

 - **Cache do cliente do Configuration Manager**: Utilize esta opção para armazenar o conteúdo na cache do cliente. Por predefinição, este caminho é `%WinDir%\ccmcache`.  

 - **Caminho personalizado**: O motor de sequência de tarefas transfere primeiro o pacote para a diretório de trabalho de sequência de tarefas. Em seguida, move o conteúdo para este caminho especificado. O motor de sequência de tarefas acrescenta o caminho com o ID do pacote.  

#### <a name="save-path-as-a-variable"></a>Guardar o caminho como uma variável
 Guarde o caminho do pacote numa variável de sequência de tarefas personalizado. Em seguida, utilize esta variável em outro passo de sequência de tarefas. 

 Gestor de configuração adiciona um sufixo numérico ao nome da variável. Por exemplo, tem de especificar uma variável de `%MyContent%` como uma variável personalizada. É a raiz em que a sequência de tarefas armazena todos os conteúdos referenciados para este passo. Este conteúdo pode conter vários pacotes. Quando consultar a variável, adicione um sufixo numérico. Para o primeiro pacote, consulte `%MyContent01%`. Quando consultar a variável nos passos subsequentes, tal como **atualizar sistema operativo**, utilize `%MyContent02%` ou `%MyContent03%`, onde o número corresponde à ordem que o **transferir conteúdo do pacote**passo lista os pacotes.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Se a transferência de um pacote falhar, continue a transferir os outros pacotes da lista
 Se a sequência de tarefas não conseguir baixar um pacote, ele começa a transferir o pacote seguinte na lista.  



##  <a name="BKMK_EnableBitLocker"></a> Ativar o BitLocker  

 Utilize este passo para ativar a encriptação BitLocker em, pelo menos, duas partições no disco rígido. A primeira partição ativa contém o código de arranque do sistema do Windows. Outra partição contém o sistema operacional. A partição de arranque do sistema tem de permanecer desencriptada.  

 Utilize o **provisão prévia do BitLocker** passo para ativar o BitLocker numa unidade no Windows PE. Para mais informações, consulte [Pre-provision BitLocker](#BKMK_PreProvisionBitLocker).  

 > [!NOTE]  
 >  A encriptação de unidade BitLocker fornece encriptação de baixo nível do conteúdo de um volume do disco.  

 Este passo é executado apenas em todo o sistema operacional. Não é executado no Windows PE.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDBitLockerRecoveryPassword](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRecoveryPassword)  
 - [OSDBitLockerStartupKey](/sccm/osd/understand/task-sequence-variables#OSDBitLockerStartupKey)  


 Quando especificar **apenas TPM**, **TPM e chave de arranque em USB**, ou **TPM e PIN**, o Trusted Platform Module (TPM) tem de ser no seguinte estado antes de poder executar o  **Ativar o BitLocker** passo:  
 - Ativado  
 - Ativado  
 - Propriedade Permitida  


 Este passo conclui qualquer inicialização de TPM restante. Os passos restantes não requerem presença física ou reinícios. O **Enable BitLocker** passo conclui forma transparente os seguintes passos TPM restantes inicialização, se necessário:  
 - Criar par de chaves de endossamento  
 - Criar valor de autorização do proprietário e efetuar caução para o Active Directory, expandido para suportar este valor  
 - Obter propriedade  
 - Criar SRK (Storage Root Key) ou repor se já existir mas for incompatível  

   
 Se pretender que a sequência de tarefas para aguardar a **ativar BitLocker** passo para concluir o processo de encriptação de unidade, em seguida, selecione a **aguardar** opção. Se não selecionar a **aguarde** opção, o processo de criptografia de unidade acontece em segundo plano. A sequência de tarefas continua imediatamente para o passo seguinte.  

 O BitLocker pode ser utilizado para encriptar várias unidades num sistema informático, unidades de SO e dados. Para encriptar uma unidade de dados, encriptar a unidade do sistema operacional e concluir o processo de encriptação. Este requisito é porque a unidade do SO armazena os protetores de chave para as unidades de dados. Se criptografar o sistema operacional e unidades de dados na mesma sequência de tarefas, selecione o **aguardar** opção a **ativar BitLocker** passo para a unidade do sistema operacional.  

 Se o disco rígido já estiver encriptado, mas o BitLocker estiver desativado, o **Enable BitLocker** passo reativa os protetores de chave e é concluído rapidamente. A reencriptação do disco rígido não é necessária neste caso.  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **discos**e selecione **ativar BitLocker**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="choose-the-drive-to-encrypt"></a>Selecione a unidade a encriptar
 Especifica a unidade a encriptar. Para encriptar a unidade do sistema operacional atual, selecione **unidade do sistema operativo atual**. Em seguida, configure uma das seguintes opções para gestão de chaves:  

 - **Apenas TPM**: Selecione esta opção para utilizar apenas Trusted Platform Module (TPM).  

 - **Chave de arranque em USB apenas**: Selecione esta opção para utilizar uma chave de arranque armazenada numa pen USB. Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até um dispositivo USB com uma chave de arranque BitLocker ser ligado ao computador.  

 - **TPM e chave de arranque em USB**: Selecione esta opção para utilizar o TPM e uma chave de arranque armazenada numa pen USB. Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até um dispositivo USB com uma chave de arranque BitLocker ser ligado ao computador.  

 - **TPM e PIN**: Selecione esta opção para utilizar o TPM e um número de identificação pessoal (PIN). Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até o utilizador fornecer o PIN.  


 Para encriptar uma unidade de dados específica, não-OS, selecione **unidade específica**. Em seguida, selecione a unidade da lista.  

#### <a name="use-full-disk-encryption"></a>Utilize a encriptação de disco completa
 <!--SCCMDocs-pr issue 2671--> Por predefinição, este passo só criptografa espaço utilizado na unidade. Este comportamento predefinido é recomendado, pois é mais rápido e eficiente. Em seguida, a partir da versão 1806, se sua organização, é necessário criptografar a unidade completa durante a configuração, ative esta opção. Configuração do Windows aguarda que a unidade completa encriptar, que demora muito tempo, especialmente em unidades de grandes dimensões. 

#### <a name="choose-where-to-create-the-recovery-key"></a>Escolha onde pretende criar a chave de recuperação
 Para especificar para o BitLocker criar a palavra-passe de recuperação e caução-lo no Active Directory, selecione **no Active Directory**. Esta opção requer que expande o Active Directory para caução de chaves do BitLocker. O BitLocker, em seguida, pode guardar as informações de recuperação associados no Active Directory. Selecione **não criar chave de recuperação** por não criar uma palavra-passe. A criação de uma palavra-passe é a opção recomendada.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Aguardar que o BitLocker conclua o processo de encriptação da unidade em todas as unidades antes de continuar a execução da sequência de tarefas
 Selecione esta opção para permitir que a criptografia de unidade de disco BitLocker concluir antes de executar o passo seguinte na sequência de tarefas. Se selecionar esta opção, o BitLocker criptografa o volume de disco inteiro antes do utilizador é capaz de iniciar sessão no computador.  

 O processo de encriptação pode demorar horas a concluir quando encriptar um disco rígido grande. Não selecionar esta opção permite que a sequência de tarefas prosseguir imediatamente.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Formatar e particionar disco  

 Utilize este passo para formatar e particionar um disco especificado no computador de destino.  

 > [!IMPORTANT]  
 >  Cada definição que especificar para este passo aplica-se para um único disco especificado. Para formatar e particionar outro disco no computador de destino, adicione mais **formatar e particionar disco** passo à sequência de tarefas.  

 Este passo é executado apenas no Windows PE. Não é executado no SO completo.  

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDDiskIndex](/sccm/osd/understand/task-sequence-variables#OSDDiskIndex)  
 - [OSDGPTBootDisk](/sccm/osd/understand/task-sequence-variables#OSDGPTBootDisk)  
 - [OSDPartitions](/sccm/osd/understand/task-sequence-variables#OSDPartitions)  
 - [OSDPartitionStyle](/sccm/osd/understand/task-sequence-variables#OSDPartitionStyle)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **discos**e selecione **formatar e particionar disco**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="disk-number"></a>Número do Disco
 O número de disco físico do disco para formatar. O número é baseado na ordem de enumeração de discos do Windows.  

#### <a name="disk-type"></a>Tipo de Disco
 O tipo de disco para formatar. Existem duas opções disponíveis para seleção na lista pendente: 
 - **Padrão (MBR)**: Registo de arranque principal  
 - **GPT**: Tabela de partições GUID  


 > [!NOTE]  
 >  Se alterar o tipo de disco de **padrão (MBR)** ao **GPT**e o esquema de partição tiver uma partição expandida, a sequência de tarefas remove todas as partições expandidas e lógicas do esquema. O editor de sequência de tarefas pede-lhe para confirmar esta ação antes de alterar o tipo de disco.  
   
#### <a name="volume"></a>Volume
 Obter informações específicas sobre a partição ou volume que cria a sequência de tarefas, incluindo os seguintes atributos:  
 - Nome  
 - Espaço em disco restante  


 Para criar uma nova partição, clique em **Novo** para iniciar a caixa de diálogo **Propriedades de Partição**. Especificar o tipo de partição e o tamanho, e se é uma partição de arranque. Para modificar uma partição existente, clique na partição que pretende modificar e, em seguida, clique nas **propriedades** botão. Para obter mais informações sobre como configurar partições de disco rígido, consulte um dos seguintes artigos:  

 - [Partições de disco rígido baseadas em UEFI/GPT](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
 - [Partições de disco rígido baseado em BIOS/MBR](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  


 Para eliminar uma partição, selecione a partição e, em seguida, clique em **eliminar**.  



##  <a name="BKMK_InstallApplication"></a> Instalar aplicação  

 Este passo instala os aplicativos especificados, ou um conjunto de aplicativos definidos por uma lista dinâmica de variáveis de sequência de tarefas. Quando a sequência de tarefas é executada neste passo, a instalação da aplicação começa de imediato, sem esperar por um intervalo de consulta de política.  

 As aplicações têm de cumprir os seguintes critérios:  

 - O aplicativo deve ter um tipo de implementação do **Windows Installer** ou **Script** instalador. Tipos de implementação do Windows app pacote (ficheiro. AppX) não são suportados.  

 - Tem de ser executada sob a conta Sistema Local e não a conta de utilizador.  

 - Não pode interagir com o ambiente de trabalho. O programa tem de ser executado no modo silencioso ou no modo automático.  

 - Não pode iniciar um reinício por si só. A aplicação tem de solicitar um reinício utilizando o padrão de reinício de código, 3010. Este comportamento certifica-se de que este passo manipula corretamente o reinício. Se a aplicação devolver um código de 3010 saída, o motor de sequência de tarefas reinicia o computador. Após o reinício, a sequência de tarefas continua automaticamente.  


 Quando este passo é executado, a aplicação verifica a aplicabilidade das regras de requisitos e método de deteção nos respetivos tipos de implementação. Com base nos resultados desta verificação, a aplicação instala o tipo de implementação aplicável. Se um tipo de implementação contiver dependências, o tipo de implementação dependente é avaliado e instalado como parte deste passo. Dependências de aplicações não são suportadas para suportes de dados autónomos.  

 > [!NOTE]  
 >  Para instalar uma aplicação que substitui outra aplicação, os ficheiros de conteúdo para a aplicação substituída devem estar disponíveis. Caso contrário, este passo de sequência de tarefas falhará. Por exemplo, o Microsoft Visio 2010 é instalado num cliente ou numa imagem capturada. Quando o **instalar aplicação** passo instala o Microsoft Visio 2013, os ficheiros de conteúdo para o Microsoft Visio 2010 (a aplicação substituída) tem de estar disponíveis num ponto de distribuição. Se o Microsoft Visio não está instalado em todos os num cliente ou capturado imagem, a sequência de tarefas instala o Microsoft Visio 2013 sem verificar pelos ficheiros de conteúdo do Microsoft Visio 2010.  

 > [!NOTE]  
 > Se o cliente não conseguir obter a lista de pontos de gestão dos serviços de localização, utilize o **SMSTSMPListRequestTimeoutEnabled** e **SMSTSMPListRequestTimeout** variáveis de sequência de tarefas. Estas variáveis especificam quantos milissegundos uma sequência de tarefas aguarda antes de tentar novamente a instalação de um aplicativo. Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables).

 Este passo de sequência de tarefas é executado apenas no SO completo. Não é executado no Windows PE.  

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [Tsappinstallstatus](/sccm/osd/understand/task-sequence-variables#TSAppInstallStatus)  
 - [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
 - [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
 - [Tserroronwarning como](/sccm/osd/understand/task-sequence-variables#TSErrorOnWarning)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **Software**e selecione **instalar aplicação**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="install-the-following-applications"></a>Instale as seguintes aplicações
 A sequência de tarefas instala esses aplicativos na ordem especificada.  

 Do Configuration Manager filtra quaisquer aplicações desativadas, ou todas as aplicações com as seguintes definições:  

 - Apenas quando um utilizador tiver sessão iniciada  
 - Executar com direitos de utilizador  


 Esses aplicativos não aparecem no **selecione a aplicação a instalar** caixa de diálogo.

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Instalar aplicações de acordo com a lista de variáveis dinâmicas
 A sequência de tarefas instala aplicações com este nome de variável base. O nome da variável base destina-se um conjunto de variáveis de sequência de tarefas definidas para uma coleção ou computador. Estas variáveis especificam as aplicações que a sequência de tarefas instala para essa coleção ou computador. Cada nome de variável é constituído pelo nome base comum e um sufixo numérico a partir de 01. O valor de cada variável tem de conter o nome da aplicação e mais nada.  

 Para a sequência de tarefas instalar aplicações, utilizando uma lista de variáveis dinâmicas, ativar a definição seguinte no **gerais** separador do aplicativo **propriedades**: **Permitir que esta aplicação ser instalada a partir da ação de sequência de tarefas instalar aplicação, sem ser implementada**.  

 > [!NOTE]  
 >  Não é possível instalar aplicativos usando uma lista de variáveis dinâmicas para implementações de suportes de dados autónomos.  

 Por exemplo, para instalar um único aplicativo, utilizando uma variável de sequência de tarefas denominada AA01, especifica a seguinte variável:  

 |Nome da Variável|Valor da Variável|  
 |-------------------|--------------------|  
 |AA01|Microsoft Office|  

 Para instalar duas aplicações, especifique as seguintes variáveis:  

 |Nome da Variável|Valor da Variável|  
 |-------------------|--------------------|  
 |AA01|Microsoft Lync|  
 |AA02|Microsoft Office|  

 As seguintes condições afetam as aplicações instaladas pela sequência de tarefas:  

 - O valor de uma variável contém quaisquer informações além do nome da aplicação. A sequência de tarefas não instala a aplicação e a sequência de tarefas continua.  

 - Se a sequência de tarefas não encontrar uma variável com o nome base especificado nem o sufixo "01", a sequência de tarefas não instala quaisquer aplicações.  


 > [!Important]  
 > Estes valores diferenciam maiúsculas de minúsculas. Por exemplo, "instalar" é diferente de "Instalar". Se precisar de alterar o valor, o editor de sequência de tarefas não Deteta uma alteração de caso. Efectuar outra editar ao mesmo tempo, por exemplo, modifique a descrição do passo.<!--509714-->   

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Se a instalação de uma aplicação falhar, continue a instalar outras aplicações na lista
 Esta definição especifica que o passo continuará quando a instalação de uma aplicação individual falhar. Se especificar esta definição, a sequência de tarefas continuará independentemente de quaisquer erros de instalação. Se não especificar esta definição e a instalação falhar, o passo termina imediatamente.  


### <a name="options"></a>Opções

 > [!NOTE]  
 > Quando seleciona **continuar com o erro** sobre o **opções** separador deste passo, a sequência de tarefas continua quando uma aplicação não consegue instalar. Quando não ativa esta opção, a sequência de tarefas falha e não instala restantes aplicações.  

 Além das opções predefinidas, configure as seguintes definições adicionais no **opções** separador deste passo de sequência de tarefas:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Repita este passo se o computador reiniciar inesperadamente
 Se uma das instalações desses aplicativos inesperadamente, reinicia o computador, repita este passo. O passo ativa esta definição por predefinição com duas tentativas. Pode especificar entre uma a cinco tentativas.  



##  <a name="BKMK_InstallPackage"></a> Instalar pacote

 Utilize este passo para instalar um pacote de software como parte da sequência de tarefas. Quando este passo é executado, a instalação começa de imediato, sem esperar por um intervalo de consulta de política.  

 O pacote tem de cumprir os seguintes critérios:  

 - Tem de ser executada sob a conta Sistema Local e não uma conta de utilizador.  

 - Ele não deve interagir com a área de trabalho. O programa tem de ser executado no modo silencioso ou no modo automático.  

 - Não pode iniciar um reinício por si só. O software tem de solicitar um reinício utilizando o padrão de reinício de código, 3010. Este comportamento certifica-se de que a sequência de tarefas processa corretamente o reinício. Se o software devolver um código de saída 3010, o motor de sequência de tarefas reinicia o computador. Após o reinício, a sequência de tarefas continua automaticamente.  


 Programas que utilizam o **executar outro programa primeiro** opção para instalar um programa dependente não são suportados quando implementar um sistema operacional. Se ativar a opção de pacote **executar outro programa primeiro**e o programa dependente já tiver executado no computador de destino, o programa dependente é executado e a sequência de tarefas continua. No entanto, se o programa dependente já não tiver sido executada no computador de destino, o passo de sequência de tarefas falhará.  

 > [!NOTE]  
 >  O site de administração central não tem as políticas de configuração de cliente necessárias para ativar o agente de distribuição de software durante a sequência de tarefas. Quando cria um suporte de dados autónomo para uma sequência de tarefas do site de administração central e a sequência de tarefas inclui um passo **Instalar Pacote**, pode aparecer o erro seguinte no ficheiro CreateTsMedia.log:  
 >   
 >  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
 >   
 >  Para suporte de dados autónomo, que inclui um **Instalar pacote** passo, criar suportes de dados autónomo num site primário que tenha o agente de distribuição de software ativado. Em alternativa, adicione uma **executar linha de comandos** passo após a **configuração do Windows e ConfigMgr** passo e antes do primeiro **Instalar pacote** passo. O **executar linha de comandos** passo é executado um comando WMIC para ativar o agente de distribuição de software antes do primeiro **Instalar pacote** passo. Utilize o seguinte comando no **executar linha de comandos** passo:  
 >   
 >  `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
 >   
 >  Para obter mais informações sobre como criar suportes de dados autónomos, consulte [criar suporte de dados autónomo](/sccm/osd/deploy-use/create-stand-alone-media).  


 Este passo de sequência de tarefas é executado apenas no SO completo. Não é executado no Windows PE.  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **Software**e selecione **Instalar pacote**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="install-a-single-software-package"></a>Instalar um pacote de software único
 Esta definição especifica um pacote de software do Configuration Manager. O passo aguardará até a conclusão da instalação.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Instalar os pacotes de software de acordo com a lista de variáveis dinâmicas
 A sequência de tarefas instala os pacotes com esse nome de variável base. O nome da variável base destina-se um conjunto de variáveis de sequência de tarefas definidas para uma coleção ou computador. Estas variáveis especificam os pacotes que a sequência de tarefas instala para essa coleção ou computador. Cada nome de variável é constituído pelo nome base comum e um sufixo numérico a partir de 001. O valor de cada variável tem de conter um ID de pacote e o nome do software separados por dois pontos.  

 Para a sequência de tarefas instalar software utilizando uma lista de variáveis dinâmicas, ativar a definição seguinte no **avançadas** Guia do pacote **propriedades**: **Permitir que este programa ser instalada a partir da sequência de tarefas Instalar pacote sem o implementar**.  

 > [!NOTE]  
 >  Não é possível instalar pacotes de software utilizando uma lista de variáveis dinâmicas para implementações de suportes de dados autónomos.  

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

 - Se não criar o valor de uma variável no formato correto ou não especifica um ID de pacote válido e um nome, a instalação de software falha.  

 - Se o ID do pacote incluir carateres minúsculos, a instalação de software falha.  

 - Se a sequência de tarefas não encontrar uma variável com o nome base especificado nem o sufixo "001", a sequência de tarefas não instala quaisquer pacotes. A sequência de tarefas continua.  


 > [!Important]  
 > Estes valores diferenciam maiúsculas de minúsculas. Por exemplo, "instalar" é diferente de "Instalar". Se precisar de alterar o valor, o editor de sequência de tarefas não Deteta uma alteração de caso. Efectuar outra editar ao mesmo tempo, por exemplo, modifique a descrição do passo.<!--509714-->   

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Se a instalação de um pacote de software falhar, continuar a instalar outros pacotes na lista
 Esta definição especifica que o passo continuará se a instalação de um pacote de software individual falhar. Se especificar esta definição, a sequência de tarefas continuará independentemente de quaisquer erros de instalação. Se não especificar esta definição e a instalação falhar, o passo termina imediatamente.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar atualizações de Software  

 Utilize este passo para instalar atualizações de software no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que este passo de sequência de tarefas é executado. Nessa altura, o computador de destino é avaliado para atualizações de software, como qualquer outro cliente do Configuration Manager. Para este passo instalar atualizações de software, implemente as atualizações para uma coleção do qual o computador de destino é um membro.  

 > [!IMPORTANT]  
 > Para obter melhor desempenho, instale a versão mais recente do Windows Update Agent.  

 Este passo de sequência de tarefas é executado apenas no SO completo. Não é executado no Windows PE. 

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget)  
 - [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
 - [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
 - [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)  
 - [SMSTSWaitForSecondReboot](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot)  


 > [!NOTE]  
 > Se o cliente não conseguir obter a lista de pontos de gestão dos serviços de localização, utilize o **SMSTSMPListRequestTimeoutEnabled** e **SMSTSMPListRequestTimeout** variáveis. Estas variáveis especificam quantos milissegundos uma sequência de tarefas aguarda antes de tentar novamente instalar uma aplicação ou software da atualização. Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables).  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **Software**e selecione **instalar atualizações de Software**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Necessário para instalação - apenas atualizações de software obrigatórias
 Selecione esta opção para instalar todas as atualizações de software obrigatórias com prazos de instalação definidos pelo administrador.  

#### <a name="available-for-installation---all-software-updates"></a>Disponível para instalação - todas as atualizações de software
 Selecione esta opção para instalar todas as atualizações de software disponíveis. Implemente primeiro estas atualizações numa coleção de que o computador é membro. A sequência de tarefas instala todas as atualizações de software disponível dos computadores de destino.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Avaliar atualizações de software a partir de resultados de análise em cache
 Por predefinição, este passo utiliza os resultados da análise em cache do agente de atualização do Windows. Desative esta opção para instruir o agente do Windows Update para transferir o catálogo mais recente a partir do ponto de atualização de software. Ative esta opção quando utilizar uma sequência de tarefas [capturar e compilar uma imagem de SO](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system). Provavelmente um grande número de atualizações de software neste cenário. 

 Muitas destas atualizações têm dependências. Por exemplo, instalar a atualização ABC antes da atualização XYZ aparece conforme aplicável. Quando Desative esta definição e implementa a sequência de tarefas para vários clientes, todos eles ligam para o ponto de atualização de software ao mesmo tempo. Este comportamento resulta em problemas de desempenho durante o processo e a transferência do catálogo de atualização. 

 Na maioria das circunstâncias, utilize a predefinição para utilizar os resultados da análise em cache. 

 O **SMSTSSoftwareUpdateScanTimeout** variável controla o tempo de limite de análise de atualizações de software durante este passo. O valor predefinido é 30 minutos. Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout).


### <a name="options"></a>Opções   

 Além das opções predefinidas, configure as seguintes definições adicionais no **opções** separador deste passo de sequência de tarefas:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Repita este passo se o computador reiniciar inesperadamente
 Se uma das atualizações inesperadamente, reinicia o computador, repita este passo. O passo ativa esta definição por predefinição com duas tentativas. Pode especificar entre uma a cinco tentativas.  

 > [!NOTE]  
 > Configurar o **SMSTSWaitForSecondReboot** variável para especificar quantos segundos a sequência de tarefas coloca em pausa após o computador ser reiniciado neste cenário. Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot).  



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Associar domínio ou grupo de trabalho  

 Utilize este passo para adicionar o computador de destino a um grupo de trabalho ou domínio.  

 Este passo de sequência de tarefas é executado apenas no SO completo. Não é executado no Windows PE.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
 - [OSDJoinDomainName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainName)  
 - [OSDJoinDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainOUName)  
 - [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
 - [OSDJoinSkipReboot](/sccm/osd/understand/task-sequence-variables#OSDJoinSkipReboot)  
 - [OSDJoinType](/sccm/osd/understand/task-sequence-variables#OSDJoinType)  
 - [OSDJoinWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDJoinWorkgroupName)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **associar domínio ou grupo de trabalho**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="join-a-workgroup"></a>Aderir a um grupo de trabalho
 Selecione esta opção para associar o computador de destino ao grupo de trabalho especificado. Se o computador for atualmente membro de um domínio, a seleção desta opção faz com que o reinício do computador.  

#### <a name="join-a-domain"></a>Aderir a um domínio
 Selecione esta opção para associar o computador de destino ao domínio especificado.  

 Opcionalmente, introduza ou procure uma unidade organizacional (UO) no domínio especificado para o computador ser associado. Se o computador for atualmente membro de outro domínio ou um grupo de trabalho, esta opção faz com que o reinício do computador. Se o computador já for membro de outra UO, uma vez que os serviços de domínio do Active Directory não permite alterar a UO através deste método, o Windows configuração ignora esta definição.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Introduzir a conta com permissões para ser associada ao domínio
 Clique em **definir** para introduzir o nome de utilizador e palavra-passe para uma conta com permissões para aderir ao domínio. Introduza a conta no formato: `Domain\account`. Para obter mais informações sobre o domínio de sequência de tarefas associar a conta, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account).  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Preparar ConfigMgr Client para captura  

 Utilize este passo para remover ou configurar o cliente do Configuration Manager no computador de referência. Esta ação prepara o computador para captura como parte do processo de geração de imagens.

 Este passo remove completamente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas implementa a imagem capturada do sistema operacional, ele instala um novo cliente de Configuration Manager cada vez.  

 > [!Note]  
 >  O motor de sequência de tarefas apenas remove o cliente durante a **compilar e capturar uma imagem de sistema operativo de referência** sequência de tarefas. O motor de sequência de tarefas não remove o cliente durante a outros métodos de captura, como suporte de dados de captura ou de uma sequência de tarefas personalizado.  

 Este passo de sequência de tarefas é executado apenas no SO completo. Não é executado no Windows PE.  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **imagens**e selecione **preparar ConfigMgr Client para captura**. 


### <a name="properties"></a>Propriedades  

 Este passo não requer quaisquer definições sobre o **propriedades** separador.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Preparar Windows para captura  

 Utilize este passo para especificar as opções de Sysprep ao capturar uma imagem de sistema operacional no computador de referência. Este passo executa o Sysprep e, em seguida, reinicia o computador para a imagem de arranque do Windows PE especificada para a sequência de tarefas. Esta ação falha se o computador de referência está associado a um domínio.  

 Este passo é executado apenas em todo o sistema operacional. Não é executado no Windows PE.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDKeepActivation](/sccm/osd/understand/task-sequence-variables#OSDKeepActivation)  
 - [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-output)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **imagens**e selecione **preparar Windows para captura**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Compilar automaticamente a lista de controladores de armazenamento de massa
 Selecione esta opção para o Sysprep compilar automaticamente uma lista de controladores de armazenamento em massa a partir do computador de referência. Esta opção ativa a opção Compilar Controladores de Armazenamento em Massa no ficheiro sysprep.inf no computador de referência. Para obter mais informações sobre esta definição, consulte a documentação do Sysprep.  

#### <a name="do-not-reset-activation-flag"></a>Não repor o sinalizador de ativação
 Selecione esta opção para impedir o Sysprep de repor o sinalizador de ativação do produto.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>O computador depois de executar esta ação de encerramento
 <!--SCCMDocs-pr issue 2695--> A partir da versão 1806, esta opção dá instruções ao Sysprep para encerrar o computador em vez de seu comportamento de reinício padrão. 



##  <a name="BKMK_PreProvisionBitLocker"></a> Provisão prévia do BitLocker  

 Utilize este passo para ativar o BitLocker numa unidade no Windows PE. Por predefinição, apenas o espaço em disco utilizado é encriptado, pelo que os tempos de encriptação são muito mais rápidos. Aplique as opções de gestão de chaves utilizando o [Enable BitLocker](#BKMK_EnableBitLocker) passo após a instalação de sistema operacional. 

 Este passo é executado apenas no Windows PE. Não é executado no SO completo.  

 > [!IMPORTANT]  
 >  Pré-provisionamento do BitLocker requer, pelo menos, Windows 7. O computador também tem de conter um suportado e ativado Trusted Platform Module (TPM).  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **discos**e selecione **provisão prévia do BitLocker**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>Aplicar BitLocker à unidade especificada
 Especifique a unidade para a qual pretende ativar o BitLocker. O BitLocker encripta apenas o espaço utilizado na unidade.  

#### <a name="use-full-disk-encryption"></a>Utilize a encriptação de disco completa
 <!--SCCMDocs-pr issue 2671--> Por predefinição, este passo só criptografa espaço utilizado na unidade. Este comportamento predefinido é recomendado, pois é mais rápido e eficiente. Em seguida, a partir da versão 1806, se sua organização, é necessário criptografar a unidade completa durante a configuração, ative esta opção. Configuração do Windows aguarda que a unidade completa encriptar, que demora muito tempo, especialmente em unidades de grandes dimensões. 

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Ignorar este passo em computadores que não têm TPM ou quando o TPM não está ativado
 Selecione esta opção para ignorar a criptografia de unidade num computador que não contém um TPM suportado ou ativado. Por exemplo, utilize esta opção quando implementar um sistema operacional a uma máquina virtual.  



##  <a name="BKMK_ReleaseStateStore"></a> Store de estado da versão  

 Utilize este passo para notificar o estado do ponto de migração de que a ação de captura ou restauro está concluída. Utilize este passo em conjunto com o **Store de estado do pedido**, **capturar estado do utilizador**, e **restaurar estado do utilizador** passos. Utilize estes passos para migrar dados de perfil do usuário com um ponto de migração de estado e a ferramenta de migração de estado de utilizador (USMT).  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](/sccm/osd/get-started/manage-user-state).  

 Se utilizar o **Store de estado do pedido** passo para solicitar acesso a um ponto de migração de estado para *capturar* de estado do utilizador, este passo notifica o ponto de migração de estado que processam a captura está concluído. O ponto de migração de estado, em seguida, marca os dados de estado de utilizador como estando disponíveis para restauro. O ponto de migração de estado define o acesso de permissões de controlo para os dados de estado do utilizador para que apenas o computador de restauro tem acesso só de leitura.  

 Se utilizar o **Store de estado do pedido** passo para solicitar acesso a um ponto de migração de estado para *restaurar* de estado do utilizador, este passo notifica o ponto de migração de estado que o processo de restauro está concluído. A migração de estado do ponto de, em seguida, Ativa as definições de retenção de dados configurada.  

 > [!IMPORTANT]  
 > Definir o **continuar com o erro** opção para qualquer passo entre a **Store de estado do pedido** e **versão Estado Store** passos. Cada **Store de estado do pedido** passo tem de ter uma correspondência **Store de estado da versão** passo.  

 Este passo é executado apenas em todo o sistema operacional. Não é executado no Windows PE.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **estado do utilizador**e selecione **versão Estado Store**. 


### <a name="properties"></a>Propriedades  

 Este passo não requer quaisquer definições sobre o **propriedades** separador.



##  <a name="BKMK_RequestStateStore"></a> Store de estado do pedido  

 Utilize este passo para pedir acesso a um ponto de migração de estado ao capturar ou restaurar o estado.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](/sccm/osd/get-started/manage-user-state).  

 Utilize este passo em conjunto com o **Store de estado da versão**, **capturar estado do utilizador**, e **restaurar estado do utilizador** passos. Utilize estes passos para migrar o estado do computador com um ponto de migração de estado e a ferramenta de migração de estado de utilizador (USMT).  

 > [!NOTE]  
 >  Ao criar um novo ponto de migração de estado, o armazenamento de Estados do utilizador não está disponível para até uma hora. Para agilizar a disponibilidade, ajuste as definições de propriedade no ponto de migração de estado para acionar uma atualização de ficheiro de controlo do site.  

 Este passo é executado no SO completo e no Windows PE para o offline USMT.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDStateFallbackToNAA](/sccm/osd/understand/task-sequence-variables#OSDStateFallbackToNAA)  
 - [OSDStateSMPRetryCount](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryCount)  
 - [OSDStateSMPRetryTime](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryTime)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **estado do utilizador**e selecione **Store de estado do pedido**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="capture-state-from-the-computer"></a>Capturar estado a partir do computador
 Localize um ponto de migração de estado que cumpre os requisitos mínimos, conforme configurado nas definições de ponto de migração de estado. Por exemplo, **número máximo de clientes** e **quantidade mínima de espaço livre em disco**. Esta opção não garante a esteja disponível espaço suficiente no momento da migração de perfil. Esta opção pedidos de acesso para o ponto de migração de estado para capturar o estado de utilizador e definições a partir de um computador.  

 Se o site do Configuration Manager tiver vários pontos de migração de estado ativo, este passo localiza um ponto de migração de estado com espaço em disco disponível. A sequência de tarefas consulta o ponto de gestão para obter uma lista de pontos de migração de estado e, em seguida, avalia cada um até encontrar um que cumpra os requisitos mínimos.  

#### <a name="restore-state-from-another-computer"></a>Restaurar estado a partir de outro computador
 Pedir acesso a um ponto de migração de estado para restaurar o estado de utilizador capturados anteriormente e definições para um computador de destino.  

 Se existirem vários pontos de migração de estado, este passo localiza o ponto de migração de estado que possui o estado para o computador de destino.  

#### <a name="number-of-retries"></a>Número de tentativas
 O número de vezes que este passo tenta encontrar um ponto de migração de estado adequado antes de falhar.  

#### <a name="retry-delay-in-seconds"></a>Intervalo de repetição (em segundos)
 Período de tempo em segundos que o passo de sequência de tarefas aguarda entre as tentativas.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Se a conta de computador falhar a ligação para um armazenamento de Estados, utilize a conta de acesso de rede
 Se a sequência de tarefas não é possível acessar o ponto de migração de estado utilizando a conta de computador, utiliza as credenciais de conta de acesso de rede para ligar. Esta opção é menos segura porque outros computadores poderiam usar a conta de acesso de rede para aceder ao estado armazenado. Esta opção poderá ser necessária se o computador de destino não estiver associado a um domínio.  



##  <a name="BKMK_RestartComputer"></a> Reiniciar computador  

 Utilize este passo para reiniciar o computador que executa a sequência de tarefas. Após o reinício, o computador continua automaticamente com o passo seguinte na sequência de tarefas.  

 Este passo pode ser executado no SO completo ou o Windows PE.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [SMSRebootMessage](/sccm/osd/understand/task-sequence-variables#SMSRebootMessage)  
 - [SMSRebootTimeout](/sccm/osd/understand/task-sequence-variables#SMSRebootTimeout)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **reiniciar o computador**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>A imagem de arranque atribuída a esta sequência de tarefas
 Selecione esta opção para o computador de destino a utilizar a imagem de arranque atribuída à sequência de tarefas. A sequência de tarefas utiliza a imagem de arranque para executar os passos subsequentes no Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>O sistema operativo predefinido atualmente instalado
 Selecione esta opção para o computador de destino ser reiniciado no sistema operacional instalado.  

#### <a name="notify-the-user-before-restarting"></a>Notificar o utilizador antes de reiniciar
 Selecione esta opção para apresentar uma notificação ao utilizador antes do reinício do computador de destino. O passo seleciona esta opção, por predefinição.  

#### <a name="notification-message"></a>Mensagem de notificação
 Introduza uma mensagem de notificação para apresentar ao utilizador antes do reinício do computador de destino.  

#### <a name="message-display-time-out"></a>Tempo limite de visualização da mensagem
 Especifique o período de tempo em segundos antes do reinício do computador de destino. A predefinição é 60 segundos.  



##  <a name="BKMK_RestoreUserState"></a> Restaurar estado do utilizador  

 Utilize este passo para iniciar a ferramenta de migração de estado (USMT) do utilizador para restaurar o estado de utilizador e as definições para o computador de destino. Utilize este passo em conjunto com o **capturar estado do utilizador** passo.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](/sccm/osd/get-started/manage-user-state).  

 Utilize este passo com o **Store de estado do pedido** e **Store de estado da versão** passos salvar ou restaurar as definições de estado com um ponto de migração de estado. Esta opção desencripta sempre o armazenamento de Estados do USMT através de uma chave de encriptação que o Configuration Manager gera e gere.  

 O **restaurar estado do utilizador** etapa fornece controlo sobre um subconjunto limitado das mais opções utilizadas pelo USMT. Especificar opções de linha de comandos adicionais com o **OSDMigrateAdditionalRestoreOptions** variável.  

 > [!IMPORTANT]  
 >  Se estiver a utilizar este passo para um objetivo não relacionado com um cenário de implementação do sistema operacional, adicionar as [reiniciar o computador](#BKMK_RestartComputer) passo imediatamente a seguir os **restaurar estado do utilizador** passo.  

 Este passo é executado apenas em todo o sistema operacional. Não é executado no Windows PE.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [_OSDMigrateUsmtRestorePackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtRestorePackageID)  
 - [OSDMigrateAdditionalRestoreOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalRestoreOptions)  
 - [OSDMigrateContinueOnRestore](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnRestore)  
 - [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
 - [OSDMigrateLocalAccounts](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccounts)  
 - [OSDMigrateLocalAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccountPassword)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **estado do utilizador**e selecione **restaurar estado do utilizador**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="user-state-migration-tool-package"></a>Pacote do User State Migration Tool
 Especifique o pacote que contém a versão do USMT para este passo a utilizar. Este pacote não requer um programa. Quando o passo é executado, a sequência de tarefas utiliza a versão do USMT no pacote especificado. Especifique um pacote com a versão de 32 bits ou 64 bits do USMT. A arquitetura do USMT depende da arquitetura do sistema operacional para o qual a sequência de tarefas é restaurar o estado. 

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Restaurar todos os perfis de utilizador capturados com opções padrão
 Restaura todos os perfis de utilizador capturados com as opções padrão. Para personalizar as opções que restaura o USMT, selecione **personalizar captura de perfil do usuário**.  

#### <a name="customize-how-user-profiles-are-restored"></a>Personalizar como os perfis de utilizador são restaurados
 Permite personalizar os ficheiros que pretende restaurar para o computador de destino. Clique em **Ficheiros** para especificar os ficheiros de configuração no pacote do USMT que pretende utilizar para restaurar os perfis de utilizador. Para adicionar um ficheiro de configuração, introduza o nome do ficheiro na caixa **Nome do ficheiro** e clique em **Adicionar**. O painel de ficheiros lista os ficheiros de configuração que utiliza a USMT. O ficheiro. XML especificado define o ficheiro de utilizador restaura do USMT.  

#### <a name="restore-local-computer-user-profiles"></a>Restaurar perfis de utilizador do computador local
 Restaura os perfis de utilizador do computador local. Estes perfis não são para os utilizadores de domínio. Atribua novas palavras-passe para as contas de utilizador locais restauradas. USMT não é possível migrar as palavras-passe original. Introduza a nova palavra-passe na caixa **Palavra-passe** e confirme-a na caixa **Confirmar Palavra-passe**.  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Continuar se não for possível restaurar alguns ficheiros
 Continua o restauro do Estado de utilizador e as definições, mesmo que o USMT é não é possível restaurar alguns ficheiros. O passo ativa esta opção, por predefinição. Se desativar esta opção, e o USMT encontra erros ao restaurar ficheiros, este passo falhe imediatamente. USMT não restaure todos os ficheiros.   

#### <a name="enable-verbose-logging"></a>Ativar registo verboso
 Ative esta opção para gerar informações de ficheiros de registo mais detalhadas. Ao restaurar o estado, a sequência de tarefas por predefinição gera **Loadstate** na pasta de registo da sequência de tarefas, `%WinDir%\ccm\logs`.  



##  <a name="BKMK_RunCommandLine"></a> Executar linha de comandos  

 Utilize este passo para executar a linha de comandos especificada.  

 Este passo pode ser executado no SO completo ou no Windows PE.   

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [OSDDoNotLogCommand](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand) (a partir da versão 1806)<!--1358493-->  
 - [SMSTSDisableWow64Redirection](/sccm/osd/understand/task-sequence-variables#SMSTSDisableWow64Redirection)  
 - [SMSTSRunCommandLineUserName](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLineUserName)  
 - [SMSTSRunCommandLinePassword](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLinePassword)  
 - [WorkingDirectory](/sccm/osd/understand/task-sequence-variables#WorkingDirectory)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **executar linha de comandos**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="command-line"></a>Linha de comandos
 Especifica a linha de comandos que executa a sequência de tarefas. Este campo é obrigatório. Inclua extensões de nome de ficheiro, por exemplo,. vbs e .exe. Inclua todos os ficheiros de definições necessárias e opções da linha de comandos.  

 Se não especificar a extensão de nome de ficheiro, a. com de tentativas de Configuration Manager, a .exe, e. bat. Se o nome do ficheiro tem uma extensão que não é um tipo de executável, o Configuration Manager tenta aplicar uma associação local. Por exemplo, se a linha de comandos for Readme, o Configuration Manager inicia a aplicação especificada no computador de destino para abrir ficheiros. gif.  

 Exemplos:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

 > [!NOTE]  
 >  Para executar com êxito, precedência sobre as ações da linha de comandos com o **cmd.exe /c** comando. Exemplo destas ações incluem o redirecionamento de saída, encaminhando e copie comandos.  

#### <a name="disable-64-bit-file-system-redirection"></a>Desativar redirecionamento de sistema de ficheiros de 64 bits
 Por predefinição, os sistemas operativos de 64 bits utilizam o redirecionador de sistema de ficheiros WOW64 para executar linhas de comandos. Este comportamento é corretamente encontrar versões de 32 bits dos executáveis de SO e bibliotecas. Selecione esta opção para desativar a utilização do redirecionador do sistema de ficheiros WOW64. Windows é executado o comando utilizando as versões de 64 bits nativas dos executáveis de SO e bibliotecas. Esta opção não tem efeito quando em execução num sistema operacional de 32 bits.  

#### <a name="start-in"></a>Iniciar em
 Especifica a pasta executável do programa, até 127 carateres. Esta pasta pode ser um caminho absoluto no computador de destino ou um caminho relativo para a pasta do ponto de distribuição que contém o pacote. Este campo é opcional.  

 Exemplos:  

 `c:\officexp`  

 `i386`  

 > [!NOTE]  
 >  O **procurar** botão navega no computador local para ficheiros e pastas. Tudo o que selecionar também tem de existir no computador de destino. Tem de existir na mesma localização e com os mesmos nomes de ficheiros e pastas.  

#### <a name="package"></a>Pacote
 Quando especificar ficheiros ou programas na linha de comando que ainda não está presente no computador de destino, selecione esta opção para especificar o pacote do Configuration Manager que contém os ficheiros necessários. O pacote não requer um programa. Se os ficheiros especificados existirem no computador de destino, esta opção não é necessária.  

#### <a name="time-out"></a>Tempo limite
 Especifica um valor que representa o tempo que o Configuration Manager permite a linha de comandos executar. Este valor pode ser de um minuto e 999 minutos. O valor predefinido é 15 minutos. Esta opção está desativada por predefinição.  

 > [!IMPORTANT]  
 >  Se introduzir um valor que não permita tempo suficiente para o comando especificado concluir com êxito, este passo falhe. A sequência de tarefas todo poderá falhar, consoante as condições de passo ou grupo. Se o tempo limite expirar, o Configuration Manager termina o processo da linha de comandos.  

#### <a name="run-this-step-as-the-following-account"></a>Executar este passo de acordo com a seguinte conta
 Especifica que a linha de comando é executada como uma conta de utilizador do Windows diferente da conta de sistema Local.  

 > [!NOTE]  
 >  Para executar scripts simples ou comandos com outra conta depois de instalar o sistema operacional, adicione a conta de computador. Além disso, terá de restaurar perfis de utilizador do Windows para executar programas mais complexos, como um instalador do Windows.  

#### <a name="account"></a>Conta
 Especifica a conta de utilizador do Windows que este passo utiliza para executar a linha de comandos. A linha de comando é executado com as permissões da conta especificada. Clique em **Definir** para especificar a conta de utilizador local ou de domínio. Para obter mais informações sobre a conta sequência de tarefas executar como, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).

 > [!IMPORTANT]  
 >  Se este passo Especifica uma conta de utilizador e é executado no Windows PE, a ação falhar. Não é possível associar o Windows PE a um domínio. O **smsts** ficheiro regista esta falha.  



##  <a name="BKMK_RunPowerShellScript"></a> Executar Script do PowerShell  

 Utilize este passo para executar o script do Windows PowerShell especificado.  

 Este passo pode ser executado no SO completo ou no Windows PE. Para executar este passo no Windows PE, ative o PowerShell na imagem de arranque. Ative o componente de WinPE-PowerShell a partir da **componentes opcionais** separador nas propriedades da imagem de arranque. Para obter mais informações sobre como modificar uma imagem de arranque, consulte [gerir imagens de arranque](/sccm/osd/get-started/manage-boot-images).  

 > [!NOTE]  
 >  PowerShell não está ativado por predefinição nos sistemas operativos Windows Embedded.  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **executar Script do PowerShell**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="package"></a>Pacote
 Especifique o pacote do Configuration Manager que contém o script do PowerShell. Um pacote pode conter vários scripts do PowerShell.  

#### <a name="script-name"></a>Nome do script
 Especifica o nome do script do PowerShell a executar. Este campo é obrigatório.  

#### <a name="parameters"></a>Parâmetros
 Especifica os parâmetros transmitidos para o script do PowerShell. Esses parâmetros são os mesmos que os parâmetros de script do PowerShell na linha de comandos.  

 > [!IMPORTANT]  
 >  Forneça parâmetros consumidos pelo script e não para a linha de comandos do Windows PowerShell.  
 >   
 >  O exemplo seguinte contém parâmetros válidos:  
 >   
 >  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
 >   
 >  O exemplo seguinte contém parâmetros inválidos. Os dois primeiros itens são parâmetros da linha de comandos do Windows PowerShell (**- NoLogo** e **- ExecutionPolicy Unrestricted**). O script não consome estes parâmetros.  
 >   
 >  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

#### <a name="powershell-execution-policy"></a>Política de execução do PowerShell
 Determinar quais scripts do PowerShell (se houver) permite serem executados no computador. Escolha uma das seguintes políticas de execução:  

 -   **AllSigned**: Execute apenas scripts assinados por um fabricante fidedigno  

 -   **Indefinido**: Não definir qualquer política de execução  

 -   **Ignorar**: Carregar todos os ficheiros de configuração e executar todos os scripts. Se baixar um script não assinado a partir da internet, o Windows PowerShell não solicita permissão antes de executar o script.  


 > [!IMPORTANT]  
 >  PowerShell 1.0 não suporta indefinido e ignorar as políticas de execução.  



##  <a name="child-task-sequence"></a> Executar a sequência de tarefas

 > [!Note]  
 > O Configuration Manager não permite esta funcionalidade opcional por predefinição. Habilite esse recurso antes de o utilizar. Para mais informações, consulte [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

 A partir do Configuration Manager versão 1710, pode adicionar um novo passo que executa outra sequência de tarefas. Este passo cria uma relação principal-subordinado entre sequências de tarefas. Com sequências de tarefas filho, pode criar sequências de tarefas modulares, reutilizáveis mais.

 Ao adicionar uma sequência de tarefas filho para uma sequência de tarefas, considere os seguintes pontos:  

 - As sequências de tarefas principais e subordinados com eficiência são combinadas numa única política que executa o cliente.  

 - O ambiente é global. Se a sequência de tarefas principal define uma variável e, em seguida, a sequência de tarefas filho altera essa variável, ela retém o valor mais recente. Se a sequência de tarefas filho cria uma nova variável, está disponível para o resto da sequência de tarefas principal.  

 - Mensagens de estado são enviadas por normal para uma operação de sequência de tarefa única.  

 - A sequência de tarefas grava entradas para o **smsts** arquivo, com novas entradas de log, deixando claro quando uma sequência de tarefas de subordinado é iniciado.  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **executar a sequência de tarefas**. 


### <a name="properties"></a>Propriedades

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="select-task-sequence-to-run"></a>Selecione a sequência de tarefas para executar
 Clique em **procurar** para selecionar a sequência de tarefas filho. O **Selecione uma sequência de tarefas** caixa de diálogo não apresenta a sequência de tarefas do pai.



##  <a name="BKMK_SetDynamicVariables"></a> Definir variáveis dinâmicas  

 Utilize este passo para executar as seguintes ações:  

 1.  Recolha informações do computador e o seu ambiente. Em seguida, defina especificar variáveis de sequência de tarefas com as informações.  

 2.  Avalie as regras definidas. Definir variáveis de sequência de tarefas com base nas regras avaliadas como verdadeiras.  


 A sequência de tarefas define automaticamente as seguintes variáveis de sequência de tarefas só de leitura:  
 - [\_SMSTSMake](/sccm/osd/understand/task-sequence-variables#SMSTSMake)  
 - [\_SMSTSModel](/sccm/osd/understand/task-sequence-variables#SMSTSModel)  
 - [\_SMSTSMacAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSMacAddresses)  
 - [\_SMSTSIPAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSIPAddresses)  
 - [\_SMSTSSerialNumber](/sccm/osd/understand/task-sequence-variables#SMSTSSerialNumber)  
 - [\_SMSTSAssetTag](/sccm/osd/understand/task-sequence-variables#SMSTSAssetTag)  
 - [\_SMSTSUUID](/sccm/osd/understand/task-sequence-variables#SMSTSUUID)  


 Este passo pode ser executado no SO completo ou o Windows PE.  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **definir variáveis dinâmicas**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="dynamic-rules-and-variables"></a>Regras e variáveis dinâmicas
 Para definir uma variável dinâmica para utilização na sequência de tarefas, adicione uma regra. Em seguida, defina um valor para cada variável especificada na regra. Além disso, adicione uma ou mais variáveis sem adicionar uma regra. Ao adicionar uma regra, escolha uma das seguintes categorias:  

 - **Computador**: Avalie os valores de etiqueta de recursos de hardware, UUID, número de série ou endereço MAC. Defina vários valores conforme necessário. Se qualquer valor for VERDADEIRO, a regra avalia como verdadeiro. Por exemplo, a regra seguinte avalia como VERDADEIRO se o número de série do dispositivo for 5892087 e o endereço MAC é 22-A4-5A-13-78-26:  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

 - **Localização**: Avaliar os valores para o gateway de rede padrão  

 - **Marca e modelo**: Avalie os valores da marca e modelo de um computador. A marca e o modelo têm de avaliar como verdadeiro para a regra avaliar como verdadeiro.   

    Especificar um asterisco (`*`) e o ponto de interrogação (`?`) como carateres universais. O asterisco corresponde a vários carateres e o ponto de interrogação corresponde a um único caráter. Por exemplo, a cadeia de caracteres `DELL*900?` corresponde `DELL-ABC-9001` e `DELL9009`.  

 - **Variável de sequência de tarefas**: Adicione uma variável de sequência de tarefas, condição e valor a avaliar. A regra avalia como verdadeiro quando o conjunto de valores da variável cumpre a condição especificada.  

    Especifique uma ou mais variáveis para definir para uma regra que avalia como VERDADEIRO ou definir variáveis sem utilizar uma regra. Selecione uma variável existente ou crie uma variável personalizada.  

     - **Variáveis de sequência de tarefas existente**: Selecione uma ou mais variáveis a partir de uma lista de variáveis de sequência de tarefas existentes. As variáveis da matriz não estão disponíveis para seleção.  

     - **Variáveis de sequência de tarefas personalizado**: Defina uma variável de sequência de tarefas personalizado. Também pode especificar uma variável de sequência de tarefas existente. Esta definição é útil para especificar uma matriz de variável existente, tal como **OSDAdapter**, uma vez que as matrizes de variáveis não estão na lista de variáveis de sequência de tarefas existente.  


 Depois de selecionar as variáveis para uma regra, forneça um valor para cada variável. A variável é definida para o valor especificado quando a regra avalia como verdadeiro. Para cada variável, pode selecionar **Valor secreto** para ocultar o valor da variável. Por predefinição, algumas variáveis existentes ocultam valores, tais como o **OSDCaptureAccountPassword** variável.  

 > [!IMPORTANT]  
 >  Gestor de configuração remove quaisquer valores das variáveis marcadas como uma **valor secreto** ao importar uma sequência de tarefas com o **definir variáveis dinâmicas** passo. Volte a introduzir o valor para a variável dinâmica depois de importar a sequência de tarefas.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Definir variável da sequência de tarefas  

 Utilize este passo para definir o valor de uma variável utilizada com a sequência de tarefas.  

 Este passo pode ser executado no SO completo ou o Windows PE. 

 As variáveis de sequência de tarefas são lidas pelas ações de sequência de tarefas e especificam o comportamento dessas ações. Para obter mais informações sobre variáveis de sequência de tarefas específicas e como usá-las, consulte os artigos seguintes:  
 - [Como utilizar variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables)  
 - [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **gerais**e selecione **Set Task Sequence Variable**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="task-sequence-variable"></a>Variável da sequência de tarefas
 Especifique o nome de uma sequência de tarefas incorporada ou uma variável de ação ou especificar seu próprio nome de variável definida pelo utilizador.  

#### <a name="do-not-display-this-value"></a>Não apresentar este valor
 <!--1358330--> A partir da versão 1806, ative esta opção para mascarar dados confidenciais armazenados em variáveis de sequência de tarefas. Por exemplo, quando especificar uma palavra-passe. 

#### <a name="value"></a>Valor  
 A sequência de tarefas define a variável para este valor. Definir esta variável de sequência de tarefas para o valor de outra variável de sequência de tarefas com a sintaxe `%varname%`.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Programa de configuração Windows e ConfigMgr  

 Utilize este passo para efetuar a transição do Windows PE para o novo sistema operacional. Este passo de sequência de tarefas é uma parte necessária de qualquer implementação do sistema operacional. Ele instala o cliente de Configuration Manager para o novo SO e prepara a sequência de tarefas continuar a execução no novo sistema operacional.  

 Este passo é executado apenas no Windows PE. Não é executado no SO completo.  

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [SMSClientInstallProperties](/sccm/osd/understand/task-sequence-variables#SMSClientInstallProperties)  


 Este passo substitui variáveis de diretório Sysprep. inf ou Unattend. XML, como `%WINDIR%` e `%ProgramFiles%`, com o diretório de instalação do Windows PE, `X:\Windows`. A sequência de tarefas ignora variáveis especificadas ao utilizar estas variáveis de ambiente.  

 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **imagens**e selecione **configuração do Windows e ConfigMgr**. 


### <a name="step-actions"></a>Ações de passo

 Este passo executa as seguintes ações:  

#### <a name="preliminaries-windows-pe"></a>Preliminares: Windows PE  

 1.  Substitua as variáveis de sequência de tarefas no ficheiro Unattend. XML.  

 2.  Transferir o pacote que contém o cliente do Configuration Manager. Adicione o pacote de imagem implementada.  

#### <a name="set-up-windows"></a>Configurar o Windows  

 -  Instalação baseada em imagem  

    1.  Desative o cliente do Configuration Manager na imagem, se existir. Em outras palavras, desative início automático para o serviço de cliente do Configuration Manager.  

    2.  Atualize o registo na imagem implementada para iniciar o sistema operativo implementado com a mesma letra de unidade que o computador de referência.  

    3.  Reiniciar para o sistema operativo implementado.  

    4.  A mini-configuração do Windows é executado com o Sysprep. inf anteriormente especificado ou o arquivo de resposta Unattend. XML, que tem todas as interações do utilizador final suprimidas. Se utilizar o **aplicar definições de rede** passo para associar um domínio, em seguida, essas informações estão no arquivo de resposta. A mini-configuração do Windows ingressa o computador ao domínio.  

 -  Instalação baseada em Setup.exe. Executa Setup.exe, que segue o processo de configuração normal do Windows:  

    1.  Pacote de atualização de copiar o sistema operacional, especificado na **aplicar sistema operativo** passo, a unidade de disco rígido.  

    2.  Reiniciar para o sistema operativo recentemente implementado.  

    3.  A mini-configuração do Windows é executado com o Sysprep. inf anteriormente especificado ou o arquivo de resposta Unattend. XML, que tem todas as definições de interface de utilizador suprimidas. Se utilizar o **aplicar definições de rede** passo para associar um domínio, em seguida, essas informações estão no arquivo de resposta. A mini-configuração do Windows ingressa o computador ao domínio.  

#### <a name="set-up-the-configuration-manager-client"></a>Configurar o cliente do Configuration Manager  

 1.  Após a conclusão da miniconfiguração do Windows, a sequência de tarefas é retomada com o setupcomplete.cmd.  

 2.  Ativar ou desativar a conta de administrador local, com base na opção selecionada na **aplicar definições do Windows** passo.  

 3.  Instale o cliente do Configuration Manager com o pacote transferido anteriormente e as propriedades de instalação especificadas neste passo. O cliente é instalado no "modo de aprovisionamento". Este modo impede que o cliente de processar novos pedidos de política até que a sequência de tarefas esteja concluída.  

 4.  Aguarde que o cliente estar totalmente operacional.  

#### <a name="the-step-completes"></a>A etapa é concluída
 A sequência de tarefas continua a executar o passo seguinte.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="client-package"></a>Pacote de cliente
 Clique em **procurar**, em seguida, selecione o pacote de instalação de cliente do Configuration Manager para utilizar neste passo.  

#### <a name="use-pre-production-client-package-when-available"></a>Utilizar o pacote de cliente de pré-produção quando disponível
 Se existir um pacote de cliente de pré-produção disponível, e o computador for um membro da coleção piloto, a sequência de tarefas utiliza este pacote em vez do pacote de cliente de produção. O cliente de pré-produção é uma versão mais recente para um teste num ambiente de produção. Clique em **procurar**, em seguida, selecione o pacote de instalação de cliente de pré-produção para utilizar com este passo.  

#### <a name="installation-properties"></a>Propriedades da Instalação
 O passo de sequência de tarefas especifica automaticamente a atribuição de sites e a configuração predefinida. Utilize este campo para especificar as propriedades de instalação adicionais a utilizar quando instalar o cliente. Para introduzir várias propriedades de instalação, separe-as com um espaço.  

 Especifique as opções da linha de comandos a utilizar durante a instalação do cliente. Por exemplo, introduza `/skipprereq: silverlight.exe` para informar CCMSetup.exe para não instalar o pré-requisito Microsoft Silverlight. Para obter mais informações sobre as opções da linha de comandos disponíveis para CCMSetup.exe, consulte [acerca das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).  


### <a name="options"></a>Opções

 > [!NOTE]  
 > Não ativar **continuar com o erro** sobre o **opções** separador. Se existir um erro durante este passo, a sequência de tarefas falhará se ou não ativar esta definição.  



##  <a name="BKMK_UpgradeOS"></a> Atualizar sistema operativo  

 > [!TIP]  
 > A partir do Windows 10, versão 1709, o suporte de dados inclui várias edições. Ao configurar uma sequência de tarefas para utilizar um pacote de atualização de SO ou a imagem do SO, certifique-se de que selecione um [suportado edition](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

 Utilize este passo para atualizar uma versão anterior do Windows para uma versão mais recente do Windows 10.  

 Este passo de sequência de tarefas é executado apenas no SO completo. Não é executado no Windows PE.  

 Utilize as seguintes variáveis de sequência de tarefas com este passo:  
 - [_SMSTSOSUpgradeActionReturnCode](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode)  
 - [OSDSetupAdditionalUpgradeOptions](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions)  


 Para adicionar este passo no editor de sequência de tarefas, clique em **Add**, selecione **imagens**e selecione **atualizar sistema operativo**. 


### <a name="properties"></a>Propriedades  

 Sobre o **propriedades** separador para este passo, configure as definições descritas nesta secção.  

#### <a name="upgrade-package"></a>Pacote de atualização
 Selecione esta opção para especificar o que pacote para utilizar para a atualização de atualização de SO Windows 10.  

#### <a name="source-path"></a>Caminho de origem
 Especifica o local ou o caminho para o suporte de dados do Windows 10 de rede que utiliza a configuração do Windows. Esta definição corresponde à opção de linha de comandos da configuração do Windows `/InstallFrom`. 

 Também pode especificar uma variável, tal como `%MyContentPath%` ou `%DPC01%`. Quando utilizar uma variável para o caminho de origem, defina o respetivo valor anteriormente na sequência de tarefas. Por exemplo, utilizar o [transferir conteúdo do pacote](#BKMK_DownloadPackageContent) passo para especificar uma variável para a localização do pacote de atualização do sistema operacional. Em seguida, utilize essa variável para o caminho de origem para este passo.  

#### <a name="edition"></a>Edição
 Especifique a edição no suporte de dados do SO a utilizar para a atualização.  

#### <a name="product-key"></a>Chave de produto
 Especifique a chave de produto a aplicar ao processo de atualização.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Fornecer o seguinte conteúdo de controlador à Configuração do Windows durante a atualização
 Adicione controladores ao computador de destino durante o processo de atualização. Esta definição corresponde à opção de linha de comandos da configuração do Windows `/InstallDriver`. Os controladores têm de ser compatíveis com o Windows 10. Especifique uma das seguintes opções:  

 - **Pacote de controladores**: Clique em **procurar** e selecione um pacote de controlador existente na lista.  

 - **Conteúdo de teste**:  Selecione esta opção para especificar a localização para o pacote de controladores. Pode especificar uma pasta local, um caminho de rede ou uma variável de sequência de tarefas. Quando utilizar uma variável para o caminho de origem, defina o respetivo valor anteriormente na sequência de tarefas. Por exemplo, ao utilizar o [transferir conteúdo do pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) passo.  

#### <a name="time-out-minutes"></a>Tempo limite (minutos)
 Especifique o número de minutos antes do Configuration Manager falhar neste passo. Esta opção é útil se a configuração do Windows interrompe o processamento, mas não terminar.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Efetuar análise de compatibilidade da Configuração do Windows sem iniciar a atualização
 Efetue a análise de compatibilidade de configuração do Windows sem iniciar o processo de atualização. Esta definição corresponde à opção de linha de comandos da configuração do Windows `/Compat ScanOnly`. Implemente o pacote de atualização de SO completo com esta opção. 

 <!--SCCMDocs-pr issue 2812--> A partir da versão 1806, quando ativa esta opção, este passo não coloca o cliente do Configuration Manager para o modo de aprovisionamento. A instalação do Windows será executada automaticamente em segundo plano e o cliente continua a funcionar normalmente. 

 A Configuração devolve um código de saída como resultado da análise. A tabela seguinte fornece alguns dos códigos de saída mais comuns:  

 |Código de saída|Detalhes|  
 |-|-|  
 |MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Não existem problemas de compatibilidade ("êxito").|  
 |MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0XC1900208)|Problemas de compatibilidade passíveis de ação.|  
 |MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0XC1900204)|Opção de migração selecionada não está disponível. Por exemplo, uma atualização do Empresarial para o Profissional.|  
 |MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Não é elegível para Windows 10.|  
 |MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0XC190020E)|Não existe espaço livre suficiente no disco.|  

 Para obter mais informações sobre este parâmetro, consulte [opções de linha de comandos de configuração do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#6).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Ignorar mensagens de compatibilidade dispensáveis
 Especifica que a configuração conclui a instalação, ignorando quaisquer mensagens de compatibilidade dispensáveis. Esta definição corresponde à opção de linha de comandos da configuração do Windows `/Compat IgnoreWarning`.  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Atualizar dinamicamente a Configuração do Windows com o Windows Update
 Ative a configuração para efetuar operações de atualização dinâmica, como pesquisa, transferir e instalar atualizações. Esta definição corresponde à opção de linha de comandos da configuração do Windows `/DynamicUpdate`. Esta definição não é compatível com atualizações de software do Configuration Manager. Ative esta opção na gestão de atualizações com autónomo Windows Server Update Services (WSUS) ou o Windows Update para empresas.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Ignorar política e utilizar o Microsoft Update por predefinição
 O substitua temporariamente a política local em tempo real para executar operações de atualização dinâmica. O computador obtém as atualizações do Windows Update.
