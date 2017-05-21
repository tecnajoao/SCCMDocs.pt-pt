---
title: "Expandir o inventário de hardware | Documentos do Microsoft"
description: "Aprenda formas de expandir o inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: 10
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: 10c1d11a5cf06f3587fb6066801c0eab802dcf9a
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Como expandir o inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Inventário de hardware lê as informações a partir de Windows PCs utilizando o Windows Management Instrumentation (WMI). WMI é a implementação Microsoft de baseada na web Enterprise Management (WBEM), uma norma da indústria para aceder a informações de gestão de uma empresa. Em versões anteriores do Configuration Manager, pode expandir o inventário de hardware, modificando sms_def o ficheiro no servidor do site. Este ficheiro continha uma lista de classes WMI que pode ser lido pelo inventário de hardware. Se editasse este ficheiro, podia ativar e desativar as classes existentes, bem como criar novas classes para o inventário.  

O ficheiro Configuration.mof é utilizado para definir as classes de dados para inventariados pelo inventário de hardware no cliente e é inalterados desde a Configuration Manager 2012. Pode criar classes de dados para inventariar classes de dados existentes ou personalizados do repositório WMI ou chaves de registo presentes em sistemas cliente.  

 O ficheiro Configuration.mof também define e regista os fornecedores WMI que acedem a informações de dispositivos durante o inventário de hardware. Registar fornecedores define o tipo de fornecedor a utilizar e as classes que o fornecedor suporta.  

 Quando os clientes do Configuration Manager pedirem uma política, por exemplo, durante o intervalo de consulta da política de cliente padrão, o Configuration.mof está ligado para o corpo de política. Em seguida, este ficheiro é transferido e compilado pelos clientes. Quando adicionar, modificar ou eliminar classes de dados a partir do ficheiro Configuration.mof, os clientes compilam automaticamente estas alterações efetuadas em classes de dados relacionadas com o inventário. Mais nenhuma ação é necessária para classes de inventário de dados novos ou modificados em clientes do Configuration Manager. Este ficheiro está localizado em **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** nos servidores de site primários.  

 No Configuration Manager, já não edita o ficheiro sms_def MOF como fez no Configuration Manager 2007. Em vez disso, pode ativar e desativar classes WMI e adicionar novas classes para recolher pelo inventário de hardware, utilizando as definições do cliente. O Configuration Manager fornece os métodos seguintes para expandir o inventário de hardware.  

