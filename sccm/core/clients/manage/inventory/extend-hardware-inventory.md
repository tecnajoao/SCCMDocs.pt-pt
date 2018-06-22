---
title: Expandir o inventário de hardware
titleSuffix: Configuration Manager
description: Saiba mais formas de expandir o inventário de hardware no System Center Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 317a143ba80607bef46a371c0e93ad9f4027abe4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344284"
---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Como expandir o inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Inventário de hardware lê as informações a partir de Windows PCs utilizando o Windows Management Instrumentation (WMI). O WMI é a implementação Microsoft de baseada na web Enterprise Management (WBEM), uma norma da indústria para aceder a informações de gestão numa empresa. Em versões anteriores do Configuration Manager, tenha expandido o inventário de hardware ao modificar o ficheiro sms_def.mof no servidor do site. Este ficheiro continha uma lista de classes WMI que podiam ser lidas pelo inventário de hardware. Editar este ficheiro, pode ativar e desativar as classes existentes e também criar novas classes ao inventário.  

O ficheiro Configuration.mof é utilizado para definir as classes de dados a inventariar pelo inventário de hardware no cliente e não de Configuration Manager 2012. Pode criar classes de dados para inventariar classes de dados existentes ou personalizados do repositório WMI ou chaves de registo presentes em sistemas cliente.  

 O ficheiro Configuration.mof também define e regista os fornecedores WMI que acedem a informações de dispositivos durante o inventário de hardware. Registar fornecedores define o tipo de fornecedor a utilizar e as classes que o fornecedor suporta.  

 Quando a política de pedido de clientes do Configuration Manager, o Configuration.mof é anexado ao corpo de política. Em seguida, este ficheiro é transferido e compilado pelos clientes. Quando adicionar, modificar ou eliminar classes de dados a partir do ficheiro Configuration.mof, os clientes compilam automaticamente estas alterações efetuadas em classes de dados relacionadas com o inventário. Nenhuma ação adicional é necessária para inventariar classes de dados novas ou modificada em clientes do Configuration Manager. Este ficheiro está localizado em **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** nos servidores de site primários.  

 No Configuration Manager, já não edita o ficheiro sms_def.mof como acontecia no Configuration Manager 2007. Em vez disso, pode ativar e desativar classes WMI e adicionar novas classes para recolher pelo inventário de hardware, utilizando as definições do cliente. Configuration Manager fornece os seguintes métodos para expandir o inventário de hardware.  

