---
title: Plano para automatizar tarefas
titleSuffix: Configuration Manager
description: Planear antes de criar sequências de tarefas para automatizar tarefas com o Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ea1b104dfbdf23a080bc71da94b88cdcad31fa1
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755953"
---
# <a name="planning-considerations-for-automating-tasks-in-configuration-manager"></a>Considerações sobre planeamento para automatizar tarefas no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode criar sequências de tarefas para automatizar tarefas no ambiente do Configuration Manager. Estas tarefas abrangem desde a captura de um sistema operacional num computador de referência para a implantação de sistema operacional para um ou mais computadores de destino. As ações da sequência de tarefas são definidas nos passos individuais da sequência. Quando a sequência de tarefas é executado, ele executa as ações de cada passo no nível da linha de comandos no contexto do sistema Local. Este comportamento significa que a sequência de tarefas é executado totalmente automatizada sem qualquer intervenção do utilizador. 



##  <a name="BKMK_TSStepsActions"></a> Passos de sequência de tarefas e ações  

 Passos são os componentes básicos de uma sequência de tarefas. Eles podem incluem comandos como:  
   - Configurem e capturem o sistema operativo do computador de referência  
   - Instalar o Windows, drivers de hardware, o cliente do Configuration Manager e o software no computador de destino   


 As ações do passo da definem os comandos de um passo de sequência de tarefas. Existem dois tipos de ações:  
   - Uma ação que define utilizando uma cadeia de caracteres da linha de comandos é referida como um *ação personalizada*  
   - Uma ação que está predefinida pelo Configuration Manager é referida como um *ações incorporadas*.  


 Uma sequência de tarefas pode executar qualquer combinação de ações personalizadas e incorporadas.  

 Passos de sequência de tarefas também poderão incluir condições que controlam o comportamento dos passos. Esses comportamentos incluem interromper a sequência de tarefas ou continuar a sequência de tarefas se ocorrer um erro. Um tipo de condição é uma variável de sequência de tarefas. Por exemplo, utilizar o **SMSTSLastActionRetCode** variável para testar a condição do passo anterior. Adicione condições a um único passo ou um grupo de passos.  

 A sequência de tarefas processa os passos sequencialmente. Esta sequência inclui a ação do passo e quaisquer condições no passo. Quando o Configuration Manager começa a processar um passo de sequência de tarefas, não começa a próxima etapa, até que a ação anterior seja concluída. 

 Uma sequência de tarefas é considerada concluída quando: 
   - Todos os seus passos estiverem concluídos  
   - Uma falha de um passo faz com que o Configuration Manager para interromper a execução da sequência de tarefas antes de todos os passos são concluídos.  


 Por exemplo, se o passo de sequência de tarefas não conseguir localizar uma imagem ou pacote referenciados num ponto de distribuição, a sequência de tarefas inclui uma referência incompleta. O Configuration Manager deixa de ser executada a sequência de tarefas nesse ponto, a menos que o passo falhado possua uma condição para continuar quando ocorre um erro.  

 > [!IMPORTANT]  
 >  Por predefinição, uma sequência de tarefas falhará se falhar um passo ou ação. Se pretender que a sequência de tarefas continue mesmo quando um passo falhar, edite a sequência de tarefas, clique no separador **Opções** e, em seguida, selecione **Continuar com o erro**.  

 Para obter mais informações sobre os passos que podem ser adicionados a uma sequência de tarefas, consulte [passos de sequência de tarefas](/sccm/osd/understand/task-sequence-steps).  



