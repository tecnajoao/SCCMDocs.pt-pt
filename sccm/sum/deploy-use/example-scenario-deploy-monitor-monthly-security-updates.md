---
title: Cenário de exemplo para implementar e monitorizar atualizações de software de segurança
titleSuffix: Configuration Manager
description: Utilize neste cenário de exemplo de como utilizar as atualizações de software no Configuration Manager para implementar e monitorizar atualizações de software de segurança para as versões mensais da Microsoft.
author: aczechowski
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 30377a9b2cfde1616114779ab7790deec1fb2bb2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132130"
---
# <a name="example-scenario-for-using-system-center-configuration-manager-to-deploy-and-monitor-the-security-software-updates-released-monthly-by-microsoft"></a>Cenário de exemplo para utilizar o System Center Configuration Manager para implementar e monitorizar as atualizações de software de segurança publicadas mensalmente pela Microsoft

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico fornece um cenário de exemplo de como pode utilizar as atualizações de software no System Center Configuration Manager para implementar e monitorizar as atualizações de software de segurança que a Microsoft divulga mensalmente.  

 Neste cenário, o João é o administrador do Configuration Manager no Woodgrove Bank. O João necessita de criar uma estratégia de implementação de atualizações de software com as condições e os requisitos seguintes:  

- A implementação ativa de atualizações de software ocorre uma semana após o lançamento das atualizações de software de segurança pela Microsoft, na segunda terça-feira de cada mês. Este evento é normalmente denominado "Patch Tuesday".  

- As atualizações de software são transferidas e configuradas nos pontos de distribuição. Em seguida, é testada uma implementação num subconjunto de clientes antes de o João implementar totalmente as atualizações de software no seu ambiente de produção.  

- O João tem de conseguir monitorizar a compatibilidade das atualizações de software mensal ou anualmente.  

  Este cenário pressupõe que a infraestrutura do ponto de atualização de software já foi implementada. Utilize as seguintes informações para planear e configurar as atualizações de software no Configuration Manager.  

|Processo|Referência|  
|-------------|---------------|  
|Rever os principais conceitos das atualizações de software.|[Introdução às atualizações de software](../understand/software-updates-introduction.md)|  
|Planear as atualizações de software. Estas informações ajudam a planear considerações em termos de capacidade e a determinar a infraestrutura do ponto de atualização de software, a instalação do ponto de atualização de software, as definições de sincronização e as definições de cliente para atualizações de software.|[Planear as atualizações de software](../plan-design/plan-for-software-updates.md)|  
|Configurar as atualizações de software. Estas informações ajudam a instalar e a configurar pontos de atualização de software na hierarquia e ajudam a configurar e a sincronizar atualizações de software.<br /><br /> Neste cenário, o João configura a agenda de sincronização de atualizações de software para ocorrem na segunda quarta-feira de cada mês para se certificar de que são obtidas as mais recentes atualizações de software de segurança da Microsoft.|[Sincronizar atualizações de software](../get-started/synchronize-software-updates.md)|  

 As secções seguintes deste tópico fornecem passos de exemplo para ajudá-lo a implementar e monitorizar atualizações de software de segurança do Configuration Manager na sua organização.

##  <a name="BKMK_Step1"></a> Passo 1: Criar um grupo de atualização de software para compatibilidade anual  
 O João cria um grupo de atualização de software que pode ser utilizado para monitorizar a compatibilidade de todas as atualizações de software de segurança lançadas em 2016. Ele efetua os passos da seguinte tabela.  

|Processo|Referência|  
|-------------|---------------|  
|Partir do **todas as atualizações de Software** nó na consola do Configuration Manager, o João adiciona critérios para visualizar apenas segurança atualizações de software que são publicadas ou revistas no ano de 2015 que satisfazem os seguintes critérios:<br /><br /><ul><li>**Critérios**: Data de lançamento ou revisão</li><li>**Condição**: é maior que ou igual à data específica<br />**Valor**: 1/1/2015</li><li>**Critérios**: Classificação da atualização<br />**Valor**: Atualizações de segurança</li><li>**Critérios**: Fora do prazo <br />**Valor**: Não</li></ul>|Não existem informações adicionais|
|O João adiciona todas as atualizações de software filtradas a um novo grupo de atualizações de software com os seguintes requisitos:<br /><br /><ul><li>**Nome**: Atualizações de grupo de compatibilidade - segurança da Microsoft 2015</li><li>**Descrição**: Atualizações de software|[Adicionar atualizações de software a um grupo de atualizações](add-software-updates-to-an-update-group.md)|  

##  <a name="BKMK_Step2"></a> Passo 2: Criar uma regra de implementação automática para o mês atual  
 O João cria uma regra de implementação automática para as atualizações de software de segurança lançadas pela Microsoft para o mês atual. Ele efetua os passos da seguinte tabela.  