> [!NOTE]  
>  Se tiver alterado manualmente o ficheiro Configuration.mof para adicionar classes de inventário personalizadas, estas alterações serão substituídas quando atualizar para a versão 1602. Para continuar a utilizar classes personalizadas depois de atualizar, deve adicioná-los para a secção "Extensões adicionadas" do ficheiro Configuration.mof depois de atualizar para a versão 1602.  
> No entanto, não deve modificar nada acima desta secção, visto que estas secções estão reservadas para serem modificadas pelo Configuration Manager. Está disponível uma cópia de segurança do Configuration.mof em:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Método|Mais informações|  
|------------|----------------------|  
|Ativar ou desativar classes de inventário existentes|Ativar ou desativar as classes de inventário predefinidas ou criar as definições que lhe permitem recolher classes de inventário de hardware diferentes a partir de coleções de clientes especificadas de cliente personalizadas. Consulte o [para ativar ou desativar classes de inventário existentes](#BKMK_Enable) procedimento neste artigo.|  
|Adicionar uma nova classe de inventário|Adicione uma nova classe de inventário do espaço de nomes WMI de outro dispositivo. Consulte o [para adicionar uma nova classe de inventário](#BKMK_Add) procedimento neste artigo.|  
|Importar e exportar classes de inventário de hardware|Importar e exportar ficheiros de formato (Managed Object) que contêm classes de inventário a partir da consola do Configuration Manager. Consulte o [para importar classes de inventário de hardware](#BKMK_Import) e [para exportar classes de inventário de hardware](#BKMK_Export) procedimentos neste artigo.|  
|Criar Ficheiros NOIDMIF|Utilize ficheiros NOIDMIF para recolher informações sobre dispositivos cliente que não podem ser inventariados pelo Configuration Manager. Por exemplo, pode pretender recolher informações sobre o número de ativos de dispositivo existentes apenas como uma etiqueta no dispositivo. O inventário NOIDMIF é automaticamente associado ao dispositivo cliente a partir do qual foi recolhido. Consulte [para criar ficheiros NOIDMIF](#BKMK_NOIDMIF) neste artigo.|  
|Criar Ficheiros IDMIF|Utilize ficheiros IDMIF para recolher informações sobre os ativos da sua organização que não estão associados um cliente de Configuration Manager, por exemplo, projetores, fotocopiadoras e impressoras de rede. Consulte [para criar ficheiros IDMIF](#BKMK_IDMIF) neste artigo.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimentos para expandir o inventário de hardware  
Estes procedimentos ajudam a configurar as predefinições de cliente para o inventário de hardware e aplicam-se a todos os clientes na sua hierarquia. Se pretender que estas definições se apliquem apenas a determinados clientes, crie uma definição de dispositivo de cliente personalizadas e atribua-a uma coleção de clientes específicos. Consulte [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="BKMK_Enable"></a> Para ativar ou desativar as classes de inventário existentes  

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente** > **predefinições de cliente**.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  No **predefinições de cliente** diálogo caixa, escolha **inventário de Hardware**.  

6.  Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  

7.  Na caixa de diálogo **Classes de Inventário de Hardware** , selecione ou desmarque as classes e propriedades de classes que pretende que sejam recolhidas pelo inventário de hardware. Pode expandir classes para selecionar ou desmarcar propriedades individuais dentro dessa classe. Utilize o campo **Procurar classes de inventário** para procurar classes individuais.  

    > [!IMPORTANT]  
    >  Quando adicionar novas classes ao inventário de hardware do Configuration Manager, o tamanho do ficheiro de inventário que é recolhido e enviado para o servidor do site aumentará. Isto poderá afetar negativamente o desempenho da sua rede e do site do Configuration Manager. Ative apenas as classes de inventário que pretende recolher.  


###  <a name="BKMK_Add"></a> Para adicionar uma nova classe de inventário  

Só pode adicionar classes de inventário do servidor de nível superior da hierarquia ao modificar as predefinições de cliente. Esta opção não está disponível quando criar definições personalizadas do dispositivo.

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente** > **predefinições de cliente**.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  No **predefinições de cliente** diálogo caixa, escolha **inventário de Hardware**.  

6.  No **definições do dispositivo** lista, escolha **definir Classes**.  

7.  No **Classes de inventário de Hardware** diálogo caixa, escolha **adicionar**.  

8.  Na caixa de diálogo **Adicionar Classe de Inventário de Hardware** , clique em **Ligar**.  

9. Na caixa de diálogo **Ligar à Windows Management Instrumentation (WMI)** , especifique o nome do computador a partir do qual irá obter as classes WMI e o espaço de nomes WMI a utilizar para obter as classes. Se pretender obter todas as classes abaixo do espaço de nomes WMI que especificou, clique em **Recursiva**. Se o computador ao qual está a ligar não for o computador local, forneça as credenciais de início de sessão para uma conta que tenha permissão para aceder ao WMI no computador remoto.  

10. Escolha **ligar**.  

11. No **adicionar classe de inventário de Hardware** caixa de diálogo a **classes de inventário** lista, selecione as classes WMI que pretende adicionar ao inventário de hardware do Configuration Manager.  

12. Se pretender editar informações sobre a classe WMI selecionada, escolha **editar**e o **qualificadores de classe** diálogo caixa, forneça as seguintes informações:  

    -   **Nome a apresentar** -este nome será apresentado no Explorador de recursos.  

    -   **Propriedades** -especifique as unidades nas quais cada propriedade da WMI classe será apresentada.  

     Também pode designar propriedades como uma propriedade de chave para o ajudar a identificar exclusivamente cada instância da classe. Se não for definida qualquer chave para a classe e várias instâncias da classe forem comunicadas a partir do cliente, apenas a instância mais recente encontrada é armazenada na base de dados.  

     Quando tiver terminado de configurar as propriedades, clique em **OK** para fechar o **qualificadores de classe** e outra a caixa de diálogo Abrir caixas de diálogo. 

###  <a name="BKMK_Import"></a> Para importar classes de inventário de hardware  

Só pode importar classes de inventário quando modificar as predefinições de cliente. No entanto, pode utilizar definições de cliente personalizadas para importar informações que não incluem uma alteração de esquema, tal como alterar a propriedade de uma classe existente de **verdadeiro** para **falso**.  

1.  Na consola do Configuration Manager, escolha **administração** >  **as definições de cliente** > **predefinições de cliente**.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  No **predefinições de cliente** diálogo caixa, escolha **inventário de Hardware**.  

6.  No **definições do dispositivo** lista, escolha **definir Classes**.  

7.  No **Classes de inventário de Hardware** diálogo caixa, escolha **importação**.  

8.  No **importar** caixa de diálogo, selecione o gerido objeto ficheiro de formato MOF (Managed) que pretende importar e, em seguida, escolha **OK**. Reveja os itens que serão importados e, em seguida, clique em **importação**.  

###  <a name="BKMK_Export"></a> Para exportar classes de inventário de hardware  

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente** > **predefinições de cliente**.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  No **predefinições de cliente** diálogo caixa, escolha **inventário de Hardware**.  

6.  No **definições do dispositivo** lista, escolha **definir Classes**.  

7.  No **Classes de inventário de Hardware** diálogo caixa, escolha **exportar**.  

    > [!NOTE]  
    >  Quando exporta classes, todas as classes atualmente selecionadas serão exportadas.  

8.  No **exportar** diálogo caixa, especifique o ficheiro de formato (Managed Object) que pretende exportar as classes e, em seguida, escolha **guardar**.  

### <a name="bkmk_GreaterThan255"></a> Configurar o inventário de hardware para recolher cadeias maiores do que 255 carateres
A partir do Configuration Manager 1802, pode especificar o período de cadeias de ser maior que 255 carateres para propriedades de inventário de hardware. Esta alteração aplica-se apenas às classes adicionadas recentemente e as propriedades de inventário de hardware que não existem chaves. <!-- 1357389 -->

1. No **administração** área de trabalho, clique em **as definições de cliente** Realce um dispositivo de cliente para editar, clique com botão direito, em seguida, selecione a definição **propriedades**.

2. Selecione **inventário de Hardware**, em seguida, **definir Classes**, e **adicionar**.

3. Clique em de **Connect** botão.

4. Preencha **nome do computador**, **espaço de nomes WMI**, selecione **recursiva** se for necessário. Forneça as credenciais, se for necessário para estabelecer a ligação. Clique em **Connect** para ver as classes de espaço de nomes.

5. Selecione uma nova classe e clique em **editar**.

6. Alterar o **comprimento** da sua propriedade que é uma cadeia, que não sejam key, ser maior que 255. Clique em **OK**. 

7. Certifique-se de que a propriedade editada está selecionada para **adicionar classe de inventário de Hardware** e clique em **OK**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Como Utilizar Ficheiros MIF (Management Information Files) para expandir o inventário de hardware  
 Utilize ficheiros de formato MIF (Management Information) para expandir as informações de inventário de hardware recolhidas nos clientes pelo Configuration Manager. Durante o inventário de hardware, as informações armazenadas em ficheiros MIF são adicionadas ao relatório de inventário de cliente e armazenadas na base de dados do site, onde pode utilizar os dados da forma mesmo que utiliza dados de inventário de cliente predefinido. Existem dois tipos de ficheiros MIF, NOIDMIF e IDMIF.

> [!IMPORTANT]  
>  Antes de poder adicionar informações de ficheiros MIF à base de dados do Configuration Manager, tem de criar ou importar informações de classe para os mesmos. Para obter mais informações, consulte as secções [para adicionar uma nova classe de inventário](#BKMK_Add) e [para importar classes de inventário de hardware](#BKMK_Import) neste artigo.  

###  <a name="BKMK_NOIDMIF"></a> Para criar ficheiros NOIDMIF  
 Os ficheiros NOIDMIF podem ser utilizados para adicionar informações a um inventário de hardware de cliente que normalmente não pode ser recolhido pelo Configuration Manager e está associados um dispositivo cliente específico. Por exemplo, muitas empresas identificam cada computador na organização com um número de recurso e, em seguida, estes números de catálogo manualmente. Quando cria um ficheiro NOIDMIF, estas informações podem ser adicionadas à base de dados do Configuration Manager e ser utilizadas para consultas e relatórios. Para obter informações sobre como criar ficheiros NOIDMIF, consulte a documentação do SDK do Configuration Manager.  

> [!IMPORTANT]  
>  Quando cria um ficheiro NOIDMIF, tem de ser guardado num formato codificado ANSI. Os ficheiros NOIDMIF guardados no formato codificado UTF-8 não não possível ler pelo Configuration Manager.  

 Depois de criar um ficheiro NOIDMIF, armazene-o no *%Windir%***\CCM\Inventory\Noidmifs** em cada cliente. O Configuration Manager irá recolher informações dos ficheiros NODMIF nesta pasta durante o próximo ciclo de inventário de hardware agendado.  

###  <a name="BKMK_IDMIF"></a> Para criar ficheiros IDMIF  
 Ficheiros IDMIF podem ser utilizados para adicionar informações sobre os recursos que, normalmente, não foi possível ser inventariadas pelo Configuration Manager e não está associados a um dispositivo cliente específico, para a base de dados do Configuration Manager. Por exemplo, pode utilizar IDMIFS para recolher informações sobre projetores, leitores de DVD, fotocopiadoras ou outro equipamento que não tenha um cliente de Configuration Manager. Para obter informações sobre como criar ficheiros IDMIF, consulte a documentação do SDK do Configuration Manager.  

 Depois de criar um ficheiro IDMIF, armazene-o no *%Windir%***\CCM\Inventory\Idmifs** nos computadores cliente. O Configuration Manager irá recolher informações deste ficheiro durante o próximo ciclo de inventário de hardware agendado. Tem de declarar as novas classes relativamente a informações incluídas no ficheiro adicionando ou importando as mesmas.  

> [!NOTE]
> Os ficheiros MIF podem conter grandes quantidades de dados e a recolha destes dados pode afetar negativamente o desempenho do seu site. Ativar a recolha de MIF apenas quando necessário e configure a opção **tamanho de ficheiro MIF personalizado do máximo (KB)** nas definições de inventário de hardware. Para obter mais informações, consulte [introdução ao inventário de hardware no System Center Configuration Manager](introduction-to-hardware-inventory.md).
