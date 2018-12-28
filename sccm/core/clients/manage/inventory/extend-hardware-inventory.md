---
title: Expandir o inventário de hardware
titleSuffix: Configuration Manager
description: Conheça formas de expandir o inventário de hardware no System Center Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f1fa9f1bb2e036e0208a72e744f66da5c1887593
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423308"
---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Como expandir o inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Inventário de hardware lê informações de Windows PCs com o Windows Management Instrumentation (WMI). O WMI é a implementação Microsoft de baseada na web Enterprise Management (WBEM), uma norma da indústria para aceder a informações de gestão numa empresa. Nas versões anteriores do Configuration Manager, tenha expandido o inventário de hardware ao modificar o ficheiro sms_def no servidor do site. Este ficheiro continha uma lista de classes WMI que podiam ser lidas pelo inventário de hardware. Editar este ficheiro, pode ativar e desativar as classes existentes e também criar novas classes para fazer o inventário.  

O ficheiro Configuration MOF é utilizado para definir as classes de dados a inventariar pelo inventário de hardware no cliente e permanece inalterado a partir do Configuration Manager 2012. Pode criar classes de dados para inventariar classes de dados existentes ou personalizados do repositório WMI ou chaves de registo presentes em sistemas cliente.  

 O ficheiro Configuration.mof também define e regista os fornecedores WMI que acedem a informações de dispositivos durante o inventário de hardware. Registar fornecedores define o tipo de fornecedor a utilizar e as classes que o fornecedor suporta.  

 Quando a política de pedido de clientes do Configuration Manager, o MOF é anexado ao corpo da política. Em seguida, este ficheiro é transferido e compilado pelos clientes. Quando adicionar, modificar ou eliminar classes de dados a partir do ficheiro Configuration.mof, os clientes compilam automaticamente estas alterações efetuadas em classes de dados relacionadas com o inventário. Nenhuma ação adicional é necessária para classes de inventário de dados novas ou modificada em clientes do Configuration Manager. Este ficheiro está localizado em **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** nos servidores de site primários.  

 No Configuration Manager, já não edite o ficheiro sms_def MOF como fazia no Configuration Manager 2007. Em vez disso, pode ativar e desativar classes WMI e adicionar novas classes para recolher pelo inventário de hardware, utilizando as definições do cliente. O Configuration Manager fornece os seguintes métodos para expandir o inventário de hardware.  

