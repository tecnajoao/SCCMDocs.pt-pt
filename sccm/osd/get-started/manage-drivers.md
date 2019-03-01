---
title: 'Gerir controladores '
titleSuffix: Configuration Manager
description: Utilizar o catálogo de controladores do Configuration Manager para importar controladores de dispositivo, controladores de grupo em pacotes e distribuir estes pacotes em pontos de distribuição.
ms.date: 01/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 727a449b956868c5dec88b4df5b8a66ac400abdc
ms.sourcegitcommit: 0bf253085adeca0d9ea62d76497eb5ebf5ce89da
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/28/2019
ms.locfileid: "57012450"
---
# <a name="manage-drivers-in-system-center-configuration-manager"></a>Gerir controladores no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager fornece um catálogo de controladores que pode utilizar para gerir os controladores de dispositivo do Windows no seu ambiente do Configuration Manager. Pode utilizar o catálogo de controladores para importar controladores de dispositivo para o Configuration Manager, ao agrupá-los em pacotes e distribuir estes pacotes em pontos de distribuição em que pode acessá-los quando implementar um sistema operativo. Os controladores de dispositivos podem ser utilizados quando instala o sistema operativo completo no computador de destino e quando instala o Windows PE com uma imagem de arranque. Os controladores do dispositivo do Windows são compostos por um ficheiro INF (Ficheiro de Informações de Configuração) e pelos ficheiros adicionais necessários para suportar o dispositivo. Quando um sistema operativo é implementado, o Configuration Manager obtém as informações de plataforma de hardware e para o dispositivo de seu arquivo INF. Utilize o seguinte para gerir controladores no ambiente do Configuration Manager.

##  <a name="BKMK_DriverCategories"></a> Categorias de controladores de dispositivos  
 Quando importa controladores de dispositivos, pode atribuir os controladores de dispositivos a uma categoria. As categorias de controladores de dispositivos ajudam a agrupar o controladores de dispositivos de utilização semelhante no catálogo de controladores. Por exemplo, é possível atribuir todos os controladores de dispositivos do adaptador de rede a uma categoria específica. Em seguida, quando criar uma sequência de tarefas que inclua o passo [Aplicar Controladores Automaticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) , pode indicar uma categoria específica de controladores de dispositivo. Configuration Manager, em seguida, analisa o hardware e seleciona os controladores adequados dessa categoria para preparar o sistema para a configuração da Windows utilizar.  

##  <a name="BKMK_ManagingDriverPackages"></a> Pacotes de controladores  
 Pode agrupar controladores de dispositivo semelhantes em pacotes para simplificar as implementações do sistema operativo. Por exemplo, poderá optar por criar um pacote de controlador para cada fabricante de computadores na sua rede. Pode criar um pacote de controlador enquanto importa controladores para o catálogo de controladores diretamente no nó **Pacotes de Controladores** . Depois de criar o pacote de controladores, tem de ser distribuído para pontos de distribuição do qual Configuration Manager computadores cliente podem instalar os controladores conforme forem necessários. Tenha em consideração o seguinte:  

- Quando cria um pacote de controladores, a localização de origem do pacote tem de apontar para uma partilha de rede vazia que não seja utilizada por outro pacote de controlador e o fornecedor de SMS tem de ter permissões de controlo total a essa localização.  

- Quando adiciona controladores de dispositivo a um pacote de controladores, o Configuration Manager copia o controlador de dispositivo para a localização de origem do pacote de controlador. Só pode adicionar controladores de dispositivos que tenham sido importados e que estão ativados no catálogo de controladores.  

- Para copiar um subconjunto de controladores de dispositivo de um pacote de controlador existente, crie um novo pacote de controlador, adicione o subconjunto de controladores de dispositivo ao novo pacote e distribua o novo pacote por um ponto de distribuição.  

  Utilize as secções seguintes para criar e gerir pacotes de controladores.  

###  <a name="CreatingDriverPackages"></a> Criar um pacote de controlador  
 Utilize o procedimento seguinte para criar um novo pacote de controladores.  

