---
title: Criar consultas
titleSuffix: Configuration Manager
description: Descubra como criar e Importar consultas no System Center Configuration Manager. Inclui as consultas de exemplo e sugestões.
ms.date: 12/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12dd7a4d806a82e3c55898e249d1caa2a6ffb508
ms.sourcegitcommit: 19fc4f27667d51502fc9d7d02d164f2837d65dae
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461295"
---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Como criar consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar este tópico para o ajudar a criar ou importar consultas no System Center Configuration Manager.  

##  <a name="BKMK_Create"></a> Como criar consultas  
 Utilize este procedimento para ajudar a criar consultas no Configuration Manager.  

#### <a name="to-create-a-query"></a>Para criar uma consulta  

1.  Na consola do Configuration Manager, escolha **monitorização**.  

2.  Na **monitorização** área de trabalho, escolha **consultas**. Em seguida, no **home page** separador a **Create** de grupo, escolha **criar consulta**.  

3.  No separador **Geral** do **Assistente para Criar Consulta**, especifique um nome único e um comentário opcional para a consulta.  

4.  Se pretender importar uma consulta existente para utilizar como base para a nova consulta, escolha **importar declaração de consulta**. Na **procurar consulta** caixa de diálogo caixa, selecione uma consulta existente que pretende importar e, em seguida, escolha **OK**.  

5.  Na **tipo de objeto** , selecione o tipo de objeto que pretende que a consulta para devolver. A tabela seguinte descreve alguns exemplos dos tipos de objetos que pode procurar:  

    |Tipo de Objeto|Descrição|  
    |-----------------|-----------------|  
    |**Recurso de Sistema**|Utilize para procurar atributos de sistema comuns, como o nome de um dispositivo NetBIOS, a versão do cliente, o endereço IP do cliente e informações dos Serviços de Domínio do Active Directory.|  
    |**Recurso de Utilizador**|Utilize para procurar informações de utilizador comuns, como nomes de utilizador, nomes de grupos de utilizador e nomes de grupos de segurança.|  
    |**Automática**|Utilize para procurar atributos comuns de uma implementação, como o nome da implementação, a agenda e a coleção que foi implementado.|  

6.  Escolher **Edit Query Statement** para abrir o *&lt;nome da consulta\>* **propriedades da declaração** caixa de diálogo.  

