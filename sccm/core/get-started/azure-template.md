---
title: Create a lab in Azure (Criar um laboratório no Azure)
titleSuffix: Configuration Manager
description: Automatizar a criação de um laboratório de pré-visualização técnica do Configuration Manager utilizando modelos do Azure
ms.date: 01/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c3f1ca26c4cbc6de21565948ab2f161e2ccf0ea0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128260"
---
# <a name="create-a-configuration-manager-technical-preview-lab-in-azure"></a>Criar um laboratório de pré-visualização técnica do Configuration Manager no Azure

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

<!--3556017-->

Este guia descreve como criar um Gestor de configuração do ambiente de laboratório no Microsoft Azure. Ele usa os modelos do Azure para simplificar e automatizar a criação de um laboratório usando recursos do Azure. Este processo instala a versão mais recente do ramo de pré-visualização técnica do Configuration Manager. 

Para obter mais informações sobre o ramo atual do Configuration Manager, consulte [Configuration Manager no Azure](/sccm/core/understand/configuration-manager-on-azure).



## <a name="prerequisites"></a>Pré-requisitos

Este processo requer uma subscrição do Azure na qual pode criar os seguintes objetos: 
- Quatro máquinas de virtuais de Standard_D2s_v3
- Conta de armazenamento Standard_LRS

> [!Tip]  
> Consulte a [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os custos potenciais.  



## <a name="process"></a>Processo

1. Vá para o [modelo de Gestor de configuração](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/).  

2. Selecione **implementar no Azure**, que abre o portal do Azure.  

3. Conclua o modelo de início rápido do Azure com as seguintes informações:

    - Noções básicas  

        - **Subscrição**: O nome da subscrição na qual pretende criar as VMs  

        - **Grupo de recursos**: Selecione um grupo de recursos para utilizar para essas VMs  

        - **Localização**: Selecione um centro de dados do Azure para alojar este ambiente de laboratório  

    - Definições  

        - **Prefixo**: O nome de prefixo das máquinas. Para obter mais informações, consulte [informações da VM do Azure](#azure-vm-info).  

        - **Nome de utilizador administrador**: O nome de um utilizador nas VMs com direitos administrativos. Utilize este utilizador para iniciar sessão para as VMs.  

        - **Palavra-passe de administrador**: A palavra-passe tem de cumprir os requisitos de complexidade do Azure. Para obter mais informações, consulte [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > As definições seguintes são necessários pelo Azure. Utilize os valores predefinidos. Não altere estes valores.  
    > 
    > - **\_artefactos localização**: A localização dos scripts para este modelo <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_Token de Sas de localização de artefactos**: O sasToken é necessária para aceder à localização de artefactos  
    > 
    > - **Localização**: A localização para todos os recursos

4. Leia os termos e condições. Se concordar, selecione **concordo com os termos e condições indicados acima**. Em seguida, selecione **Compra** para continuar. 

O Azure valida as definições e, em seguida, começa a implementação. Verificar o estado da implementação no portal do Azure. O processo pode demorar horas de 2 a 4. Mesmo quando o portal do Azure mostra a implementação com êxito, os scripts de configuração continuam a executar. Não reinicie as VMs durante o processo.

Para ver o estado dos scripts de configuração, ligue para o `<prefix>PS1` do servidor e ver o seguinte ficheiro: `%windir%\TEMP\ProvisionScript\PS1.json`. Se ela mostra todos os passos como concluído, o processo é feito.

Para ligar às VMs, obtenha primeiro no portal do Azure os endereços IP públicos para cada VM. Quando ligar à VM, o nome de domínio é `contoso.com`. Utilize as credenciais que especificou no modelo de implementação. Para obter mais informações, consulte [como ligar e iniciar sessão a uma máquina virtual do Azure a executar o Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Informações VM do Azure

Todos os quatro VMs têm as seguintes especificações:
- Standard_D2s_v3, que tem dois núcleos de CPU e 8 GB de memória  
- Windows Server 2016 Datacenter edition
- 150 GB de espaço em disco
- Ambos os um público e privado endereço IP. Os IPs públicos estão num grupo de segurança de rede que só permite ligações de ambiente de trabalho remotas na porta TCP 3389. 

O prefixo que especificou no modelo de implementação é o prefixo de nome VM. Por exemplo, se definir "contoso" como o prefixo, em seguida, o nome de computador do controlador de domínio é `contosoDC`.


### `<prefix>DC`

Controlador de domínio do Active Directory

#### <a name="windows-features-and-roles"></a>Funcionalidades e funções do Windows
- Serviços de domínio do Active Directory (ADDS)
- .NET
- Compressão de diferencial remota (RDC)


### `<prefix>PS1`

- SQL Server
- Windows 10 ADK com o Windows PE 
- Site primário do Configuration Manager

#### <a name="windows-features-and-roles"></a>Funcionalidades e funções do Windows
- .NET
- Compressão de diferencial remota (RDC) 
- Serviço de informação Internet (IIS)


### `<prefix>MPDP`

- Ponto de gestão
- Ponto de distribuição

#### <a name="windows-features-and-roles"></a>Funcionalidades e funções do Windows
- .NET
- Compressão de diferencial remota (RDC) 
- Serviço de informação Internet (IIS)
- Serviço de transferência inteligente em segundo plano (BITS)


### `<prefix>Other`

Esta VM pode ser utilizado como um cliente, ou para hospedar outras funções de site.

#### <a name="windows-features-and-roles"></a>Funcionalidades e funções do Windows
- .NET
- Compressão de diferencial remota (RDC) 


