---
title: Gerir controladores
titleSuffix: Configuration Manager
description: Utilizar o catálogo de controladores do Configuration Manager para importar controladores de dispositivo, controladores de grupo em pacotes e distribuir estes pacotes em pontos de distribuição.
ms.date: 03/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be3cc24721674e9da276e7a65af03a5b4a266eed
ms.sourcegitcommit: 33a006204f7f5f9b9acd1f3e84c4bc207362d00a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305699"
---
# <a name="manage-drivers-in-configuration-manager"></a>Gerir controladores no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager fornece um catálogo de controladores que pode utilizar para gerir os controladores de dispositivo do Windows no seu ambiente do Configuration Manager. Utilize o catálogo de controladores para importar controladores de dispositivo para o Configuration Manager, ao agrupá-los em pacotes e distribuir estes pacotes em pontos de distribuição. Controladores de dispositivo podem ser utilizados quando instala o sistema operacional completo no computador de destino e quando usa o Windows PE numa imagem de arranque. Controladores de dispositivo do Windows é composto por um arquivo de informações (. INF) de instalação e arquivos adicionais que são necessários para suportar o dispositivo. Quando implementa um sistema operacional, o Configuration Manager obtém as informações de plataforma de hardware e para o dispositivo de seu arquivo INF. 



## <a name="BKMK_DriverCategories"></a> Categorias de controladores

Quando importa controladores de dispositivos, pode atribuir os controladores de dispositivos a uma categoria. As categorias de controladores de dispositivos ajudam a agrupar o controladores de dispositivos de utilização semelhante no catálogo de controladores. Por exemplo, defina todos os controladores de dispositivo do adaptador de rede a uma categoria específica. Em seguida, quando criar uma sequência de tarefas que inclui a [aplicar controladores automaticamente](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers) passo, especificar uma categoria de controladores de dispositivo. Configuration Manager, em seguida, analisa o hardware e seleciona os controladores adequados dessa categoria para preparar o sistema para a configuração da Windows utilizar.  



## <a name="BKMK_ManagingDriverPackages"></a> Pacotes de controladores

Agrupe controladores de dispositivo semelhantes em pacotes para simplificar as implementações de sistema operacional. Por exemplo, crie um pacote de controladores para cada fabricante de computador na sua rede. Pode criar um pacote de controladores quando importa controladores para o catálogo de controladores diretamente no **pacotes de controladores** nó. Depois de criar um pacote de controladores, distribuí-la aos pontos de distribuição. Em seguida, os computadores de cliente do Configuration Manager podem instalar os controladores conforme necessário. 

Considere os seguintes pontos:  

- Quando cria um pacote de controladores, a localização de origem do pacote tem de apontar para uma partilha de rede vazia que não seja utilizada por outro pacote de controladores. O fornecedor de SMS tem de ter **controlo total** permissões para essa localização.  

- Quando adiciona controladores de dispositivo a um pacote de controladores, o Configuration Manager copia-o para a localização de origem do pacote. Pode adicionar um driver apenas controladores de dispositivo que importar o pacote e que estão ativados no catálogo de controladores.  

- Pode copiar um subconjunto de controladores de dispositivo de um pacote de controlador existente. Primeiro, crie um novo pacote de controladores. Em seguida, adicione o subconjunto de controladores de dispositivo para o novo pacote e, em seguida, distribua o novo pacote para um ponto de distribuição.  

- Quando utiliza sequências de tarefas para instalar controladores, crie pacotes de controladores que contenham menos de 500 controladores de dispositivo.


### <a name="BKMK_CreatingDriverPackages"></a> Criar um pacote de controlador  

> [!IMPORTANT]  
> Para criar um pacote de controladores, tem de ter uma pasta de rede vazia que não seja utilizada por outro pacote de controladores. Na maioria dos casos, crie uma nova pasta antes de iniciar este procedimento.  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **sistemas operativos**e, em seguida, selecione a **pacotes de controladores** nó.  

2. Sobre o **home page** separador do Friso, no **criar** grupo, selecione **criar pacote de controladores**.  