> [!IMPORTANT]  
>  Para criar um pacote de controladores, terá de ter uma pasta de rede vazia que não seja utilizada por outro pacote de controladores. Na maioria dos casos, terá de criar uma nova pasta antes de iniciar este procedimento.  

> [!NOTE]  
>  Quando utiliza sequências de tarefas para instalar controladores, crie pacotes de controladores que contenham menos de 500 controladores de dispositivo.  

 Utilize o procedimento seguinte para criar um pacote de controladores.  

#### <a name="to-create-a-driver-package"></a>Para criar um pacote de controladores  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Pacotes de Controladores**.  

3. No separador **Home page** , no grupo **Criar** , clique em **Criar Pacote de Controladores**.  

4. Na caixa **Nome** , especifique um nome descritivo para o pacote de controladores.  

5. Na caixa **Comentário** , introduza uma descrição opcional para o pacote de controladores. Certifique-se de que a descrição fornece informações sobre o conteúdo ou objetivo do pacote de controladores.  

6. Na caixa **Caminho** , especifique uma pasta de origem vazia para o pacote de controladores. Introduza o caminho para a pasta de origem no formato UNC (Universal Naming Convention). Cada pacote de controladores terá de utilizar uma pasta exclusiva.  

   > [!IMPORTANT]  
   >  A conta de servidor do site tem de ter **controlo total** permissões para a pasta de origem especificada.  

   O novo pacote de controladores não contém quaisquer controladores. O passo seguinte consiste em adicionar controladores ao pacote.  

   Se o nó **Pacotes de Controladores** contiver diversos pacotes, poderá adicionar pastas ao mesmo para separar os pacotes em grupos lógicos.  

###  <a name="BKMK_PackageActions"></a> Ações adicionais para pacotes de controladores  
 Pode realizar ações adicionais para gerir os pacotes de controladores quando seleciona um ou mais pacotes de controladores no nó **Pacotes de Controladores** . Estas ações incluem o seguinte:  

|Action|Descrição|  
|------------|-----------------|  
|**Criar Ficheiro de Conteúdo Pré-configurado**|Cria ficheiros que podem ser utilizados para importar manualmente o conteúdo e os metadados associados. Utilize conteúdo pré-configurado quando tiver reduzida largura de banda de rede entre o servidor de site e os pontos de distribuição em que o pacote de controladores se encontra armazenado.|  
|**Eliminar**|Remove o pacote de controladores do nó **Pacotes de Controladores** .|  
|**Distribuir Conteúdo**|Distribui o pacote de controladores aos pontos de distribuição, grupos de pontos de distribuição e grupos de pontos de distribuição associados a coleções.|  
|**Gerir Contas de Acesso**|Adiciona, modifica ou remove as contas de acesso do pacote de controladores.<br /><br /> Para obter mais informações sobre as contas de acesso de pacotes, consulte [contas utilizadas no Configuration Manager](../../core/plan-design/hierarchy/accounts.md).|  
|**Moverr**|Move o pacote de controladores para outra pasta do nó **Pacotes de Controladores** .|  
|**Atualizar Pontos de Distribuição**|Atualiza o pacote de controladores de dispositivo em todos os pontos de distribuição em que o pacote se encontra armazenado. Esta ação copia apenas o conteúdo que foi alterado desde a última vez em que foi distribuído.|  
|**Propriedades**|Abre a caixa de diálogo **Propriedades** , onde pode consultar e alterar o conteúdo e as propriedades do controlador de dispositivo. Por exemplo, poderá mudar o nome e a descrição do controlador de dispositivo, ativá-lo ou especificar em que plataformas poderá ser executado.|  

