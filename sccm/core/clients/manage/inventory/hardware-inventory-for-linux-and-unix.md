---
title: "Inventário de hardware para Linux e UNIX"
titleSuffix: Configuration Manager
description: "Saiba como utilizar o inventário de hardware para Linux e UNIX no System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 6f71478f6a2a8e5a2a41068624debfe3ac3e915d
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="hardware-inventory-for-linux-and-unix-in-system-center-configuration-manager"></a>Inventário de hardware para Linux e UNIX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O cliente do System Center Configuration Manager para Linux e UNIX suporta o inventário de hardware. Depois de recolher o inventário de hardware pode executar ver o inventário no Explorador de recursos ou relatórios do Configuration Manager e utilize estas informações para criar consultas e coleções que permitam as seguintes operações:  

-   Implementação de software  

-   Impor janelas de manutenção  

-   Implementar definições de cliente personalizadas  

 O inventário de hardware para servidores Linux e UNIX utiliza um servidor CIM (Common Information Model) baseado em normas. O servidor CIM é executado como serviço de software (ou daemon) e fornece uma infraestrutura de gestão baseada em normas DMTF (Distributed Management Task Force). O servidor CIM proporciona uma funcionalidade semelhante às capacidades CIM do Windows Management Infrastructure (WMI) que estão disponíveis nos computadores baseados em Windows.  

 A partir da atualização cumulativa 1, o cliente para Linux e UNIX utiliza a versão 1.0.6 do **omiserver** de código aberto do **Open Group**. (Antes da atualização cumulativa 1, o cliente utilizava **nanowbem** como o servidor CIM).  

 O servidor CIM é instalado como parte do cliente para Linux e UNIX. O cliente para Linux e UNIX comunica diretamente com o servidor CIM e não utiliza a interface WS-MAN do servidor CIM. A porta WS-MAN no servidor CIM está desativada quando o cliente é instalado. A Microsoft desenvolveu o servidor CIM que está agora disponível como código aberto através do projeto Open Management Infrastructure (OMI). Para obter mais informações sobre o projeto Open Management Infrastructure, veja o Web site [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) .  

 O Inventário de Hardware nos servidores Linux e UNIX funciona mediante o mapeamento de classes e propriedades WMI Win32 existentes para as classes e propriedades equivalentes dos servidores Linux e UNIX. Este mapeamento unidirecional de classes e propriedades permite que o inventário de hardware de Linux e UNIX integrar com o Configuration Manager. Apresenta dados de inventário de servidores Linux e UNIX, juntamente com o inventário de computadores baseados em Windows na consola do Configuration Manager e relatórios. Isto oferece uma experiência de gestão heterogénea e consistente.  

> [!TIP]  
>  Pode utilizar o valor **Legenda** para a classe **Sistema Operativo** para identificar os diferentes sistemas operativos Linux e UNIX em consultas e coleções.  

##  <a name="BKMK_ConfigHardwareforLnU"></a> Configurar o inventário de hardware para servidores Linux e UNIX  
 Pode utilizar as predefinições de cliente ou criar definições de dispositivos cliente personalizadas para configurar o inventário de hardware. Se utilizar definições de dispositivos cliente personalizadas, pode configurar as classes e propriedades que pretende recolher apenas dos servidores Linux e UNIX. Também pode especificar agendamentos personalizados para recolher inventários completos e diferenciais dos servidores Linux e UNIX.  

 O cliente para Linux e UNIX suporta as seguintes classes de inventário de hardware, que estão disponíveis em servidores Linux e UNIX:  

-   Win32_BIOS  

-   Win32_ComputerSystem  

-   Win32_DiskDrive  

-   Win32_DiskPartition  

-   Win32_NetworkAdapter  

-   Win32_NetworkAdapterConfiguration  

-   Win32_OperatingSystem  

-   Win32_Process  

-   Win32_Service  

-   Win32Reg_AddRemovePrograms  

-   SMS_LogicalDisk  

-   SMS_Processor  

 Nem todas as propriedades para estas classes de inventário estão ativadas para computadores Linux e UNIX no Configuration Manager.  

##  <a name="BKMK_OperationsforHardwareforLnU"></a> Operações de inventário de hardware  
 Depois de recolher o inventário de hardware dos servidores Linux e UNIX, pode ver e utilizar estas informações da mesma forma que visualiza o inventário recolhido dos outros computadores:  

-   Utilize o Explorador de Recursos para ver informações detalhadas sobre o inventário de hardware dos servidores Linux e UNIX  

