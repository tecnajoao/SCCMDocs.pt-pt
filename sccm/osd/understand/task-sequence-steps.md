---
title: "Passos de sequência - Configuration Manager tarefas | Microsoft Docs"
description: "Saiba mais sobre os passos de sequência de tarefas que pode adicionar uma sequência de tarefas do Configuration Manager."
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: 26
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: MT
ms.sourcegitcommit: b7461f89f483314bd07248bbc9d5dde85ca6b6c2
ms.openlocfilehash: e0726febc4c36a26c5e067914734838bf2681e6c
ms.contentlocale: pt-pt
ms.lasthandoff: 08/03/2017

---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Variáveis de passos de tarefas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os seguintes passos de sequência de tarefas podem ser adicionados a uma sequência de tarefas do Configuration Manager. Para obter informações sobre a edição de uma sequência de tarefas, veja [Editar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  


##  <a name="BKMK_ApplyDataImage"></a>Aplique o passo de sequência de tarefas de imagem de dados  
 Utilize o passo de sequência de tarefas **Aplicar Imagem de Dados** para copiar a imagem de dados para a partição de destino especificada.  

 Este passo é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, consulte [variáveis de ação da sequência de tarefas](task-sequence-action-variables.md).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Pacote de imagem**  
 Especifique o **Pacote de Imagem** que será utilizado por este passo de sequência de tarefas, clicando em **Procurar**. Selecione o pacote que pretende instalar na caixa de diálogo **Selecionar um Pacote**. As informações sobre propriedades associadas para cada pacote de imagem existente são apresentadas na parte inferior da caixa de diálogo **Selecionar um Pacote**. Utilize a lista pendente para selecionar a **Imagem** que pretende instalar a partir do **Pacote de Imagem** selecionado.  

> [!NOTE]  
>  Esta ação de sequência de tarefas processa a imagem como um ficheiro de dados e não efetua nenhuma configuração necessária para arrancar a imagem como sistema operativo.  

 **Destino**  
 Especifica uma partição e um disco rígido formatados existentes, uma letra de unidade lógica específica ou o nome de uma variável de sequência de tarefas que contém a letra de unidade lógica.  

-   **Partição disponível seguinte** -utilize a partição sequencial seguinte que não tenha sido direcionada anteriormente por uma ação aplicar sistema operativo ou aplicar imagem de dados nesta sequência de tarefas.  

-   **Partição e disco específico** - selecione o **disco** número (começando com 0) e o **partição** número (começando com 1).  

-   **Letra de unidade lógica específica** -especifique o **letra de unidade** atribuída à partição pelo Windows PE. Tenha em atenção que esta letra de unidade pode ser diferente da letra de unidade que o sistema operativo recentemente implementado atribuirá.  

-   **Letra de unidade lógica armazenada numa variável** -especifique a variável de sequência de tarefas que contém a letra de unidade atribuída à partição pelo Windows PE. Normalmente, esta variável seria definida na secção Avançadas da caixa de diálogo **Propriedades de Partição** para a ação de sequência de tarefas **Formatar e Particionar Disco**.  

 **Elimine todo o conteúdo na partição antes de aplicar a imagem**  
 Especifica que todos os ficheiros na partição de destino serão eliminados antes de a imagem ser instalada. Ao não eliminar o conteúdo da partição, este passo pode ser utilizado para aplicar conteúdo adicional a uma partição direcionada anteriormente.  

##  <a name="BKMK_ApplyDriverPackage"></a>Aplicar pacote de controlador  
 Utilize o passo de sequência de tarefas **Aplicar Pacote de Controlador** para transferir todos os controladores no pacote de controlador e instalá-los no sistema operativo Windows.

 O passo de sequência de tarefas **Aplicar Pacote de Controlador** torna todos os controladores de dispositivo num pacote de controlador disponíveis para serem utilizados pelo Windows. Este passo pode ser adicionado a uma sequência de tarefas entre os passos **Aplicar Sistema Operativo** e **Configurar Windows e ConfigMgr** para tornar os controladores de dispositivo no pacote de controlador disponíveis no Windows. Normalmente, o passo **Aplicar Pacote de Controlador** é colocado depois do passo de sequência de tarefas **Aplicar Controladores Automaticamente**. O passo de sequência de tarefas **Aplicar Pacote de Controlador** também é útil em cenários de implementação de suportes de dados autónomos.  

 Certifique-se de que os controladores de dispositivo semelhantes são colocados num pacote de controlador e distribuídos para os pontos de distribuição adequados. Depois de serem distribuídos computadores de cliente do Configuration Manager podem instalá-los. Por exemplo, pode colocar todos os controladores de dispositivo de um fabricante num pacote de controlador e, em seguida, distribuir o pacote para os pontos de distribuição onde os computadores associados podem aceder aos mesmos.

 Este passo é útil para suportes de dados autónomos e administradores que pretendem instalar um conjunto específico de controladores, incluindo controladores para dispositivos que não seriam detetados numa análise Plug-n-Play (por exemplo, impressoras de rede).  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Pacote de Controlador](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Pacote de controladores**  
 Especifique o pacote de controlador que contém os controladores de dispositivo necessários, clicando em **Procurar** e iniciando a caixa de diálogo **Selecionar um Pacote**. Especifique um pacote existente para ser disponibilizado. As propriedades do pacote associado são apresentadas na parte inferior da caixa de diálogo.  

 **Selecione o controlador de armazenamento em massa no pacote que tem de ser instalado antes da configuração em sistemas de operativos anteriores ao Windows Vista**  
 Especifique quaisquer controladores de dispositivo de armazenamento em massa necessários para instalações de sistemas operativos anteriores ao Windows Vista.  

 **Controlador**  
 Selecione o ficheiro do controlador de dispositivo de armazenamento em massa a instalar antes da configuração em implementações de sistemas operativos anteriores ao Windows Vista. A lista pendente é preenchida a partir do pacote especificado.  

 **Modelo**  
 Especifique o dispositivo crítico de arranque necessário para implementações de sistemas operativos anteriores ao Windows Vista.  

 **Efetuar a instalação autónoma de controladores não assinados numa versão do Windows em que tal é permitido**  
 Selecione esta opção para permitir que o Windows instale controladores não assinados no computador de referência.  

##  <a name="BKMK_ApplyNetworkSettings"></a>Aplique o passo de definições de rede  
 Utilize o passo de sequência de tarefas **Aplicar Definições de Rede** para especificar as informações de configuração da rede ou do grupo de trabalho para o computador de destino. Os valores especificados são armazenados no formato de ficheiro de resposta adequado que será utilizado pela Configuração do Windows quando for executado o passo de sequência de tarefas **Configurar Windows e ConfigMgr**.  

 Este passo de sequência de tarefas é executado num sistema operativo padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Definições de Rede](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Aderir a um grupo de trabalho**  
 Selecione esta opção para associar o computador de destino ao grupo de trabalho especificado. Introduza o nome do grupo de trabalho na linha **Grupo de Trabalho**. Este valor pode ser substituído pelo valor capturado pelo passo de sequência de tarefas **Capturar Definições de Rede**.  

 **Aderir a um domínio**  
 Selecione esta opção para associar o computador de destino ao domínio especificado. Especifique ou navegue até ao domínio, tal como *fabricam.com*. Especifique ou navegue até um caminho LDAP (Lightweight Directory Access Protocol) para uma unidade organizacional (ou seja, LDAP//OU=computadores, DC=Fabricam.com, C=com).  

 **Conta**  
 Clique em **Definir** para especificar uma conta com as permissões necessárias para associar o computador ao domínio. No **conta de utilizador do Windows** caixa de diálogo, pode introduzir o nome de utilizador usando o seguinte formato: **Domínio \ utilizador** .  

 **Definições do adaptador**  
 Especifique as configurações de rede para cada placa de rede no computador. Clique em **Novo** para abrir a caixa de diálogo **Definições de Rede** e, em seguida, especifique as definições de rede. Se as definições de rede tiverem sido capturadas num passo de sequência de tarefas **Capturar Definições de Rede** anterior, as definições anteriores são aplicadas à placa de rede e as definições especificadas neste passo não são aplicadas. Se as definições de rede não tiverem sido capturadas anteriormente, as definições especificadas no passo **Aplicar Definições de Rede** são aplicada às placas de rede pela ordem de enumeração do dispositivo Windows.  

##  <a name="BKMK_ApplyOperatingSystemImage"></a>Aplicar imagem do sistema operativo  
 Utilize o passo de sequência de tarefas **Aplicar Imagem do Sistema Operativo** para instalar um sistema operativo no computador de destino. Este passo de sequência de tarefas executa um conjunto de ações consoante estiver a utilizar uma imagem do sistema operativo ou um pacote de instalação para instalar o sistema operativo.  

 O passo **Aplicar Imagem do Sistema Operativo** executa as ações seguintes quando é utilizada uma imagem do sistema operativo.  

1.  Elimina todo o conteúdo no volume de destino, exceto os ficheiros na pasta especificada pelo &#95; Variável de sequência de tarefas SMSTSUserStatePath.  

2.  Extrai o conteúdo do ficheiro .wim especificado para a partição de destino especificada.  

3.  Prepara o ficheiro de resposta:  

    1.  Cria um novo ficheiro de resposta de Configuração do Windows predefinido (sysprep.inf ou unattend.xml) para o sistema operativo que está a ser implementado.  

    2.  Intercala quaisquer valores do ficheiro de resposta fornecido pelo utilizador.  

4.  Copia carregadores de arranque do Windows para a partição ativa.  

5.  Configura o ficheiro boot.ini ou a BCD (Boot Configuration Database) para referenciar o sistema operativo recentemente instalado.  

 O passo **Aplicar Imagem do Sistema Operativo** executa as ações seguintes quando é utilizado um pacote de instalação do sistema operativo.  

1.  Elimina todo o conteúdo no volume de destino, exceto os ficheiros na pasta especificada pelo &#95; Variável de sequência de tarefas SMSTSUserStatePath.  

2.  Prepara o ficheiro de resposta:  

    1.  Cria um ficheiro de resposta novo com valores padrão criados pelo Configuration Manager.  

    2.  Intercala quaisquer valores do ficheiro de resposta fornecido pelo utilizador.  

> [!NOTE]  
>  A instalação real do Windows é iniciada pelo passo de sequência de tarefas **Configurar Windows e ConfigMgr**. Após a execução da ação de sequência de tarefas **Aplicar Sistema Operativo**, a variável de sequência de tarefas OSDTargetSystemDrive é definida para a letra de unidade da partição que contém os ficheiros do sistema operativo.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Imagem do Sistema Operativo](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   **Aceder ao conteúdo diretamente a partir do ponto de distribuição**:  

     Utilize esta opção para especificar se pretende que a sequência de tarefas aceda diretamente à imagem do sistema operativo a partir do ponto de distribuição. Por exemplo, pode utilizar esta opção quando implementar sistemas operativos em dispositivos incorporados com uma capacidade de armazenamento limitada. Quando esta opção é selecionada, também tem de configurar as definições de partilha de pacote no separador **Acesso a Dados** das propriedades do pacote.  

    > [!NOTE]  
    >  Esta definição substitui a opção de implementação configurada na página **Pontos de Distribuição** no **Assistente de Implementação de Software** apenas para a imagem do sistema operativo especificada neste passo de sequência de tarefas e não para todo o conteúdo da sequência de tarefas.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Aplicar o sistema operativo a partir de uma imagem capturada**  
 Instala uma imagem do sistema operativo capturada anteriormente. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar um pacote** e selecione o pacote de imagem existente que pretende instalar. Se estiverem associadas várias imagens ao **Pacote de imagem** especificado, utilize a lista pendente para especificar a imagem associada que será utilizada para esta implementação. Pode ver informações básicas sobre cada imagem existente clicando na imagem.  

 **Aplicar imagem do sistema operativo a partir de uma origem de instalação original**  
 Instala um sistema operativo utilizando uma origem de instalação original. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar um Pacote de Instalação do Sistema Operativo** e selecione o pacote de instalação do sistema operativo existente que pretende utilizar. Pode ver informações básicas sobre cada origem de imagem existente clicando na origem da imagem. As propriedades da origem da imagem associada são apresentadas no painel de resultados, na parte inferior da caixa de diálogo. Se existirem várias edições associadas ao pacote especificado, utilize a lista pendente para especificar a **Edição** associada que será utilizada.  

 **Utilizar um ficheiro de resposta sysprep ou autónomo para uma instalação personalizada**  
 Utilize esta opção para fornecer um ficheiro de resposta de configuração do Windows (**unattend.xml**, **unattend.txt** ou **sysprep.inf**), consoante a versão do sistema operativo e o método de instalação. O ficheiro que especificar pode incluir qualquer uma das opções de configuração padrão suportadas pelos ficheiros de resposta do Windows. Por exemplo, pode utilizá-lo para especificar a home page predefinida do Internet Explorer. Tem de especificar o pacote que contém o ficheiro de resposta e o caminho associado para o ficheiro no pacote.  

> [!NOTE]  
>  O ficheiro de resposta de configuração do Windows que fornecer pode conter variáveis de sequência de tarefas incorporadas no formato %*varname*%, em que varname corresponde ao nome da variável. A cadeia %*varname*% será substituída pelos valores da variável real na ação de sequência de tarefas **Configurar Windows e ConfigMgr**. No entanto, tenha em atenção que essas variáveis de sequência de tarefas incorporadas não podem ser utilizadas em campos apenas numéricos num ficheiro de resposta unattend.xml.  

 Se não fornecer um ficheiro de resposta de configuração do Windows, esta ação de sequência de tarefas irá gerar automaticamente um ficheiro de resposta.  

 **Destino**  
 Especifica uma partição e um disco rígido formatados existentes, uma letra de unidade lógica específica ou o nome de uma variável de sequência de tarefas que contém a letra de unidade lógica.  

-   **Partição disponível seguinte** -utilize a partição sequencial seguinte que não tenha sido direcionada anteriormente por uma ação aplicar sistema operativo ou aplicar imagem de dados nesta sequência de tarefas.  

-   **Partição e disco específico** - selecione o **disco** número (começando com 0) e o **partição** número (começando com 1).  

-   **Letra de unidade lógica específica** -especifique o **letra de unidade** atribuída à partição pelo Windows PE. Tenha em atenção que esta letra de unidade pode ser diferente da letra de unidade que o sistema operativo recentemente implementado atribuirá.  

-   **Letra de unidade lógica armazenada numa variável** -especifique a variável de sequência de tarefas que contém a letra de unidade atribuída à partição pelo Windows PE. Normalmente, esta variável seria definida na secção Avançadas da caixa de diálogo **Propriedades de Partição** para a ação de sequência de tarefas **Formatar e Particionar Disco**.  

##  <a name="BKMK_ApplyWindowsSettings"></a>Aplicar definições do Windows  
 Utilize o passo de sequência de tarefas **Aplicar Definições do Windows** para configurar as definições do Windows para o computador de destino. Os valores especificados são armazenados no formato de ficheiro de resposta adequado que será utilizado pela Configuração do Windows quando for executado o passo de sequência de tarefas **Configurar Windows e ConfigMgr**.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Definições do Windows](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Nome de utilizador**  
 Especifique o nome de utilizador registado associado ao computador de destino. Este valor pode ser substituído pelo valor capturado pela ação de sequência de tarefas **Capturar Definições do Windows**.  

 **Nome da organização**  
 Especifique o nome da organização registado associado ao computador de destino. Este valor pode ser substituído pelo valor capturado pela ação de sequência de tarefas **Capturar Definições do Windows**.  

 **Chave de produto**  
 Especifique a chave de produto utilizada para a instalação do Windows no computador de destino.  

 **Licenciamento do servidor**  
 Especifique o modo de licenciamento do servidor. Pode selecionar **Por servidor** ou **Por utilizador** como modo de licenciamento. Se selecionar Por servidor como modo de licenciamento, também terá de especificar o número máximo de ligações que será permitido por contrato de licença. Selecione **Não especificar** se o computador de destino não for um servidor ou o utilizador não pretender especificar o modo de licenciamento.  

 **Número máximo de ligações**  
 Especifique o número máximo de ligações disponíveis para este computador, conforme indicado no contrato de licença.  

 **Aleatoriamente gerar a palavra-passe de administrador local e desativar a conta nas plataformas suportadas (recomendado)**  
 Selecione esta opção para gerar aleatoriamente uma palavra-passe de administrador local. É criada uma palavra-passe de administrador local e a conta é desativada nas plataformas suportadas.  

 **Ativar a conta e especificar a palavra-passe de administrador local**  
 Selecione esta opção para ativar a conta de administrador local e criar a palavra-passe de administrador local. Introduza a palavra-passe na linha **Palavra-passe** e confirme-a na linha **Confirmar palavra-passe**.  

 **Fuso horário**  
 Especifique o fuso horário a configurar no computador de destino. Este valor pode ser substituído pelo valor capturado pelo passo de sequência de tarefas **Capturar Definições do Windows**.  

##  <a name="BKMK_AutoApplyDrivers"></a>Aplicar controladores automaticamente  
 Utilize o passo de sequência de tarefas **Aplicar Controladores Automaticamente** para corresponder e instalar controladores como parte da implementação do sistema operativo.  

 O passo de sequência de tarefas **Aplicar Controladores Automaticamente** executa as seguintes ações:  

1.  Analisa o hardware e localiza os IDs Plug-n-Play para todos os dispositivos existentes no sistema.  

2.  Envia a lista de dispositivos e os respetivos IDs Plug-n-Play para o ponto de gestão. O ponto de gestão devolve uma lista de controladores compatíveis a partir do catálogo de controladores de cada dispositivo. O ponto de gestão considera todos os controladores independentemente do pacote de controlador em que possam estar incluídos. Apenas são considerados os controladores marcados com a categoria de controlador especificada e os controladores não marcados como desativados.  

3.  Para cada dispositivo, o cliente escolhe o controlador mais adequado para o sistema operativo no qual está a ser implementado e que esteja num ponto de distribuição acessível.  

4.  Os controladores selecionados são transferidos a partir de um ponto de distribuição e pré-configurados no sistema operativo de destino.  

    1.  Para instalações baseadas em imagens, os controladores são colocados no arquivo de controladores do sistema operativo.  

    2.  Para instalações baseadas em configurações, a Configuração do Windows é efetuada com a localização dos controladores.  

5.  Quando a ação de sequência de tarefas **Configurar Windows e ConfigMgr** for executada e o Windows arrancar inicialmente, os controladores pré-configurados serão localizados por esta ação.  

> [!IMPORTANT]
>  O **aplicar controladores automaticamente** passo de sequência de tarefas não pode ser utilizado com suportes de dados autónomos, porque a configuração do Windows não terá nenhuma ligação ao site do Configuration Manager.

Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Aplicar Controladores Automaticamente](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Instalar apenas o melhor correspondência de controladores compatíveis**  
 Especifica que o passo de sequência de tarefas instala apenas os controladores com melhor compatibilidade para cada dispositivo de hardware detetado.  

 **Instalar todos os controladores compatíveis**  
 Especifica que o passo de sequência de tarefas instala todos os controladores compatíveis para cada dispositivo de hardware detetado e permite que a configuração do Windows escolha o melhor controlador. Esta opção utiliza mais largura de banda de rede e espaço em disco porque transfere mais controladores, mas pode resultar na seleção de um controlador mais adequado.  

 **Considerar controladores de todas as categorias**  
 Especifica que a ação de sequência de tarefas procura todas as categorias de controladores disponíveis para obter os controladores de dispositivo adequados.  

 **Limitar a correspondência de controladores para apenas considerar controladores nas categorias selecionadas**  
 Especifica que a ação de sequência de tarefas procura controladores de dispositivo nas categorias de controladores especificadas para obter os controladores de dispositivo adequados.  

 **Efetuar a instalação autónoma de controladores não assinados nas versões do Windows em que tal é permitido**  
 Permite que esta ação de sequência de tarefas instale controladores de dispositivo do Windows não assinados.  

> [!IMPORTANT]  
>  Esta opção não é aplicável a sistemas operativos em que não é possível configurar a política de assinatura de controladores.  

##  <a name="BKMK_CaptureNetworkSettings"></a>Capturar definições de rede  
 Utilize o passo de sequência de tarefas **Capturar Definições de Rede** para capturar as definições de rede Microsoft do computador que está a executar a sequência de tarefas. As definições são guardadas em variáveis de sequência de tarefas que substituirão as predefinições configuradas no passo de sequência de tarefas **Aplicar Definições de Rede**.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Capturar Definições de Rede](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifica um nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Fornece informações mais detalhadas sobre a ação executada neste passo.  

 **Migrar a associação ao domínio e grupo de trabalho**  
 Captura as informações de associação de domínios e grupos de trabalho do computador de destino.  

 **Migrar a configuração do adaptador de rede**  
 Captura a configuração da placa de rede do computador de destino. As informações capturadas incluem as definições de rede globais, o número de placas e as definições de rede associadas a cada placa. Estas definições incluem as definições associadas a DNS, WINS, IP e filtros de portas.  

##  <a name="BKMK_CaptureOperatingSystemImage"></a>Capturar imagem do sistema operativo  
 Utilize o passo de sequência de tarefas **Capturar Imagem do Sistema Operativo** para capturar uma ou mais imagens de um computador de referência e armazená-las num ficheiro WIM na partilha de rede especificada. O assistente pacote da imagem de sistema operativo adicionar, em seguida, pode ser utilizado para importar este. Ficheiro WIM para o Configuration Manager para que possam ser utilizado para implementações do sistema de operativo baseada em imagem.  

 Cada volume (unidade) no computador de referência é capturado como uma imagem separada no ficheiro .wim. Se o computador referenciado tiver vários volumes, o ficheiro WIM resultante irá conter uma imagem separada para cada volume. Apenas são capturados os volumes formatados como NTFS ou FAT32. Os volumes com outros formatos e os volumes USB são ignorados.  

 O sistema operativo instalado no computador de referência tem de ser uma versão do Windows que são suportados pelo Configuration Manager e tem de ter sido preparado através da ferramenta SysPrep. O volume do sistema operativo instalado e o volume de arranque têm de ser o mesmo volume.  

 Também tem de introduzir uma conta do Windows com permissões de escrita para a partilha de rede selecionada.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Capturar Imagem do Sistema Operativo](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

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
 Utilize o passo de sequência de tarefas **Capturar Estado do Utilizador** para utilizar o User State Migration Tool (USMT) para capturar o estado e as definições de utilizador do computador que está a executar a sequência de tarefas. Este passo de sequência de tarefas é utilizado em conjunto com o passo de sequência de tarefas **Restaurar Estado do Utilizador**. Com o USMT 3.0.1 e posterior, esta opção encripta sempre o armazenamento de Estados do USMT através de uma chave de encriptação gerada e gerida pelo Configuration Manager.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

 Também pode utilizar o **capturar estado do utilizador** passo de sequência de tarefas com o **solicitar armazenamento de Estados** e **disponibilizar armazenamento de Estados** passos de sequência de tarefas se pretender guardar as definições de estado ou restaurar definições a partir de uma migração de estado para o ponto no site do Configuration Manager.  

 O passo de sequência de tarefas **Capturar Estado do Utilizador** fornece controlo sobre um subconjunto limitado das opções mais utilizadas pelo USMT. Podem ser especificadas opções da linha de comandos adicionais com a variável de sequência de tarefas OSDMigrateAdditionalCaptureOptions.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Capturar Estado do Utilizador](task-sequence-action-variables.md#BKMK_CaptureUserState).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Pacote de ferramenta de migração de estado de utilizador**  
 Introduza o pacote de Configuration Manager que contém a versão do USMT para este passo de sequência de tarefas a utilizar ao capturar o estado do utilizador e as definições. Este pacote não requer um programa. Quando o passo de sequência de tarefas for executado, a sequência de tarefas utilizará a versão do USMT no pacote especificado. Especifique um pacote com a versão de 32 bits ou x64 do USMT, consoante a arquitetura do sistema operativo a partir do qual está a capturar o estado.  

 **Capturar todos os perfis de utilizador com opções padrão**  
 Selecione esta opção para migrar todas as informações dos perfis de utilizador. Esta opção está selecionada por predefinição.  

 Se selecionar esta opção, mas não selecionar a opção para restaurar perfis de utilizador do computador local no passo de sequência de tarefas restaurar estado do utilizador, a sequência de tarefas irá falhar porque o Configuration Manager não é possível migrar as novas contas sem lhes atribuir palavras-passe. Além disso, se utilizar o assistente **Nova Sequência de Tarefas** e criar uma sequência de tarefas para **Instalar um pacote de imagem existente**, a sequência de tarefas resultante utilizará a predefinição Capturar todos os perfis de utilizador com opções padrão, mas não selecionará a opção para Restaurar perfis de utilizador do computador local (ou seja, contas não pertencentes ao domínio).  

 Selecione **Restaurar perfis de utilizador do computador local** e forneça uma palavra-passe para a conta a ser migrada. Numa sequência de tarefas criada manualmente, esta definição pode ser encontrada no passo Restaurar Estado do Utilizador. Numa sequência de tarefas criada pelo assistente **Nova Sequência de Tarefas**, esta definição pode ser encontrada na página do assistente no passo **Restaurar Definições e Ficheiros do Utilizador**.  

 Se não tiver contas de utilizador locais, isto não é aplicável.  

 **Personalizar como os perfis de utilizador são capturados**  
 Selecione esta opção para especificar uma migração de ficheiros de perfil personalizados. Clique em **Ficheiros** para selecionar os ficheiros de configuração para o USMT utilizar neste passo. Tem de especificar um ficheiro .xml personalizado que contenha regras que definam os ficheiros de estado do utilizador a migrar.  

 **Clique aqui para selecionar os ficheiros de configuração:**  
 Selecione esta opção para selecionar os ficheiros de configuração no pacote do USMT que pretende utilizar para capturar os perfis de utilizador. Clique no botão **Ficheiros** para iniciar a caixa de diálogo **Ficheiros de Configuração**. Para especificar um ficheiro de configuração, introduza o nome do ficheiro na linha **Nome do ficheiro** e clique no botão **Adicionar**.  

 **Ativar o registo verboso**  
 Ative esta opção para gerar informações de ficheiros de registo mais detalhadas. Ao capturar o estado, o registo Scanstate.log é gerado e armazenado por predefinição na pasta de Registo da sequência de tarefas na pasta \windows\system32\ccm\logs.  

 **Ignorar ficheiros que utilizam o sistema de ficheiros encriptados**  
 Ative esta opção se pretender ignorar a captura de ficheiros encriptados com o Sistema de Encriptação de Ficheiros (EFS), incluindo ficheiros de perfil. Consoante o sistema operativo e a versão do USMT, os ficheiros encriptados podem não ser legíveis após o restauro. Para mais informações, consulte a documentação do USMT.  

 **Copiar utilizando o acesso do sistema de ficheiros**  
 Ative esta opção para especificar qualquer uma das seguintes definições:  

-   **Continuar se não for possível capturar alguns ficheiros**: Ative esta definição continuar o processo de migração, mesmo se não for possível capturar alguns ficheiros. Se desativar esta opção e não for possível capturar um ficheiro, o passo de sequência de tarefas falhará. Por predefinição, esta opção encontra-se ativada.  

-   **Capturar localmente ao utilizar hiperligações em vez de copiar ficheiros**: Ative esta definição para utilizar ligações fixas NTFS para capturar ficheiros.  

     Para obter mais informações sobre a migração de dados com ligações fixas, veja [Hard-Link Migration Store](http://go.microsoft.com/fwlink/p/?LinkId=240222) (em inglês).  

-   **Capturar no modo offline (apenas Windows PE)**: Ative esta definição capturar o estado do utilizador no Windows PE em vez do sistema operativo completo.  

 **Capturar utilizando o serviço de sombra de cópia de Volume (VSS)**  
 Esta opção permite-lhe capturar ficheiros mesmo que estejam bloqueados para edição por outra aplicação.  

##  <a name="BKMK_CaptureWindowsSettings"></a>Capturar definições do Windows  
 Utilize o passo de sequência de tarefas **Capturar Definições do Windows** para capturar as definições do Windows do computador que está a executar a sequência de tarefas. As definições são guardadas em variáveis de sequência de tarefas que substituirão as predefinições configuradas no passo de sequência de tarefas **Aplicar Definições do Windows**.  

 Este passo de sequência de tarefas é executado no Windows PE ou num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Capturar Definições do Windows](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Migrar o nome do computador**  
 Selecione esta opção para capturar o nome NetBIOS do computador.  

 **Migrar nomes organizacionais e de utilizador registados**  
 Selecione esta opção para capturar os nomes de utilizador e organização registados do computador.  

 **Migrar fuso horário**  
 Selecione esta opção para capturar a definição de fuso horário do computador.  

##  <a name="BKMK_CheckReadiness"></a>Verificar preparação  
 Utilize o passo de sequência de tarefas **Verificar a Preparação** para verificar se o computador de destino cumpre as condições de pré-requisitos de implementação especificadas.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo. Para este passo, não selecione esta definição ou o passo apenas registará as verificações de disponibilidade e não parará a sequência de tarefas quando uma verificação falhar.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Certifique-se a memória mínima (MB)**  
 Selecione esta definição para verificar se a quantidade de memória, em megabytes, instalada no computador de destino cumpre ou excede o valor especificado. Por predefinição, esta definição está selecionada.  

 **Certifique-se a velocidade mínima do processador (MHz)**  
 Selecione esta definição para verificar se a velocidade do processador, em megahertz (MHz), instalada no computador de destino cumpre ou excede o valor especificado. Por predefinição, esta definição está selecionada.  

 **Certifique-se o espaço mínimo livre em disco (MB)**  
 Selecione esta definição para verificar se a quantidade de espaço livre em disco, em megabytes, no computador de destino cumpre ou excede o valor especificado.  

 **Certifique-se de SO atual atualizar**  
 Selecione esta definição para verificar se o sistema operativo instalado no computador de destino cumpre o requisito especificado. Por predefinição, esta definição está selecionada com um valor de **CLIENT**.  

##  <a name="BKMK_ConnectToNetworkFolder"></a>Ligar à pasta de rede  
 Utilize a ação de sequência de tarefas **Ligar à Pasta de Rede** para criar uma ligação para uma pasta de rede partilhada.  

 Este passo de sequência de tarefas é executado num sistema operativo padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Ligar à Pasta de Rede](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

##  <a name="BKMK_ConvertDisktoDynamic"></a>Converter disco em dinâmico  
 Utilize o passo de sequência de tarefas **Converter Disco em Dinâmico** para converter um disco físico de um tipo de disco básico num tipo de disco dinâmico.  

 Este passo é executado num sistema operativo padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Converter Disco em Dinâmico](task-sequence-action-variables.md#BKMK_ConvertDisk).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Número do disco**  
 O número do disco físico do disco que será convertido.  

##  <a name="BKMK_DisableBitLocker"></a>Desativar BitLocker  
 Utilize o passo de sequência de tarefas **Desativar BitLocker** para desativar a encriptação BitLocker na unidade do sistema operativo atual ou numa unidade específica. Esta ação deixa os protetores de chave visíveis em texto não encriptado no disco rígido, mas não desencripta o conteúdo da unidade. Por conseguinte, esta ação é concluída quase instantaneamente.  

> [!NOTE]  
>  A encriptação de unidade BitLocker fornece encriptação de baixo nível do conteúdo de um volume do disco.  

 Se tiver várias unidades encriptadas, tem de desativar o BitLocker em todas as unidades de dados antes de desativar o BitLocker na unidade do sistema operativo.  

 Este passo é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifica um nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Fornece informações mais detalhadas sobre a ação executada neste passo.  

 **Unidade de sistema operativo atual**  
 Desativa o BitLocker na unidade do sistema operativo atual.  

 **Unidade específica**  
 Desativa o BitLocker numa unidade específica. Utilize a lista pendente para especificar a unidade na qual o BitLocker está desativado.  

##  <a name="BKMK_DownloadPackageContent"></a>Transferir conteúdo do pacote  
 Utilize o passo de sequência de tarefas **Transferir Conteúdo do Pacote** para transferir qualquer um dos seguintes tipos de pacotes:  

-   Imagens de sistema operativo  

-   Pacotes de atualização do sistema operativo  

-   Pacotes de controladores  

-   Pacotes  

 Este passo funciona bem numa sequência de tarefas para atualizar um sistema operativo nos seguintes cenários:  

-   Para utilizar uma única sequência de tarefas de atualização que funciona com plataformas x86 e x64. Para tal, inclua dois passos **Transferir Conteúdo do Pacote** no grupo **Preparar para Atualização** com condições para detetar a arquitetura do cliente e transferir apenas o pacote de atualização do sistema operativo adequado. Configure cada passo **Transferir Conteúdo do Pacote** para utilizar a mesma variável e utilize a variável para o caminho do suporte de dados no passo **Atualizar Sistema Operativo** .  

-   Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada passo **Transferir Conteúdo do Pacote** para utilizar a mesma variável e utilize a variável para o valor **Conteúdo de teste** na secção de controladores no passo **Atualizar Sistema Operativo**.  

> [!NOTE]    
> Ao implementar uma sequência de tarefas que contém o passo transferir conteúdo do pacote, não selecione **transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas** para **opções de implementação** no **pontos de distribuição** página do Assistente de implementação de Software.  

Este passo é executado num sistema operativo padrão ou no Windows PE. No entanto, a opção para guardar o pacote na cache do cliente do Configuration Manager não é suportada no WinPE.

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifica um nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Fornece informações mais detalhadas sobre a ação executada neste passo.  

 Ícone **Selecionar pacote**  
 Clique no ícone para selecionar o pacote a transferir. Depois de selecionar um pacote, pode clicar no ícone novamente para escolher outro.  

 **Colocar na seguinte localização**  
 Guarde o pacote numa das seguintes localizações:  

 -   **Diretório de trabalho de sequência de tarefas**  

 -   **Cache do cliente do Configuration Manager**: Utilize esta opção para armazenar o conteúdo na cache de clientes. Isto permite que o cliente atue como uma origem de cache ponto a ponto para outros clientes de cache ponto a ponto. Para obter mais informações, consulte [cache ponto a ponto de preparar o Windows PE para reduzir o tráfego WAN](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -   **Caminho personalizado**  

 **Guardar caminho como uma variável**  
 É possível guardar o caminho como uma variável que pode utilizar noutro passo de sequência de tarefas. Gestor de configuração adiciona um sufixo numérico ao nome da variável. Por exemplo, se especificar uma variável de %*omeuconteúdo*% como uma variável personalizada, é a raiz para armazenar todos os conteúdos referenciados (que pode ser vários pacotes). Quando fizer referência à variável, irá adicionar um sufixo numérico para a variável. Por exemplo, para o primeiro pacote, irá referir-se a %*osmeusconteúdos01*variável %. Quando fizer referência à variável num passos subsequentes, tais como atualizar sistema operativo, teria de utilizar %*osmeusconteúdos02*% ou %*mycontent03*% onde o número corresponde à ordem na qual o pacote está listado no passo.  

 **Se a transferência de um pacote falhar, continue a transferir os outros pacotes na lista**  
 Especifica que, se a transferência do pacote falhar, irá para o pacote seguinte da lista e iniciará a transferência.  

##  <a name="BKMK_EnableBitLocker"></a>Ativar o BitLocker  
 Utilize o passo de sequência de tarefas **Ativar BitLocker** para ativar a encriptação BitLocker em, pelo menos, duas partições no disco rígido. A primeira partição ativa contém o código de arranque do sistema do Windows. Outra partição contém o sistema operativo. A partição de arranque do sistema tem de permanecer desencriptada.  

 Utilize o passo de sequência de tarefas **Provisão prévia do BitLocker** para ativar o BitLocker numa unidade no Windows PE. Para obter mais informações, veja a secção [Provisão prévia do BitLocker](#BKMK_PreProvisionBitLocker) deste tópico.  

> [!NOTE]  
>  A encriptação de unidade BitLocker fornece encriptação de baixo nível do conteúdo de um volume do disco.  

 O passo **Ativar BitLocker** é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Ativar BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

 O Trusted Platform Module (TPM) tem de estar no seguinte estado quando especificar **Apenas TPM**, **TPM e Chave de Arranque em USB** ou **TPM e PIN**, para poder executar o passo **Ativar BitLocker**:  

-   Ativado  

-   Ativado  

-   Propriedade Permitida  

 O passo de sequência de tarefas pode concluir qualquer inicialização de TPM restante, porque os passos restantes não requerem presença física ou reinícios. Os passos de inicialização de TPM restantes que podem ser concluídos de forma transparente pelo passo **Ativar BitLocker** (se necessário) incluem:  

-   Criar par de chaves de endossamento  

-   Criar valor de autorização do proprietário e efetuar caução para o Active Directory, expandido para suportar este valor  

-   Obter propriedade  

-   Criar SRK (Storage Root Key) ou repor se já existir mas for incompatível  

 Se pretender que o passo **Ativar BitLocker** aguarde pela conclusão do processo de encriptação da unidade antes de prosseguir para o passo seguinte na sequência de tarefas, selecione a caixa de verificação **Aguardar**. Se não selecionar a caixa de verificação **Aguardar**, o processo de encriptação da unidade será realizado em segundo plano e a execução da sequência de tarefas prosseguirá de imediato para o passo seguinte.  

 O BitLocker pode ser utilizado para encriptar várias unidades num sistema informático (sistema operativo e unidades de dados). Para encriptar uma unidade de dados, o sistema operativo já tem de estar encriptado e o processo de encriptação tem de estar concluído, porque os protetores de chave das unidades de dados estão armazenados na unidade do sistema operativo. Como resultado, se encriptar a unidade do sistema operativo e a unidade de dados no mesmo processo, a opção de aguardar tem de ser selecionada para o passo que ativa o BitLocker para a unidade do sistema operativo.  

 Se o disco rígido já estiver encriptado mas o BitLocker estiver desativado, o passo Ativar BitLocker reativa os protetores de chave e será concluído quase instantaneamente. A reencriptação do disco rígido não é necessária neste caso.  

 Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Ativar BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifica um nome descritivo para este passo de sequência de tarefas.  

 **Descrição**  
 Permite introduzir opcionalmente uma descrição para este passo de sequência de tarefas.  

 **Selecione a unidade a encriptar**  
 Especifica a unidade a encriptar. Para encriptar a unidade do sistema operativo atual, selecione **Unidade do sistema operativo atual** e, em seguida, configure uma das seguintes opções para a gestão de chaves:  

-   **Apenas TPM**: Selecione esta opção para utilizar apenas Trusted Platform Module (TPM).  

-   **Chave de arranque em USB apenas**: Selecione esta opção para utilizar uma chave de arranque armazenada numa pen USB. Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até um dispositivo USB com uma chave de arranque BitLocker ser ligado ao computador.  

-   **TPM e chave de arranque em USB**: Selecione esta opção para utilizar o TPM e uma chave de arranque armazenada numa pen USB. Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até um dispositivo USB com uma chave de arranque BitLocker ser ligado ao computador.  

-   **TPM e PIN**:  Selecione esta opção para utilizar o TPM e um número de identificação pessoal (PIN). Ao selecionar esta opção, o BitLocker bloqueia o processo de arranque normal até o utilizador fornecer o PIN.  

 Para encriptar uma unidade de dados específica, não pertencente ao sistema operativo, selecione **Unidade específica** e, em seguida, selecione a unidade a partir da lista.  

 **Selecione onde criar a chave de recuperação**  
 Para especificar onde será criada a palavra-passe de recuperação, selecione **No Active Directory** para fazer a caução da palavra-passe no Active Directory. Se selecionar esta opção, tem de expandir o Active Directory para o site, para que as informações de recuperação do BitLocker associadas sejam guardadas. Pode optar por não criar uma palavra-passe, selecionando **Não criar chave de recuperação**. No entanto, criar uma palavra-passe é uma melhor prática.  

 **Aguarde que o BitLocker conclua o processo de encriptação de unidade em todas as unidades antes da execução de sequência de tarefas continuar**  
 Selecione esta opção para permitir que a encriptação de unidade BitLocker seja concluída antes da execução do passo seguinte na sequência de tarefas. Se esta opção estiver selecionada, todo o volume do disco será encriptado para que o utilizador consiga iniciar sessão no computador.  

 O processo de encriptação pode demorar horas a ser concluído quando está a ser encriptado um disco rígido grande. A não seleção desta opção permitirá continuar a sequência de tarefas de imediato.  

##  <a name="BKMK_FormatandPartitionDisk"></a>Formatar e particionar disco  
 Utilize o passo de sequência de tarefas **Formatar e Particionar Disco** para formatar e particionar um disco especificado no computador de destino.  

> [!IMPORTANT]  
>  Cada definição que especificar para este passo de sequência de tarefas aplica-se a um único disco especificado. Se pretender formatar e particionar outro disco no computador de destino, tem de adicionar um passo de sequência de tarefas **Formatar e Particionar Disco** adicional à sequência de tarefas.  

 Este passo de sequência de tarefas é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação, veja [Variáveis de Ação da Sequência de Tarefas Formatar e Particionar Disco](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Número do disco**  
 O número do disco físico do disco que será formatado. O número é baseado na ordem de enumeração de discos do Windows.  

 **Tipo de disco**  
 O tipo do disco formatado. Existem duas opções disponíveis para seleção na lista pendente:  

-   Padrão (MBR) - registo de arranque principal.  

-   GPT - tabela de partições GUID  

> [!NOTE]  
>  Se alterar o tipo de disco de **Padrão (MBR)** para **GPT** e o esquema de partição tiver uma partição expandida, todas as partições expandidas e lógicas serão removidas do esquema. Ser-lhe-á pedido para confirmar esta ação antes de alterar o tipo de disco.  

 **Volume**  
 Informações específicas sobre a partição ou o volume que será criado, incluindo as seguintes:  

-   Nome  

-   Espaço em disco restante  

 Para criar uma nova partição, clique em **Novo** para iniciar a caixa de diálogo **Propriedades de Partição**. Pode especificar o tipo e o tamanho da partição, e se será uma partição de arranque. Para modificar uma partição existente, clique na partição que pretende modificar e, em seguida, clique no botão de propriedades. Para mais informações sobre como configurar partições de discos rígidos, consulte um dos seguintes artigos:  

-   [Como configurar partições de disco rígido baseadas em UEFI/GPT](http://go.microsoft.com/fwlink/?LinkID=272104)  

-   [Como configurar partições de disco rígido baseados em BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

 Para eliminar uma partição, selecione a partição que pretende eliminar e clique em **Eliminar**.  

##  <a name="BKMK_InstallApplication"></a>Instalar a aplicação  
 Utilize o passo de sequência de tarefas **Instalar Aplicação** para instalar aplicações como parte da sequência de tarefas. Este passo pode instalar um conjunto de aplicações especificadas pelo passo de sequência de tarefas ou um conjunto de aplicações especificadas por uma lista dinâmica de variáveis de sequência de tarefas. Quando este passo é executado, a instalação da aplicação começa de imediato, sem aguardar por um intervalo de consulta da política.  

 A aplicação instalada tem de cumprir os seguintes critérios:  

-   Esta aplicação tem de ser um tipo de implementação do Windows Installer ou instalador de Script. Os tipos de implementação do pacote de aplicação do Windows (ficheiro .appx) não são suportados.  

-   Tem de ser executada na conta do sistema local e não na conta de utilizador.  

-   Não pode interagir com o ambiente de trabalho. O programa tem de ser executado no modo silencioso ou no modo automático.  

-   Não pode iniciar um reinício por si só. A aplicação tem de solicitar um reinício utilizando o código de reinício padrão, um código de saída 3010. Isto assegura que o passo de sequência de tarefas processará o reinício corretamente. Se a aplicação devolver um código de saída 3010, o motor de sequência de tarefas subjacente executa o reinício. Após o reinício, a sequência de tarefas continua automaticamente.  

 Quando o passo **Instalar Aplicação** é executado, a aplicação verifica a aplicabilidade das regras de requisitos e o método de deteção nos tipos de implementação da aplicação. Com base nos resultados desta verificação, a aplicação instala o tipo de implementação aplicável. Se um tipo de implementação tiver dependências, o tipo de implementação dependente é avaliado e instalado como parte do passo de instalação da aplicação. As dependências da aplicação não são suportadas no suporte de dados autónomo.  

> [!NOTE]  
>  Para instalar uma aplicação que substitui outra aplicação, os ficheiros de conteúdo da aplicação substituída têm de estar disponíveis ou o passo de sequência de tarefas falhará. Por exemplo, o Microsoft Visio 2010 é instalado num cliente ou numa imagem capturada. Quando o passo de sequência de tarefas Instalar Aplicação é executado para instalar o Microsoft Visio 2013, os ficheiros de conteúdo do Microsoft Visio 2010 (a aplicação substituída) têm de estar disponíveis num ponto de distribuição ou a sequência de tarefas falhará. Um cliente ou imagem capturada sem o Microsoft Visio instalado concluirá a instalação do Microsoft Visio 2013 sem verificar os ficheiros de conteúdo do Microsoft Visio 2010.  

> [!NOTE]
> Pode utilizar o SMSTSMPListRequestTimeoutEnabled e lista de pontos de variáveis incorporadas de SMSTSMPListRequestTimeout para ativar e especificar quantos milissegundos uma sequência de tarefas aguarda antes de tentar para instalar uma aplicação ou software da atualização após a falha ao obter a gestão dos serviços de localização. Para obter mais informações, consulte [varliables incorporadas de sequência de tarefas](task-sequence-built-in-variables.md).

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   especificar para repetir este passo se o computador reiniciar inesperadamente. Também pode especificar o número de vezes a repetir após o computador reiniciar.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Instale as seguintes aplicações**  
 Esta definição especifica as aplicações instaladas pela ordem que estão especificadas.  

 O Configuration Manager filtrará quaisquer aplicações desativadas ou aplicações com as seguintes definições. Estas aplicações não serão apresentadas na caixa de diálogo **Selecionar a aplicação a instalar**.  

-   Apenas quando um utilizador tiver sessão iniciada  

-   Executar com direitos de utilizador  

 **Instalar aplicações de acordo com a lista de variáveis dinâmicas**  
 Esta definição especifica o nome base de um conjunto de variáveis de sequência de tarefas definidas para uma coleção ou um computador. Estas variáveis especificam as aplicações que serão instaladas para essa coleção ou computador. Cada nome de variável é constituído pelo nome base comum e um sufixo numérico a partir de 01. O valor de cada variável tem de conter o nome da aplicação e mais nada.  

 Para as aplicações sejam instaladas através da utilização de uma lista de variáveis dinâmicas, a definição seguinte tem de ser ativada no **geral** separador da aplicação **propriedades** caixa de diálogo: **Permitir que esta aplicação ser instalado a partir da ação de sequência de tarefas instalar aplicação, sem ser implementada**  

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

 As seguintes condições afetarão o que é instalado:  

-   O valor de uma variável contém quaisquer informações além do nome da aplicação. Essa aplicação não é instalada e a sequência de tarefas continua.  

-   Se não for encontrada nenhuma variável com o nome base especificado nem o sufixo "01", não é instalada nenhuma aplicação. Quando seleciona **continuar com o erro** no separador Opções do passo de sequência de tarefas, a sequência de tarefas continua quando a instalação de uma aplicação falha. Quando a definição não estiver selecionada, a sequência de tarefas falha e não instalará as restantes aplicações.  

 **Se uma aplicação falhar, continue a instalar outras aplicações na lista**  
 Esta definição especifica que o passo continuará se a instalação de uma aplicação individual falhar. Se esta definição for especificada, a sequência de tarefas continuará independentemente de quaisquer erros de instalação devolvidos. Se não for especificada, a instalação falhará e a sequência de tarefas terminará de imediato.  

##  <a name="BKMK_InstallDeploymentTools"></a>Instalar ferramentas de implementação  
 Utilize o **instalar ferramentas de implementação** passo de sequência de tarefas para instalar o pacote de Configuration Manager que contém as ferramentas de implementação Sysprep.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Pacote Sysprep**  
 Esta definição especifica o pacote de Configuration Manager que contém as ferramentas de implementação Sysprep para os seguintes sistemas operativos:  

-   Windows XP SP3  

-   Windows XP X64 SP2  

-   Windows Server 2003 SP2  

##  <a name="BKMK_InstallPackage"></a>Instalar pacote

 Utilize o passo de sequência de tarefas **Instalar Pacote** para instalar software como parte da sequência de tarefas. Quando este passo é executado, a instalação começa de imediato, sem aguardar por um intervalo de consulta da política.  

 O software instalado tem de cumprir os seguintes critérios:  

-   Tem de ser executada na conta do sistema local e não na conta de utilizador.  

-   Não deve interagir com o ambiente de trabalho. O programa tem de ser executado no modo silencioso ou no modo automático.  

-   Não pode iniciar um reinício por si só. O software tem de solicitar um reinício utilizando o código de reinício padrão, um código de saída 3010. Isto assegura que o passo de sequência de tarefas processará o reinício corretamente. Se o software devolver um código de saída 3010, o motor de sequência de tarefas subjacente executará o reinício. Após o reinício, a sequência de tarefas continuará automaticamente.  

 Os programas que utilizam a opção **Executar outro programa primeiro** para instalar um programa dependente não são suportados quando implementar um sistema operativo. Se a opção **Executar outro programa primeiro** estiver ativada para o software e o programa dependente já tiver sido executado no computador de destino, o programa dependente será executado e a sequência de tarefas continuará. No entanto, se o programa dependente ainda não tiver sido executado no computador de destino, o passo de sequência de tarefas falhará.  

> [!NOTE]  
>  O site de administração central não possui as políticas de configuração de cliente necessárias para ativar o agente de distribuição de software durante a execução da sequência de tarefas. Quando cria um suporte de dados autónomo para uma sequência de tarefas do site de administração central e a sequência de tarefas inclui um passo **Instalar Pacote**, pode aparecer o erro seguinte no ficheiro CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  No caso de suportes de dados autónomos que incluem um passo Instalar Pacote, tem de criar o suporte de dados autónomo num site primário com o agente de distribuição de software ativado ou adicionar um passo **Executar Linha de Comandos** a seguir ao passo **Configurar Windows e ConfigMgr** e antes do primeiro passo **Instalar Pacote**. O passo **Executar Linha de Comandos** executa um comando WMIC para ativar o agente de distribuição de software antes da execução do primeiro passo Instalar Pacote. Pode utilizar o seguinte no passo da sequência de tarefas **Executar Linha de Comandos** :  
>   
>  **Linha de comandos**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig caminho ccm_SoftwareDistributionClientConfig criar ComponentName = "Ativar SWDist", ativado = "true", LockSettings = "TRUE", PolicySource = "local", PolicyVersion = "1.0" SiteSettingsKey = "1" /NOINTERACTIVE**  
>   
>  Para obter mais informações sobre como criar suportes de dados autónomos, consulte [criar suportes de dados autónomos](../deploy-use/create-stand-alone-media.md).  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Instalar um único pacote de software**  
 Esta definição especifica um pacote de software do Configuration Manager. O passo aguardará pela conclusão da instalação.  

 **Instalar pacotes de software, de acordo com a lista de variável dinâmicas**  
 Esta definição especifica o nome base de um conjunto de variáveis de sequência de tarefas definidas para uma coleção ou um computador. Estas variáveis especificam os pacotes que serão instalados para essa coleção ou computador. Cada nome de variável é constituído pelo nome base comum e um sufixo numérico a partir de 001. O valor de cada variável tem de conter um ID de pacote e o nome do software separados por dois pontos.  

 Para o software seja instalado utilizando uma lista de variáveis dinâmicas, a definição seguinte tem de estar ativada no **avançadas** separador do pacote **propriedades** caixa de diálogo: **Permitir que este programa ser instalado a partir da sequência de tarefas Instalar pacote sem ser implementada**  

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

 As seguintes condições afetarão o que é instalado:  

-   Se o valor de uma variável não for criado no formato correto ou não especificar um ID e um nome de aplicação válidos, a instalação do software falhará.  

-   Se o ID do pacote incluir carateres minúsculos, a instalação desse software falhará.  

-   Se não for encontrada nenhuma variável com o nome base especificado nem o sufixo "001", não é instalado nenhum pacote e a sequência de tarefas continuará.  

 **Se a instalação de um pacote de software falhar, continue a instalar outros pacotes na lista**  
 Esta definição especifica que o passo continuará se a instalação de um pacote de software individual falhar. Se esta definição for especificada, a sequência de tarefas continuará independentemente de quaisquer erros de instalação devolvidos. Se não for especificada, a instalação falhará e a sequência de tarefas terminará de imediato.  

##  <a name="BKMK_InstallSoftwareUpdates"></a>Instalar atualizações de Software  
 Utilize o passo de sequência de tarefas **Instalar Atualizações de Software** para instalar atualizações de software no computador de destino. O computador de destino não é avaliado relativamente a atualizações de software aplicáveis até ser executado este passo de sequência de tarefas. Nessa altura, o computador de destino é avaliado relativamente a atualizações de software como qualquer outro cliente gerido pelo Configuration Manager. Em particular, este passo instala apenas as atualizações de software direcionadas para coleções das quais o computador é atualmente membro.  
>  [!IMPORTANT]
>Recomendamos vivamente que instale a versão mais recente do Windows Update Agent para um melhor desempenho ao utilizar o passo de sequência de tarefas instalar atualizações de Software.
>* Para Windows 7, veja o [Artigo da Base de dados de conhecimento 3161647](https://support.microsoft.com/kb/3161647).
>* Para Windows 8, veja o [Artigo da Base de dados de conhecimento 3163023](https://support.microsoft.com/kb/3163023).

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Instalar Atualizações de Software](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Pode utilizar o SMSTSMPListRequestTimeoutEnabled e lista de pontos de variáveis incorporadas de SMSTSMPListRequestTimeout para ativar e especificar quantos milissegundos uma sequência de tarefas aguarda antes de tentar para instalar uma aplicação ou software da atualização após a falha ao obter a gestão dos serviços de localização. Para obter mais informações, consulte [variáveis incorporadas de sequência de tarefas](task-sequence-built-in-variables.md).

> [!NOTE]
>No separador de opções, pode configurar esta sequência de tarefas para repetir se o computador reiniciar inesperadamente. Por exemplo, a instalação de uma atualização de software que reinicia automaticamente o computador. A partir do Configuration Manager 1602, pode configurar a variável de SMSTSWaitForSecondReboot para especificar o período de tempo (em segundos) a sequência de tarefas deve colocar em pausa depois de reiniciar o computador ao instalar as atualizações de software. Para obter mais informações, consulte [variáveis incorporadas de sequência de tarefas](task-sequence-built-in-variables.md).

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   especificar para repetir este passo se o computador reiniciar inesperadamente. Também pode especificar o número de vezes a repetir após o computador reiniciar.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Necessário para instalação - apenas atualizações de software obrigatórias**  
 Selecione esta opção para instalar todas as atualizações de software sinalizadas no Configuration Manager como obrigatórias para os computadores de destino que recebem a sequência de tarefas. As atualizações de software obrigatórias têm prazos de instalação definidos pelo administrador.  

 **Disponível para instalação - todas as atualizações de software**  
 Selecione esta opção para instalar todas as atualizações de software disponível direcionadas para a coleção do Configuration Manager que receberá a sequência de tarefas. Todas as atualizações de software disponíveis serão instaladas nos computadores de destino.  

 **Avaliar atualizações de software a partir dos resultados de análise em cache**  
A partir do Configuration Manager versão 1606, terá a opção de realizar uma pesquisa completa de atualizações de software em vez de utilizar os resultados da análise em cache. Por predefinição, a sequência de tarefas utiliza resultados em cache. Pode desmarcar a caixa de verificação para que o cliente estabeleça ligação ao ponto de atualização de software para processar e transferir o catálogo de atualizações de software mais recente. Poderá escolher esta opção quando utiliza uma sequência de tarefas para [capturar e compilar uma imagem do sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md), onde sabe que haverá um grande número de atualizações de software, especialmente muitas que têm dependências (necessidade de instalar X antes de Y irá aparecer como aplicável). Ao desmarcar esta definição e implementar a sequência de tarefas para um grande número de clientes, todos serão ligados ao ponto de atualização de software ao mesmo tempo. Isto poderá dar origem a problemas de desempenho durante o processo e a transferência do catálogo. Na maioria dos casos, recomendamos que utilize a predefinição.

Uma nova variável de sequência de tarefas, SMSTSSoftwareUpdateScanTimeout, foi introduzida no Configuration Manager versão 1606 para lhe dar a capacidade de controlar o tempo limite da pesquisa de atualizações de software durante o passo de sequência de tarefas Instalar atualizações de software. O valor predefinido é 30 minutos. Para obter mais informações, consulte [variáveis incorporadas de sequência de tarefas](task-sequence-built-in-variables.md).


##  <a name="BKMK_JoinDomainorWorkgroup"></a>Associar domínio ou grupo de trabalho  
 Utilize o passo de sequência de tarefas **Associar Domínio ou Grupo de Trabalho** para adicionar o computador de destino a um grupo de trabalho ou domínio.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Associar Domínio ou Grupo de Trabalho](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Aderir a um grupo de trabalho**  
 Selecione esta opção para associar o computador de destino ao grupo de trabalho especificado. Se o computador for atualmente membro de um domínio, a seleção desta opção causará o reinício do computador.  

 **Aderir a um domínio**  
 Selecione esta opção para associar o computador de destino ao domínio especificado.  

 Opcionalmente, introduza ou procure uma unidade organizacional (UO) no domínio especificado para o computador ser associado. Se o computador for atualmente membro de outro domínio ou grupo de trabalho, isto causará o reinício do computador. Se o computador já for membro de outra UO, o Active Directory Domain Services não permite a alteração da UO e esta definição é ignorada.  

 **Introduza a conta que tenha permissão para aderir ao domínio**  
 Clique em **Definir** para introduzir uma conta e uma palavra-passe com permissões para ser associada ao domínio. A conta tem de ser introduzida no seguinte formato:  

 *Domínio \ conta*  

## <a name="BKMK_PrepareConfigMgrClientforCapture"></a>Preparar ConfigMgr Client para captura  
Utilize o **preparar ConfigMgr Client para captura** passo para remover o cliente do Configuration Manager ou configurar o cliente no computador de referência para o preparar para captura como parte do processamento de imagens.

A partir do Configuration Manager versão 1610, o passo de preparar ConfigMgr Client remove completamente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas, implementa a imagem do sistema operativo capturada, instalará um novo cliente de Configuration Manager cada vez.  

Antes do Configuration Manager versão 1610, este passo efetua as seguintes tarefas:  

-   Remove a secção de propriedades de configuração do cliente do ficheiro smscfg.ini no diretório do Windows. Estas propriedades incluem informações específicas do cliente, incluindo o GUID de Configuration Manager e outros identificadores do cliente.  

-   Elimina todos os certificados SMS ou o Configuration Manager da máquina.  

-   Elimina a cache do cliente do Configuration Manager.  

-   Limpa a variável de site atribuído do cliente do Configuration Manager.  

-   Elimina todas as política local do Configuration Manager.  

-   Remove a chave de raiz fidedigna para o cliente do Configuration Manager.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

##  <a name="BKMK_PrepareWindowsforCapture"></a>Preparar Windows para captura  
 Utilize o passo de sequência de tarefas **Preparar Windows para Captura** para especificar as opções do Sysprep a utilizar ao capturar uma imagem do sistema operativo no computador de referência. Esta ação de sequência de tarefas executa o Sysprep e, em seguida, reinicia o computador na imagem de arranque do Windows PE especificada para a sequência de tarefas. O computador de referência não deve ser associado a um domínio para que esta ação seja concluída com êxito.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Preparar Windows para Captura](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Compilar automaticamente a lista de controladores de armazenamento em massa**  
 Selecione esta opção para o Sysprep compilar automaticamente uma lista de controladores de armazenamento em massa a partir do computador de referência. Esta opção ativa a opção Compilar Controladores de Armazenamento em Massa no ficheiro sysprep.inf no computador de referência. Para mais informações sobre esta definição, consulte a documentação do Sysprep.  

 **Repor o sinalizador de ativação**  
 Selecione esta opção para impedir o Sysprep de repor o sinalizador de ativação do produto.  

##  <a name="BKMK_PreProvisionBitLocker"></a>Provisão prévia do BitLocker  
 Utilize o passo de sequência de tarefas **Provisão prévia do BitLocker** para ativar o BitLocker numa unidade no Windows PE. Apenas o espaço de disco utilizado é encriptado e, portanto, os tempos de encriptação são muito mais rápidos. Aplique as opções de gestão de chaves utilizando o passo de sequência de tarefas [Ativar BitLocker](#BKMK_EnableBitLocker) após a instalação do sistema operativo. Este passo é executado apenas no Windows PE. Não é executado num sistema operativo padrão.  

> [!IMPORTANT]  
>  Para pré-aprovisionar o BitLocker, tem de implementar um sistema operativo mínimo do Windows 7 e o TPM tem de ser suportado e ativado no computador.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifique um nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Especifique informações detalhadas sobre a ação executada neste passo.  

 **Aplicar BitLocker ao drive especificado**  
 Especifique a unidade para a qual pretende ativar o BitLocker. Apenas o espaço utilizado na unidade é encriptado.  

 **Ignore este passo em computadores que não têm TPM ou quando o TPM não está ativado**  
 Selecione esta opção para ignorar a encriptação da unidade quando o hardware do computador não suportar o TPM ou quando o TPM não estiver ativado. Por exemplo, pode utilizar esta opção ao implementar um sistema operativo numa máquina virtual.  

##  <a name="BKMK_ReleaseStateStore"></a>Disponibilizar armazenamento de Estados  
 Utilize o passo de sequência de tarefas **Disponibilizar Armazenamento de Estados** para notificar o ponto de migração de estado de que a ação de captura ou restauro está concluída. Este passo é utilizado em conjunto com os passos de sequência de tarefas **Solicitar Armazenamento de Estados**, **Capturar Estado do Utilizador** e **Restaurar Estado do Utilizador** para migrar os dados de estado do utilizador com um ponto de migração de estado e o User State Migration Tool (USMT).  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

 Se tiver solicitado acesso a um ponto de migração de estado para capturar o estado do utilizador no passo de sequência de tarefas **Solicitar Armazenamento de Estados**, este passo notifica o ponto de migração de estado de que o processo de captura está concluído e de que os dados de estado do utilizador estão disponíveis para serem restaurados. O ponto de migração de estado define as permissões de controlo de acesso para o estado capturado, para que apenas possa ser acedido (como só de leitura) pelo computador de restauro.  

 Se tiver solicitado acesso a um ponto de migração de estado para restaurar o estado do utilizador no passo de sequência de tarefas **Solicitar Armazenamento de Estados**, este passo notifica o ponto de migração de estado de que o processo de restauro está concluído. Nesta altura, são ativadas as definições de retenção que tiver configurado para o ponto de migração de estado.  

> [!IMPORTANT]  
>  Uma melhor prática é definir **Continuar com o erro** em quaisquer passos de sequência de tarefas entre os passos **Solicitar Armazenamento de Estados** e **Disponibilizar Armazenamento de Estados**, para que todas as ações de sequência de tarefas **Solicitar Armazenamento de Estados** tenham uma ação de sequência de tarefas **Disponibilizar Armazenamento de Estados** correspondente.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência Disponibilizar Armazenamento de Estados](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

##  <a name="BKMK_RequestStateStore"></a>Solicitar armazenamento de Estados  
 Utilize o passo de sequência de tarefas **Solicitar Armazenamento de Estados** para solicitar acesso a um ponto de migração de estado ao capturar o estado de um computador ou ao restaurar o estado para um computador.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

 Pode utilizar o passo de sequência de tarefas **Solicitar Armazenamento de Estados** em conjunto com os passos de sequência de tarefas **Disponibilizar Armazenamento de Estados**, **Capturar Estado do Utilizador** e **Restaurar Estado do Utilizador**, para migrar o estado do computador com um ponto de migração de estado e o User State Migration Tool (USMT).  

> [!NOTE]  
>  Se tiver acabado de estabelecer uma nova função de sites do ponto de migração de estado (SMP), pode demorar até uma hora a estar disponível para armazenamento do estado do utilizador. Para agilizar a disponibilidade do SMP, pode ajustar qualquer definição de propriedade do ponto de migração de estado para acionar uma atualização do ficheiro de controlo do site.  

 Este passo de sequência de tarefas é executado num sistema operativo padrão e no Windows PE para o USMT offline. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Solicitar Armazenamento de Estados](task-sequence-action-variables.md#BKMK_RequestState).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Capturar estado do computador**  
 Localiza um ponto de migração de estado que cumpre os requisitos mínimos, conforme configurado nas definições do ponto de migração de estado (número máximo de clientes e quantidade mínima de espaço livre em disco), mas não garante que esteja disponível espaço suficiente no momento da migração de estado. A seleção desta opção solicitará acesso ao ponto de migração de estado para capturar o estado e as definições de utilizador de um computador.  

 Se o site do Configuration Manager tiver vários pontos de migração de estado ativados, este passo de sequência de tarefas localiza um ponto de migração de estado com espaço em disco disponível consultando o ponto de gestão do site para obter uma lista dos pontos de migração de estado e, em seguida, avaliando cada um até encontrar um que cumpra os requisitos mínimos.  

 **Restaurar estado a partir de outro computador**  
 Selecione esta opção para solicitar acesso a um ponto de migração de estado para restaurar o estado e as definições de utilizador capturados anteriormente para um computador de destino.  

 Se o site do Configuration Manager tiver vários pontos de migração de estado, este passo de sequência de tarefas localiza o ponto de migração de estado que possui o estado do computador armazenado para o computador de destino.  

 **Número de tentativas**  
 Número de vezes que este passo de sequência de tarefas tentará localizar um ponto de migração de estado adequado antes de falhar.  

 **Intervalo de repetição (em segundos)**  
 Período de tempo em segundos que o passo de sequência de tarefas aguarda entre as tentativas.  

 **Se a conta de computador falhar a ligação ao armazenamento de Estados, utilize a conta de acesso de rede.**  
 Especifica que as credenciais de conta de acesso de rede do Configuration Manager irão ser utilizadas para ligar ao ponto de migração de estado se o cliente do Configuration Manager não é possível aceder ao armazenamento de estado SMP com a conta de computador. Esta opção é menos segura porque outros computadores poderão utilizar a conta de acesso à rede para aceder ao estado armazenado, mas pode ser necessária se o computador de destino não estiver associado ao domínio.  

##  <a name="BKMK_RestartComputer"></a>Reiniciar computador  
 Utilize o passo de sequência de tarefas **Reiniciar Computador** para reiniciar o computador que está a executar a sequência de tarefas. Após o reinício, o computador prosseguirá automaticamente para o passo seguinte na sequência de tarefas.  

 Este passo pode ser executado num sistema operativo padrão ou no Windows PE. Para obter mais informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, consulte [reiniciar variáveis de ação de sequência de tarefas do computador](task-sequence-action-variables.md#BKMK_RestartComputer).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **A imagem de arranque atribuída a esta sequência de tarefas**  
 Selecione esta opção para o computador de destino utilizar a imagem de arranque atribuída à sequência de tarefas. A imagem de arranque será utilizada para executar passos de sequência de tarefas subsequentes executados no Windows PE.  

 **O sistema operativo predefinido atualmente instalado**  
 Selecione esta opção para o computador de destino ser reiniciado no sistema operativo instalado.  

 **Notificar o utilizador antes de reiniciar**  
 Selecione esta opção para apresentar uma notificação ao utilizador a informar que o computador de destino será reiniciado. Esta opção está selecionada por predefinição.  

 **Mensagem de notificação**  
 Introduza uma mensagem de notificação que será apresentada ao utilizador antes de o computador de destino ser reiniciado.  

 **Tempo limite de visualização da mensagem**  
 Especifique o período de tempo em segundos concedido a um utilizador antes de o computador de destino ser reiniciado. O período de tempo predefinido é sessenta (60) segundos.  

##  <a name="BKMK_RestoreUserState"></a>Restaurar estado do utilizador  
 Utilize o passo de sequência de tarefas **Restaurar Estado do Utilizador** para iniciar o User State Migration Tool (USMT) para restaurar o estado e as definições de utilizador para o computador de destino. Este passo de sequência de tarefas é utilizado em conjunto com o passo de sequência de tarefas **Capturar Estado do Utilizador**.  

 Para obter mais informações sobre como gerir o estado do utilizador ao implementar sistemas operativos, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

 Também pode utilizar o **restaurar estado do utilizador** passo de sequência de tarefas com o **solicitar armazenamento de Estados** e **disponibilizar armazenamento de Estados** passos de sequência de tarefas se pretender guardar as definições de estado ou restaurar definições a partir de uma migração de estado para o ponto no site do Configuration Manager. Com o USMT 3.0 e superior, esta opção desencripta sempre o armazenamento de Estados do USMT através de uma chave de encriptação gerada e gerida pelo Configuration Manager.  

 O passo de sequência de tarefas **Restaurar Estado do Utilizador** fornece controlo sobre um subconjunto limitado das opções mais utilizadas pelo USMT. Podem ser especificadas opções da linha de comandos adicionais através da variável de sequência de tarefas OSDMigrateAdditionalRestoreOptions.  

> [!IMPORTANT]  
>  Se estiver a utilizar o passo de sequência de tarefas **Restaurar Estado do Utilizador** para um objetivo não relacionado com um cenário de implementação de sistema operativo, adicione o passo de sequência de tarefas [Reiniciar Computador](#BKMK_RestartComputer) imediatamente a seguir ao passo de sequência de tarefas **Restaurar Estado do Utilizador**.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Restaurar Estado do Utilizador](task-sequence-action-variables.md#BKMK_RestoreUserState).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifica um nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Especifica informações mais detalhadas sobre a ação executada neste passo.  

 **Pacote de ferramenta de migração de estado de utilizador**  
 Introduza o pacote de Configuration Manager que contém a versão do USMT para este passo a utilizar ao restaurar o estado do utilizador e as definições. Este pacote não requer um programa. Quando o passo de sequência de tarefas for executado, a sequência de tarefas utilizará a versão do USMT no pacote especificado. Especifique um pacote com a versão de 32 bits ou x64 do USMT, consoante a arquitetura do sistema operativo para o qual está a restaurar o estado.  

 **Restaurar todos os perfis de utilizador capturados com opções padrão**  
 Restaura todos os perfis de utilizador capturados com as opções padrão. Para personalizar as opções que serão restauradas, selecione **Personalizar captura de perfil do utilizador**.  

 **Personalizar como os perfis de utilizador são restaurados**  
 Permite personalizar os ficheiros que pretende restaurar para o computador de destino. Clique em **Ficheiros** para especificar os ficheiros de configuração no pacote do USMT que pretende utilizar para restaurar os perfis de utilizador. Para adicionar um ficheiro de configuração, introduza o nome do ficheiro na caixa **Nome do ficheiro** e clique em **Adicionar**. Os ficheiros de configuração que serão utilizados para a operação estão listados no painel Ficheiros. O ficheiro .xml especificado define o ficheiro de utilizador que será restaurado.  

 **Restaurar perfis de utilizador do computador local**  
 Restaura os perfis de utilizador do computador local (e não perfis de utilizador do domínio). Terá de atribuir novas palavras-passe para as contas de utilizador locais restauradas, porque as palavras-passe das contas de utilizador locais originais não podem ser migradas. Introduza a nova palavra-passe na caixa **Palavra-passe** e confirme-a na caixa **Confirmar Palavra-passe**.  

 **Continuar se não não possível restaurar alguns ficheiros**  
 Continua o restauro do estado e das definições de utilizador, mesmo se não for possível restaurar alguns ficheiros. Por predefinição, esta opção encontra-se ativada. Se desativar esta opção e forem encontrados erros ao restaurar ficheiros, o passo de sequência de tarefas terminará de imediato com uma falha e nem todos os ficheiros serão restaurados.  

 **Ativar o registo verboso**  
 Ative esta opção para gerar informações de ficheiros de registo mais detalhadas. Ao restaurar o estado, o registo Loadstate.log é gerado e armazenado por predefinição na pasta de registo da sequência de tarefas na pasta \windows\system32\ccm\logs.  

##  <a name="BKMK_RunCommandLine"></a>Executar linha de comandos  
 Utilize o passo de sequência de tarefas **Executar Linha de Comandos** para executar uma linha de comandos especificada.  

 Este passo pode ser executado num sistema operativo padrão ou no Windows PE. Para obter informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, veja [Variáveis de Ação da Sequência de Tarefas Executar Linha de Comandos](task-sequence-action-variables.md#BKMK_RunCommand).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifica um nome abreviado definido pelo utilizador que descreve a linha de comandos que é executada.  

 **Descrição**  
 Especifica informações mais detalhadas sobre a linha de comandos que é executada.  

 **Linha de comandos**  
 Especifica a linha de comandos que é executada. Este campo é obrigatório. As extensões de nome de ficheiro, incluindo são uma melhor prática, por exemplo,. vbs e .exe. Inclua todos os ficheiros de definições necessários, opções da linha de comandos ou parâmetros.  

 Se o nome de ficheiro não tiver uma extensão de nome de ficheiro especificado, o Configuration Manager tenta empresa>.com, .exe, e. bat. Se o nome do ficheiro tem uma extensão que não seja um executável, o Configuration Manager tenta aplicar uma associação local. Por exemplo, se a linha de comandos for readme.gif, o Configuration Manager inicia a aplicação especificada no computador de destino para abrir ficheiros GIF.  

 Exemplos:  

 **Setup.exe /a**  

 **cmd.exe /c cópia Jan98.dat c:\sales\Jan98.dat**  

> [!NOTE]  
>  Ações da linha de comandos, como redirecionamento de saída, encaminhamento ou cópia, como no exemplo anterior, tem de ser precedidas pelo **cmd.exe /c** comando a executar com êxito.  

 **Desativar redirecionamento de sistema de ficheiros de 64 bits**  
 Por predefinição, numa execução num sistema operativo de 64 bits, o executável na linha de comandos está localizado e é executado com o redirecionador do sistema de ficheiros WOW64, para que sejam encontradas as versões de 32 bits dos executáveis e DLLs do sistema operativo.  A seleção desta opção desativa a utilização do redirecionador do sistema de ficheiros WOW64, para que sejam encontradas as versões de 64 bits nativas dos executáveis e DLLs do sistema operativo.  A seleção desta opção não tem efeito numa execução num sistema operativo de 32 bits.  

 **Iniciar**  
 Especifica a pasta executável do programa, até 127 carateres. Esta pasta pode ser um caminho absoluto no computador de destino ou um caminho relativo para a pasta do ponto de distribuição que contém o pacote. Este campo é opcional.  

 Exemplos:  

 **c:\OfficeXP**  

 **i386**  

> [!NOTE]  
>  O botão **Procurar** procura ficheiros e pastas no computador local, pelo que tudo o que selecionar desta forma também tem de existir no computador de destino na mesma localização e com os mesmos nomes de ficheiros e pastas.  

 **Pacote**  
 Ao especificar ficheiros ou programas na linha de comandos que já não estão presentes no computador de destino, selecione esta opção para especificar o pacote de Configuration Manager que contém os ficheiros adequados. O pacote não requer um programa. Esta opção não é necessária se os ficheiros especificados existirem no computador de destino.  

 **Tempo limite**  
 Especifica um valor que representa o período de retenção do Configuration Manager irá permitir que a linha de comandos executar. Este valor pode ser de 1 minuto a 999 minutos. O valor predefinido é 15 minutos.  

 Esta opção está desativada por predefinição.  

> [!IMPORTANT]  
>  Se introduzir um valor que não permita tempo suficiente para o passo de sequência de tarefas Executar Linha de Comandos ser concluído com êxito, o passo de sequência de tarefas falhará e toda a sequência de tarefas poderá falhar, consoante as restantes definições de controlo. Se o tempo limite expirar, o Configuration Manager irá terminar o processo da linha de comandos.  

 **Executar este passo de como a seguinte conta**  
 Especifica que a linha de comandos é executada como uma conta de utilizador do Windows em vez da conta de sistema local.  

> [!NOTE]  
>  Quando especificar outra conta para este passo e ocorrer depois de um passo de instalação do sistema operativo, a conta tem de ser adicionada para o computador antes de poder executar scripts simples ou comandos e o perfil para a conta de utilizador do Windows tem de ser restaurados para executar programas mais complexos, como um MSI.  

 **Conta**  
 Especifica a conta de utilizador do Windows Run As para a tarefa da linha de comandos na sequência de tarefas a ser executada por esta ação. A linha de comandos será executada com as permissões da conta especificada. Clique em **Definir** para especificar a conta de utilizador local ou de domínio.  

> [!IMPORTANT]  
>  Se uma ação de sequência de tarefas **Executar Linha de Comandos** que especifique uma conta de utilizador for executada no Windows PE, a ação falhará porque o Windows PE não pode ser associado a um domínio. A falha será registada no ficheiro smsts.log.  

##  <a name="BKMK_RunPowerShellScript"></a>Executar Script do PowerShell  
 Utilize o passo de sequência de tarefas **Executar Script do PowerShell** para executar um script do PowerShell especificado.  

 Este passo pode ser executado num sistema operativo padrão ou no Windows PE. Para executar este passo no Windows PE, o PowerShell tem de estar ativado na imagem de arranque. Pode ativar o Windows PowerShell (WinPE-PowerShell) a partir do separador **Componentes Opcionais** nas propriedades da imagem de arranque. Para obter mais informações sobre como modificar uma imagem de arranque, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  Por predefinição, o PowerShell não está ativado nos sistemas operativos Windows Embedded.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifica um nome abreviado definido pelo utilizador que descreve a linha de comandos que é executada.  

 **Descrição**  
 Especifica informações mais detalhadas sobre a linha de comandos que é executada.  

 **Pacote**  
 Especifique o pacote de Configuration Manager que contém o script do PowerShell. Um pacote pode conter vários scripts do PowerShell.  

 **Nome do script**  
 Especifica o nome do script do PowerShell a executar. Este campo é obrigatório.  

 **Parâmetros**  
 Especifica os parâmetros a transmitir ao script do Windows PowerShell. Configure os parâmetros como se estivesse a adicioná-los ao script do Windows PowerShell a partir de uma linha de comandos.  

> [!IMPORTANT]  
>  Forneça parâmetros consumidos pelo script e não para a linha de comandos do Windows PowerShell.  
>   
>  O exemplo seguinte contém parâmetros válidos:  
>   
>  **-MyParameter1 MyValue1-MyParameter2 MyValue2**  
>   
>  O exemplo seguinte contém parâmetros inválidos. Os itens a negrito são parâmetros da linha de comandos do Windows PowerShell (-nologo e - executionpolicy sem restrições) e não são consumidos pelo script.  
>   
>  **-nologo-executionpolicy sem restrições ficheiro MyScript.ps1-MyParameter1 MyValue1-MyParameter2 MyValue2**  

 **Política de execução do PowerShell**  
 A seleção da política de execução do PowerShell permite determinar quais os scripts do Windows PowerShell (se existirem) cuja execução será permitida no computador. Escolha uma das seguintes políticas de execução:  

-   **AllSigned**: Apenas os scripts assinados por um fabricante fidedigno podem ser executados.  

-   **Indefinido**: Está definida qualquer política de execução. .  

-   **Ignorar**: Carrega todos os ficheiros de configuração e executa todos os scripts. Se executar um script não assinado transferido da Internet, não lhe é pedida permissão antes da execução.  

> [!IMPORTANT]  
>  O PowerShell 1.0 não suporta as políticas de execução Indefinido e Ignorar.  

##  <a name="BKMK_SetDynamicVariables"></a>Definir variáveis dinâmicas  
 Utilize o passo de sequência de tarefas **Definir Variáveis Dinâmicas** para fazer o seguinte:  

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

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

**Nome**  
 Nome abreviado definido pelo utilizador para este passo de sequência de tarefas.  

**Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

**Regras e variáveis dinâmicas**  
 Para definir uma variável dinâmica para utilizar na sequência de tarefas, pode adicionar uma regra e, em seguida, especificar um valor para cada variável especificada para a regra ou adicionar uma ou mais variáveis para definir sem adicionar uma regra. Ao adicionar uma regra, pode escolher de entre as seguintes categorias de regras:  

 -   **Computador**: Utilize esta categoria de regra para avaliar os valores de etiqueta de recursos, UUID, número de série ou endereço mac. Pode definir vários valores e, se qualquer valor for verdadeiro, a regra avaliará como verdadeiro. Por exemplo, a regra seguinte avalia como verdadeiro se o Número de Série for 5892087, independentemente de o endereço MAC ser 26-78-13-5A-A4-22.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Localização**: Utilize esta categoria de regra para avaliar os valores para o gateway predefinido.  

-   **Marca e modelo**: Utilize esta categoria de regra para avaliar os valores da marca e modelo de um computador. A marca e o modelo têm de avaliar como verdadeiro para a regra avaliar como verdadeiro.   

    A partir do Configuration Manager versão 1610, pode especificar um asterisco (*) e o ponto de interrogação (**?**) como os carateres universais, onde *** corresponde a vários carateres e **?** corresponde a um único caráter. Por exemplo, a cadeia "DELL * 900?" corresponderá DELL-ABC-9001 e DELL9009.

-   **Variável de sequência de tarefas**: Utilize esta categoria de regra para adicionar uma variável de sequência de tarefas, condição e valor a avaliar. A regra avalia como verdadeiro quando o conjunto de valores da variável cumpre a condição especificada.  

Pode especificar uma ou mais variáveis que serão definidas para uma regra que avalia como verdadeiro ou definir variáveis sem utilizar uma regra. Pode selecionar de entre as variáveis existentes ou criar uma variável personalizada.  

 -   **Variáveis de sequência de tarefas existente**: Utilize esta definição para selecionar uma ou mais variáveis a partir de uma lista de variáveis de sequência de tarefas existentes. As variáveis da matriz não estão disponíveis para seleção.  

 -   **As variáveis de sequência de tarefas personalizada**: Utilize esta definição para definir uma variável de sequência de tarefas personalizada. Também pode especificar uma variável de sequência de tarefas existente. Isto é útil para especificar uma matriz de variável existente, como OSDAdapter, uma vez que as matrizes de variáveis não estão na lista de variáveis de sequência de tarefas existentes.  

Depois de selecionar as variáveis para uma regra, tem de fornecer um valor para cada variável. A variável é definida para o valor especificado quando a regra avalia como verdadeiro. Para cada variável, pode selecionar **Valor secreto** para ocultar o valor da variável. Por predefinição, algumas variáveis existentes ocultam valores, como a variável de sequência de tarefas OSDCaptureAccountPassword.  

> [!IMPORTANT]  
>  Ao importar uma sequência de tarefas com o passo Definir Variáveis Dinâmicas e **Valor secreto** estiver selecionado para o valor da variável, o valor é removido quando importar a sequência de tarefas. Como resultado, tem de reintroduzir o valor para a variável dinâmica depois de importar a sequência de tarefas.  

##  <a name="BKMK_SetTaskSequenceVariable"></a>Definir variável da sequência de tarefas  
Utilize o passo de sequência de tarefas **Definir Variável da Sequência de Tarefas** para definir o valor de uma variável utilizada com a sequência de tarefas.  

Este passo pode ser executado num sistema operativo padrão ou no Windows PE. As variáveis de sequência de tarefas são lidas pelas ações de sequência de tarefas e especificam o comportamento dessas ações. Para obter mais informações sobre variáveis de sequência de tarefas específicas, consulte [variáveis de ação da sequência de tarefas](task-sequence-action-variables.md).  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador para este passo de sequência de tarefas.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Variável de sequência de tarefas**  
 Nome definido pelo utilizador para a variável da sequência de tarefas.  

 **Valor**  
 Valor associado à variável da sequência de tarefas. O valor pode ser outra variável da sequência de tarefas na sintaxe %<varname\>%.  

## <a name="hide-task-sequence-progress"></a>Ocultar o progresso da sequência de tarefas
<!-- 1354291 -->
Com o lançamento 1706, pode controlar quando o progresso da sequência de tarefas é apresentado aos utilizadores finais através da utilização de uma nova variável. Na sua sequência de tarefas, utilize o **definir variável da sequência de tarefas** passo para definir o valor para o **TSDisableProgressUI** variável para ocultar ou mostrar progresso da sequência de tarefas. Pode utilizar o passo Definir variável da sequência de tarefas múltiplas vezes numa sequência de tarefas para alterar o valor da variável. Isto permite-lhe ocultar ou mostrar progresso da sequência de tarefas nas secções diferentes da sequência de tarefas.

 - **Para ocultar o progresso da sequência de tarefas**  
No editor de sequência de tarefas, utilize o [definir variável da sequência de tarefas](#BKMK_SetTaskSequenceVariable) passo para definir o valor da **TSDisableProgressUI** variável à **verdadeiro** para ocultar o progresso da sequência de tarefas.

 - **Para apresentar o progresso da sequência de tarefas**  
No editor de sequência de tarefas, utilize o [definir variável da sequência de tarefas](#BKMK_SetTaskSequenceVariable) passo para definir o valor da **TSDisableProgressUI** variável à **falso** para apresentar o progresso da sequência de tarefas.

##  <a name="BKMK_SetupWindowsandConfigMgr"></a>Configurar Windows e ConfigMgr  
 Utilize o passo de sequência de tarefas **Configurar Windows e ConfigMgr** para fazer a transição do Windows PE para o novo sistema operativo. Este passo da sequência de tarefas é uma parte necessária de qualquer implementação do sistema operativo. Instala o cliente do Configuration Manager para o novo sistema operativo e prepara a sequência de tarefas continuar a execução no novo sistema operativo.  

 Este passo é executado apenas no Windows PE. Não é executado num sistema operativo padrão. Para mais informações sobre as variáveis de sequência de tarefas para esta ação de sequência de tarefas, consulte [variáveis de ação da sequência de tarefas configurar Windows e ConfigMgr](task-sequence-action-variables.md#BKMK_SetupWindows).  

 O **configurar Windows e ConfigMgr** ação de sequência de tarefas substitui variáveis de diretório sysprep.inf ou unattend.xml, como % WINDIR % e % ProgramFiles %, pelo diretório de instalação do Windows PE X:\Windows. As variáveis de sequência de tarefas especificadas através destas variáveis de ambiente serão ignoradas.  

 Utilize este passo de sequência de tarefas para executar as seguintes ações:  

1.  Preliminares: Windows PE  

    1.  Faz uma substituição de variável de sequência de tarefas no ficheiro unattend.xml.  

    2.  Transfere o pacote que contém o cliente do Configuration Manager e coloca-o na imagem implementada.  

2.  Configurar o Windows  

    1.  Instalação baseada em imagem.  

        1.  Desativa o cliente do Configuration Manager na imagem (ou seja, desativa o início automático para o serviço de cliente do Configuration Manager).  

        2.  Atualiza o registo na imagem implementada para assegurar que o sistema operativo implementado começa pela mesma letra de unidade que tinha no computador de referência.  

        3.  Reinicia no sistema operativo implementado.  

        4.  A mini-configuração do Windows é executada através do ficheiro sysprep.inf ou unattend.xml especificado anteriormente, que tem todas as interações do utilizador final suprimidas. Nota: Se **aplicar definições de rede** especificado para associar um domínio, em seguida, essas informações estão no ficheiro sysprep.inf ou unattend.xml e a mini-configuração do Windows efetua a associação ao domínio.  

    2.  Instalação baseada em Setup.exe.  Executa Setup.exe, que segue o processo de configuração normal do Windows:  

        1.  Copia o pacote de instalação do sistema operativo especificado numa sequência de tarefas **Aplicar Sistema Operativo** anterior para o disco rígido.  

        2.  Reinicia no sistema operativo recentemente implementado.  

        3.  A mini-configuração do Windows é executada através do ficheiro sysprep.inf ou unattend.xml especificado anteriormente, que tem todas as definições da interface de utilizador suprimidas. Nota: Se **aplicar definições de rede** especificado para associar um domínio, em seguida, essas informações estão no ficheiro sysprep.inf ou unattend.xml e a mini-configuração do Windows efetua a associação ao domínio.  

3.  Configurar o cliente do Configuration Manager  

    1.  Após a conclusão da miniconfiguração do Windows, a sequência de tarefas é retomada com o setupcomplete.cmd.  

    2.  Ativa ou desativa a conta de administrador local com base na opção selecionada no passo **Aplicar Definições do Windows**.  

    3.  Instala o cliente do Configuration Manager, utilizando o pacote transferido anteriormente (1.b) e as propriedades de instalação especificadas no Editor de sequência de tarefas. O cliente é instalado no "modo de aprovisionamento" para impedi-lo de processar novos pedidos de políticas até a sequência de tarefas estar concluída.  

    4.  Aguarda até o cliente estar totalmente operacional.  

    5.  Se o computador estiver a funcionar num ambiente com a Proteção de Acesso à Rede ativada, o cliente procura e instala todas as atualizações necessárias para que estas estejam presentes antes de a sequência de tarefas continuar a execução.  

4.  A sequência de tarefas continua a ser executada através do passo seguinte.  

> [!NOTE]  
>  A ação de sequência de tarefas **Configurar Windows e ConfigMgr** é responsável pela execução da Política de Grupo no computador recentemente instalado. A Política de Grupo é aplicada após a conclusão da sequência de tarefas.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Não selecionar para que a sequência de tarefas continue se ocorrer um erro ao executar o passo. Se ocorrer um erro, a sequência de tarefas falhará independentemente de selecionar esta definição.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Especifica um nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Especifica informações adicionais sobre a ação executada neste passo.  

 **Pacote de cliente**  
 Especifica o pacote de instalação de cliente do Configuration Manager que será utilizado por este passo de sequência de tarefas. Clique em **procurar** e selecione o pacote de instalação de cliente que pretende utilizar para instalar o cliente do Configuration Manager.  

 **Utilize o pacote de cliente de pré-produção quando disponível**  
 Especifica que, se existir um pacote de cliente de pré-produção disponível, o passo de sequência de tarefas irá utilizar esse pacote em vez do pacote de cliente de produção. Normalmente, o cliente de pré-produção é uma versão mais recente que está a ser testada no ambiente de produção. Clique em **procurar** e selecione o pacote de instalação de cliente de pré-produção que pretende utilizar para instalar o cliente do Configuration Manager.  

 **Propriedades de instalação**  
 A atribuição de sites e a configuração predefinida são especificadas automaticamente pela ação de sequência de tarefas. Pode utilizar este campo para especificar propriedades de instalação adicionais a utilizar quando instalar o cliente. Para introduzir várias propriedades de instalação, separe-as com um espaço.  

 Pode especificar opções da linha de comandos a utilizar durante a instalação do cliente. Por exemplo, pode introduzir **/skipprereq: silverlight.exe** para informar o ficheiro CCMSetup.exe para não instalar o pré-requisito Microsoft Silverlight. Para obter mais informações sobre as opções da linha de comandos disponíveis para CCMSetup.exe, consulte [acerca das propriedades de instalação de cliente](../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="BKMK_UpgradeOS"></a>Atualizar sistema operativo  
 Utilize o passo de sequência de tarefas **Atualizar Sistema Operativo** para atualizar um sistema operativo Windows 7, Windows 8, Windows 8.1 ou Windows 10 existente para o Windows 10.  

 Este passo de sequência de tarefas é executado apenas num sistema operativo padrão. Não é executado no Windows PE.  

### <a name="details"></a>Detalhes  
 No separador **Propriedades** para este passo, pode configurar as definições descritas nesta secção.  

 Além disso, utilize o separador **Opções** para executar as seguintes ações:  

-   Desativar o passo.  

-   Especificar se a sequência de tarefas continua se ocorrer um erro ao executar o passo.  

-   Especificar condições que têm de ser cumpridas para o passo ser executado.  

 **Nome**  
 Nome abreviado definido pelo utilizador que descreve a ação executada neste passo.  

 **Descrição**  
 Informações mais detalhadas sobre a ação executada neste passo.  

 **Pacote de atualização**  
 Selecione esta opção para especificar o pacote de atualização do sistema operativo Windows 10 para utilizar na atualização.  

 **Caminho de origem**  
 Especifica um caminho de rede ou local para o suporte de dados do Windows 10 que vai ser utilizado (corresponde à opção da linha de comandos /installFrom). Também pode especificar uma variável, tal como %caminhodomeuconteúdo% ou %DPC01%. Quando utilizar uma variável para o caminho de origem, esta tem de ter sido especificada anteriormente na sequência de tarefas. Por exemplo, se utilizar o passo [Transferir Conteúdo do Pacote](#BKMK_DownloadPackageContent) na sequência de tarefas, pode especificar uma variável para a localização do pacote de atualização do sistema operativo. Em seguida, pode utilizar essa variável para o caminho de origem deste passo.  

 **Edição**  
 Especifique a edição no suporte de dados do sistema operativo a utilizar para a atualização.  

 **Chave de produto**  
 Especifique a chave de produto a aplicar ao processo de atualização  

 **Fornecer o seguinte conteúdo de controladores à configuração do Windows durante a atualização**  
 Selecione esta definição para adicionar controladores ao computador de destino durante o processo de atualização (corresponde à opção da linha de comandos /InstallDriver). Os controladores têm de ser compatíveis com o Windows 10. Especifique uma das seguintes opções:  

-   **Pacote de controladores**: Clique em **procurar** e selecione um pacote de controladores existente na lista.  

-   **Conteúdo de teste**:  Selecione esta opção para especificar a localização para o pacote de controladores. Pode especificar uma pasta local, um caminho de rede ou uma variável de sequência de tarefas. Quando utilizar uma variável para o caminho de origem, esta tem de ter sido especificada anteriormente na sequência de tarefas. Por exemplo, utilizando o passo [Transferir Conteúdo do Pacote](task-sequence-steps.md#BKMK_DownloadPackageContent).  

 **Tempo limite (minutos)**  
 Especifica o número de minutos que a configuração tem de executar antes do Configuration Manager irá falhar o passo de sequência de tarefas.  

 **Efetuar análise de compatibilidade de configuração do Windows sem iniciar a atualização**  
 Especifica como fazer a análise de compatibilidade da Configuração do Windows sem iniciar o processo de atualização (corresponde à opção da linha de comandos /Compat ScanOnly). Tem de implementar a origem da instalação completa quando utilizar esta opção. A Configuração devolve um código de saída como resultado da análise. A tabela seguinte fornece alguns dos códigos de saída mais comuns.  

|Código de saída|Detalhes|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Não existem problemas de compatibilidade ("êxito").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0XC1900208)|Problemas de compatibilidade passíveis de ação.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0XC1900204)|A opção de migração selecionada não está disponível. Por exemplo, uma atualização do Empresarial para o Profissional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Não é elegível para Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0XC190020E)|Não existe espaço livre suficiente no disco.|  

 Para obter mais informações sobre este parâmetro, veja [Windows Setup Command-Line Options](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx) (Opções da Linha de Comandos de Configuração do Windows)  

 **Ignorar mensagens de compatibilidade dispensáveis**  
 Especifica que a Configuração conclui a instalação, ignorando quaisquer mensagens de compatibilidade dispensáveis (corresponde à opção da linha de comandos /Compat IgnoreWarning).  

 **Atualizar dinamicamente a configuração do Windows com o Windows Update**  
 Especifica se a Configuração irá efetuar operações de Atualização Dinâmica, como atualizações de pesquisa, de transferência e de instalação (corresponde à opção da linha de comandos /DynamicUpdate). Esta definição não é compatível com atualizações de software do Configuration Manager, mas pode ser ativada quando para processar as atualizações com WSUS (autónomo) ou o Windows Update.  

 **Ignorar política e utilizar o Microsoft Update por predefinição**: Selecione esta definição para substituir temporariamente a política local em tempo real para executar operações de atualização dinâmica e o computador obter as atualizações do Windows Update.  