3. Especifique um descritivo **nome** para o pacote de controladores.  

4. Introduza um opcional **comentário** para o pacote de controladores. Utilize esta descrição para fornecer informações sobre o conteúdo ou o objetivo do pacote de controladores.  

5. Na caixa **Caminho** , especifique uma pasta de origem vazia para o pacote de controladores. Cada pacote de controladores terá de utilizar uma pasta exclusiva. Este caminho é necessário como uma localização de rede.  

   > [!IMPORTANT]  
   > A conta de servidor do site tem de ter **controlo total** permissões para a pasta de origem especificada.  

O novo pacote de controladores não contém quaisquer controladores. O passo seguinte adiciona controladores ao pacote.  

Se o nó **Pacotes de Controladores** contiver diversos pacotes, poderá adicionar pastas ao mesmo para separar os pacotes em grupos lógicos.  


### <a name="BKMK_PackageActions"></a> Ações adicionais para pacotes de controladores  

Pode realizar ações adicionais para gerir pacotes de controladores quando seleciona um ou mais pacotes de controladores a **pacotes de controladores** nó. 


#### <a name="create-prestage-content-file"></a>Criar Ficheiro de Conteúdo Pré-configurado
Cria ficheiros que pode utilizar para importar manualmente o conteúdo e metadados associados. Utilize conteúdo pré-configurado quando tiver reduzida largura de banda de rede entre o servidor de site e os pontos de distribuição em que o pacote de controladores se encontra armazenado.

#### <a name="delete"></a>Eliminar
Remove o pacote de controladores do nó **Pacotes de Controladores**.

#### <a name="distribute-content"></a>Distribuir Conteúdo
Distribui o pacote de controladores aos pontos de distribuição, grupos de pontos de distribuição e grupos de pontos de distribuição associados a coleções.

#### <a name="manage-access-accounts"></a>Gerir Contas de Acesso
Adiciona, modifica ou remove as contas de acesso do pacote de controladores.

Para obter mais informações sobre as contas de acesso de pacotes, consulte [contas utilizadas no Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).

#### <a name="move"></a>Mover
Move o pacote de controladores para outra pasta do nó **Pacotes de Controladores**.

#### <a name="update-distribution-points"></a>Atualizar Pontos de Distribuição
Atualiza o pacote de controladores de dispositivo em todos os pontos de distribuição em que o pacote se encontra armazenado. Esta ação copia apenas o conteúdo que foi alterado desde a última vez em que foi distribuído.

#### <a name="properties"></a>Propriedades
Abre o **propriedades** caixa de diálogo. Rever e alterar o conteúdo e propriedades do controlador. Por exemplo, altere o nome e descrição do controlador, ativar ou desativá-la e especificar em que plataformas pode executar. 

<!--3607716, fka 1358270--> A partir da versão 1810, pacotes de controladores têm campos de metadados para **fabricante** e **modelo**. Utilize estes campos para os pacotes de controladores de etiqueta com informações para auxiliar na manutenção geral ou para identificar controladores antigos e duplicados, que pode eliminar. Sobre o **gerais** separador, selecione um valor existente listas suspensas ou introduza uma cadeia de caracteres para criar uma nova entrada. 

Na **pacotes de controladores** nó, estes campos apresentam na lista como a **fabricante de Driver** e **modelo de Driver** colunas. Eles também podem ser usados como critérios de pesquisa. 



## <a name="BKMK_DeviceDrivers"></a> Controladores de dispositivo

Pode instalar controladores em computadores de destino sem os incluir na imagem do sistema operacional que está implementada. O Configuration Manager fornece um catálogo de controladores que contém referências a todos os controladores que importar para o Configuration Manager. O catálogo de controladores está localizado na **biblioteca de Software** área de trabalho e é composta por dois nós: **Drivers** e **pacotes de controladores**. O **Drivers** nó apresenta uma lista de todos os controladores que importar para o catálogo de controladores.  


### <a name="BKMK_ImportDrivers"></a> Importar controladores de dispositivo para o catálogo de controladores  

