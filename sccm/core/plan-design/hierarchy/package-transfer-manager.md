---
title: Gestor de Transferência de Pacotes
titleSuffix: Configuration Manager
description: Compreenda a forma como o Gestor de transferência de pacotes no System Center Configuration Manager transfere conteúdo de um servidor de site para pontos de distribuição remotos.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3a465317334879e048ef9fe628a0efbdd5dbad78
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139573"
---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Gestor de transferência de pacotes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Num site do System Center Configuration Manager, o Gestor de transferência do pacote é um componente do serviço SMS_Executive que gere a transferência de conteúdo de um computador do servidor de site para pontos de distribuição remotos num site. (Um ponto de distribuição remoto é aquele que não se encontra num computador do servidor do site.) O Gestor de transferência do pacote não oferece suporte a configurações pelo administrador, mas entender como ele funciona pode ajudá-lo a planear a sua infraestrutura de gerenciamento de conteúdo. Ele pode também ajudar a resolver problemas com a distribuição de conteúdo.


Quando distribui conteúdo por um ou mais pontos de distribuição remotos num site, o **Gestor de distribuição** cria uma tarefa de transferência de conteúdo. Em seguida, notifica o Gestor de transferência de pacotes em servidores de site primário e secundário para transferir o conteúdo aos pontos de distribuição remoto.

 Gestor de transferência de pacotes regista as ações **pkgxfermgr** ficheiro no servidor do site. O ficheiro de registo é o único local onde pode ver as atividades do Gestor de transferência.  

> [!NOTE]  
>  Nas versões anteriores do Configuration Manager, o Gestor de distribuição gere a transferência de conteúdo para um ponto de distribuição remoto. Gestor de distribuição também gere a transferência de conteúdo entre sites. Com o System Center Configuration Manager, o Gestor de distribuição continua a gerir a transferência de conteúdo entre dois sites. No entanto, o Gestor de transferência de pacotes agora gere a transferência de conteúdo para um grande número de pontos de distribuição. Isto ajuda a aumentar o desempenho geral de implantação de conteúdo entre sites e pontos de distribuição num site.  

Para transferir conteúdo para um ponto de distribuição padrão, o Gestor de transferência de pacotes funciona do mesmo modo como o Gestor de distribuição está disponível em versões anteriores do Configuration Manager. Ou seja, gere ativamente a transferência de ficheiros para cada ponto de distribuição remoto. No entanto, para distribuir conteúdo para um ponto de distribuição de solicitação, o Gestor de transferência de pacote notifica que o ponto de distribuição de extração ou conteúdo está disponível. A distribuição de extração de ponto, em seguida, tem sobre o processo de transferência.  

As informações seguintes descrevem como o Gestor de transferência de pacotes gere a transferência de conteúdo para pontos de distribuição padrão e para pontos de distribuição configurados como pontos de distribuição de extração:
1.  **Administrador implementa conteúdo de um ou mais pontos de distribuição num site.**  

    -   **Ponto de distribuição padrão:** Gestor de distribuição cria uma tarefa de transferência de conteúdo para esse conteúdo.  

    -   **Ponto de distribuição de extração:** Gestor de distribuição cria uma tarefa de transferência de conteúdo para esse conteúdo.  

2.  **Gestor de distribuição executa verificações preliminares.**  

    -   **Ponto de distribuição padrão:** Gestor de distribuição executa uma verificação básica para confirmar que cada ponto de distribuição está preparado para receber o conteúdo. Após esta verificação, o Gestor de distribuição notifica o Gestor de transferência de pacotes para iniciar a transferência de conteúdo ao ponto de distribuição.  

    -   **Ponto de distribuição de extração:** Do ponto de Gestor de distribuição é iniciado o Gestor de transferência de pacotes, que, em seguida, notifica a distribuição de extração que existe uma nova tarefa de transferência de conteúdo. O Gestor de distribuição não verifica o estado dos pontos de distribuição remotos que são pontos de distribuição de extração porque cada ponto de distribuição de extração gere as suas próprias transferências de conteúdo.  