##  <a name="BKMK_DeviceDrivers"></a> Controladores de dispositivo  
 Pode instalar controladores de dispositivo em computadores de destino sem os incluir na imagem do sistema operativo que está a ser implementada. O Configuration Manager fornece um catálogo de controladores que contém referências a todos os controladores de dispositivo que importar para o Configuration Manager. O catálogo de controladores está localizado na **biblioteca de Software** área de trabalho e é composta por dois nós: **Drivers** e **pacotes de controladores**. O nó **Controladores** lista todos os controladores que importou para o catálogo de controladores. Utilize este nó para saber os detalhes de cada controlador importado, modificar os controladores num pacote de controlador ou imagem de arranque, ativar ou desativar um controlador, etc.  

###  <a name="BKMK_ImportDrivers"></a> Importar controladores de dispositivo para o catálogo de controladores  
 Tem de importar os controladores de dispositivos para o catálogo de controladores antes de os poder utilizar para implementar um sistema operativo. Para melhor gerir os controladores de dispositivos, importe apenas aqueles que tenciona instalar como parte da implementação do sistema operativo. Porém, pode também armazenar várias versões dos controladores de dispositivos no catálogo de dispositivos para facilitar a atualização dos controladores de dispositivos existentes quando forem efetuadas alterações nos requisitos do dispositivo de hardware da rede.  

 Como parte do processo de importação para o controlador de dispositivo, o Configuration Manager lê o fornecedor, classe, versão, assinatura, hardware suportado e informações de plataforma que está associadas ao dispositivo suportado. Por predefinição, o controlador é denominado de acordo com o primeiro dispositivo de hardware que suporta. No entanto, poderá posteriormente mudar o nome do controlador de dispositivo. A lista de plataformas suportadas baseia-se nas informações do ficheiro INF do controlador. Uma vez que a exatidão destas informações poderá variar, verifique manualmente se o controlador de dispositivo é suportado após a sua importação para o catálogo de controladores.  

 Depois de importar controladores de dispositivo para o catálogo, poderá adicionar os controladores de dispositivo a pacotes de controladores ou a pacotes de imagens de arranque.  

> [!IMPORTANT]  
>  Não pode importar controladores de dispositivo diretamente para uma subpasta do nó **Controladores** . Para importar um controlador de dispositivo para uma subpasta, importe-o primeiro para o nó **Controladores** e, em seguida, mova-o para a subpasta.  

 Utilize o procedimento seguinte para importar controladores de dispositivo do Windows.  

#### <a name="to-import-windows-device-drivers-into-the-driver-catalog"></a>Para importar controladores de dispositivo do Windows para o catálogo de controladores  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Controladores**.  

3. No separador **Home page** , no grupo **Criar** , clique em **Importar Controlador** para iniciar o **Assistente para Importar Novo Controlador**.  

4. Na página **Localizar Controlador** , especifique as seguintes opções e clique em **Seguinte**:  

   -   **Importar todos os controladores no seguinte caminho de rede (UNC)**: Para importar todos os controladores de dispositivo contidos numa pasta específica, especifique o caminho de rede para a pasta de driver de dispositivo. Por exemplo,  **\\\\servername\folder**.  

       > [!NOTE]  
       >  O processo para importar todos os controladores pode demorar algum tempo se existirem muitas pastas e muitos ficheiros de controlador (.inf).  

   -   **Importar um controlador específico**: Para importar um controlador específico a partir de uma pasta, especifique o caminho de rede (UNC) para o controlador de dispositivo do Windows. INF ou em massa armazenamento ficheiro Txtsetup OEM do controlador.  

   -   **Especificar a opção para duplicar controladores**: Selecione como pretende que o Configuration Manager para gerir categorias de controladores quando for importada uma unidade de dispositivo duplicado.  

   > [!IMPORTANT]  
   >  Quando importa controladores, o servidor do site tem de ter permissão de **Leitura** na pasta ou a importação falhará.  

