---
title: Criar consultas | Microsoft Docs
description: Saiba como criar e importar consultas no System Center Configuration Manager. Inclui dicas e consultas de exemplo.
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
ms.sourcegitcommit: 2087badc9dd1d216352dce232b145a786783ac89
ms.openlocfilehash: 9f38d86ff6227bb6ea88c358a3d61242372d449e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/18/2017


---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Como criar consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Você pode usar este tópico para ajudá-lo a criar ou importar consultas no System Center Configuration Manager.  

##  <a name="BKMK_Create"></a> Como criar consultas  
 Use este procedimento para ajudá-lo a criar consultas no Configuration Manager.  

#### <a name="to-create-a-query"></a>Para criar uma consulta  

1.  No console do Configuration Manager, escolha **monitoramento**.  

2.  No **monitoramento** espaço de trabalho, escolha **consultas**. Em seguida, no **início** guia o **criar** de grupo, escolha **criar consulta**.  

3.  No separador **Geral** do **Assistente para Criar Consulta**, especifique um nome único e um comentário opcional para a consulta.  

4.  Se você deseja importar uma consulta existente para usar como base para a nova consulta, escolha **Importar instrução de consulta**. No **procurar consulta** caixa de diálogo, selecione uma consulta existente que você deseja importar e, em seguida, escolha **Okey**.  

5.  No **tipo de objeto** , selecione o tipo de objeto que você deseja que a consulta para retornar. A tabela seguinte descreve alguns exemplos dos tipos de objetos que pode procurar:  

    |Tipo de Objeto|Descrição|  
    |-----------------|-----------------|  
    |**Recurso de Sistema**|Utilize para procurar atributos de sistema comuns, como o nome de um dispositivo NetBIOS, a versão do cliente, o endereço IP do cliente e informações dos Serviços de Domínio do Active Directory.|  
    |**Recurso de Utilizador**|Use para procurar informações típicas de usuário, como nomes de usuário, nomes de grupo de usuário e nomes de grupo de segurança.|  
    |**Automática**|Use para procurar atributos típicos de uma implantação, como o nome da implantação, o agendamento e a coleção que ela foi implantada.|  

6.  Escolha **Edit Query Statement** para abrir o  *&lt;nome de consulta\>*  **propriedades de instrução** caixa de diálogo.  

