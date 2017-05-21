---
title: Criar consultas | Documentos do Microsoft
description: "Descubra como criar e Importar consultas no System Center Configuration Manager. Inclui as consultas de exemplo e sugestões."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 89bd798339489071fdb69325c957fefda32621e9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Como criar consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as secções seguintes deste tópico para o ajudar a criar ou importar consultas no System Center Configuration Manager.  

-   [How to Create Queries](#BKMK_Create)  

-   [How to Import Queries](#BKMK_Import)  

-   [Example WQL Queries](#BKMK_Example)  

##  <a name="BKMK_Create"></a> Como criar consultas  
 Utilize este procedimento para o ajudar a criar consultas no Configuration Manager.  

#### <a name="to-create-a-query"></a>Para criar uma consulta  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , clique em **Consultas** e, em seguida, no separador **Início** , no grupo **Criar** , clique em **Criar Consulta**.  

3.  No separador **Geral** do **Assistente para Criar Consulta**, especifique um nome único e um comentário opcional para a consulta.  

4.  Se pretender importar uma consulta existente para utilizar como base para a nova consulta, clique em **Importar Declaração de Consulta** e, em seguida, na caixa de diálogo **Procurar Consulta** , selecione a consulta que quer importar e clique em **OK**.  

5.  Na lista **Tipo de Objeto** , selecione o tipo de objeto que pretende que a consulta devolva. A tabela seguinte descreve alguns exemplos dos tipos de objetos que pode procurar:  

    |Tipo de Objeto|Descrição|  
    |-----------------|-----------------|  
    |**Recurso de Sistema**|Utilize para procurar atributos de sistema comuns, como o nome de um dispositivo NetBIOS, a versão do cliente, o endereço IP do cliente e informações dos Serviços de Domínio do Active Directory.|  
    |**Recurso de Utilizador**|Utilize para procurar informações de utilizador comuns, como nomes de utilizador, nomes de grupos de utilizadores e nomes de grupos de segurança.|  
    |**Automática**|Utilize para procurar atributos comuns de uma implementação, como o nome da implementação, a agenda e a coleção em que foi implementada.|  

6.  Clique em **editar instrução de consulta** para abrir o  *&lt;nome da consulta\>***propriedades da instrução** caixa de diálogo.  

7.  No **geral** separador o  *&lt;nome da consulta\>***propriedades da instrução** diálogo caixa, especifique os atributos que esta consulta e como estão a ser apresentado. Clique no ícone **Novo** para adicionar um novo atributo. Também pode clicar em **Mostrar Linguagem da Consulta** para introduzir ou editar a consulta diretamente na Linguagem WQL (WMI Query Language). Para obter exemplos de consultas da WMI, consulte a secção [Example WQL queries](#BKMK_Example) deste tópico.  

    > [!TIP]  
    >  Pode utilizar a seguinte documentação de referência do MSDN para o ajudar a criar as suas próprias consultas de WQL:  
    >   
    >  -   [WQL (SQL para WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Cláusula ONDE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Operadores da WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  No **critérios** separador do  *&lt;nome da consulta\>***propriedades da instrução** diálogo caixa, especifique os critérios que são utilizados para refinar os resultados da consulta. Por exemplo, pode devolver apenas os recursos que têm um código de site do **XYZ** nos resultados da consulta. Pode configurar vários critérios para uma consulta.  

    > [!IMPORTANT]  
    >  Se criar uma consulta sem critérios, a consulta devolverá todos os dispositivos da coleção **Todos os Sistemas** .  

9. No **junta** separador o  *&lt;nome da consulta\>***propriedades da instrução** caixa de diálogo, pode combinar dados a partir de dois dos atributos diferentes para resultados da sua consulta. Apesar do Configuration Manager cria automaticamente associações de consulta quando escolher atributos diferentes para o resultado da consulta, o **associações** separador fornece opções mais avançadas. As classes de atributo suportadas pelo System Center 2012 Configuration Manager são apresentadas na tabela seguinte:  

    |Tipo de associação|Descrição|  
    |---------------|-----------------|  
    |Interna|Apresenta apenas os resultados correspondentes - sempre utilizados pelo associações externas que são criadas automaticamente.|  
    |Esquerda|Apresenta todos os resultados para o atributo base e apenas os resultados correspondentes ao atributo de associação.|  
    |Direita|Apresenta todos os resultados para o atributo de associação e apenas os resultados correspondentes ao atributo base.|  
    |Completa|Apresenta todos os resultados para o atributo base e o atributo de associação.|  

     Para obter mais informações sobre como utilizar operações de Associação, consulte a documentação do SQL Server.  

10. Clique em **OK** para fechar o  *&lt;nome da consulta\>***propriedades da instrução** caixa de diálogo.  

11. No separador **Geral** do **Assistente para Criar Consulta**, especifique se os resultados desta consulta não estão limitados aos membros de uma coleção, se estão limitados a membros de uma coleção especificada ou se pedem uma coleção sempre que a consulta é executada.  

12. Conclua o assistente para criar a consulta. A consulta nova é apresentada no nó **Consultas** na área de trabalho **Monitorização** .  

##  <a name="BKMK_Import"></a> Como importar consultas  
 Utilize este procedimento para o ajudar a importar uma consulta para o Configuration Manager. Para obter informações sobre como exportar consultas, consulte o artigo [como gerir consultas no System Center Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### <a name="to-import-a-query"></a>Para importar uma consulta  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , clique em **Consultas** e, em seguida, no separador **Home Page** , no grupo **Criar** , clique em **Importar Objetos**.  

3.  Na página **Nome do Ficheiro MOF** do **Assistente Importar Objetos**, clique em **Procurar** para selecionar o ficheiro de formato MOF (Managed Object Format) que contém a consulta que pretende importar.  

4.  Reveja as informações sobre a consulta a importar e, em seguida, conclua o assistente. A consulta nova é apresentada no nó **Consultas** na área de trabalho **Monitorização** .  

##  <a name="BKMK_Example"></a> Example WQL queries  
 Esta secção contém consultas da WMI de exemplo que pode utilizar na sua hierarquia ou modificar para outros fins. Para utilizar estas consultas, clique em **Mostrar Linguagem da Consulta** na caixa de diálogo **Propriedades da Declaração de Consulta** e, em seguida, copie e cole a consulta no campo **Declaração da Consulta** .  

> [!TIP]  
>  Utilize o caráter universal **%** para indicar qualquer cadeia de carateres. Por exemplo, **%Visio%** devolve Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-7"></a>Computadores com o Windows 7  
 Utilize a seguinte consulta para devolver a versão do sistema operativo e o nome NetBIOS de todos os computadores com o Windows 7.  

> [!TIP]  
>  Para devolver os computadores que executam o Windows Server 2008 R2, altere **%Workstation 6.1%** para **%Server 6.1%**.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computadores com um pacote de software específico instalado  
 Utilize a seguinte consulta para devolver o nome NetBIOS e o nome do pacote de software de todos os computadores que tenham um pacote de software específico instalado. Este exemplo apresenta todos os computadores com uma versão do Microsoft Visio instalado. Substitua **%Visio%** pelo pacote de software que pretende consultar.  

> [!TIP]  
>  Para procurar o pacote de software, esta consulta utiliza os nomes que são apresentados na lista de programas do Painel de Controlo do Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit-ou"></a>Computadores que estão numa Unidade Organizacional (UO) dos Serviços de Domínio do Active Directory  
 Utilize a seguinte consulta para devolver o nome NetBIOS e o nome da UO de todos os computadores numa UO específica. Substitua o texto **OU Name** pelo nome da UO que pretende consultar.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computadores com um nome NetBIOS específico  
 Utilize a seguinte consulta para devolver o nome NetBIOS de todos os computadores que começam com uma cadeia de carateres específica. Neste exemplo, a consulta devolve todos os computadores com um nome NetBIOS que comece com **ABC**.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Dispositivos de um tipo específico  
 Tipos de dispositivos são armazenados na base de dados do Configuration Manager, sob a classe de recurso **sms_r_system** e o nome do atributo **AgentEdition**. Utilize a seguinte consulta para obter apenas os dispositivos que correspondem à edição do agente do tipo de dispositivo que especificar:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

 Utilize um dos seguintes valores para  *&lt;ID de dispositivo\>*:  

|Tipo de Dispositivo|Valor de AgentEdition|  
|-----------------|---------------------------|  
|Computador Windows ou portátil|0|  
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
|Sistema Num Chip Intel|12|  
|Servidores Unix e Linux|13|  

 Por exemplo, se pretender que a consulta devolva apenas computadores Mac, utilize a seguinte consulta:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Consulte Também  
 [Operações e manutenção de consultas no System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)