-   Criar consultas baseadas em configurações de hardware específicas  

-   Crie coleções baseadas em consultas que se baseiam em configurações de hardware específicas  

-   Execute relatórios que apresentam detalhes específicos sobre as configurações de hardware  

 O inventário de hardware em servidores Linux ou UNIX é executado de acordo com o agendamento que configurar nas definições de cliente. Por predefinição, é executado a cada sete dias. O cliente para Linux e UNIX suporta ciclos de inventário completo e ciclos de inventário diferencial.  

 Pode também forçar o cliente num servidor Linux ou UNIX a executar imediatamente o inventário de hardware. Para executar o inventário de hardware, utilize as credenciais **raiz** num cliente para executar o comando seguinte e iniciar um ciclo de inventário de hardware: **/opt/microsoft/configmgr/bin/ccmexec -rs hinv**  

 As ações do inventário de hardware são introduzidas no ficheiro de registo do cliente, **scxcm.log**.  

##  <a name="BKMK_CustomHINVforLinux"></a> Como utilizar a Open Management Infrastructure para criar um inventário de hardware personalizado  
 O cliente para Linux e UNIX suporta o inventário de hardware personalizado, que pode criar com a Open Management Infrastructure (OMI). Para tal, utilize os passos seguintes:  

1.  Criar um fornecedor de inventário personalizado ao utilizar a fonte OMI  

2.  Configurar computadores para utilizar o novo fornecedor para comunicar inventário  

3.  Ativar o Configuration Manager para o novo fornecedor de suporte  

###  <a name="BKMK_LinuxProvider"></a> Criar um fornecedor de inventário de hardware personalizado para computadores Linux e UNIX:  
 Para criar um fornecedor de inventário de hardware personalizado para o cliente do Configuration Manager para Linux e UNIX, utilize **OMI Source - 1.0.6** e siga as instruções do OMI guia de introdução. Este processo inclui a criação de um ficheiro MOF (Managed Object Format) que define o esquema do novo fornecedor. Posteriormente, importe o ficheiro MOF para o Configuration Manager para ativar o suporte da nova classe de inventário personalizado.  

 Tanto o OMI Source - v.1.0.6, como o Guia de Introdução da OMI, estão disponíveis para transferência a partir do Web site [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) . Pode localizar estas transferências no **documentos** separador na página seguinte web site OpenGroup.org: [Abra o Management Infrastructure (OMI)](http://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="BKMK_AddProvidertoLinux"></a> Configure cada computador com Linux ou UNIX com o fornecedor de inventário de hardware personalizado:  
 Depois de criar um fornecedor de inventário personalizado, tem de copiar e, em seguida, registar o ficheiro da biblioteca de fornecedores em cada computador que tem o inventário que pretende recolher.  

1.  Copie a biblioteca de fornecedores para cada computador Linux e UNIX a partir do qual pretende recolher o inventário. O nome da biblioteca de fornecedores é semelhante a: **XYZ_MyProvider.SO**  

2.  Depois, em cada computador Linux e UNIX, registe a biblioteca de fornecedores no servidor OMI. O servidor OMI é instalado no computador quando instala o cliente do Configuration Manager para Linux e UNIX, mas tem de registar manualmente fornecedores personalizados. Utilize a seguinte linha de comandos para registar o fornecedor: **/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so**  

3.  Depois de registar o novo fornecedor, utilize a ferramenta **omicli** para testar o fornecedor. O **omicli** ferramenta está instalada em cada computador Linux e UNIX quando instala o cliente do Configuration Manager para Linux e UNIX. Por exemplo, quando **XYZ_MyProvider** for o nome do fornecedor que criou, execute o seguinte comando no computador: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Para obter informações sobre o **omicli** e para testar fornecedores personalizados, veja o Guia de Introdução da OMI.  

> [!TIP]  
>  Utilize a distribuição de software para implementar e registar fornecedores personalizados em cada computador cliente Linux e UNIX.  

###  <a name="BKMK_AddLinuxProvidertoCM"></a> Ative a nova classe de inventário no Configuration Manager:  
 Antes de o Configuration Manager poder comunicar o inventário comunicado pelo novo fornecedor nos computadores Linux e UNIX, tem de importar o ficheiro MOF (Managed Object Format) que define o esquema do seu fornecedor personalizado.  

 Para importar um ficheiro MOF personalizado para o Configuration Manager, consulte [como configurar inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
