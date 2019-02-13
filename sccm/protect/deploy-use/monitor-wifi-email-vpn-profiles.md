---
title: Monitorizar perfis de E-Mail, Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Saiba como monitorizar o estado de conformidade de e-mail, Wi-Fi e perfis VPN no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49602002a789c0bd1e8d8cc128d3062fde9194fc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137699"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Monitorizar perfis de E-Mail, Wi-Fi e VPN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de ter implementado o System Center Configuration Manager E-Mail, Wi-Fi ou perfis VPN para os utilizadores na sua hierarquia, pode utilizar os procedimentos seguintes para monitorizar o estado de conformidade do perfil:  

-   [Como Ver Resultados de Compatibilidade na consola do Configuration Manager](#BKMK_console)  

-   [Como Ver Resultados de Compatibilidade através da Utilização de Relatórios](#BKMK_Reports)  

##  <a name="BKMK_console"></a> Como Ver Resultados de Compatibilidade na consola do Configuration Manager  
 Utilize este procedimento para ver os detalhes sobre a compatibilidade dos perfis implementados na consola do System Center Configuration Manager.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver os resultados de compatibilidade na consola do Configuration Manager  

1.  Na consola do System Center Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , clique em **Implementações**.  

3.  Na **implementações** , selecione a implementação de perfil para o qual pretende rever as informações de conformidade.  

4.  Pode rever informações de resumo sobre a compatibilidade da implementação do perfil na página principal. Para ver informações mais detalhadas, selecione a implementação de perfil e, em seguida, no **home page** separador a **implantação** , clique em **Ver estado** para abrir o **Estado da implementação** página.  

     A página **Estado da Implementação** contém os seguintes separadores:  

    -   **Em conformidade:** Apresenta a compatibilidade do perfil que baseia-se no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário sob o nó **Utilizadores** da área de trabalho **Ativos e Conformidade** , contendo todos os utilizadores em conformidade com este perfil. O **detalhes do ativo** painel apresenta os utilizadores que estão em conformidade com o perfil. Faça duplo clique num utilizador da lista para visualizar informações adicionais.  

        > [!IMPORTANT]  
        >  Um perfil não é avaliado se não for aplicável num dispositivo cliente; No entanto, é devolvido como compatível.  

    -   **Erro:** Mostra uma lista de todos os erros para a implementação de perfil selecionado com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário sob o nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** , contendo todos os utilizadores que geraram erros com este perfil. Quando selecionar um utilizador, o painel **Detalhes do Ativo** apresenta os utilizadores que são afetados pelo problema selecionado. Faça duplo clique num utilizador da lista para visualizar informações adicionais sobre o problema.  

    -   **Não compatível:** Mostra uma lista de todas as regras não compatíveis no perfil com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário sob o nó **Utilizadores** da área de trabalho **Ativos e Conformidade** , contendo todos os utilizadores não conformes com este perfil. Quando selecionar um utilizador, o painel **Detalhes do Ativo** apresenta os utilizadores que são afetados pelo problema selecionado. Faça duplo clique num utilizador da lista para visualizar mais informações sobre o problema.  

    -   **Desconhecido:** Apresenta uma lista de todos os utilizadores que não comunicaram compatibilidade para a implementação de perfil selecionado, juntamente com o estado atual do cliente dos dispositivos.  

5.  Sobre o **estado de implementação** página, poderá rever informações detalhadas sobre a compatibilidade do perfil implementado. É criado um nó temporário no nó **Implementações** que o ajuda a localizar novamente estas informações de forma rápida.  

##  <a name="BKMK_Reports"></a> Como Ver Resultados de Compatibilidade através da Utilização de Relatórios  
 Definições de compatibilidade, que incluem perfis no System Center Configuration Manager, também inclui vários relatórios incorporados que permitem monitorizar informações sobre os perfis. Estes relatórios têm a categoria de relatório de **Gestão de Compatibilidade e Definições**.  

> [!IMPORTANT]  
>  Deverá utilizar um caráter universal (%) ao utilizar os parâmetros **Filtro do dispositivo** e **Filtro do utilizador** nos relatórios de definições de compatibilidade.  

 Para obter mais informações sobre como configurar os relatórios no System Center Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