5. Na página **Detalhes do Controlador** , especifique as seguintes opções e clique em **Seguinte**:  

   -   **Ocultar controladores que não estão numa classe de armazenamento ou de rede (para imagens de arranque)**: Utilize esta definição para apresentar apenas controladores de rede e de armazenamento e ocultar outros controladores que normalmente não são necessários para imagens de arranque, como um controlador de vídeo ou controlador do modem.  

   -   **Ocultar controladores que não estejam assinados digitalmente**: Utilize esta definição para ocultar controladores que não estejam assinados digitalmente.  

   -   Na lista de controladores, selecione os que pretende importar para o catálogo de controladores.  

   -   **Ativar estes controladores e permitir que os computadores instalem**: Selecione esta definição para permitir que os computadores instalem os controladores de dispositivo. Por predefinição, esta caixa de verificação está selecionada.  

       > [!IMPORTANT]  
       >  Se um controlador de dispositivo estiver a causar um problema ou quiser suspender a instalação de um controlador de dispositivo, pode desativar o controlador de dispositivo ao desmarcar a caixa de verificação **Ativar estes controladores e permitir que os computadores os instalem** . Também pode desativar controladores após estes terem sido importados.  

   -   Para atribuir os controladores de dispositivo a uma categoria administrativa para efeitos de filtragem, tal como "Computadores de Secretária" ou "Portáteis", clique em **Categorias** e selecione uma categoria existente ou crie uma nova. Também pode utilizar a atribuição de categorias para configurar que controladores de dispositivo serão aplicados à implementação pelo passo [Aplicar Controladores Automaticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) da sequência de tarefas.  

6. Na página **Adicionar Controlador a Pacotes** , escolha se pretende adicionar os controladores a um pacote e clique em **Seguinte**. Considere o seguinte procedimento para adicionar os controladores a um pacote:  

   -   Selecione os pacotes de controladores utilizados para distribuir os controladores de dispositivo.  

        Opcionalmente, clique em **Novo Pacote** para criar um novo pacote de controladores. Ao criar um novo pacote de controladores, terá de fornecer uma partilha de rede que não se encontre em utilização por outros pacotes de controladores.  

   -   Se o pacote já tiver sido distribuído para pontos de distribuição, clique em **Sim**, na caixa de diálogo, para atualizar as imagens de arranque nos pontos de distribuição. Não é possível utilizar controladores de dispositivo que ainda não tenham sido distribuídos a pontos de distribuição. Se clicar em **Não**, tem de executar a ação **Atualizar Ponto de Distribuição** antes de a imagem de arranque incluir os controladores atualizados. Se o pacote de controlador nunca tiver sido distribuído, tem de clicar em **Distribuir Conteúdo** , no nó **Pacotes de Controladores** .  

7. Na página **Adicionar Controlador a Imagens de Arranque** , escolha se pretende adicionar os controladores de dispositivo a imagens de arranque existentes e clique em **Seguinte**. Se selecionar uma imagem de arranque, considere o seguinte:  

   > [!NOTE]  
   >  Como melhor prática, adicione apenas armazenamento em massa e controladores de dispositivos de rede às imagens de arranque em cenários de implementação do sistema operativo.  

   - Clique em **Sim** , na caixa de diálogo, para atualizar as imagens de arranque nos pontos de distribuição. Não é possível utilizar controladores de dispositivo que ainda não tenham sido distribuídos a pontos de distribuição. Se clicar em **Não**, tem de executar a ação **Atualizar Ponto de Distribuição** antes de a imagem de arranque incluir os controladores atualizados. Se o pacote de controlador nunca tiver sido distribuído, tem de clicar em **Distribuir Conteúdo** , no nó **Pacotes de Controladores** .  

   - O Configuration Manager avisa-o se a arquitetura de um ou mais controladores não correspondem à arquitetura das imagens de arranque que selecionou. Se não corresponderem, clique em **OK** e volte à página **Detalhes do Controlador** para desmarcar os controladores que não correspondem à arquitetura da imagem de arranque selecionada. Por exemplo, se selecionar uma imagem de arranque x64 e x86, todos os controladores têm de suportar ambas as arquiteturas. Se selecionar uma imagem de arranque x64, todos os controladores têm de suportar a arquitetura x64.  

     > [!NOTE]
     > - A arquitetura baseia-se na arquitetura reportada no .INF do fabricante.  
     >   -   Se um controlador suportar ambas as arquiteturas, pode importá-lo para qualquer imagem de arranque.  

   - O Configuration Manager avisa-o se adicionar controladores de dispositivo que não sejam controladores de armazenamento ou de rede a uma imagem de arranque porque na maioria dos casos, não são necessários para a imagem de arranque. Clique em **Sim** para adicionar os controladores à imagem de arranque ou em **Não** para voltar atrás e modificar a seleção de controlador.  

   - O Configuration Manager avisa-o se um ou mais controladores selecionados não estiverem assinados digitalmente de forma correta. Clique em **Sim** para continuar e clique em **Não** para voltar atrás e fazer alterações à seleção de controlador.  

