---
title: Gerir clientes com Linux e UNIX | Documentos do Microsoft
description: Gerir clientes em servidores Linux e UNIX no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 689af6998d9454d76d060b89ca1365d328c08020
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Como gerir os clientes para servidores Linux e UNIX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando gere com o System Center Configuration Manager em servidores Linux e UNIX, pode configurar coleções, janelas de manutenção e as definições de cliente para ajudar a gerir os servidores. Além disso, apesar do cliente do Configuration Manager para Linux e UNIX não tem uma interface de utilizador, pode forçar o cliente de manualmente a consulta de política de cliente.

##  <a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Utilizar coleções para gerir grupos de servidores Linux e UNIX na mesma forma que utiliza coleções para gerir outros tipos de cliente. As coleções podem ser coleções de associação direta ou as coleções baseadas em consulta que identificam os sistemas operativos cliente, configurações de hardware ou outros detalhes sobre o cliente que estão armazenados na base de dados do site. Por exemplo, pode utilizar coleções que incluem os servidores Linux e UNIX para gerir o seguinte:  

-   Definições do cliente  

-   Implementações de software  

-   Impor janelas de manutenção  

 Para que possa identificar um cliente de Linux ou UNIX através do sistema operativo ou distribuição, tem de recolher [inventário de hardware](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) do cliente.  

 As predefinições de cliente para inventário de hardware incluem informações sobre o sistema operativo de um computador cliente. Pode utilizar a propriedade **Legenda** da classe **Sistema Operativo** para identificar o sistema operativo de um servidor Linux ou UNIX.  

 Pode ver detalhes sobre os computadores que executam o cliente do Configuration Manager para Linux e UNIX no nó de dispositivos de ativos e compatibilidade área de trabalho na consola do Configuration Manager. Na área de ativos e compatibilidade trabalho da consola do Configuration Manager, pode ver o nome do sistema operativo de cada computador no **sistema operativo** coluna.  

 Por predefinição, os servidores Linux e UNIX são membros da coleção **Todos os Sistemas** . É recomendável criar coleções personalizadas que inclua apenas servidores Linux e UNIX, ou um subconjunto dos mesmos. Isto permite-lhe gerir operações como a implementação de software ou atribuir definições de cliente para os grupos de tal como computadores, para que pode medir com precisão o sucesso de uma implementação.   

 Quando criar uma coleção personalizada para servidores Linux e UNIX, inclua as consultas de regra de associação que contenham o atributo Legenda para o atributo Sistema Operativo. Para obter informações sobre como criar coleções, consulte o artigo [como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 O cliente do Configuration Manager para servidores Linux e UNIX suporta a utilização de [janelas de manutenção](../../../core/clients/manage/collections/use-maintenance-windows.md). Este suporte é igual ao dos clientes baseados em Windows.  

##  <a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 Pode [configurar definições de cliente](../../../core/clients/deploy/configure-client-settings.md) que se aplicam a servidores Linux e UNIX da mesma forma que configura definições para outros clientes.  

 Por predefinição, as **Predefinições de Agente do Cliente** aplicam-se a servidores Linux e UNIX. Também pode criar definições personalizadas de cliente e implementá-los em coleções de clientes específicos.  

 Não existem definições de cliente adicionais que se apliquem apenas a clientes Linux e UNIX. No entanto, existem predefinições de cliente que não se aplicam a clientes Linux e UNIX. O cliente para Linux e UNIX apenas aplica definições para a funcionalidade que suporta.  

 Por exemplo, uma definição de dispositivo de cliente personalizado que ativa e configura definições de controlo remoto seria ignorada por servidores Linux e UNIX, porque o cliente para Linux e UNIX não suporta o controlo remoto.  

##  <a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 O cliente para servidores Linux e UNIX periodicamente consulta o respetivo site de política de computador para saber mais sobre configurações de pedido e verificar a existência de implementações.  

 Pode também forçar o cliente num servidor Linux ou UNIX a consultar imediatamente a política do computador. Para tal, utilize **raiz** credenciais no servidor a executar o seguinte comando: **política de - rs /opt/microsoft/configmgr/bin/ccmexec**  

 Os detalhes da consulta de política do computador são introduzidos no ficheiro de registo de cliente partilhado, **scxcm.log**.  

> [!NOTE]  
>  Cliente do Configuration Manager para Linux e UNIX nunca pedidos nem processa a política de utilizador.  

##  <a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 Depois de instalar o cliente para Linux e UNIX, pode utilizar a ferramenta **certutil** para atualizar o cliente com um novo certificado PKI e para importar uma nova lista de Revogação de Certificados (CRL). Quando instala o cliente para Linux e UNIX, esta ferramenta é colocada na **/opt/microsoft/configmgr/bin/certutil**. 

 Para gerir os certificados, execute o certutil em cada cliente com uma das seguintes opções:  

|Opção|Mais informações|  
|------------|----------------------|  
|importPFX|Utilize esta opção para especificar um certificado para substituir o certificado que está a ser utilizado por um cliente.<br /><br /> Quando utiliza **- importPFX**, também tem de utilizar o **-palavra-passe** parâmetro de linha de comandos para fornecer a palavra-passe associada ao ficheiro PKCS #12.<br /><br /> Utilize **-rootcerts** para especificar requisitos de certificado de raiz adicionais.<br /><br /> Exemplo: **certutil - importPFX &lt;caminho para o certificado de PKCS #12 >-palavra-passe &lt;palavra-passe do certificado\> [-rootcerts &lt;lista separada por vírgulas de certificados >]**|  
|-importsitecert|Utilize esta opção para atualizar o certificado de assinatura do servidor de site que se encontra no servidor de gestão.<br /><br /> Exemplo: **certutil - importsitecert &lt;caminho para o certificado DER\>**|  
|-importcrl|Utilize esta opção para atualizar a CRL no cliente com um ou mais caminhos de ficheiro CRL.<br /><br /> Exemplo: **certutil - importcrl &lt;caminhos de ficheiro de CRL separados por vírgulas\>**|  