Antes de poder utilizar um driver ao implementar um sistema operacional, importe-o para o catálogo de controladores. Para melhor gerenciá-los, importar apenas os controladores que pretende instalar como parte das suas implementações do sistema operacional. Store várias versões de controladores no catálogo para fornecer uma forma fácil de atualizar os controladores existentes quando são alteram de requisitos de hardware de dispositivos na sua rede.  

Como parte do processo de importação para o controlador de dispositivo, o Gerenciador de configuração lê as seguintes propriedades sobre o controlador:
- Fornecedor
- Classe
- Versão
- assinatura
- Hardware suportado
- Informações de plataforma suportada

Por predefinição, o controlador é denominado após o primeiro dispositivo de hardware que suporta. Pode renomear o controlador de dispositivo mais tarde. A lista de plataformas suportadas baseia-se nas informações do ficheiro INF do controlador. Uma vez que a exatidão destas informações pode variar, verifique manualmente se o driver é suportado depois de importar para o catálogo.  

Depois de importar controladores de dispositivo para o catálogo, adicioná-los para pacotes de controladores ou pacotes de imagens de arranque.  

> [!IMPORTANT]  
> Não é possível importar controladores de dispositivo diretamente para uma subpasta dos **Drivers** nó. Para importar um controlador de dispositivo para uma subpasta, importe-o primeiro para o nó **Controladores** e, em seguida, mova-o para a subpasta.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Processo para importar controladores de dispositivo do Windows para o catálogo de controladores  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **sistemas operativos**e selecione o **Drivers** nó.  

2. No **home page** separador do Friso, no **Create** grupo, selecione **importar controlador** para iniciar o **Assistente para importar novo controlador**.  

3. Sobre o **localizar controlador** página, especifique as seguintes opções:  

    - **Importar todos os controladores no seguinte caminho de rede (UNC)**: Para importar todos os controladores de dispositivo numa pasta específica, especifique o caminho de rede. Por exemplo: `\\servername\share\folder`.  

        > [!NOTE]  
        > Se existirem muitos subpastas e muitos ficheiros INF de controlador, este processo pode demorar tempo.  

    - **Importar um controlador específico**: Para importar um controlador específico a partir de uma pasta, especifique o caminho de rede para o ficheiro de INF do controlador de dispositivo Windows.  

    - **Especificar a opção para duplicar controladores**: Selecione como pretende que o Configuration Manager para gerir categorias de controladores ao importar um controlador de dispositivo duplicados  
        - **Importar o controlador e anexar uma nova categoria às categorias existentes**  
        - **Importar o controlador e manter as categorias existentes**  
        - **Importar o controlador e substituir as categorias existentes**  
        - **Não importar o controlador**  

    > [!IMPORTANT]  
    > Quando importa controladores, o servidor do site tem de ter permissão de **Leitura** na pasta ou a importação falhará.  

4. Sobre o **detalhes do controlador** página, especifique as seguintes opções:  

    - **Ocultar controladores que não estão numa classe de armazenamento ou de rede (para imagens de arranque)**: Utilize esta definição para apresentar apenas controladores de armazenamento e rede. Esta opção oculta outros controladores que normalmente não são necessários para imagens de arranque, como um controlador de vídeo ou controlador do modem.  

    - **Ocultar controladores que não estejam assinados digitalmente**: A Microsoft recomenda utilizar apenas os controladores que são assinados digitalmente  

    - Na lista de controladores, selecione os que pretende importar para o catálogo de controladores.  

    - **Ativar estes controladores e permitir que os computadores instalem**: Selecione esta definição para permitir que os computadores instalem os controladores de dispositivo. Por predefinição, esta opção encontra-se ativada.  

        > [!IMPORTANT]  
        > Se um driver de dispositivo está a causar um problema ou pretender suspender a instalação de um driver de dispositivo, desativá-lo durante a importação. Também pode desativar controladores após importá-los.  

    - Para atribuir os controladores de dispositivo a uma categoria administrativa para filtragem fins, como "Computadores de secretária" ou "Portáteis", selecione **categorias**. Em seguida, escolha uma categoria existente ou criar uma nova categoria. Utilizar categorias de controle que drivers de dispositivo são aplicados pela [aplicar controladores automaticamente](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers) passo de sequência de tarefas.  

