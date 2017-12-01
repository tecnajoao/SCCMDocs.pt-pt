---
title: "Verificador de pré-requisitos"
titleSuffix: Configuration Manager
description: "Saiba como utilizar o Verificador de pré-requisitos para identificar e corrigir problemas que poderão bloquear a um site ou a instalação de função do sistema de sites."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: "3"
author: mstewart
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 6709ee7e9e570c827ec9fc3433fa3acded11e0e4
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>Verificador de pré-requisitos do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Antes de executar a configuração para instalar ou atualizar um site do System Center Configuration Manager ou antes de instalar uma função de sistema de sites num servidor novo, pode utilizar esta aplicação autónoma (**Prereqchk.exe**) da versão do Configuration Manager que pretende utilizar para verificar a preparação do servidor. Utilize o Verificador de pré-requisitos para identificar e corrigir problemas que bloqueariam um site ou a instalação de função do sistema de sites.  

> [!NOTE]  
>  Verificador de pré-requisitos é executado sempre como parte da configuração.  

Por predefinição, quando executa o Verificador de pré-requisitos:  

-   Valida o servidor onde é executado.  
-   É procurado um servidor de site existente no computador local e só as verificações aplicáveis ao site são executadas.  
-   Se não detetados sites existentes são, serão executadas todas as regras de pré-requisitos.  
-   Executa regras para verificar se o software e as definições necessárias para a configuração estão instaladas. É possível que o software necessário será requer configuração adicional ou atualizações de software que não são verificadas pelo verificador de pré-requisitos.  
-   Regista os respetivos resultados **ConfigMgrPrereq.log** ficheiro na unidade do sistema do computador. O ficheiro de registo pode conter informações adicionais que não aparecem na interface de aplicação.  

Quando executar o Verificador de pré-requisitos numa linha de comandos e especificar opções da linha de comandos específicas:  

-   Verificador de pré-requisitos só as verificações que estão associadas ao servidor do site ou sistemas de sites que especificou na linha de comandos.  
-   Para verificar um computador remoto, a conta de utilizador tem de ter direitos de administrador no computador remoto.  