8. Conclua o assistente.  

###  <a name="BKMK_ModifyDriverPackage"></a> Gerir controladores de dispositivo num pacote de controlador  
 Utilize os procedimentos seguintes para modificar pacotes de controladores e imagens de arranque. Para adicionar ou remover controladores de dispositivo, localize-os no nó **Controladores** e edite os pacotes ou as imagens de arranque a que os controladores selecionados estão associados.  

#### <a name="to-modify-the-device-drivers-in-a-driver-package"></a>Para modificar os controladores de dispositivo num pacote de controlador  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Controladores**.  

3.  No nó **Controladores** , selecione os controladores de dispositivo que pretende adicionar ao pacote de controladores.  

4.  No separador **Home page** , no grupo **Controlador** , clique em **Editar**e em **Pacotes de Controladores**.  

5.  Para adicionar um controlador de dispositivo, selecione a caixa de verificação dos pacotes de controladores aos quais pretende adicionar os controladores de dispositivo. Para remover um controlador de dispositivo, desmarque a caixa de verificação dos pacotes de controladores de que pretende remover o controlador de dispositivo.  

     Se estiver a adicionar controladores de dispositivo associados a pacotes de controladores, pode, opcionalmente, criar um novo pacote ao clicar em **Novo Pacote**, o que abre a caixa de diálogo **Novo Pacote de Controladores** .  

6.  Se o pacote já tiver sido distribuído para pontos de distribuição, clique em **Sim** , na caixa de diálogo, para atualizar as imagens de arranque nos pontos de distribuição. Não é possível utilizar controladores de dispositivo que ainda não tenham sido distribuídos a pontos de distribuição. Se clicar em **Não**, tem de executar a ação **Atualizar Ponto de Distribuição** antes de a imagem de arranque incluir os controladores atualizados. Se o pacote de controlador nunca tiver sido distribuído, tem de clicar em **Distribuir Conteúdo** , no nó **Pacotes de Controladores** . Antes de os controladores estarem disponíveis, tem de atualizar o pacote de controlador nos pontos de distribuição.  

     Clique em **OK**.  

###  <a name="BKMK_ManageDriversBootImage"></a> Gerir controladores de dispositivo numa imagem de arranque  
 Pode adicionar controladores do dispositivo do Windows que tenham sido importados para o catálogo de controladores a imagens de arranque. Para adicionar controladores de dispositivos a uma imagem de arranque, utilize as seguintes diretrizes:  

- Adicione apenas controladores de dispositivos de armazenamento em massa e de adaptador de rede a imagens de arranque, pois normalmente não são necessários outros tipos de controladores. Os controladores que não são obrigatórios aumentam desnecessariamente o tamanho da imagem de arranque.  

- Adicione apenas controladores de dispositivos para Windows 10 a uma imagem de arranque, uma vez que a versão necessária do Windows PE se baseia no Windows 10.  

- Certifique-se de que utiliza o controlador de dispositivo correto para a arquitetura da imagem de arranque.  Não adicione um controlador de dispositivo de x86 a uma imagem de arranque de x64.  

  Utilize o seguinte procedimento para adicionar ou remover controladores de dispositivo numa imagem de arranque.  

#### <a name="to-modify-the--device-drivers-associated-with-a-boot-image"></a>Para modificar os controladores de dispositivo associados a uma imagem de arranque  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Controladores**.  