|Processo|Referência|  
|-------------|---------------|  
|O João cria uma regra de implementação automática com os seguintes requisitos:<br /><br /><ol><li>No separador **Geral** , o João configura o seguinte:<br /> <ul><li>Especifica **atualizações de segurança mensais** para o nome.</li><li>Seleciona uma coleção de teste com clientes limitados.</li><li>Seleciona **criar um novo grupo de atualização de Software**.</li><li>Verifica se **ativar a implementação após a execução desta regra** não está selecionada.</li></ul></li><li>No separador **Definições de Implementação** , o João seleciona as predefinições.</li><li>Sobre o **atualizações de Software** página, o João configura os seguintes filtros de propriedade e critérios de pesquisa:<br /><ul><li>Data de lançamento ou revisão **Último 1 mês**.</li><li>Classificação da atualização **Atualizações de Segurança**.</li></ul></li><li>Sobre o **avaliação** página, o João ativa a regra seja executada com base numa agenda para o **segunda quinta-feira** de cada **mês**. O João também verifica se a agenda de sincronização está definida para ser executado no **segunda quarta-feira** de cada **mês**.</li><li>O João utiliza as predefinições das páginas Agenda de Implementação, Experiência do Utilizador, Alertas e Definições de Transferência.</li><li>Sobre o **pacote de implementação** página, o João Especifica um novo pacote de implementação.</li><li>O João utiliza as predefinições das páginas Localização de Transferência e Seleção de Idioma.</li></ol>|[Implementar atualizações de software automaticamente](automatically-deploy-software-updates.md)|  

##  <a name="BKMK_Step3"></a> Passo 3: Certifique-se de que as atualizações de software estão prontas para implementar  
 Na segunda quinta-feira de cada mês, o João verifica se as atualizações de software estão prontas para ser implementadas. Ele efetua o passo seguinte.  

|Processo|Referência|  
|-------------|---------------|  
|O João verifica se a sincronização das atualizações de software foi concluída com sucesso.|[Estado de sincronização de atualizações de software](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="BKMK_Step4"></a> Passo 4: Implementar o grupo de atualização de software  
 Depois de se certificar de que as atualizações de software estão prontas para implementar, o João efetua a implementação. Ele efetua os passos da seguinte tabela.  

|Processo|Referência|  
|-------------|---------------|  
|O João cria duas implementações de teste para o novo grupo de atualizações de software. Considera os seguintes ambientes para cada implementação:<br /><br /> **Implementação de teste da estação de trabalho**: O João considera as seguintes opções para a implementação de teste da estação de trabalho:<br /><br /><ul><li>Especifica uma coleção de implementação que contém um subconjunto de clientes de estação de trabalho para verificar a implementação.</li><li>Configura as definições de implementação que são adequadas para os clientes de estação de trabalho em seu ambiente.</li></ul><br />**Implementação de teste do servidor**: O João considera as seguintes opções para a implementação de teste do servidor:<br /><br /><ul><li>Especifica uma coleção de implementação que contém um subconjunto de clientes de servidor para verificar a implementação.</li><li>Configura as definições de implementação que são adequadas para os clientes de servidor em seu ambiente.</li></ul>|[Implementar atualizações de software](deploy-software-updates.md)|  
|O João verifica se as implementações de teste foram implementadas com sucesso.|[Estado de implementação de atualizações de software](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|O João atualiza as duas implementações com novas coleções que incluem os servidores e as estações de trabalho de produção.|Não existem informações adicionais|  

##  <a name="BKMK_Step5"></a> Passo 5: Monitorizar a compatibilidade de atualizações de software implementadas  
 O João monitoriza a compatibilidade das implementações de atualizações de software. Ele efetua o passo da seguinte tabela.  

|Processo|Referência|  
|-------------|---------------|  
|João monitoriza o estado de implementação de atualizações de software na consola do Configuration Manager e verifica os relatórios de implementação de atualização de software disponível a partir da consola.|[Monitorizar atualizações de software no System Center Configuration Manager](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="BKMK_Step6"></a> Passo 6: Adicionar atualizações de software mensais ao grupo de atualizações anuais  
 O João adiciona as atualizações de software do grupo de atualizações de software mensais ao grupo de atualizações de software anuais. Ele efetua o passo da seguinte tabela.  

|Processo|Referência|  
|-------------|---------------|  
|O João seleciona as atualizações de software do grupo de atualizações de software mensais e adiciona-as ao grupo de atualizações de software criado para compatibilidade anual. Ele controla a compatibilidade das atualizações de software e cria vários relatórios para gestão.|[Adicionar atualizações de software a um grupo de atualização implementado](add-software-updates-to-an-update-group.md)|  

O João concluiu com sucesso a implementação mensal de atualizações de software de segurança. Ele continua a monitorizar e a reportar a compatibilidade das atualizações de software para garantir que os clientes do seu ambiente estão nos níveis de compatibilidade aceitáveis.  

##  <a name="BKMK_MonthlyProcess"></a> Processo mensal recorrente para implementar atualizações de software  
 Após o primeiro mês da implementação de atualizações de software, o João efetua os passos três a seis para implementar as atualizações de software de segurança mensais lançadas pela Microsoft.  