##  <a name="BKMK_TSGroups"></a> Grupos de sequências de tarefas  

 Pode agrupar vários passos numa sequência de tarefas. Um grupo de sequência de tarefas é composta por um nome, uma descrição opcional e eventuais condições opcionais. A sequência de tarefas avalia as condições de grupo como uma unidade antes de prosseguir com a próxima etapa. Aninhar grupos dentro de uns aos outros ou incluir uma mistura de passos e subgrupos. Os grupos são úteis para combinar diversos passos que partilhem uma condição comum.  

 Atribua um nome para grupos de sequências de tarefas. Ele não tem de ser exclusivo. Também poderá fornecer uma descrição opcional para o grupo de sequência de tarefas.  

 > [!IMPORTANT]  
 >  Por predefinição, um grupo de sequência de tarefas falhará se falhar qualquer passo ou grupo incorporado no grupo. Se pretender que a sequência de tarefas continue após a definir um passo ou grupo incorporado falhar, o **continuar com o erro** opção no passo ou grupo.  

 A tabela seguinte mostra como o **continuar com o erro** opção funciona quando agrupa passos.  

 Neste exemplo, existem dois grupos de sequências de tarefas que incluem três passos de sequência tarefas cada.  

 |Grupo ou passo de sequência de tarefas|Definição Continuar com o erro|  
 |---------------------------------|-------------------------------|  
 |**Grupo de sequência de tarefas 1**|**Continuar com o erro** selecionado.|  
 |Passo de sequência de tarefas 1|**Continuar com o erro** selecionado.|  
 |Passo de sequência de tarefas 2|Não definido.|  
 |Passo de sequência de tarefas 3|Não definido.|  
 |**Grupo de sequência de tarefas 2**|Não definido.|  
 |Passo de sequência de tarefas 4|Não definido.|  
 |Passo de sequência de tarefas 5|Não definido.|  
 |Passo de sequência de tarefas 6|Não definido.|  


 -   Se o passo de sequência de tarefas 1 falhar, a sequência de tarefas continua com o passo de sequência de tarefas 2.  

 -   Se o passo de sequência de tarefas 2 falhar, a sequência de tarefas não é executado o passo de sequência de tarefas 3. Porque o grupo de sequência de tarefas 1 está configurado para **continuar com o erro**, a sequência de tarefas continua para o grupo de sequência de tarefas 2. -Lo em seguida, executa o passo de sequência de tarefas 4.  

 -   Se o passo de sequência de tarefas 4 falhar, não existem mais passos são executados. A sequência de tarefas falha porque o **continuar com o erro** definição não está configurada para o grupo de sequência de tarefas 2.  



## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas filho a uma sequência de tarefas
 <!--1261338--> A partir do Configuration Manager versão 1710, pode adicionar um novo passo de sequência de tarefas que executa outra sequência de tarefas. Este passo cria uma relação principal-subordinado entre sequências de tarefas. Utilizar este passo permite-lhe criar mais sequências de tarefas modulares que pode reutilizar.  

 Para obter mais informações, consulte [executar a sequência de tarefas](/sccm/osd/understand/task-sequence-steps#child-task-sequence). 

 > [!Note]  
 > O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



##  <a name="BKMK_TSVariables"></a> Variáveis de sequência de tarefas  

 Variáveis de sequência de tarefas são um conjunto de pares nome / valor. Eles fornecem configuração e definições de implementação do sistema operacional para o computador, sistema operacional e tarefas de configuração de estado de utilizador num cliente do Configuration Manager. As variáveis de sequência de tarefas fornecem um mecanismo de configuração e personalização dos passos de uma sequência de tarefas.  

 Quando executa uma sequência de tarefas, ele armazena muitas das definições de sequência de tarefas como variáveis de ambiente. Pode aceder ou alterar os valores de variáveis de sequência de tarefas incorporadas. Também pode criar nova tarefa a variáveis de sequência para personalizar a forma como uma sequência de tarefas é executado num computador de destino.  

 Utilize variáveis de sequência de tarefas para realizar as seguintes ações:  

 -   Configurar as definições para uma ação de sequência de tarefas  

 -   Fornecer argumentos de linha de comandos para um passo de sequência de tarefas  

 -   Avaliar uma condição que determina se um passo de sequência de tarefas ou grupo é executada  

 -   Fornecer valores para scripts personalizados utilizados numa sequência de tarefas  


 Por exemplo, tem uma sequência de tarefas que inclui um **associar domínio ou grupo de trabalho** passo de sequência de tarefas. Implemente a sequência de tarefas para diferentes coleções, em que a associação da coleção é determinada pela associação ao domínio. Especifique uma variável de sequência de tarefas por coleção para o nome de domínio de cada coleção. Em seguida, utilize essa variável de sequência de tarefas para fornecer o nome de domínio apropriado na sequência de tarefas.  

 Para obter mais informações, consulte [como utilizar variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables).



##  <a name="BKMK_TSCreate"></a> Criar uma sequência de tarefas  

 Crie sequências de tarefas utilizando o Assistente de Criação de Sequência de Tarefas. O assistente pode criar sequências de tarefas incorporadas que efetuem tarefas específicas ou sequências de tarefas personalizadas que podem executar muitas tarefas diferentes. O assistente permite-lhe criar os seguintes tipos de sequências de tarefas:

 - Instalar uma imagem de sistema operacional existente num computador de destino  

 - Compilar e capturar uma imagem de SO de um computador de referência  

 - Atualizar para o Windows 10 de um pacote de atualização do sistema operacional no computador de destino   

 - Criar uma sequência de tarefas personalizada que realiza uma tarefa personalizada ou a implementação do SO especializada  


 Para obter mais informações, consulte [criar sequências de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTaskSequence).  



##  <a name="BKMK_TSEdit"></a> Editar uma sequência de tarefas  

 Edita a sequência de tarefas, utilizando o **Editor de sequência de tarefas**. O editor pode efetuar as seguintes alterações à sequência de tarefas:  

 - Adicionar ou remover passos da sequência de tarefas  

 - Alterar a ordem dos passos da sequência de tarefas  

 - Adicionar ou remover grupos de passos  

 - Especificar se a sequência de tarefas continua quando ocorre um erro  

 - Adicionar condições aos passos e grupos de uma sequência de tarefas  


 > [!IMPORTANT]  
 >  Se a sequência de tarefas tiver quaisquer referências não associadas a um objeto em resultado da edição, o editor necessita de que corrigir a referência antes de pode fechar. Ações possíveis incluem:  
 > - Corrigir a referência  
 > - Eliminar o objeto sem referência da sequência de tarefas  
 > - Desativar temporariamente o passo de sequência de tarefas falhado até a referência quebrada é corrigida ou removida  


 Para obter mais informações sobre como editar sequências de tarefas, consulte [editar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  



##  <a name="BKMK_TSDeploy"></a> Implementar uma sequência de tarefas  

 Implemente uma sequência de tarefas nos computadores de destino que estão em qualquer coleção do Configuration Manager. Utilizar o incorporado **todos os computadores desconhecidos** coleção para implementar sistemas operativos em computadores desconhecidos. Não é possível implementar uma sequência de tarefas em coleções de utilizadores.  

 > [!IMPORTANT]  
 >  Não implemente sequências de tarefas que instalem sistemas operativos em coleções inadequadas. Certifique-se de que a coleção em que pretende implementar a sequência de tarefas inclui apenas os computadores onde pretende instalar o sistema operacional. Para ajudar a impedir a implementações de sistema operacional indesejadas, configure definições para implementações de alto risco. Para obter mais informações, consulte [definições para gerir implementações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

 Cada computador de destino que recebe a sequência de tarefas executa a sequência de tarefas, de acordo com as definições especificadas na implementação. As sequências de tarefas em si não contém ficheiros ou programas associados. Todos os ficheiros que faz referência a uma sequência de tarefas já tem de estar presente no computador de destino ou residir num ponto de distribuição que os clientes podem aceder. 

 > [!NOTE]  
 > A sequência de tarefas instala os pacotes que são referenciados por programas, mesmo que o programa ou o pacote já está instalado no computador de destino. 
 > 
 > Se a sequência de tarefas instala uma aplicação, a aplicação é instalada apenas se as regras de requisitos para a aplicação são cumpridas e a aplicação já não estiver instalada, com base no método de deteção especificado para a aplicação.  

 O cliente do Configuration Manager é executado uma implementação de sequência de tarefas quando transfere a política de cliente. Para disparar essa ação em vez de aguardar até o próximo ciclo de consulta, consulte [iniciar a obtenção de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

 Ao implementar sequências de tarefas em dispositivos Windows Embedded que estão ativados com um filtro de escrita, pode especificar se pretende desativar o filtro de escrita no dispositivo durante a implementação e, em seguida, reiniciar o dispositivo após a implementação. Se o filtro de escrita não estiver desativado, a sequência de tarefas é implementada para uma sobreposição temporária e não estará disponível quando o dispositivo for reiniciado.  

 > [!NOTE]  
 >  Quando implementa uma sequência de tarefas num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Isto permite-lhe gerir quando o filtro de escrita é desabilitado e habilitado e quando o dispositivo for reiniciado.  
 >   
 >  Se os clientes transferirem sequências de tarefas fora da janela de manutenção, a sequência de tarefas é transferida duas vezes. Neste cenário, o cliente transfere a sequência de tarefas, desativa o filtro de escrita, reinicia o computador e, em seguida, transfere a sequência de tarefas novamente. Este comportamento acontece porque a sequência de tarefas foi originalmente transferida para a sobreposição temporária, o que é apagada quando o dispositivo for reiniciado.  

 Para obter mais informações sobre como implementar sequências de tarefas, consulte a [implementar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  



##  <a name="BKMK_TSExportImport"></a> Exportar e importar sequências de tarefas  

 O Configuration Manager permite-lhe exportar e importar sequências de tarefas. Quando exporta uma sequência de tarefas, pode incluir os objetos referenciados pela sequência de tarefas. 

 Para obter mais informações, consulte [exportar e importar sequências de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ExportImport).  



##  <a name="BKMK_TSRun"></a> Executar uma sequência de tarefas  

 Sequências de tarefas são sempre executadas utilizando a conta Sistema Local. Quando a sequência de tarefas é executada, o cliente do Configuration Manager começa por verificar quaisquer pacotes referenciados antes de iniciar os passos da sequência de tarefas. Se ele não é possível validar ou transferir um pacote referenciado, a sequência de tarefas devolve um erro para o passo de sequência de tarefas associados.  

 > [!Note]  
 > O passo de sequência de tarefas **executar linha de comandos** fornece a capacidade de executar um comando como uma conta diferente.  

 Se configurar uma implementação de sequência de tarefas para transferir e executar, o cliente do Configuration Manager transfere todo o conteúdo dependente para seu cache. Se o tamanho da cache do cliente é demasiado pequeno ou não é possível localizar o conteúdo, a sequência de tarefas falhará. O cliente gera uma mensagem de estado. 

 Também pode especificar que o cliente transfere conteúdo apenas quando necessário. Para efetuar esta ação, selecione **transferir o conteúdo localmente quando necessário para executar a sequência de tarefas** na implementação de sequência de tarefas. Outra opção é **executar programa a partir do ponto de distribuição**. Com esta opção, o cliente instala os ficheiros diretamente a partir do ponto de distribuição sem transferi-los primeiro para a cache. 

 Ao configurar a implementação de sequência de tarefas como **disponível**, se o cliente não conseguir localizar conteúdo dependente para a sequência de tarefas, envia imediatamente um erro. Para uma **necessário** implementação, o cliente de Configuration Manager aguardará nesta situação. Tentar transferir o conteúdo até ao prazo, no caso do conteúdo ainda não é replicado para uma localização de conteúdo que o cliente pode aceder.  

 Quando uma sequência de tarefas for concluída com êxito ou falha, o Configuration Manager regista neste estado no histórico do cliente. 

 Assim que uma sequência de tarefas for iniciada num computador, não é possível cancelar ou impedi-lo.  

 > [!IMPORTANT]  
 >  Se um passo de sequência de tarefas requer o reinício do computador, o cliente deve conseguir arrancar para uma partição de disco formatado. Caso contrário, a sequência de tarefas falha independentemente de qualquer tratamento de erros que especificou na sequência de tarefas.  

 Quando um objeto dependente de uma sequência de tarefas é atualizado para uma versão mais recente, qualquer sequência de tarefas que referencia o pacote é atualizada automaticamente. Faz referência a versão mais recente, independentemente de quantas atualizações que implementar.  



##  <a name="BKMK_TSMaintenanceWindow"></a> Utilizar uma janela de manutenção para especificar quando pode executar uma sequência de tarefas  

 Pode especificar quando a sequência de tarefas pode a ser executada definindo uma janela de manutenção para a coleção de dispositivos. Configurar janelas de manutenção com uma data de início, uma para o início e de fim tempo e um padrão de periodicidade. Ao definir a agenda para a janela de manutenção, pode especificar que a janela de manutenção só se aplica a sequências de tarefas. Para obter mais informações, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

 > [!IMPORTANT]  
 >  Quando configura uma janela de manutenção para executar uma sequência de tarefas, uma vez as sequências de tarefas iniciadas, continuam a ser executadas mesmo que a janela de manutenção se feche.  



##  <a name="BKMK_TSNetworkAccessAccount"></a> Sequências de tarefas e conta de acesso à rede  

 Apesar de sequências de tarefas serem executadas apenas no contexto da conta do sistema Local, poderá ter de configurar o [conta de acesso de rede](/sccm/core/plan-design/hierarchy/accounts#network-access) nas seguintes circunstâncias:  

 - Se a sequência de tarefas tenta aceder ao conteúdo do Configuration Manager em pontos de distribuição. Configurar a conta de acesso à rede corretamente ou a sequência de tarefas falhará.   

 - Quando utiliza uma imagem de arranque para iniciar uma implantação de sistema operacional. Neste caso, o Configuration Manager utiliza o ambiente do Windows PE, que não é um SO completo. O ambiente do Windows PE utiliza um nome aleatório gerado automaticamente que não seja um membro de qualquer domínio. Se não configurar corretamente a conta de acesso de rede, o computador não é possível acessar o conteúdo necessário para a sequência de tarefas.  


 > [!NOTE]  
 >  A conta de acesso à rede nunca é utilizada como o contexto de segurança para executar programas, instalar aplicações, instalar atualizações ou executar sequências de tarefas. A conta de acesso de rede só é utilizada para aceder aos recursos associados na rede.  


 Para obter mais informações sobre a conta de acesso de rede, consulte [conta de acesso à rede](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#bkmk_NAA).  



##  <a name="BKMK_TSCreateMedia"></a> Criar suportes de dados para sequências de tarefas  

 É possível escrever sequências de tarefas e seus arquivos relacionados e dependências para vários tipos de suportes de dados. O Configuration Manager suporta a mídia removível como um DVD ou uma USB flash drive para captura, autónomos e suportes de dados. Suportes de dados utiliza um arquivo de imagem (WIM) do Windows.  

 Quando cria suportes de dados, especifique uma palavra-passe para controlar o acesso. Em seguida, uma pessoa tem de introduzir a palavra-passe no computador de destino para executar a sequência de tarefas.  

 Quando executa uma sequência de tarefas do suporte de dados, a arquitetura de processador especificado do suporte de dados não é reconhecida. Se a arquitetura especificada não corresponde ao computador de destino, a sequência de tarefas continua a tentar executar. Se a arquitetura do suporte de dados não corresponde à arquitetura do computador de destino, a sequência de tarefas falhará.  

 Para obter mais informações, consulte [criar suporte de dados de sequência de tarefas](/sccm/osd/deploy-use/create-task-sequence-media).  


### <a name="media-types"></a>Tipos de suportes de dados
 O Configuration Manager suporta os seguintes tipos de suportes de dados:  

#### <a name="capture-media"></a>Suporte de dados de captura
 Capture uma imagem de SO que configure e crie fora da infraestrutura do Configuration Manager de capturas de suporte de dados. O suporte de dados de captura pode conter programas personalizados que podem ser executados antes da execução de uma sequência de tarefas. O programa personalizado pode interagir com a área de trabalho, solicitar ao utilizador valores de entrada ou criar variáveis para serem utilizadas pela sequência de tarefas.  

 Para obter mais informações, consulte [criar suporte de dados de captura](/sccm/osd/deploy-use/create-capture-media).  

#### <a name="stand-alone-media"></a>Suporte de dados autónomo
 O suporte de dados autónomo contém a sequência de tarefas e todos os objetos associados necessários à execução da sequência de tarefas. Tarefas de suporte de dados autónomo sequências podem ser executadas quando o Configuration Manager tem limitada ou nenhuma conectividade à rede. Execute o suporte de dados autónomo das seguintes formas:  

 - Se o computador de destino não está inicializado, a imagem do Windows PE associada com a sequência de tarefas é utilizada a partir do suporte de dados autónomo e começa a sequência de tarefas.  

 - Inicie manualmente o suporte de dados autónomo. Se um utilizador tem sessão iniciado no computador, eles podem iniciar a sequência de tarefas do suporte de dados.  


 > [!IMPORTANT]  
 >  Os passos de uma sequência de tarefas de suporte de dados autónomo tem de ser capazes de executar sem obter dados a partir da rede. Caso contrário, o passo de sequência de tarefas que tenta obter os dados de falha. Por exemplo, um passo de sequência de tarefas que requer um ponto de distribuição para obter um pacote falhará. Se o suporte de dados autónomo contém o pacote necessário, o passo de sequência de tarefas for concluída com êxito.  


 Para obter mais informações, consulte [criar suporte de dados autónomo](/sccm/osd/deploy-use/create-stand-alone-media).  

#### <a name="bootable-media"></a>Suporte de dados de arranque
 Suportes de dados contém os ficheiros necessários para iniciar um computador de destino para que ele pode se conectar à infraestrutura do Configuration Manager. Em seguida, determina que sequências de tarefas executada com base em suas associações de coleção. Este suporte de dados não inclui a sequência de tarefas ou objetos dependentes. Em vez disso, o cliente transfere o conteúdo através da rede. Esse método é útil para novos computadores ou implementações bare-metal, quando nenhum sistema operacional está no computador de destino.  

 Para obter mais informações, consulte [criar suportes de dados](/sccm/osd/deploy-use/create-bootable-media).  

#### <a name="prestaged-media"></a>Suportes de dados de pré-configuração
 Suporte de dados pré-configurado implementa uma imagem de SO para um computador de destino que não está aprovisionado. O suporte de dados pré-configurado é armazenado como um arquivo de imagem (WIM) do Windows. Este ficheiro pode ser instalado num computador bare-metal pelo fabricante ou num centro de transição empresarial. Dos benefícios de suporte de dados pré-configurado é que esses locais não necessitam de uma ligação ao ambiente do Configuration Manager.  

 Para obter mais informações, consulte [criar suportes de dados pré-configurados](/sccm/osd/deploy-use/create-prestaged-media).  
