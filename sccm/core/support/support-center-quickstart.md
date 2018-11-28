---
title: Início rápido do Centro de suporte
titleSuffix: Configuration Manager
description: Rapidamente, capture o estado de um cliente do Configuration Manager para resolução de problemas.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a9865a591f6947447ebb088b5e5e25db1e9fa54
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458300"
---
# <a name="support-center-quickstart-guide"></a>Guia de início rápido do Centro de suporte

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Support Center possui capacidades poderosas, incluindo a solução de problemas e visualização de registos em tempo real. Também pode ser utilizado em apenas alguns minutos para capturar o estado de um computador de cliente do Configuration Manager. Esta capacidade inclui acesso a clientes remotos.

Criar uma *pacote de solução de problemas* ficheiro (. zip) que captura o estado do cliente. O pacote não apenas contém ficheiros de registo. Ele pode incluir outros tipos de dados, tais como definições de registo e configurações de cliente. Forneça o pacote para um técnico de suporte que usa o Support Center Viewer.



## <a name="prerequisites"></a>Pré-requisitos

- Direitos administrativos locais para um cliente do Configuration Manager  

- O instalador do Support Center. Este ficheiro está no servidor do site em `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. Para obter mais informações, consulte [Support Center - instalação](/sccm/core/support/support-center#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Passo 1: Criar um pacote de dados num cliente local

1.  Centro de suporte de instalação no cliente do Configuration Manager.  

2.  Vá para o **começar** menu, na **Microsoft System Center** grupo, selecione **Centro de suporte**.  

3.  No separador base do Friso, selecione **recolher dados selecionados**. Por predefinição, o Support Center recolhe apenas o conjunto de dados mínimo: registo de ficheiros, a configuração do cliente e o sistema operativo.  

4.  Guarde o ficheiro de pacote de solução de problemas (. zip) para uma pasta no computador. Por predefinição, o nome de ficheiro é semelhante ao seguinte exemplo: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Passo 2: Ver o pacote de dados utilizando o Support Center Viewer

1.  Inicie **Support Center Viewer**. Esta ação pode acontecer em qualquer computador no qual instala o Support Center.  

2.  Selecione **abrir pacote**, procure o ficheiro de pacote e selecione **aberto**.  

3.  Depois do Support Center Viewer processa o arquivo, mude para cada separador disponível. Ver os tipos de dados que recolhe de centro de suporte por predefinição:  

    - **Configuração**  

        - Configuração de cliente do Configuration Manager  

        - Sistema Operativo  

        - Computador  

        - Serviços  

        - Adaptadores de rede  

    - **Registos**: Selecione uma ou mais entradas na lista e selecione **aberto**. Esta ação abre os ficheiros de registo selecionado no Log Viewer. Utilize esta funcionalidade para procurar por códigos de erro e utilizar filtros avançados para ajudá-lo mais rapidamente a analisar ficheiros de registo.  



## <a name="collect-more-data"></a>Recolher mais dados

Além destas capacidades básicas, o Support Center também pode recolher uma ampla variedade de outras informações de estado do cliente. Open **Centro de suporte** e selecione **recolher todos os dados**. Esse processo normalmente dura vários minutos, até mesmo nos computadores mais recentes. Centro de suporte recolhe os seguintes dados adicionais:

  - **Política**: Definições de política do Configuration Manager, incluindo a configuração da política pedida e a configuração da política real  

  - **Certificados**: Informações de chaves públicas para certificados de cliente. Centro de suporte não recolhe as chaves privadas do certificado.  

  - **Registo de cliente**: Recolhe informações de configuração de cliente a partir do registo. Centro de suporte só recolhe informações de registo do Configuration Manager.  

  - **WMI cliente**: Informações de configuração de cliente do WMI. Centro de suporte não recolhe a política de cliente.  

  - **Resolução de problemas**: Dados de resolução de problemas em tempo real para ajudar a diagnosticar problemas comuns de clientes com o Active Directory, pontos de gestão, redes, atribuições de políticas e registo.  

  - **Informações de depuração**: Efetue a depuração de despejo do cliente e os processos relacionados. Informações de depuração podem ser grandes. Permitir que esta opção apenas quando a resolução de problemas com o desempenho do cliente.  