3. No nó **Controladores**, selecione os controladores de dispositivo que pretende adicionar ao pacote de controladores.  

4. No separador **Home page** , no grupo **Controlador** , clique em **Editar**e em **Imagens de arranque**.  

5. Para adicionar um controlador de dispositivo, selecione a caixa de verificação da imagem de arranque à qual pretende adicionar os controladores de dispositivo. Para remover um controlador de dispositivo, desmarque a caixa de verificação da imagem de arranque de que pretende remover o controlador de dispositivo.  

6. Se não quiser atualizar os pontos de distribuição em que a imagem de arranque está armazenada, desmarque a caixa de verificação **Atualizar pontos de distribuição após concluir** . Por predefinição, os pontos de distribuição são atualizados quando a imagem de arranque é atualizada.  

    Clique em **OK** e considere o seguinte:  

   - Clique em **Sim** , na caixa de diálogo, para atualizar as imagens de arranque nos pontos de distribuição. Não é possível utilizar controladores de dispositivo que ainda não tenham sido distribuídos a pontos de distribuição. Se clicar em **Não**, tem de executar a ação **Atualizar Ponto de Distribuição** antes de a imagem de arranque incluir os controladores atualizados. Se o pacote de controlador nunca tiver sido distribuído, tem de clicar em **Distribuir Conteúdo** , no nó **Pacotes de Controladores** .  

   - O Configuration Manager avisa-o se a arquitetura de um ou mais controladores não correspondem à arquitetura das imagens de arranque que selecionou. Se não corresponderem, clique em **OK** e volte à página **Detalhes do Controlador** para desmarcar os controladores que não correspondem à arquitetura da imagem de arranque selecionada. Por exemplo, se selecionar uma imagem de arranque x64 e x86, todos os controladores têm de suportar ambas as arquiteturas. Se selecionar uma imagem de arranque x64, todos os controladores têm de suportar a arquitetura x64.  

     > [!NOTE]
     > - A arquitetura baseia-se na arquitetura reportada no .INF do fabricante.  
     >   -   Se um controlador suportar ambas as arquiteturas, pode importá-lo para qualquer imagem de arranque.  

   - O Configuration Manager avisa-o se adicionar controladores de dispositivo que não sejam controladores de armazenamento ou de rede a uma imagem de arranque porque na maioria dos casos, não são necessários para a imagem de arranque. Clique em **Sim** para adicionar os controladores à imagem de arranque ou em **Não** para voltar atrás e modificar a seleção de controlador.  

   - O Configuration Manager avisa-o se um ou mais controladores selecionados não estiverem assinados digitalmente de forma correta. Clique em **Sim** para continuar e clique em **Não** para voltar atrás e fazer alterações à seleção de controlador.  

7. Clique em **OK**.  

###  <a name="BKMK_DriverActions"></a> Ações adicionais para controladores de dispositivo  
 Pode realizar ações adicionais para gerir os controladores de dispositivo quando seleciona um ou mais controladores de dispositivo no nó **Controladores** . Estas ações incluem o seguinte:  

|Action|Descrição|  
|------------|-----------------|  
|**Categorizar**|Elimina, gere ou define uma categoria administrativa para os controladores de dispositivo selecionados.|  
|**Eliminar**|Remove o controlador de dispositivo do nó **Controladores** e remove também o controlador dos pontos de distribuição associados.|  
|**Desativar**|Proíbe a instalação do controlador de dispositivo. Pode desativar temporariamente controladores de dispositivo para que os computadores de cliente do Configuration Manager e sequências de tarefas não é possível instalá-los quando estiver a implementar sistemas operativos. **Nota:**  A ação de Desativação apenas impede que os controladores instalem com o passo de sequência de tarefas aplicar controladores automaticamente.|  
|**Ativar**|Permite que os computadores de cliente do Configuration Manager e sequências de tarefas instale o controlador de dispositivo quando o sistema operativo é implementado.|  
|**Moverr**|Move o controlador de dispositivo para outra pasta do nó **Controladores** .|  
|**Propriedades**|Abre a caixa de diálogo **Propriedades** , onde pode consultar e alterar as propriedades do controlador de dispositivo. Por exemplo, poderá mudar o nome e a descrição do controlador de dispositivo, ativá-lo ou especificar em que plataformas poderá ser executado.|  

