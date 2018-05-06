---
title: Gerir clientes Linux e UNIX
titleSuffix: Configuration Manager
description: Gerir clientes em servidores Linux e UNIX no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1bafded91dcdcddacd45134ce6b52f4da9d916ac
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Como gerir clientes para servidores Linux e UNIX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando gere servidores Linux e UNIX com o System Center Configuration Manager, pode configurar coleções, janelas de manutenção e as definições de cliente para ajudar a gerir os servidores. Além disso, embora o cliente do Configuration Manager para Linux e UNIX não tem uma interface de utilizador, pode forçar o cliente consultar manualmente a política de cliente.

##  <a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Utilizar coleções para gerir grupos de servidores Linux e UNIX da mesma forma que utilize coleções para gerir outros tipos de cliente. As coleções podem ser coleções de associação direta ou coleções baseadas em consulta. As coleções baseadas em consulta identificam sistemas operativos cliente, configurações de hardware ou outros detalhes sobre o cliente que estão armazenados na base de dados do site. Por exemplo, pode utilizar coleções que incluem os servidores Linux e UNIX para gerir as seguintes definições:  

-   Definições do cliente  

-   Implementações de software  

-   Impor janelas de manutenção  

 Para que possa identificar um cliente Linux ou UNIX através do sistema operativo ou distribuição, tem de recolher [inventário de hardware](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) do cliente.  

 As predefinições de cliente para inventário de hardware incluem informações sobre o sistema operativo de um computador cliente. Pode utilizar a propriedade **Legenda** da classe **Sistema Operativo** para identificar o sistema operativo de um servidor Linux ou UNIX.  

 Pode ver detalhes sobre os computadores que executam o cliente do Configuration Manager para Linux e UNIX no **dispositivos** o nó do **ativos e compatibilidade** área de trabalho na consola do Configuration Manager. No **ativos e compatibilidade** área de trabalho da consola do Configuration Manager, pode ver o nome do sistema de operativo de cada computador no **sistema operativo** coluna.  

 Por predefinição, os servidores Linux e UNIX são membros da coleção **Todos os Sistemas** . Recomendamos que crie coleções personalizadas que incluam apenas servidores Linux e UNIX, ou um subconjunto dos mesmos. Coleções personalizadas permitem-lhe gerir operações como a implementação de software ou a atribuição de definições de cliente para grupos de como computadores, para que pode medir com precisão o êxito de uma implementação.   

 Quando criar uma coleção personalizada para servidores Linux e UNIX, inclua as consultas de regra de associação que contenham o atributo Legenda para o atributo Sistema Operativo. Para obter informações sobre como criar coleções, consulte [como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 O cliente do Configuration Manager para servidores Linux e UNIX suporta a utilização de [janelas de manutenção](../../../core/clients/manage/collections/use-maintenance-windows.md). Este suporte é igual de clientes baseados em Windows.  

##  <a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 Pode [configurar definições de cliente](../../../core/clients/deploy/configure-client-settings.md) que se aplicam a servidores Linux e UNIX da mesma forma que configura definições para outros clientes.  

 Por predefinição, as **Predefinições de Agente do Cliente** aplicam-se a servidores Linux e UNIX. Também pode criar definições personalizadas de cliente e implementá-las em coleções de clientes específicos.  

 Não existem definições de cliente adicionais que se apliquem apenas a clientes Linux e UNIX. No entanto, existem predefinições de cliente que não se aplicam a clientes Linux e UNIX. O cliente para Linux e UNIX só aplica definições para a funcionalidade que suporta.  

 Por exemplo, uma definição de dispositivo de cliente personalizado que ativa e configura as definições de controlo remoto seria ignorada pelos servidores Linux e UNIX, porque o cliente para Linux e UNIX não suporta o controlo remoto.  

##  <a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 O cliente para servidores Linux e UNIX consulta periodicamente se existem respetivo site para a política de computador para saber mais sobre as configurações pedidas e verificar a existência de implementações.  

 Pode também forçar o cliente num servidor Linux ou UNIX a consultar imediatamente a política do computador. Para tal, utilize **raiz** credenciais no servidor para executar o seguinte comando: **política do /opt/microsoft/configmgr/bin/ccmexec - rs**  

 Os detalhes da consulta de política do computador são introduzidos no ficheiro de registo de cliente partilhado, **scxcm.log**.  

> [!NOTE]  
>  O cliente do Configuration Manager para Linux e UNIX nunca pede nem processa a política de utilizador.  

##  <a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 Depois de instalar o cliente para Linux e UNIX, pode utilizar a ferramenta **certutil** para atualizar o cliente com um novo certificado PKI e para importar uma nova lista de Revogação de Certificados (CRL). Quando instala o cliente para Linux e UNIX, esta ferramenta é colocada na **/opt/microsoft/configmgr/bin/certutil**. 

 Para gerir os certificados, execute o certutil em cada cliente com uma das seguintes opções:  

|Opção|Mais informações|  
|------------|----------------------|  
|importPFX|Utilize esta opção para especificar um certificado para substituir o certificado que está a ser utilizado por um cliente.<br /><br /> Quando utiliza **- importPFX**, também tem de utilizar o **-palavra-passe** parâmetro de linha de comandos para fornecer a palavra-passe associada ao ficheiro PKCS #12.<br /><br /> Utilize **-rootcerts** para especificar requisitos de certificado de raiz adicionais.<br /><br /> Exemplo: **certutil - importPFX &lt;caminho para o certificado de PKCS #12 >-palavra-passe &lt;palavra-passe do certificado\> [-rootcerts &lt;lista separada por vírgulas de certificados >]**|  
|-importsitecert|Utilize esta opção para atualizar o certificado de assinatura do servidor de site que se encontra no servidor de gestão.<br /><br /> Exemplo: **certutil - importsitecert &lt;caminho para o certificado DER\>**|  
|-importcrl|Utilize esta opção para atualizar a CRL no cliente com um ou mais caminhos de ficheiro CRL.<br /><br /> Exemplo: **certutil - importcrl &lt;caminhos de ficheiro CRL separados por vírgulas\>**|  
