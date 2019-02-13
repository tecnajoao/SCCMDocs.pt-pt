---
title: Lista de verificação de administrador para gestão de energia
titleSuffix: Configuration Manager
description: Utilize a lista de verificação de administrador para o ajudar a planejar e implementar a gestão de energia no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8198669fdf7d0acf3273af2d8a2e83f5b89f520c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156996"
---
# <a name="administrator-checklist-for-power-management-in-system-center-configuration-manager"></a>Lista de verificação de administrador para a gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Esta lista de verificação do administrador fornece os passos recomendados para utilizar a gestão de energia do System Center Configuration Manager na sua organização.  

## <a name="configuring-power-management"></a>Configurar a gestão de energia  
 Utilize estes passos para obter ajuda ao configurar a hierarquia para recolher informações de gestão de energia dos computadores cliente.  

> [!IMPORTANT]  
>  Não aplique esquemas de energia aos computadores na sua hierarquia até ter recolhido e analisado os dados de energia dos computadores cliente. Se aplicar novas definições de gestão de energia a computadores sem examinar primeiro as definições existentes, isto pode representar um aumento do consumo de energia.  

|Tarefa|Detalhes|  
|----------|-------------|  
|Reveja os conceitos de gestão de energia na biblioteca de documentação do Configuration Manager.|Ver [introdução à gestão de energia](introduction-to-power-management.md).|  
|Reveja os pré-requisitos de gestão de energia na biblioteca de documentação do Configuration Manager.|Ver [pré-requisitos para gestão de energia](prerequisites-for-power-management.md).|  
|Reveja as informações relativas às melhores práticas para a gestão de energia.|Ver [melhores práticas para gestão de energia](best-practices-for-power-management.md).|  
|Configure as suas coleções para gerir o consumo de energia dos computadores no seu ambiente.|Utilize o **coleção para relatórios de dados de linha de base**, **coleção para relatórios de dados de linha de base**, **coleção de computadores sem capacidade de gestão de energia**,  **Coleções de computadores para o qual power serão aplicados planos**, **coleções de computadores para o qual power serão aplicados planos**, e **coleções de computadores que estejam a executar o Windows Servidor** para ajudar a gerir as definições de energia para computadores na sua hierarquia. Pode criar várias coleções e aplicar diferentes esquemas de energia a cada coleção.|  
|Ativar a gestão de energia.|Antes de poder começar a utilizar a gestão de energia, tem de ativá-la e configurar as definições de cliente necessárias. Para obter mais informações, consulte [configurar a gestão de energia](configuring-power-management.md).|  
|Recolha informações de gestão de energia dos computadores cliente.|Dados de gestão de energia são comunicados pelos clientes através do inventário de hardware do Configuration Manager. Consoante a agenda de inventário de hardware que tiver configurado, poderá demorar algum tempo para obter o inventário de todos os computadores cliente.|  

## <a name="monitoring-and-planning-phase"></a>Fase de monitorização e planeamento  

|Tarefa|Detalhes|  
|----------|-------------|  
|Executar o relatório **Atividade do Computador**.|O relatório **Atividade do Computador** mostra um gráfico com a atividade do monitor, computador e utilizador numa coleção especificada e num período de tempo especificado. Este relatório contém ligações para o relatório **Detalhes da Atividade do Computador** , que apresenta as capacidades de suspensão e reativação dos computadores na coleção especificada. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Executar o relatório **Consumo de Energia** ou **Consumo de Energia por Dia**.|Os relatórios **Consumo de Energia** e **Consumo de Energia por Dia** apresentam o consumo de energia mensal total em kilowatt por hora (kWh) de uma coleção especificada num período de tempo especificado. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Executar o relatório **Impacto Ambiental** ou  **Impacto Ambiental por Dia**.|Os relatórios **Impacto Ambiental** e **Impacto Ambiental por Dia** apresentam um gráfico que mostra as emissões de dióxido de carbono (CO2) guardadas numa coleção especificada de computadores num período de tempo especificado. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Executar o relatório **Custo da Energia** ou **Custo da Energia por Dia**.|Os relatórios **Custo da Energia** e **Custo da Energia por Dia** apresentam o custo total do consumo de energia num período de tempo especificado. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Executar o relatório **Capacidades de Energia**.|O relatório **Capacidades de Energia** mostra as funcionalidades de gestão de energia dos computadores na coleção especificada. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Definições de Energia**.|O relatório **Definições de Energia** mostra uma lista agregada de definições atuais de energia utilizadas pelos computadores numa coleção especificada. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Exclua todas as coleções de computadores necessárias da gestão de energia.|Ver [configurar a gestão de energia](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Certifique-se de que guarda as informações dos relatórios de gestão de energia gerados durante a fase de monitorização e planeamento. Pode comparar estes dados com as informações de gestão de energia geradas durante as fases de aplicação e compatibilidade, para o ajudar a avaliar a utilização de energia, o custo da energia e a poupança no impacto ambiental, aplicando um plano de energia aos computadores da sua hierarquia.  

## <a name="enforcement-phase"></a>Fase de imposição  

|Tarefa|Detalhes|  
|----------|-------------|  
|Selecionar esquemas de energia existentes ou crie esquemas novos para coleções de computadores na sua organização.|Ver [como criar e aplicar esquemas de energia](create-and-apply-power-plans.md).|  
|Aplicar estes esquemas de energia aos computadores.|Ver [como criar e aplicar esquemas de energia](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Fase de conformidade  

|Tarefa|Detalhes|  
|----------|-------------|  
|Executar o relatório **Atividade do Computador**.|O relatório **Atividade do Computador** mostra um gráfico com a atividade do monitor, computador e utilizador numa coleção especificada e num período de tempo especificado. Este relatório contém ligações para o relatório **Detalhes da Atividade do Computador de Energia** que apresenta as capacidades de suspensão e reativação dos computadores na coleção especificada. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Executar o relatório **Consumo de Energia** ou **Consumo de Energia por Dia**.|Os relatórios **Consumo de Energia** e **Consumo de Energia por Dia** apresentam o consumo de energia mensal total em kilowatt por hora (kWh) de uma coleção especificada num período de tempo especificado. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Executar o relatório **Impacto Ambiental** ou **Impacto Ambiental por Dia**.|Os relatórios **Impacto Ambiental** e **Impacto Ambiental por Dia** apresentam um gráfico que mostra as emissões de dióxido de carbono (CO2) guardadas numa coleção especificada de computadores num período de tempo especificado. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Executar o relatório **Custo da Energia** ou **Custo da Energia por Dia**.|Os relatórios **Custo da Energia** e **Custo da Energia por Dia** apresentam o custo total do consumo de energia num período de tempo especificado. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Resolução de Problemas  

|Tarefa|Detalhes|  
|----------|-------------|  
|Se os computadores da hierarquia não entraram em modo de suspensão ou hibernação, execute o relatório **Relatório de Insónia** para apresentar as causas possíveis.|O **Relatório Insónia** mostra uma lista de causas comuns que impedem os computadores de entrarem em suspensão ou hibernação e o número de computadores que foram afetados por cada causa durante um período de tempo especificado. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
|Se forem aplicados vários planos de energia a um computador, é aplicado o esquema de energia menos restritivo. Execute o relatório **Computadores com Vários Planos de Energia** para ver computadores com vários planos de energia aplicados.|Ver **computadores com vários esquemas de energia** na [como monitorizar e planear a gestão de energia](monitor-and-plan-for-power-management.md).|  