5. Sobre o **Adicionar controlador a pacotes** página, escolha se pretende adicionar os controladores a um pacote.  

    - Selecione os pacotes de controladores utilizados para distribuir os controladores de dispositivo.  

        Se necessário, selecione **novo pacote** para criar um novo pacote de controladores. Quando cria um novo pacote de controladores, fornece uma partilha de rede que não está em utilização por outros pacotes de controladores.  

    - Se o pacote já tiver sido distribuído para pontos de distribuição, selecione **Sim** na caixa de diálogo para atualizar as imagens de arranque nos pontos de distribuição. Não é possível utilizar controladores de dispositivo até que eles estão distribuídos para pontos de distribuição. Se selecionou **não**, execute o **atualizar ponto de distribuição** ação antes de utilizar a imagem de arranque. Se o pacote de controlador nunca tiver sido distribuído, tem de utilizar o **distribuir conteúdo** ação no **pacotes de controladores** nó.  

6. Sobre o **Adicionar controlador a imagens de arranque** página, selecione se pretende adicionar os controladores de dispositivo a imagens de arranque existentes.  

    > [!NOTE]  
    > Adicione apenas controladores de armazenamento e de rede às imagens de arranque.  

    - Selecione **Sim** na caixa de diálogo para atualizar as imagens de arranque nos pontos de distribuição. Não é possível utilizar controladores de dispositivo até que eles estão distribuídos para pontos de distribuição. Se selecionou **não**, execute o **atualizar ponto de distribuição** ação antes de utilizar a imagem de arranque. Se o pacote de controlador nunca tiver sido distribuído, tem de utilizar o **distribuir conteúdo** ação no **pacotes de controladores** nó.  

    - O Configuration Manager avisa-o se a arquitetura de um ou mais controladores não corresponde à arquitetura das imagens de arranque que selecionou. Se não coincidirem, selecione **OK**. Volte para o **detalhes do controlador** de páginas e desmarcar os controladores que não correspondem à arquitetura da imagem de arranque selecionada. Por exemplo, se selecionar uma imagem de arranque x64 e x86, todos os controladores têm de suportar ambas as arquiteturas. Se selecionar uma imagem de arranque x64, todos os controladores têm de suportar a arquitetura x64.  

        > [!NOTE]  
        > - A arquitetura baseia-se na arquitetura reportada no INF do fabricante.  
        > - Se um controlador oferece suporte a ambas as arquiteturas, em seguida, pode importá-lo em qualquer imagem de arranque.  

    - O Configuration Manager avisa-o se adicionar controladores de dispositivo que não são controladores de armazenamento ou de rede para uma imagem de arranque. Na maioria dos casos, não são necessários para a imagem de arranque. Selecione **Sim** para adicionar os controladores à imagem de arranque, ou **não** para voltar atrás e modificar a sua seleção de controlador.  

    - O Configuration Manager avisa-o se um ou mais dos controladores selecionados não estão a ser assinados digitalmente de forma correta. Selecione **Sim** para continuar e selecione **não** para voltar atrás e fazer alterações à seleção de controlador.  

7. Conclua o assistente.  


### <a name="BKMK_ModifyDriverPackage"></a> Gerir controladores de dispositivo num pacote de controlador  

Utilize os procedimentos seguintes para modificar pacotes de controladores e imagens de arranque. Para adicionar ou remover um driver, primeiro localizá-la na **Drivers** nó. Em seguida, edite os pacotes ou imagens de arranque à qual o controlador selecionado está associado.  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **sistemas operativos**e, em seguida, selecione a **Drivers** nó.  

2. Selecione os controladores de dispositivo que pretende adicionar a um pacote de controladores.  

3. Na **home page** separador do Friso, no **Driver** grupo, selecione **editar**e, em seguida, selecione **pacotes de controladores**.  