> [!NOTE]  
>  Se tiver alterado manualmente o ficheiro de Configuration.mof para adicionar classes de inventário personalizada, estas alterações serão substituídas quando atualizar para versão 1602. Para continuar a utilizar classes personalizadas depois de atualizar, tem de adicionar estas para a secção "Adicionadas extensões" do ficheiro Configuration.mof depois de atualizar para 1602.  
> No entanto, é necessário não modificar nada acima nesta secção, como estas secções estejam reservadas para modificação pelo Configuration Manager. Está disponível uma cópia de segurança do Configuration.mof em:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Método|Mais informações|  
|------------|----------------------|  
|Ativar ou desativar classes de inventário existentes|Ativar ou desativar as classes de inventário predefinido ou criar as definições que permitem-lhe recolher classes de inventário de hardware diferente a partir de coleções de clientes especificadas de cliente personalizadas. Consulte o [para ativar ou desativar as classes de inventário existente](#BKMK_Enable) procedimento deste tópico.|  
|Adicionar uma nova classe de inventário|Adicione uma nova classe de inventário a partir do espaço de nomes WMI do outro dispositivo. Consulte o [para adicionar uma nova classe de inventário](#BKMK_Add) procedimento deste tópico.|  
|Importar e exportar classes de inventário de hardware|Importar e exportar ficheiros de formato de objeto gerido (MOF) que contêm classes de inventário a partir da consola do Configuration Manager. Consulte o [para importar as classes de inventário de hardware](#BKMK_Import) e [para exportar as classes de inventário de hardware](#BKMK_Export) procedimentos neste tópico.|  
|Criar Ficheiros NOIDMIF|Utilize os ficheiros NOIDMIF para recolher informações sobre os dispositivos cliente que não pode ser inventariado pelo Configuration Manager. Por exemplo, pode pretender recolher informações sobre o número de ativos de dispositivo existentes apenas como uma etiqueta no dispositivo. O inventário NOIDMIF é automaticamente associado ao dispositivo cliente a partir do qual foi recolhido. Consulte o artigo [para criar os ficheiros NOIDMIF](#BKMK_NOIDMIF) neste tópico.|  
|Criar Ficheiros IDMIF|Utilize os ficheiros IDMIF para recolher informações sobre elementos na sua organização que não estão associadas um cliente do Configuration Manager, por exemplo, os projetores, photocopiers e impressoras de rede. Consulte o artigo [para criar ficheiros IDMIF](#BKMK_IDMIF) neste tópico.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimentos para expandir o inventário de hardware  
Estes procedimentos ajudam a configurar as predefinições de cliente para o inventário de hardware e aplicam-se a todos os clientes na sua hierarquia. Se pretender que estas definições aplicam-se para apenas alguns clientes, crie uma definição de dispositivo de cliente personalizadas e atribua-a para uma coleção de clientes específicos. Consulte o artigo [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="BKMK_Enable"></a> Para ativar ou desativar as classes de inventário existentes  

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente** > **predefinições de cliente**.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  No **predefinições de cliente** diálogo caixa, selecione **inventário de Hardware**.  

6.  Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  

7.  Na caixa de diálogo **Classes de Inventário de Hardware** , selecione ou desmarque as classes e propriedades de classes que pretende que sejam recolhidas pelo inventário de hardware. Pode expandir classes para selecionar ou desmarcar propriedades individuais dentro dessa classe. Utilize o campo **Procurar classes de inventário** para procurar classes individuais.  

    > [!IMPORTANT]  
    >  Ao adicionar novas classes de inventário de hardware do Configuration Manager, irá aumentar o tamanho do ficheiro de inventário recolhido e enviado para o servidor de site. Isto poderá afetar negativamente o desempenho da rede e o site do Configuration Manager. Ative apenas as classes de inventário que pretende recolher.  


###  <a name="BKMK_Add"></a> Para adicionar uma nova classe de inventário  

Só é possível adicionar classes de inventário do servidor de nível superior na hierarquia e ao modificar as predefinições de cliente. Esta opção não está disponível quando criar definições personalizadas do dispositivo.

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente** > **predefinições de cliente**.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  No **predefinições de cliente** diálogo caixa, selecione **inventário de Hardware**.  

6.  No **definições do dispositivo** lista, escolha **definir Classes**.  

7.  No **Classes de inventário de Hardware** diálogo caixa, selecione **adicionar**.  

8.  Na caixa de diálogo **Adicionar Classe de Inventário de Hardware** , clique em **Ligar**.  

9. Na caixa de diálogo **Ligar à Windows Management Instrumentation (WMI)** , especifique o nome do computador a partir do qual irá obter as classes WMI e o espaço de nomes WMI a utilizar para obter as classes. Se pretender obter todas as classes abaixo do espaço de nomes WMI que especificou, clique em **Recursiva**. Se o computador ao qual está a ligar não for o computador local, forneça as credenciais de início de sessão para uma conta que tenha permissão para aceder ao WMI no computador remoto.  

10. Escolher **ligar**.  

11. No **adicionar classe de inventário de Hardware** caixa de diálogo a **classes de inventário** lista, selecione as classes WMI que pretende adicionar ao inventário de hardware do Configuration Manager.  

12. Se pretender editar informações sobre a classe WMI selecionada, escolher **editar**e no **qualificadores de classe** diálogo caixa, forneça as seguintes informações:  

    -   **Nome a apresentar** -esta será apresentada no Explorador de recursos.  

    -   **Propriedades** -especificar as unidades nas qual cada propriedade do WMI classe será apresentada.  

     Também pode designar propriedades como uma propriedade de chave para o ajudar a identificar exclusivamente cada instância da classe. Se não for definida qualquer chave para a classe e várias instâncias da classe forem comunicadas a partir do cliente, apenas a instância mais recente encontrada é armazenada na base de dados.  

     Quando tiver concluído a configuração de propriedades, clique em **OK** para fechar o **qualificadores de classe** e os outros a caixa de diálogo abrem caixas de diálogo. 


###  <a name="BKMK_Import"></a> Para importar classes de inventário de hardware  

Só pode importar classes de inventário quando modificar as predefinições de cliente. No entanto, pode utilizar definições de cliente personalizadas para importar informações que não contenham uma alteração de esquema, tal como alterar a propriedade de uma classe existente de **Verdadeiro** para **Falso**.  

1.  Na consola do Configuration Manager, escolha **administração** >  **definições de cliente** > **predefinições de cliente**.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  No **predefinições de cliente** diálogo caixa, selecione **inventário de Hardware**.  

6.  No **definições do dispositivo** lista, escolha **definir Classes**.  

7.  No **Classes de inventário de Hardware** diálogo caixa, selecione **importação**.  

8.  No **importar** caixa de diálogo, selecione ficheiro de formato MOF (Managed) que pretende importar e, em seguida, selecione o objeto a gerida **OK**. Reveja os itens que serão importados e, em seguida, clique em **importação**.  

###  <a name="BKMK_Export"></a> Para exportar classes de inventário de hardware  

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente** > **predefinições de cliente**.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  No **predefinições de cliente** diálogo caixa, selecione **inventário de Hardware**.  

6.  No **definições do dispositivo** lista, escolha **definir Classes**.  

7.  No **Classes de inventário de Hardware** diálogo caixa, selecione **exportar**.  

    > [!NOTE]  
    >  Quando exporta classes, todas as classes atualmente selecionadas serão exportadas.  

8.  No **exportar** diálogo caixa, especifique o ficheiro de formato de objeto gerido (MOF) que pretende exportar classes a e, em seguida, escolha **guardar**.  

## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Como Utilizar Ficheiros MIF (Management Information Files) para expandir o inventário de hardware  
 Utilize ficheiros de formato MIF (Management Information) para expandir as informações de inventário de hardware recolhidas dos clientes pelo Configuration Manager. Durante o inventário de hardware, as informações armazenadas em ficheiros MIF são adicionadas ao relatório de inventário de cliente e armazenadas na base de dados do site, onde pode utilizar os dados da forma mesmo que utiliza dados de inventário de cliente predefinido. Existem dois tipos de ficheiros MIF: NOIDMIF e IDMIF.

> [!IMPORTANT]  
>  Antes de poder adicionar informações a partir de ficheiros MIF na base de dados do Configuration Manager, tem de criar ou importar informações de classe para os mesmos. Para obter mais informações, veja as secções [Para adicionar uma nova classe de inventário](#BKMK_Add) e [Para importar classes de inventário de hardware](#BKMK_Import) , neste tópico.  

###  <a name="BKMK_NOIDMIF"></a> Para criar ficheiros NOIDMIF  
 Os ficheiros NOIDMIF podem ser utilizados para adicionar informações a um inventário de hardware do cliente que normalmente não pode ser recolhido pelo Configuration Manager e está associados um dispositivo de cliente específico. Por exemplo, várias empresas cada computador da organização com um número de ativos de etiqueta e, em seguida, catálogo estas manualmente. Quando cria um ficheiro NOIDMIF, estas informações podem ser adicionadas à base de dados do Configuration Manager e ser utilizadas para consultas e relatórios. Para obter informações sobre como criar os ficheiros NOIDMIF, consulte a documentação do SDK do Configuration Manager.  

> [!IMPORTANT]  
>  Quando cria um ficheiro NOIDMIF tem de ser guardada num formato codificado ANSI. Os ficheiros NOIDMIF guardados no formato UTF-8 codificado não não possível ler pelo Configuration Manager.  

 Depois de criar um ficheiro NOIDMIF, armazená-la no *% Windir %***\System32\CCM\Inventory\Noidmifs** pasta em cada cliente. O Configuration Manager irá recolher informações a partir dos ficheiros NODMIF nesta pasta durante o próximo ciclo de inventário de hardware agendado.  

###  <a name="BKMK_IDMIF"></a> Para criar ficheiros IDMIF  
 Os ficheiros IDMIF podem ser utilizados para adicionar informações sobre os ativos que foi não normalmente inventariados pelo Configuration Manager e não está associado um dispositivo de cliente específico, para a base de dados do Configuration Manager. Por exemplo, poderia utilizar IDMIFS para recolher informações sobre projetores, os leitores do DVD, photocopiers ou outro equipamento que não contenha um cliente do Configuration Manager. Para obter informações sobre como criar ficheiros IDMIF, consulte a documentação do SDK do Configuration Manager.  

 Depois de criar um ficheiro IDMIF, armazená-la no *% Windir %***\System32\CCM\Inventory\Idmifs** pasta nos computadores cliente. O Configuration Manager irá recolher informações a partir deste ficheiro durante o próximo ciclo de inventário de hardware agendado. Tem de declarar as novas classes relativamente a informações incluídas no ficheiro adicionando ou importando as mesmas.  

> [!NOTE]
> Os ficheiros MIF podem conter grandes quantidades de dados e a recolha destes dados pode afetar negativamente o desempenho do seu site. Ativar a recolha de MIF apenas quando necessário e configure a opção **máximo personalizado tamanho do ficheiro MIF (KB)** nas definições de inventário de hardware. Para obter mais informações, consulte o artigo [introdução ao inventário de hardware no System Center Configuration Manager](introduction-to-hardware-inventory.md).