7.  No **geral** guia o  *&lt;nome de consulta\>*  **propriedades de instrução** caixa de diálogo, especifique os atributos que esta consulta retorna e como eles devem ser exibidos. Escolha o **novo** ícone para adicionar um novo atributo. Você também pode escolher **Mostrar linguagem de consulta** para inserir ou editar a consulta diretamente no WMI Query Language (WQL). Para obter exemplos de consultas da WMI, consulte a secção [Example WQL queries](#BKMK_Example) deste tópico.  

    > [!TIP]  
    > Pode utilizar a seguinte documentação de referência do MSDN para o ajudar a criar as suas próprias consultas de WQL:  
    >   
    > -   [WQL (SQL para WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Cláusula ONDE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Operadores da WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  No **critérios** guia do  *&lt;nome de consulta\>*  **propriedades de instrução** caixa de diálogo, especifique os critérios que são usados para refinar os resultados da consulta. Por exemplo, pode devolver apenas os recursos que têm um código de site do **XYZ** nos resultados da consulta. Pode configurar vários critérios para uma consulta.  

    > [!IMPORTANT]  
    > Se criar uma consulta sem critérios, a consulta devolverá todos os dispositivos da coleção **Todos os Sistemas** .  

9. No **une** guia o  *&lt;nome de consulta\>*  **propriedades de instrução** caixa de diálogo, você pode combinar dados de dois atributos diferentes nos resultados da consulta. Embora o Configuration Manager cria automaticamente associações de consulta quando você escolhe diferentes atributos para o resultado da consulta, o **junções** guia fornece mais opções avançadas. As classes de atributo que dá suporte ao System Center 2012 Configuration Manager são mostradas na tabela a seguir:  

    |Tipo de associação|Descrição|  
    |---------------|-----------------|  
    |Interna|Exibe resultados correspondentes apenas — sempre usados pelas associações que são criadas automaticamente.|  
    |Esquerda|Apresenta todos os resultados para o atributo base e apenas os resultados correspondentes ao atributo de associação.|  
    |Direita|Apresenta todos os resultados para o atributo de associação e apenas os resultados correspondentes ao atributo base.|  
    |Completa|Apresenta todos os resultados para o atributo base e o atributo de associação.|  

     Para obter mais informações sobre como usar as operações de associação, consulte a documentação do SQL Server.  

10. Escolha **Okey** para fechar o  *&lt;nome de consulta\>*  **propriedades de instrução** caixa de diálogo.  

11. No **geral** guia do **criar Assistente de consulta**, especifique se os resultados dessa consulta não estão limitados a membros de uma coleção, se eles são limitados aos membros de uma coleção especificada, ou se houver um pedido para uma coleção cada vez que a consulta é executada.  

12. Conclua o assistente para criar a consulta. A consulta nova é apresentada no nó **Consultas** na área de trabalho **Monitorização** .  

##  <a name="BKMK_Import"></a> Como importar consultas  
 Use este procedimento para ajudá-lo a importar uma consulta no Configuration Manager. Para obter informações sobre como exportar consultas, consulte [como gerenciar consultas no System Center Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### <a name="to-import-a-query"></a>Para importar uma consulta  

1.  No console do Configuration Manager, escolha **monitoramento**.  

2.  No **monitoramento** espaço de trabalho, escolha **consultas**. No **início** guia o **criar** de grupo, escolha **importar objetos**.  

3.  No **nome do arquivo MOF** página do **Assistente de importação de objetos**, escolha **procurar** para selecionar o arquivo de formato MOF (Managed Object) que contém a consulta que você deseja importar.  

4.  Reveja as informações sobre a consulta a importar e, em seguida, conclua o assistente. A nova consulta é exibida no **consultas** nó o **monitoramento** espaço de trabalho.  

##  <a name="BKMK_Example"></a> Example WQL queries

Esta secção contém consultas da WMI de exemplo que pode utilizar na sua hierarquia ou modificar para outros fins. Para usar essas consultas, escolha **Mostrar linguagem de consulta** no **Query Statement Properties** caixa de diálogo. Em seguida, copie e cole a consulta no **instrução de consulta** campo.  

> [!TIP]  
> Use o caractere curinga `%` para significar qualquer cadeia de caracteres. Por exemplo, `%Visio%` retorna o Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-7"></a>Computadores com o Windows 7

Utilize a seguinte consulta para devolver a versão do sistema operativo e o nome NetBIOS de todos os computadores com o Windows 7.  

> [!TIP]  
> Para retornar os computadores que executam o Windows Server 2008 R2, alterar `%Workstation 6.1%` para `%Server 6.1%`.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computadores com um pacote de software específico instalado  

Utilize a seguinte consulta para devolver o nome NetBIOS e o nome do pacote de software de todos os computadores que tenham um pacote de software específico instalado. Este exemplo apresenta todos os computadores com uma versão do Microsoft Visio instalado. Substituir `%Visio%` com o pacote de software que você deseja consultar.  

> [!TIP]  
> Para procurar o pacote de software, esta consulta utiliza os nomes que são apresentados na lista de programas do Painel de Controlo do Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit"></a>Computadores que estão em uma unidade organizacional específica do serviços de domínio do Active Directory

Use a seguinte consulta para retornar o nome NetBIOS e o nome da unidade organizacional (UO) de todos os computadores em uma UO especificada. Substitua o texto `OU Name` com o nome da UO que você deseja consultar.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computadores com um nome NetBIOS específico

Utilize a seguinte consulta para devolver o nome NetBIOS de todos os computadores que começam com uma cadeia de carateres específica. Neste exemplo, a consulta retorna todos os computadores com um nome NetBIOS que começa com `ABC`.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Dispositivos de um tipo específico

Tipos de dispositivo são armazenados no banco de dados do Configuration Manager na classe de recurso **sms_r_system** e o nome do atributo **AgentEdition**. Use a seguinte consulta para recuperar apenas os dispositivos que correspondem à edição de agente do tipo de dispositivo que você especificar:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Use um dos seguintes valores para  *&lt;ID do dispositivo\>*:  

|Tipo de Dispositivo|Valor de AgentEdition|  
|-----------------|---------------------------|  
|Computador com Windows desktop ou laptop|0|  
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
|Sistema-em-um-Chip do Intel|12|  
|Servidores Unix e Linux|13|  

 Por exemplo, se pretender que a consulta devolva apenas computadores Mac, utilize a seguinte consulta:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Consulte também  
 [Operações e manutenção de consultas no System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)

