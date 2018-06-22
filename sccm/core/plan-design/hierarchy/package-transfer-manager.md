---
title: Gestor de Transferência de Pacotes
titleSuffix: Configuration Manager
description: Compreenda a forma como o Gestor de transferência de pacotes no System Center Configuration Manager transfere conteúdo de um servidor de site para pontos de distribuição remoto.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44041fd0eb2a71cc72d809eea0a0b8d15ba6c53e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338004"
---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Gestor de transferência de pacotes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Um site do System Center Configuration Manager, o Gestor de transferência do pacote é um componente do serviço do SMS_Executive que gere a transferência de conteúdo de um computador de servidor do site para pontos de distribuição remotos num site. (Um ponto de distribuição remoto é aquele que não se encontra num computador do servidor do site.) O Gestor de transferência do pacote não suporta configurações pelo administrador, mas a compreender como funciona o pode ajudar a planear a infraestrutura de gestão de conteúdo. Também o pode ajudar a resolver problemas com a distribuição de conteúdo.


Quando distribui conteúdo por um ou mais pontos de distribuição remotos num site, o **Gestor de distribuição** cria uma tarefa de transferência de conteúdo. Em seguida, notifica o Gestor de transferência de pacotes em servidores de site primário e secundário para transferir o conteúdo aos pontos de distribuição remoto.

 Gestor de transferência de pacotes regista as respetivas ações no **pkgxfermgr.log** ficheiro no servidor do site. O ficheiro de registo é a única localização onde pode ver as atividades do Gestor de transferência de pacotes.  

> [!NOTE]  
>  Em versões anteriores do Configuration Manager, o Gestor de distribuição gere a transferência de conteúdo para um ponto de distribuição remoto. O Gestor de distribuição também gere a transferência de conteúdo entre sites. Com o System Center Configuration Manager, o Gestor de distribuição continua a gerir a transferência de conteúdo entre dois sites. No entanto, o Gestor de transferência do pacote agora gere a transferência de conteúdo a um grande número de pontos de distribuição. Isto ajuda a aumentar o desempenho global da implementação de conteúdo entre sites e pontos de distribuição num site.  

Para transferir conteúdo para um ponto de distribuição padrão, o Gestor de transferência de pacotes tem um funcionamento igual o Gestor de distribuição em versões anteriores do Configuration Manager. Isto é, gere ativamente a transferência de ficheiros para cada ponto de distribuição remoto. No entanto, para distribuir conteúdo para um ponto de distribuição de solicitação, o Gestor de transferência de pacotes notifica que o ponto de distribuição de solicitação que conteúdo está disponível. A distribuição de solicitação ponto, em seguida, assume o processo de transferência.  

As informações seguintes descrevem como o Gestor de transferência de pacotes gere a transferência de conteúdo para pontos de distribuição padrão e para pontos de distribuição configurados como pontos de distribuição de solicitação:
1.  **Administrador implementa conteúdo para um ou mais pontos de distribuição num site.**  

    -   **Ponto de distribuição padrão:** Gestor de distribuição cria uma tarefa de transferência de conteúdo para esse conteúdo.  

    -   **Ponto de distribuição de solicitação:** Gestor de distribuição cria uma tarefa de transferência de conteúdo para esse conteúdo.  

2.  **Gestor de distribuição executa verificações preliminares.**  

    -   **Ponto de distribuição padrão:** Gestor de distribuição executa uma verificação básica para confirmar que cada ponto de distribuição está preparado para receber o conteúdo. Após esta verificação, o Gestor de distribuição notifica o Gestor de transferência de pacotes para iniciar a transferência de conteúdo ao ponto de distribuição.  

    -   **Ponto de distribuição de solicitação:** No Gestor de transferência de pacotes notifica a distribuição de solicitação do Gestor de distribuição inicia ponto que não há uma nova tarefa de transferência de conteúdo. O Gestor de distribuição não verifica o estado dos pontos de distribuição remotos que são pontos de distribuição de solicitação, porque cada ponto de distribuição de solicitação gere as suas próprias transferências de conteúdo.  