##  <a name="BKMK_TSDrivers"></a> Utilizar sequências de tarefas para instalar controladores de dispositivo  
 Utilize sequências de tarefas para automatizar a forma como o sistema operativo é implementado. Cada passo da sequência de tarefas pode executar uma ação específica, como por exemplo, instalar um controlador de dispositivo. Pode utilizar estes dois passos da sequência de tarefas para instalar controladores de dispositivos durante a implementação de sistemas operativos:  

- [Aplicar controladores automaticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): Este passo permite-lhe fazer corresponder e instalar controladores de dispositivo como parte da implementação do sistema operativo automaticamente. Pode configurar o passo da sequência de tarefas para instalar apenas o controlador mais compatível com cada dispositivo de hardware detetado ou especificar que o passo da sequência de tarefas instale todos os controladores compatíveis com cada dispositivo de hardware detetado, deixando então que a Configuração do Windows escolha o controlador mais adequado. Além disso, pode especificar uma categoria de controladores de dispositivos para limitar os controladores que estão disponíveis neste passo.  

- [Aplicar pacote de controlador](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): Este passo permite-lhe disponibilizar todos os controladores de dispositivo num pacote de controladores específico para a configuração do Windows. Nos pacotes de controladores especificados, a Configuração do Windows procura os controladores de dispositivos necessários. Quando cria suportes de dados autónomos, tem de utilizar este passo para instalar controladores de dispositivo.  

  Quando utiliza estes passos da sequência de tarefas, também pode especificar a forma como os controladores de dispositivos são instalados no computador em que implementa o sistema operativo. Para obter mais informações, consulte [gerir sequências de tarefas para automatizar tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md).  

##  <a name="BKMK_InstallingDeviceDiriversTS"></a> Utilizar sequências de tarefas para instalar controladores de dispositivo em computadores  
 Utilize o procedimento seguinte para instalar controladores de dispositivo como parte da implementação do sistema operativo.  

#### <a name="use-a-task-sequence-to-install-device-drivers"></a>Utilizar uma sequência de tarefas para instalar controladores de dispositivo  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3. No nó **Sequências de Tarefas** , selecione a sequência de tarefas que pretende modificar para instalar o controlador de dispositivo e clique em **Editar**.  

4. Vá para a localização onde quer adicionar os passos **Controlador** , clique em **Adicionar**e selecione **Controladores**.  

5. Adicione o passo **Aplicar Controladores Automaticamente** se quiser que a sequência de tarefas instale todos os dispositivos de controlador ou as categorias específicas indicadas. Especifique as opções do passo no separador **Propriedades** e outras condições para o mesmo no separador **Opções** .  

    Adicione o passo **Aplicar Pacote de Controlador** se pretender que a sequência de tarefas instale apenas os controladores de dispositivo do pacote especificado. Especifique as opções do passo no separador **Propriedades** e outras condições para o mesmo no separador **Opções** .  

   > [!IMPORTANT]  
   >  Pode selecionar **Desativar este passo** no separador **Opções** para desativar o passo para resolver problemas da sequência de tarefas.  

6. Clique em **OK** para guardar a sequência de tarefas.  

   Para obter mais informações sobre como criar uma sequência de tarefas para instalar um sistema operativo, consulte [criar uma sequência de tarefas para instalar um sistema operativo](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).  

##  <a name="BKMK_DriverReports"></a> Relatórios de gestão de controladores  
 Na categoria de relatórios **Gestão do Controlador** , pode utilizar vários relatórios para determinar as informações gerais sobre os controladores de dispositivos no catálogo de controladores. Para obter mais informações sobre relatórios, consulte [relatórios](../../core/servers/manage/reporting.md).