7.  No **gerais** separador a *&lt;nome da consulta\>* **propriedades da declaração** caixa de diálogo caixa, especifique os atributos que esta consulta devolve e como eles estão a ser exibido. Escolha o **New** ícone para adicionar um novo atributo. Também pode escolher **Mostrar linguagem da consulta** para introduzir ou editar a consulta diretamente na consulta de linguagem WQL (WMI). Para obter exemplos de consultas da WMI, consulte a secção [Example WQL queries](#BKMK_Example) deste tópico.  

    > [!TIP]  
    > Pode utilizar a seguinte documentação de referência do MSDN para o ajudar a criar as suas próprias consultas de WQL:  
    >   
    > -   [WQL (SQL para WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Cláusula ONDE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Operadores da WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Na **critérios** separador da *&lt;nome da consulta\>* **propriedades da declaração** caixa de diálogo caixa, especifique os critérios que são utilizados para refinar os resultados da consulta. Por exemplo, pode devolver apenas os recursos que têm um código de site do **XYZ** nos resultados da consulta. Pode configurar vários critérios para uma consulta.  

    > [!IMPORTANT]  
    > Se criar uma consulta sem critérios, a consulta devolverá todos os dispositivos da coleção **Todos os Sistemas** .  

9. Na **associa** separador o *&lt;nome da consulta\>* **propriedades da declaração** caixa de diálogo, pode combinar dados de dois atributos diferentes para os resultados de consulta. Embora o Configuration Manager crie automaticamente associações de consulta quando escolhe atributos diferentes para o resultado da consulta, o **associações** separador oferece opções mais avançadas. As classes de atributo que suporta o System Center 2012 Configuration Manager são mostradas na tabela a seguir:  

    |Tipo de associação|Descrição|  
    |---------------|-----------------|  
    |Interna|Apresenta apenas os resultados correspondentes — sempre utilizado por associações externas que são criadas automaticamente.|  
    |Esquerda|Apresenta todos os resultados para o atributo base e apenas os resultados correspondentes ao atributo de associação.|  
    |Direita|Apresenta todos os resultados para o atributo de associação e apenas os resultados correspondentes ao atributo base.|  
    |Completa|Apresenta todos os resultados para o atributo base e o atributo de associação.|  

     Para obter mais informações sobre como utilizar operações de associação, consulte a documentação do SQL Server.  

10. Escolher **OK** para fechar a *&lt;nome da consulta\>* **propriedades da declaração** caixa de diálogo.  

11. Na **gerais** separador da **Assistente para criar consulta**, especifique se os resultados desta consulta não estão limitados a membros de uma coleção, se eles estão limitados a membros de uma coleção especificada, ou se existe uma linha de comandos para uma coleção sempre que a consulta é executada.  

12. Conclua o assistente para criar a consulta. A consulta nova é apresentada no nó **Consultas** na área de trabalho **Monitorização** .  

##  <a name="BKMK_Import"></a> Como importar consultas  
 Utilize este procedimento para importar uma consulta para o Configuration Manager. Para obter informações sobre como exportar consultas, consulte [como gerir consultas no System Center Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### <a name="to-import-a-query"></a>Para importar uma consulta  

1.  Na consola do Configuration Manager, escolha **monitorização**.  

2.  Na **monitorização** área de trabalho, escolha **consultas**. Sobre o **home page** separador a **criar** de grupo, escolha **importar objetos**.  

3.  Sobre o **nome de ficheiro MOF** página do **Assistente Importar objetos**, escolha **procurar** para selecionar o ficheiro de formato MOF (Managed Object) que contém a consulta que pretende importar.  

4.  Reveja as informações sobre a consulta a importar e, em seguida, conclua o assistente. A consulta nova é apresentada no **consultas** nó a **monitorização** área de trabalho.  

##  <a name="BKMK_Example"></a> Example WQL queries

Esta secção contém consultas da WMI de exemplo que pode utilizar na sua hierarquia ou modificar para outros fins. Para utilizar estas consultas, escolha **Mostrar linguagem da consulta** no **propriedades da instrução de consulta** caixa de diálogo. Em seguida, copie e cole a consulta para o **instrução de consulta** campo.  

> [!TIP]  
> Utilize o caráter universal `%` para indicar qualquer cadeia de caracteres. Por exemplo, `%Visio%` devolve Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-7"></a>Computadores com o Windows 7

Utilize a seguinte consulta para devolver a versão do sistema operativo e o nome NetBIOS de todos os computadores com o Windows 7.  

> [!TIP]  
> Para devolver os computadores que executam o Windows Server 2008 R2, altere `%Workstation 6.1%` para `%Server 6.1%`.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computadores com um pacote de software específico instalado  

Utilize a seguinte consulta para devolver o nome NetBIOS e o nome do pacote de software de todos os computadores que tenham um pacote de software específico instalado. Este exemplo apresenta todos os computadores com uma versão do Microsoft Visio instalado. Substitua `Microsoft%Visio%` com o pacote de software que pretende consultar.  

> [!TIP]  
> Para procurar o pacote de software, esta consulta utiliza os nomes que são apresentados na lista de programas do Painel de Controlo do Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit"></a>Computadores que estão numa unidade organizacional específica do Active Directory Domain Services

Utilize a seguinte consulta para devolver o nome NetBIOS e o nome de unidade organizacional (UO) de todos os computadores numa UO específica. Substitua o texto `OU Name` com o nome da UO que pretende consultar.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computadores com um nome NetBIOS específico

Utilize a seguinte consulta para devolver o nome NetBIOS de todos os computadores que começam com uma cadeia de carateres específica. Neste exemplo, a consulta devolve todos os computadores com um nome NetBIOS que comece com `ABC`.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Dispositivos de um tipo específico

Tipos de dispositivos são armazenados na base de dados do Configuration Manager com a classe de recursos **sms_r_system** e o nome de atributo **AgentEdition**. Utilize a seguinte consulta para obter apenas os dispositivos que correspondam a edição do agente do tipo de dispositivo que especificou:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Utilize um dos seguintes valores para  *&lt;ID do dispositivo\>*:  

|Tipo de Dispositivo|Valor de AgentEdition|  
|-----------------|---------------------------|  
|Computador desktop ou laptop do Windows|0|  
|Dispositivo baseado em Windows ARM (com o Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Computador Mac|5|  
|Windows CE|6|  
|Dispositivos Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Intel sistema-em-um-Chip|12|  
|Servidores Unix e Linux|13|  
|Apple macOS (MDM)|14|
|Microsoft HoloLens (MDM)|15|
|(MDM) do Microsoft Surface Hub|16|
|Android for Work|17|

 Por exemplo, se pretender que a consulta devolva apenas computadores Mac, utilize a seguinte consulta:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Consulte também  
 [Operações e manutenção de consultas no System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