Para obter mais informações sobre as verificações que executa o Verificador de pré-requisitos, consulte [lista das verificações pré-requisitos para o System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copie os ficheiros do Verificador de pré-requisitos para outro computador  

1.  No Explorador do Windows, aceda a uma das seguintes localizações:  

    -   **&lt;*Suporte de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Configuration Manager*\>\BIN\X64**  

2.  Copie os seguintes ficheiros para a pasta de destino no outro computador:  

    -   Prereqchk.exe  
    -   Prereqcore.dll  
    -   Basesql.dll  
    -   Basesvr.dll  
    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>Executar o Verificador de pré-requisitos com verificações predefinidas  

1.  No Explorador do Windows, aceda a uma das seguintes localizações:  

    -   **&lt;*Suporte de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Configuration Manager*\>\BIN\X64**  

2.  Executar **prereqchk.exe** para iniciar o Verificador de pré-requisitos.   
    Verificador de pré-requisitos Deteta sites existentes e se encontrar algum, verifica preparação para atualização. Se não existir nenhum site, todas as verificações são executadas. O **tipo de Site** coluna fornece informações sobre o servidor de site ou o sistema de sites a que a regra está associada.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Executar o Verificador de pré-requisitos numa linha de comandos para todas as verificações predefinidas  

1.  Abra uma janela de linha de comandos e mude de diretório para uma das seguintes localizações:  

    -   **&lt;*Suporte de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Configuration Manager*\>\BIN\X64**  

2.  Introduza **prereqchk.exe /LOCAL** para iniciar o Verificador de pré-requisitos e executar verificações de todos os pré-requisitos no servidor.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Executar o Verificador de pré-requisitos numa linha de comandos para utilizar opções  

1.  Abra uma janela de linha de comandos e mude de diretório para uma das seguintes localizações:  

    -   **&lt;*Suporte de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Configuration Manager*\>\BIN\X64**  

2.  Introduza **prereqchk.exe** com a adição de uma ou mais das seguintes opções da linha de comandos.  

    Por exemplo, para verificar um site primário, poderá utilizar o seguinte:  

       **prereqchk.exe [/NOUI] / /pri /SQL &lt;FQDN do SQL Server\> /SDK &lt;FQDN do fornecedor de SMS\> [/ associar &lt;FQDN do site de administração central\>] [/MP &lt;FQDN do ponto de gestão\>] [/DP &lt;FQDN do ponto de distribuição\>]**  

    **Servidor do site de administração central:**  

    -   **/SEMIU**  

         Não é necessária. Inicia o Verificador de pré-requisitos sem apresentar a interface de utilizador. Tem de especificar esta opção antes de qualquer outra opção na linha de comandos.  

    -   **/ AS ACS**  

         Necessário. Verifica se o computador local cumpre os requisitos para o site de administração central.  

    -   **/ SQL Server &lt;* FQDN do SQL Server*>**  

         Necessário. Utilizar o nome de domínio completamente qualificado (FQDN), verifica se o computador especificado cumpre os requisitos para o SQL Server alojar a base de dados do site do Configuration Manager.  

    -   **/ SDK &lt;* FQDN do fornecedor de SMS*>**  

         Necessário. Verifica se o computador especificado cumpre os requisitos para o fornecedor de SMS.  

    -   **/ Ssbport**  

         Não é necessária. Verifica se uma exceção de firewall está em vigor permitir comunicações na porta do SQL Server Service Broker (SSB). A porta do SSB predefinido é 4022.  

    -   **InstallDir &lt;* caminho de instalação do Configuration Manager*>**  

         Não é necessária. Verifica o espaço mínimo em disco nos requisitos de instalação de site.  

    **Servidor do site primário:**  

    -   **/SEMIU**  

        Não é necessária. Inicia o Verificador de pré-requisitos sem apresentar a interface de utilizador. Tem de especificar esta opção antes de qualquer outra opção na linha de comandos.  

    -   **/ /PRI**  

         Necessário. Verifica se o computador local cumpre os requisitos para o site primário.  

    -   **/ SQL Server &lt;* FQDN do SQL Server*>**  

         Necessário. Verifica se o computador especificado cumpre os requisitos para o SQL Server alojar a base de dados do site do Configuration Manager.  

    -   **/ SDK &lt;* FQDN do fornecedor de SMS*>**  

         Necessário. Verifica se o computador especificado cumpre os requisitos para o fornecedor de SMS.  

    -   **/ ASSOCIAR &lt;* FQDN do site de administração central*>**  

         Não é necessária. Verifica se o computador local cumpre os requisitos para ligar ao servidor do site de administração central.  

    -   **/MP &lt;* FQDN do ponto de gestão*>**  

         Não é necessária. Verifica se o computador especificado cumpre os requisitos para a função de sistema de sites de ponto de gestão. Esta opção só é suportada quando utiliza o **/PRI** opção.  

    -   **/DP &lt;* FQDN do ponto de distribuição*>**  

         Não é necessária. Verifica se o computador especificado cumpre os requisitos para a função de sistema de sites de ponto de distribuição. Esta opção só é suportada quando utiliza o **/PRI** opção.  

    -   **/ Ssbport**  

         Não é necessária. Verifica se uma exceção de firewall está em vigor permitir comunicações na porta do SSB. A porta do SSB predefinido é 4022.  

    -   **InstallDir &lt;* caminho de instalação do Configuration Manager*>**  

         Não é necessária. Verifica o espaço mínimo em disco nos requisitos de instalação de site.  

    **Servidor do site secundário:**  

    -   **/SEMIU**  

         Não é necessária. Inicia o Verificador de pré-requisitos sem apresentar a interface de utilizador. Tem de especificar esta opção antes de qualquer outra opção na linha de comandos.  

    -   **/ SEG &lt;* FQDN do servidor do site secundário*>**  

         Necessário. Verifica se o computador especificado cumpre os requisitos para o site secundário.  

    -   **/ INSTALLSQLEXPRESS**  

         Não é necessária. Verifica se o SQL Server Express pode ser instalado no computador especificado.  

    -   **/ Ssbport**  

         Não é necessária. Verifica se uma exceção de firewall está em vigor permitir comunicações para a porta do SSB. A porta do SSB predefinido é 4022.  

    -   **/ Sqlport**  

         Não é necessária. Verifica se uma exceção de firewall está em vigor para permitir comunicações para o SQL Server porta de serviço e que a porta não está a ser utilizado por outra instância nomeada do SQL Server. A porta predefinida é 1433.  

    -   **InstallDir &lt;* caminho de instalação do Configuration Manager*>**  

         Não é necessária. Verifica o espaço mínimo em disco nos requisitos de instalação de site.  

    -   **/ SourceDir**  

         Não é necessária. Verifica-se de que a conta de computador do site secundário consegue aceder à pasta que aloja os ficheiros de origem para a configuração.  

   **Consola do Configuration Manager:**  

    -   **/ Adminui**  

         Necessário. Verifica se o computador local cumpre os requisitos para instalar o Configuration Manager.  

3.  Na interface de utilizador do Verificador de pré-requisitos, o Verificador de pré-requisitos cria uma lista de problemas detetados no **resultado dos pré-requisitos** secção.  

    -   Clique num item na lista para obter detalhes sobre como resolver o problema.  
    -   Tem de resolver todos os itens na lista que tenham um **erro** estado antes de instalar o servidor do site, sistema de sites ou a consola do Configuration Manager.  
    -   Também pode abrir o **ConfigMgrPrereq.log** ficheiro na raiz da unidade de sistema para rever os resultados do Verificador de pré-requisitos. O ficheiro de registo pode conter informações adicionais que não são apresentadas na interface de utilizador do Verificador de pré-requisitos.  