4. Para adicionar um controlador de dispositivo, selecione a caixa de verificação dos pacotes de controladores aos quais pretende adicionar os controladores de dispositivo. Para remover um controlador de dispositivo, desmarque a caixa de verificação dos pacotes de controladores de que pretende remover o controlador de dispositivo.  

    Se estiver a adicionar controladores de dispositivo associados a pacotes de controladores, opcionalmente, pode criar um novo pacote. Selecione **novo pacote**, que abre o **novo pacote de controladores** caixa de diálogo.  

5. Se o pacote já tiver sido distribuído para pontos de distribuição, selecione **Sim** na caixa de diálogo para atualizar as imagens de arranque nos pontos de distribuição. Não é possível utilizar controladores de dispositivo até que eles estão distribuídos para pontos de distribuição. Se selecionou **não**, execute o **atualizar ponto de distribuição** ação antes de utilizar a imagem de arranque. Se o pacote de controlador nunca tiver sido distribuído, tem de utilizar o **distribuir conteúdo** ação no **pacotes de controladores** nó. Antes de os controladores estarem disponíveis, tem de atualizar o pacote de controlador nos pontos de distribuição.  

    Selecione **OK** quando terminar.  


### <a name="BKMK_ManageDriversBootImage"></a> Gerir controladores de dispositivo numa imagem de arranque  

É possível adicionar a controladores de dispositivo do Windows que foram importados para o catálogo de imagens de arranque. Para adicionar controladores de dispositivos a uma imagem de arranque, utilize as seguintes diretrizes:  

- Adicione apenas controladores de armazenamento e de rede a imagens de arranque. Outros tipos de controladores não são normalmente necessários no Windows PE. Controladores que não são necessários desnecessariamente aumentam o tamanho da imagem de arranque.  

- Adicione apenas controladores de dispositivos para Windows 10 para uma imagem de arranque. A versão necessária do Windows PE baseia-se no Windows 10.  

- Certifique-se de que utiliza o driver de dispositivo correto para a arquitetura da imagem de arranque. Não adicione um x86 driver de dispositivo a um x64 imagem de arranque.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Processo para modificar os controladores de dispositivo associados a uma imagem de arranque  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **sistemas operativos**e, em seguida, selecione a **Drivers** nó.  

2. Selecione os controladores de dispositivo que pretende adicionar ao pacote de controladores.  

3. Na **home page** separador do Friso, no **Driver** grupo, selecione **editar**e, em seguida, selecione **imagens de arranque**.  

4. Para adicionar um controlador de dispositivo, selecione a caixa de verificação da imagem de arranque à qual pretende adicionar os controladores de dispositivo. Para remover um controlador de dispositivo, desmarque a caixa de verificação da imagem de arranque de que pretende remover o controlador de dispositivo.  

5. Se não pretender atualizar os pontos de distribuição em que a imagem de arranque é armazenada, desmarque a **atualizar pontos de distribuição após concluir** caixa de verificação. Por predefinição, os pontos de distribuição são atualizados quando a imagem de arranque é atualizada.  

    - Selecione **Sim** na caixa de diálogo para atualizar as imagens de arranque nos pontos de distribuição. Não é possível utilizar controladores de dispositivo até que eles estão distribuídos para pontos de distribuição. Se selecionou **não**, execute o **atualizar ponto de distribuição** ação antes de utilizar a imagem de arranque. Se o pacote de controlador nunca tiver sido distribuído, tem de utilizar o **distribuir conteúdo** ação no **pacotes de controladores** nó.  

    - O Configuration Manager avisa-o se a arquitetura de um ou mais controladores não corresponde à arquitetura das imagens de arranque que selecionou. Se não coincidirem, selecione **OK**. Volte para o **detalhes do controlador** página e desmarcar os controladores que não correspondem à arquitetura da imagem de arranque selecionada. Por exemplo, se selecionar uma imagem de arranque x64 e x86, todos os controladores têm de suportar ambas as arquiteturas. Se selecionar uma imagem de arranque x64, todos os controladores têm de suportar a arquitetura x64.  

        > [!NOTE]
        > - A arquitetura baseia-se na arquitetura reportada no INF do fabricante.  
        > - Se um controlador suportar ambas as arquiteturas, pode importá-lo para qualquer imagem de arranque.  

    - O Configuration Manager avisa-o se adicionar controladores de dispositivo que não são controladores de armazenamento ou de rede para uma imagem de arranque. Na maioria dos casos, não são necessários para a imagem de arranque. Selecione **Sim** para adicionar os controladores à imagem de arranque ou **não** para voltar atrás e modificar a sua seleção de controlador.  

    - O Configuration Manager avisa-o se um ou mais dos controladores selecionados não estão a ser assinados digitalmente de forma correta. Selecione **Sim** para continuar ou selecione **não** para voltar atrás e fazer alterações à seleção de controlador.  


