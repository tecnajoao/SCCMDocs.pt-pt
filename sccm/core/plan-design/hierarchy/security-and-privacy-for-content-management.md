---
title: "Gestão de segurança e privacidade do conteúdo | Documentos do Microsoft"
description: "Otimize a segurança e privacidade para gestão de conteúdo no System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 46af86ef8b18a8a7c4dfa593b3daf8235081b104
ms.openlocfilehash: c4b9d13079c313879c6d43b10867c616fa962668
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-content-management-for-system-center-configuration-manager"></a>Segurança e privacidade para gestão de conteúdo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém informações de segurança e privacidade para gestão de conteúdo no System Center Configuration Manager. Leia-o em conjunto com os seguintes tópicos:  

-   [Segurança e privacidade da gestão de aplicações no System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

-   [Segurança e privacidade para atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

-   [Segurança e privacidade para implementação do sistema operativo no System Center Configuration Manager](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  

##  <a name="BKMK_Security_ContentManagement"></a> Melhores práticas de segurança para gestão de conteúdo  
 Utilize os seguintes procedimentos recomendados de segurança para gestão de conteúdo:  

 **Para pontos de distribuição da intranet, considere as vantagens e desvantagens da utilização do HTTPS e HTTP**: Na maioria dos cenários, utilização contas de acesso HTTP e pacotes para autorização proporciona mais segurança do que a utilização do HTTPS com encriptação, mas sem autorização. No entanto, se o conteúdo incluir dados confidenciais que pretende encriptar durante a transferência, utilize o HTTPS.  

-   **Quando utilizar HTTPS para um ponto de distribuição**, o Configuration Manager não utiliza contas de acesso pacotes para autorizar o acesso ao conteúdo, mas o conteúdo é encriptado quando é transferido através da rede.  

-   **Se utilizar HTTP para um ponto de distribuição**, pode utilizar contas de acesso aos pacotes para autorização, mas o conteúdo não é encriptado quando é transferido através da rede.  


**Se utilizar um certificado de autenticação de cliente PKI em vez de um certificado autoassinado para o ponto de distribuição, proteja o ficheiro de certificado (.pfx) com uma palavra-passe segura. Se armazenar o ficheiro na rede, proteja o canal de rede quando importar o ficheiro para o Configuration Manager**: Ao exigir uma palavra-passe para importar o certificado de autenticação de cliente que utiliza o ponto de distribuição para comunicar com pontos de gestão, isto ajuda a proteger o certificado contra eventuais atacantes. Utilize a assinatura de bloco de mensagem de servidor (SMB) ou IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere o ficheiro de certificado.  

**Remover a função de ponto de distribuição do servidor do site**: Por predefinição, um ponto de distribuição está instalado no mesmo servidor como servidor do site. Os clientes não precisam de comunicar diretamente com o servidor do site; por conseguinte, para reduzir a superfície de ataque, atribua a função do ponto de distribuição a outros sistemas de sites e remova-a do servidor do site.  

**Proteja o conteúdo ao nível de acesso a pacote**: A partilha do ponto de distribuição permite o acesso de leitura a todos os utilizadores. Para restringir os utilizadores que podem aceder ao conteúdo, utilize contas de acesso aos pacotes quando o ponto de distribuição estiver configurado para HTTP. Isto não é aplicável aos pontos de distribuição baseado na nuvem que não suportam contas de acesso do pacote. Para mais informações sobre contas de acesso a pacote, consulte o artigo [gerir contas para aceder ao conteúdo](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).


**Se o Configuration Manager instala o IIS quando adicionar uma função de sistema de sites de ponto de distribuição, remova o redirecionamento HTTP nem ou Scripts de gestão do IIS e ferramentas quando a instalação do ponto de distribuição estiver concluída**: O ponto de distribuição não necessitam de redirecionamento HTTP nem ou ferramentas e Scripts de gestão do IIS. Para reduzir a superfície de ataque, remova estes serviços de função para a função do servidor Web (IIS).  Para mais informações sobre os serviços de função para a função de servidor (IIS) da web para pontos de distribuição, consulte o artigo [Site e os pré-requisitos de sistema de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

**Defina a permissões de acesso do pacote ao criar o pacote**: Uma vez que as alterações às contas de acesso nos ficheiros do pacote em vigor apenas quando redistribuir o pacote, defina cuidadosamente as pacote permissões de acesso quando cria pela primeira vez o pacote. Isto é especialmente importante quando o pacote é grande ou está distribuído por muitos pontos de distribuição e quando a capacidade de largura de banda de rede para a distribuição de conteúdo é limitada.  

**Implemente controlos de acesso para proteger os suportes de dados que contêm conteúdo pré-configurado**: Conteúdo pré-configurado está comprimido, mas não encriptado. Um atacante poderia ler e modificar os ficheiros que, em seguida, são transferidos para dispositivos. Clientes do Configuration Manager rejeitar conteúdo que é adulterado, mas mesmo assim transferi-lo.  

**Importe o conteúdo pré-configurado utilizando apenas a linha de comandos ferramenta ExtractContent (ExtractContent.exe) que é fornecida com o Configuration Manager e certifique-se de que está assinado pela Microsoft**: Para evitar a adulteração e a elevação de privilégios, utilize o apenas a linha de comandos ferramenta autorizada que é fornecida com o Configuration Manager.  

**Proteja o canal de comunicação entre o servidor do site e a localização de origem do pacote**: Utilize IPsec ou assinatura SMB entre o servidor do site e a localização de origem do pacote ao criar aplicações e pacotes. Isto ajuda a impedir que um intruso adultere os ficheiros de origem.  

**Se alterar a opção de configuração do site para utilizar um Web site personalizado em vez do Web site predefinido após a instalação de funções de ponto de distribuição, remova os diretórios virtuais predefinidos**: Quando muda do Web site predefinido para um Web site personalizado, o Configuration Manager não remove os diretórios virtuais antigos. Remova os diretórios virtuais que originalmente criou o Configuration Manager no Web site predefinido:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Para os pontos de distribuição baseado na nuvem, proteja os detalhes da subscrição e os certificados**: Quando utiliza pontos de distribuição baseado na nuvem, proteger itens de alto valor, incluindo o nome de utilizador e palavra-passe da sua subscrição do Azure, o certificado de gestão do Azure e o certificado de serviço de ponto de distribuição baseado na nuvem. Armazene os certificados de forma segura e se os procurar através da rede quando configurar o ponto de distribuição baseado na nuvem, utilize o IPsec ou a assinatura SMB entre o servidor do site e a localização de origem.  

**Para pontos de distribuição baseado na nuvem: Para a continuidade do serviço, monitorize a data de expiração dos certificados**: O Configuration Manager não avisar quando os certificados importados para gestão de distribuição baseado na nuvem do ponto de serviços está prestes a expirar. Tem de monitorizar as datas de expiração independentemente do Configuration Manager e certifique-se de que renova e importa os novos certificados antes da data de expiração. Isto é especialmente importante se adquirir um Gestor de configuração baseado na nuvem do ponto de distribuição certificado de serviço a partir de uma autoridade de certificação externa (AC), pois pode necessitar de mais tempo para obter um certificado renovado.  

 Se um dos certificados expirar, o Gestor de serviços de nuvem gera o ID de mensagem de estado **9425** e o ficheiro Cloudmgr contém uma entrada que indica que o certificado **está no estado expirado**, com a data de expiração também registada em UTC.  

## <a name="security-considerations-for-content-management"></a>Considerações de segurança para gestão de conteúdo  
Quando planear a gestão de conteúdo, considere o seguinte:  

-   Os clientes não validam o conteúdo enquanto é transferido.  

     Clientes do Configuration Manager validam o hash do conteúdo apenas após a transferência para a respetiva cache do cliente. Se um intruso adulterar a lista de ficheiros para transferência ou o próprio conteúdo, o processo de transferência pode ocupar largura de banda da rede considerável, apenas para o cliente rejeite o conteúdo quando encontrar o hash inválido.  

-   Quando utiliza pontos de distribuição baseado na nuvem, o acesso ao conteúdo é restrito automaticamente para a sua empresa, não podendo restringi-la utilizadores ou grupos selecionados.  

-   Quando utiliza pontos de distribuição baseado na nuvem, os clientes são autenticados pelo ponto de gestão e, em seguida, utilizam um token do Configuration Manager para aceder aos pontos de distribuição baseado na nuvem. O token é válido para ter oito horas. Isto significa que, se um cliente for bloqueado porque já não for fidedigno, este pode continuar a transferir conteúdo a partir de um ponto de distribuição baseado na nuvem enquanto não o período de validade do token expirou. Neste momento, o ponto de gestão não irá emitir outro token para o cliente, porque o cliente está bloqueado.  

     Para evitar um cliente bloqueado Transfira conteúdo durante esse período de oito horas, é possível parar o serviço de nuvem a partir de **nuvem** nó, **configuração da hierarquia**, no **administração** área de trabalho na consola do Configuration Manager.  

##  <a name="BKMK_Privacy_ContentManagement"></a> Informações de privacidade da gestão de conteúdo  
 Gestor de configuração não inclui os dados de utilizador nos ficheiros de conteúdo, embora um utilizador administrativo possa optar por fazê-lo.  

 Antes de configurar a gestão de conteúdo, considere os requisitos de privacidade.  