> [!NOTE]  
>  Se alterou manualmente o ficheiro Configuration MOF para adicionar classes de inventário personalizado, essas alterações serão substituídas quando atualizar para a versão 1602. Para continuar a utilizar classes personalizadas depois de atualizar, deve adicioná-los para a secção "Extensões adicionadas" do ficheiro Configuration MOF depois de atualizar para a versão 1602.  
> No entanto, não deve modificar nada acima desta secção, como estas secções estão reservadas para serem modificadas pelo Configuration Manager. Está disponível uma cópia de segurança do Configuration.mof em:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Método|Mais informações|  
|------------|----------------------|  
|Ativar ou desativar classes de inventário existentes|Ativar ou desativar as classes de inventário do padrão ou criar personalizadas de cliente definições que permitem recolher classes de inventário de hardware diferentes de coleções de clientes especificadas. Consulte a [para ativar ou desativar classes de inventário existentes](#BKMK_Enable) procedimento neste artigo.|  
|Adicionar uma nova classe de inventário|Adicione uma nova classe de inventário do espaço de nomes WMI de outro dispositivo. Consulte a [para adicionar uma nova classe de inventário](#BKMK_Add) procedimento neste artigo.|  
|Importar e exportar classes de inventário de hardware|Importar e exportar ficheiros de formato MOF (Managed Object) que contêm classes de inventário a partir da consola do Configuration Manager. Consulte a [para importar classes de inventário de hardware](#BKMK_Import) e [para exportar classes de inventário de hardware](#BKMK_Export) procedimentos neste artigo.|  
|Criar Ficheiros NOIDMIF|Utilize ficheiros NOIDMIF para recolher informações sobre os dispositivos de cliente que não podem ser inventariados pelo Configuration Manager. Por exemplo, pode pretender recolher informações sobre o número de ativos de dispositivo existentes apenas como uma etiqueta no dispositivo. O inventário NOIDMIF é automaticamente associado ao dispositivo cliente a partir do qual foi recolhido. Ver [para criar ficheiros NOIDMIF](#BKMK_NOIDMIF) neste artigo.|  
|Criar Ficheiros IDMIF|Utilize ficheiros IDMIF para recolher informações sobre os recursos da sua organização que não estão associados um cliente do Configuration Manager, por exemplo, projetores, fotocopiadoras e impressoras de rede. Ver [para criar ficheiros IDMIF](#BKMK_IDMIF) neste artigo.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimentos para expandir o inventário de hardware  
Estes procedimentos ajudam a configurar as predefinições de cliente para o inventário de hardware e aplicam-se a todos os clientes na sua hierarquia. Se pretender que estas definições se apliquem apenas a determinados clientes, crie uma definição de dispositivo de cliente personalizadas e atribua-a uma coleção de clientes específicos. Ver [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="BKMK_Enable"></a> Para ativar ou desativar as classes de inventário existentes  

1.  Na consola do Configuration Manager, escolha **Administration** > **definições de cliente** > **predefinições de cliente**.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Na **predefinições de cliente** caixa de diálogo caixa, escolha **inventário de Hardware**.  

6.  Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  

7.  Na caixa de diálogo **Classes de Inventário de Hardware** , selecione ou desmarque as classes e propriedades de classes que pretende que sejam recolhidas pelo inventário de hardware. Pode expandir classes para selecionar ou desmarcar propriedades individuais dentro dessa classe. Utilize o campo **Procurar classes de inventário** para procurar classes individuais.  

    > [!IMPORTANT]  
    >  Quando adiciona novas classes ao inventário de hardware do Configuration Manager, irá aumentar o tamanho do ficheiro de inventário recolhido e enviado para o servidor de site. Isto poderá afetar negativamente o desempenho da sua rede e o site do Configuration Manager. Ative apenas as classes de inventário que pretende recolher.  


###  <a name="BKMK_Add"></a> Para adicionar uma nova classe de inventário  

Só é possível adicionar classes de inventário de servidor de nível superior da hierarquia ao modificar as predefinições de cliente. Esta opção não está disponível quando criar definições personalizadas do dispositivo.

1. Na consola do Configuration Manager, escolha **Administration** > **definições de cliente** > **predefinições de cliente**.  

2. Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

3. Na **predefinições de cliente** caixa de diálogo caixa, escolha **inventário de Hardware**.  

4. Na **definições do dispositivo** lista, escolha **definir Classes**.  

5. Na **Classes de inventário de Hardware** caixa de diálogo caixa, escolha **Add**.  

6. Na caixa de diálogo **Adicionar Classe de Inventário de Hardware** , clique em **Ligar**.  

7. Na caixa de diálogo **Ligar à Windows Management Instrumentation (WMI)** , especifique o nome do computador a partir do qual irá obter as classes WMI e o espaço de nomes WMI a utilizar para obter as classes. Se pretender obter todas as classes abaixo do espaço de nomes WMI que especificou, clique em **Recursiva**. Se o computador ao qual está a ligar não for o computador local, forneça as credenciais de início de sessão para uma conta que tenha permissão para aceder ao WMI no computador remoto.  

8. Escolha **Ligar**.  

9. Na **adicionar classe de inventário de Hardware** caixa de diálogo a **classes de inventário** , selecione as classes WMI que pretende adicionar ao inventário de hardware do Configuration Manager.  

10. Se pretender editar informações sobre a classe WMI selecionada, escolha **edite**e, no **qualificadores de classe** diálogo caixa, forneça as seguintes informações:  

    - **Nome a apresentar** -este nome será apresentado no Explorador de recursos.  

    - **Propriedades** -especifique as unidades nas quais cada propriedade da WMI classe será apresentada.  

      Também pode designar propriedades como uma propriedade de chave para o ajudar a identificar exclusivamente cada instância da classe. Se não for definida qualquer chave para a classe e várias instâncias da classe forem comunicadas a partir do cliente, apenas a instância mais recente encontrada é armazenada na base de dados.  

      Quando tiver terminado de configurar as propriedades, clique em **OK** para fechar a **qualificadores de classe** e o outro, a caixa de diálogo abrem caixas de diálogo. 

###  <a name="BKMK_Import"></a> Para importar classes de inventário de hardware  

Só pode importar classes de inventário quando modificar as predefinições de cliente. No entanto, pode utilizar definições de cliente personalizadas para importar informações que não incluem uma alteração de esquema, tal como alterar a propriedade de uma classe existente de **True** ao **falso**.  

1.  Na consola do Configuration Manager, escolha **Administration** >  **definições de cliente** > **predefinições de cliente**.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Na **predefinições de cliente** caixa de diálogo caixa, escolha **inventário de Hardware**.  

6.  Na **definições do dispositivo** lista, escolha **definir Classes**.  

7.  Na **Classes de inventário de Hardware** caixa de diálogo caixa, escolha **importação**.  

8.  Na **importe** caixa de diálogo, selecione a gerida objeto ficheiro de formato (MOF) que pretende importar e, em seguida, escolha **OK**. Reveja os itens que serão importados e, em seguida, clique em **importação**.  

###  <a name="BKMK_Export"></a> Para exportar classes de inventário de hardware  

1.  Na consola do Configuration Manager, escolha **Administration** > **definições de cliente** > **predefinições de cliente**.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Na **predefinições de cliente** caixa de diálogo caixa, escolha **inventário de Hardware**.  

6.  Na **definições do dispositivo** lista, escolha **definir Classes**.  

7.  Na **Classes de inventário de Hardware** caixa de diálogo caixa, escolha **exportar**.  

    > [!NOTE]  
    >  Quando exporta classes, todas as classes atualmente selecionadas serão exportadas.  

8.  Na **exportar** caixa de diálogo caixa, especifique o ficheiro de formato MOF (Managed Object) que pretende exportar as classes e, em seguida, escolha **guardar**.  

### <a name="bkmk_GreaterThan255"></a> Configurar o inventário de hardware para recolher as cadeias de caracteres superiores a 255 carateres
A partir na versão 1802 do Gestor de configuração, pode especificar o comprimento de cadeias de caracteres para ter mais de 255 carateres para propriedades de inventário de hardware. Esta alteração aplica-se apenas a classes adicionadas recentemente e para as propriedades de inventário de hardware que não são as chaves. <!-- 1357389 -->

1. Na **administração** área de trabalho, clique em **definições de cliente** realçar um dispositivo de cliente na definição de editar, clique com botão direito e selecione **propriedades**.

2. Selecione **inventário de Hardware**, em seguida, **definir Classes**, e **adicionar**.

3. Clique nas **Connect** botão.

4. Preencha **nome do computador**, **espaço de nomes WMI**, selecione **recursiva** se for necessário. Forneça as credenciais se necessário, para ligar. Clique em **Connect** para ver as classes de espaço de nomes.

5. Selecione uma nova classe, em seguida, clique em **editar**.

6. Alteração da **comprimento** da sua propriedade que seja uma cadeia de caracteres, que não seja a chave, para ser superior a 255. Clique em **OK**. 

7. Certifique-se de que a propriedade editada está selecionada para **adicionar classe de inventário de Hardware** e clique em **OK**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Como Utilizar Ficheiros MIF (Management Information Files) para expandir o inventário de hardware  
 Utilize ficheiros de formato MIF (Management Information Format) para expandir as informações de inventário de hardware recolhidas nos clientes pelo Configuration Manager. Durante o inventário de hardware, as informações armazenadas em ficheiros MIF são adicionadas ao relatório de inventário de cliente e armazenadas na base de dados do site, onde pode utilizar os dados da forma mesmo que utiliza dados de inventário de cliente predefinido. Existem dois tipos de ficheiros MIF, NOIDMIF e IDMIF.

> [!IMPORTANT]  
>  Antes de poder adicionar informações de ficheiros MIF à base de dados do Configuration Manager, tem de criar ou importar informações de classe para os mesmos. Para obter mais informações, consulte as secções [para adicionar uma nova classe de inventário](#BKMK_Add) e [para importar classes de inventário de hardware](#BKMK_Import) neste artigo.  

###  <a name="BKMK_NOIDMIF"></a> Para criar ficheiros NOIDMIF  
 Ficheiros NOIDMIF podem ser utilizados para adicionar informações a um inventário de hardware de cliente que normalmente não pode ser recolhido pelo Configuration Manager e está associados um dispositivo cliente específico. Por exemplo, muitas empresas identificam cada computador na organização com um número de ativos e, em seguida, esses números de catálogo manualmente. Quando cria um ficheiro NOIDMIF, estas informações podem ser adicionadas à base de dados do Configuration Manager e ser utilizadas para consultas e relatórios. Para obter informações sobre como criar ficheiros NOIDMIF, consulte a documentação do SDK do Configuration Manager.  

> [!IMPORTANT]  
>  Quando cria um ficheiro NOIDMIF, tem de ser guardado no formato codificado ANSI. Ficheiros NOIDMIF guardados no formato codificado UTF-8 não podem ser lido pelo Configuration Manager.  

 Depois de criar um ficheiro NOIDMIF, armazene-o do *%Windir%***\CCM\Inventory\Noidmifs** em cada cliente. O Configuration Manager irá recolher informações dos ficheiros NODMIF nesta pasta durante o próximo ciclo de inventário de hardware agendado.  

###  <a name="BKMK_IDMIF"></a> Para criar ficheiros IDMIF  
 Ficheiros IDMIF podem ser utilizados para adicionar informações sobre os recursos que normalmente não puderam ser inventariados pelo Configuration Manager e não está associados a um dispositivo de cliente específico, para a base de dados do Configuration Manager. Por exemplo, pode utilizar IDMIFS para recolher informações sobre projetores, leitores de DVD, fotocopiadoras ou outro equipamento que não tem um cliente do Configuration Manager. Para obter informações sobre como criar ficheiros IDMIF, consulte a documentação do SDK do Configuration Manager.  

 Depois de criar um ficheiro IDMIF, armazene-o do *%Windir%***\CCM\Inventory\Idmifs** nos computadores cliente. O Configuration Manager irá recolher informações deste ficheiro durante o próximo ciclo de inventário de hardware agendado. Tem de declarar as novas classes relativamente a informações incluídas no ficheiro adicionando ou importando as mesmas.  

> [!NOTE]
> Os ficheiros MIF podem conter grandes quantidades de dados e a recolha destes dados pode afetar negativamente o desempenho do seu site. Ative a recolha de MIF apenas quando necessário e configure a opção **tamanho de ficheiro MIF personalizado do máximo (KB)** nas definições de inventário de hardware. Para obter mais informações, consulte [introdução ao inventário de hardware no System Center Configuration Manager](introduction-to-hardware-inventory.md).