3.  **Gestor de transferência de pacotes prepara a transferência de conteúdo.**  

    -   **Ponto de distribuição padrão:** Gestor de transferência de pacotes examina o arquivo de conteúdos de instância única de cada ponto de distribuição remoto especificado. O objetivo é identificar ficheiros que já estejam nesse ponto de distribuição. Em seguida, filas de Gestor de transferência de pacotes para transferência apenas os ficheiros que ainda não está presente.  

        > [!NOTE]  
        >  Para copiar cada ficheiro da distribuição para o ponto de distribuição, mesmo se os ficheiros já estejam presentes no single instance store do ponto de distribuição, utilize o **redistribuir** ação para o conteúdo.  

    -   **Ponto de distribuição de solicitação:** Para cada ponto de distribuição de extração na distribuição, o Gestor de transferência de pacotes verifica que os pontos de distribuição de origem, para confirmar se o conteúdo está disponível de pontos de distribuição de extração.  

        -   Quando o conteúdo está disponível no ponto de distribuição de origem pelo menos, o Gestor de transferência de pacotes envia uma notificação a esse ponto de distribuição de solicitação. A notificação direciona esse ponto de distribuição para iniciar o processo de transferência de conteúdo. A notificação inclui nomes de ficheiro e tamanhos, atributos e valores de hash.  

        -   Quando o conteúdo ainda não estiver disponível, o Gestor de transferência de pacotes envia uma notificação para o ponto de distribuição. Em vez disso, repete a verificação a cada 20 minutos até que o conteúdo está disponível. Em seguida, quando o conteúdo estiver disponível, o Gestor de transferência de pacotes envia a notificação a esse ponto de distribuição de solicitação.  

        > [!NOTE]  
        >  Para o ponto de distribuição de solicitação de copiar cada ficheiro da distribuição para o ponto de distribuição, mesmo que os ficheiros já estejam presentes no single instance store do ponto de distribuição de solicitação, utilize o **redistribuir** ação para o conteúdo.  

4.  **Conteúdo começa a transferência.**  

    -   **Ponto de distribuição padrão:** Gestor de transferência de pacotes copia ficheiros para cada ponto de distribuição remoto. Durante a transferência para um ponto de distribuição padrão:  

        -   Por predefinição, o Gestor de transferência do pacote pode em simultâneo processar três pacotes exclusivos e distribuí-los por cinco pontos de distribuição em paralelo. No seu conjunto, estas são designadas por **definições de distribuição simultânea**. Para configurar a distribuição simultânea, além de **propriedades do componente de distribuição de Software** para cada site, aceda ao **geral** separador.  

        -   Gestor de transferência de pacotes utiliza as configurações de largura de banda de agendamento e a rede de cada ponto de distribuição ao transferir conteúdo para esse ponto de distribuição. Para configurar estas definições, o **propriedades** de cada ponto de distribuição remoto, avance para o **agenda** e **limites de velocidade** separadores. Para obter mais informações, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Ponto de distribuição de solicitação:** Quando um ponto de distribuição de extração recebe um ficheiro de notificação, o ponto de distribuição inicia o processo para transferir o conteúdo. O processo de transferência é executado independentemente em cada ponto de distribuição de solicitação:  

        1.   A distribuição de extração identifica os ficheiros na distribuição de conteúdo que já não tem no seu single instance store e prepara a transferência desse conteúdo a partir de um dos respetivos pontos de distribuição de origem.  

        2.   Em seguida, as verificações de ponto de distribuição de solicitação com cada um dos respetivos pontos de distribuição de origem, por ordem, até localizar um ponto de distribuição de origem que tenha o conteúdo disponível. Quando o ponto de distribuição de extração identifica um ponto de distribuição de origem com o conteúdo, inicia a transferência desse conteúdo.  

        > [!NOTE]  
        >  O processo para transferir o conteúdo pelo ponto de distribuição de extração é igual à que é utilizado por clientes do Configuration Manager. Para a transferência de conteúdo pelo ponto de distribuição de solicitação, não são utilizadas em simultâneo transferir definições. Agendamento e limitação opções em que configura para pontos de distribuição padrão não são utilizados o.  

5.  **Conclusão da transferência de conteúdo.**  

    -   **Ponto de distribuição padrão:** Depois do Gestor de transferência de pacotes terminar transferir ficheiros para cada ponto de distribuição remoto designado, verifica o hash do conteúdo no ponto de distribuição. Em seguida, notifica o Gestor de distribuição que a distribuição foi concluída.  

    -   **Ponto de distribuição de solicitação:** Após o ponto de distribuição de extração concluir a transferência de conteúdo, o ponto de distribuição verifica o hash do conteúdo. Em seguida, submete uma mensagem de estado ao ponto de gestão do site para indicar o êxito. Se, após 60 minutos este estado não for recebido, o Gestor de transferência do pacote reativado novamente. Verificar a existência de com o ponto de distribuição de extração para confirmar se o ponto de distribuição de solicitação transferiu o conteúdo. Se a transferência de conteúdo está em curso, o Gestor de transferência de pacotes permanecerá suspenso durante outro 60 minutos antes de verifica novamente com o ponto de distribuição de solicitação. Este ciclo continuará até o ponto de distribuição de extração concluir a transferência do conteúdo.  