### <a name="BKMK_DriverActions"></a> Ações adicionais para controladores de dispositivo  

Pode realizar ações adicionais para gerir controladores, quando selecioná-los no **Drivers** nó.  

#### <a name="categorize"></a>Categorizar
Limpa, gere ou define uma categoria administrativa para os controladores selecionados.

#### <a name="delete"></a>Eliminar
Remove o controlador dos **Drivers** nó e também remove o controlador de distribuição associados pontos.

#### <a name="disable"></a>Desativar
Proíbe o driver de que está a ser instalado. Esta ação desativa temporariamente o driver. A sequência de tarefas não é possível instalar um driver desativado ao implementar um sistema operacional. 

> [!Note]  
> Esta ação só impede que os controladores instalem com o **aplicar controladores automaticamente** passo de sequência de tarefas.

#### <a name="enable"></a>Ativar
Permite que os computadores de cliente do Configuration Manager e sequências de tarefas instale o controlador de dispositivo quando implantar o sistema operacional.

#### <a name="move"></a>Mover
Move o controlador de dispositivo para outra pasta do nó **Controladores**.

#### <a name="properties"></a>Propriedades
Abre o **propriedades** caixa de diálogo. Rever e alterar as propriedades do controlador. Por exemplo, alterar o nome e descrição, ativar ou desativá-la e especificar as plataformas que pode ser executada no.



## <a name="BKMK_TSDrivers"></a> Utilizar sequências de tarefas para instalar controladores  

Utilize sequências de tarefas para automatizar a forma como o sistema operativo é implementado. Cada passo na sequência de tarefas pode fazer uma ação específica, como instalar um driver. Pode utilizar os seguintes passos de sequência de tarefas duas para instalar controladores de dispositivo ao implementar um sistema operacional:  

- [Aplicar controladores automaticamente](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers): Este passo permite-lhe fazer corresponder e instalar controladores de dispositivo como parte da implementação do sistema operativo automaticamente. Pode configurar o passo de sequência de tarefas para instalar apenas os controladores com melhor compatibilidade para cada dispositivo de hardware detetado. Em alternativa, especificar que o passo instala todos os controladores compatíveis para cada dispositivo de hardware detetado e, em seguida, deixe o programa de configuração do Windows escolha o melhor controlador. Também pode especificar uma categoria de controlador para limitar os controladores que estão disponíveis para este passo.  

- [Aplicar pacote de controlador](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage): Este passo permite-lhe disponibilizar todos os controladores de dispositivo num pacote de controladores específico para a configuração do Windows. Nos pacotes de controladores especificados, a Configuração do Windows procura os controladores de dispositivos necessários. Quando cria suportes de dados autónomos, tem de utilizar este passo para instalar controladores de dispositivo.  

Quando utiliza estes passos de sequência de tarefas, também pode especificar como os drivers são instalados no computador em que implantar o sistema operacional. Para obter mais informações, consulte [gerir sequências de tarefas para automatizar tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks).  



## <a name="BKMK_DriverReports"></a> Relatórios de controladores  

Na categoria de relatórios **Gestão do Controlador** , pode utilizar vários relatórios para determinar as informações gerais sobre os controladores de dispositivos no catálogo de controladores. Para obter mais informações sobre relatórios, consulte [relatórios](/sccm/core/servers/manage/reporting).