3.  **Gestor de transferência de pacotes prepara a transferência de conteúdo.**  

    -   **Ponto de distribuição padrão:** Gestor de transferência de pacotes examina o arquivo de conteúdos de instância única de cada ponto de distribuição remoto especificado. O objetivo é identificar ficheiros que já estejam nesse ponto de distribuição. Em seguida, filas de Gestor de transferência de pacotes para transferência apenas os ficheiros que ainda não estão presentes.  

        > [!NOTE]  
        >  Para copiar cada ficheiro da distribuição para o ponto de distribuição, mesmo que os ficheiros já estejam presentes no single instance store do ponto de distribuição, utilize o **redistribuir** ação para o conteúdo.  

    -   **Ponto de distribuição de extração:** Para cada ponto de distribuição de extração na distribuição, Gestor de transferência de pacotes verifica que os pontos de distribuição de origem, para confirmar se o conteúdo está disponível de pontos de distribuição de extração.  

        -   Quando o conteúdo está disponível num ponto de distribuição de pelo menos uma origem, o Gestor de transferência de pacotes envia uma notificação a esse ponto de distribuição de extração. A notificação direciona esse ponto de distribuição para iniciar o processo de transferência de conteúdo. A notificação inclui nomes de ficheiros e tamanhos, atributos e valores de hash.  

        -   Quando o conteúdo ainda não está disponível, o Gestor de transferência de pacotes não envia uma notificação para o ponto de distribuição. Em vez disso, repete a verificação a cada 20 minutos até que o conteúdo está disponível. Em seguida, quando o conteúdo estiver disponível, o Gestor de transferência de pacotes envia a notificação a esse ponto de distribuição de extração.  

        > [!NOTE]  
        >  Para o ponto de distribuição de extração copiar cada ficheiro da distribuição para o ponto de distribuição, mesmo que os ficheiros já estejam presentes no single instance store do ponto de distribuição de extração de, utilizar o **redistribuir** ação para conteúdo.  

4.  **Conteúdo começa a transferir.**  

    -   **Ponto de distribuição padrão:** Gestor de transferência de pacotes copia ficheiros para cada ponto de distribuição remoto. Durante a transferência para um ponto de distribuição padrão:  

        -   Por predefinição, Gestor de transferência pode simultaneamente processar três pacotes exclusivos e distribuí-los por cinco pontos de distribuição em paralelo. Coletivamente, eles são chamados **definições de distribuição simultânea**. Para configurar a distribuição simultânea, além da **propriedades do componente de distribuição de Software** para cada site, vá para o **geral** separador.  

        -   Gestor de transferência de pacotes utiliza as configurações de largura de banda de rede e de agendamento de cada ponto de distribuição ao transferir conteúdo para esse ponto de distribuição. Para configurar estas definições, na **propriedades** de cada ponto de distribuição remoto, vá para o **agenda** e **limites de velocidade** separadores. Para obter mais informações, consulte [gerir conteúdo e conteúda a infraestrutura do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Ponto de distribuição de extração:** Quando um ponto de distribuição de extração recebe um ficheiro de notificação, o ponto de distribuição inicia o processo para transferir o conteúdo. O processo de transferência é executado de forma independente em cada ponto de distribuição de extração:  

        1.   A distribuição de extração identifica os ficheiros na distribuição de conteúdo que não tem no seu single instance store e prepara a transferência desse conteúdo a partir de um dos respetivos pontos de distribuição de origem.  

        2.   Em seguida, as verificações de ponto de distribuição de extração com cada um dos respetivos pontos de distribuição de origem, por ordem, até localizar um ponto de distribuição de origem que tenha o conteúdo disponível. Quando o ponto de distribuição de extração identifica um ponto de distribuição de origem com o conteúdo, inicia a transferência desse conteúdo.  

        > [!NOTE]  
        >  O processo para transferir o conteúdo pelo ponto de distribuição de extração é o mesmo que foi utilizado por clientes do Configuration Manager. A transferência de conteúdo pelo ponto de distribuição de extração, não são utilizadas as definições de transferência em simultâneo. Agendamento e limitação de opções que configurar para pontos de distribuição padrão não são utilizados qualquer um.  

5.  **Conclusão da transferência de conteúdo.**  

    -   **Ponto de distribuição padrão:** Depois de terminar o Gestor de transferência do pacote de transferência de arquivos para cada ponto de distribuição remoto designado, verifica o hash do conteúdo no ponto de distribuição. Em seguida, notifica o Gestor de distribuição que a distribuição foi concluída.  

    -   **Ponto de distribuição de extração:** Depois do ponto de distribuição de extração concluir a transferência do conteúdo, o ponto de distribuição verifica o hash do conteúdo. Em seguida, submete uma mensagem de estado ao ponto de gestão do site para indicar êxito. Se, após 60 minutos este estado não for recebido, o Gestor de transferência de pacote reativado novamente. Ele verifica-se com o ponto de distribuição de extração para confirmar se o ponto de distribuição de extração transferiu o conteúdo. Se a transferência do conteúdo está em curso, o Gestor de transferência de pacotes permanecerá suspenso durante mais 60 minutos antes de ele verifica novamente com o ponto de distribuição de extração. Este ciclo continuará até o ponto de distribuição de extração concluir a transferência do conteúdo.  
