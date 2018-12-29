---
title: Pré-visualização do UUP
titleSuffix: Configuration Manager
description: Instruções para a pré-visualização de integração de UUP
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 0b0da585-0096-410b-8035-6b7a312f37f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: d2aac5945d4b7678acf78d215c557a34aaef9c72
ms.sourcegitcommit: f5fa9e657350ceb963a7928497d2adca9caef3d4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/22/2018
ms.locfileid: "53748588"
---
# <a name="uup-private-preview-instructions"></a>Instruções de pré-visualização privada UUP

> [!Note]  
> Estas informações está relacionado com uma funcionalidade de pré-visualização que pode ser substancialmente modificada antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

## <a name="benefits"></a>Benefícios

### <a name="feature-updates"></a>Atualizações de funcionalidade

Atualizações de funcionalidades com UUP destinam-se a minimizar vários problemas que os clientes têm com manutenção hoje mesmo. Experimente as atualizações de funcionalidade UUP, incluindo:

- Atualizar diretamente para o nível de conformidade de segurança mais recente, já não tem de instalar atualizações de segurança imediatamente após a atualização para estar em conformidade. Cada mês será publicada uma nova atualização de funcionalidade para incluir a atualização cumulativa mais recente. de segurança. Não precisará transfira ou distribuir a maioria do conteúdo da funcionalidade atualização todos os meses, apenas o segurança componente de atualização, que também é partilhado com a atualização cumulativa.

- Todos os pacotes de idiomas e FODs devem ser mantidas e não são perdidos durante o processo de atualização.

- Atualizações de funcionalidades com UUP suportam ficheiros de instalação rápida, permitindo que os clientes reduzir a quantidade de conteúdo de que cada cliente tem de transferir.

### <a name="cumulative-updates"></a>Atualizações cumulativas

As atualizações cumulativas com UUP permitem conteúdo para FODs e os pacotes de idiomas a serem distribuídos offline permitir que os utilizadores finais adquiri-los sob demanda sem a necessidade de ir para a internet ou os esforços de testes tediosos pelos administradores.



## <a name="set-up-instructions"></a>Instruções de configuração

### <a name="1-send-your-wsus-id-to-your-uup-preview-contact-at-microsoft"></a>1. Enviar o seu ID de WSUS ao seu contacto de pré-visualização do UUP na Microsoft

Para participar na pré-visualização privada UUP, tem de partilhar o ID do WSUS com a Microsoft para que possamos lista branca de seu ambiente para a pré-visualização. Sem essa ID, estará não é possível ver as atualizações UUP até a pré-visualização passem pública.

Para obter sua ID do WSUS:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId
```

### <a name="2-upgrade-configmgr-to-a-supported-version"></a>2. Atualização do ConfigMgr para uma versão suportada

Se estiver a sincronizar ficheiros de instalação rápida no seu ambiente, é necessária para ambientes de produção ou 1812 Technical Preview para ambientes de pré-visualização técnica do ConfigMgr 1810 (TOQUE, cadência rápida ou compilações de GA tudo aceitável).

Se não estiver a sincronizar ficheiros de instalação rápida no seu ambiente, é necessária para ambientes de produção ou 1812 Technical Preview para ambientes de pré-visualização técnica do ConfigMgr 1810 UUP correção sobre 1810 GA.


#### <a name="configmgr-1810-uup-hotfix-kb4482615-from-1810-ga-slow-ring"></a>1810 GA (anel lenta) do ConfigMgr 1810 UUP correção (KB4482615)
Se estiver atualmente a ConfigMgr 1810 GA (anel lenta), terá de atualizar do ConfigMgr para o rollup UUP.

1. Aplicar "Correção (KB4482615) do Gestor de configuração 1810" pacote GUI 86450B7D-3574-4CF7-8B11-486A2C1F62A6) – Esta correção permitirá UUP para cenários de não-express.  

    1. Transferir a correção do Microsoft Download Center (ligação será fornecida uma vez publicado)  

    2. Depois de transferir esta correção, consulte a página de Web do Microsoft Docs seguinte para obter instruções de instalação: [Utilizar a ferramenta de registo de atualização para importar correções](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

    3. Para obter informações sobre como transferir ficheiros de suporte da Microsoft, clique no seguinte número de artigo para visualizar o artigo da Base de dados de Conhecimento Microsoft: [Como obter ficheiros de suporte da Microsoft a partir de serviços online](https://support.microsoft.com/help/119591/how-to-obtain-microsoft-support-files-from-online-services)  

2. Depois de atualizar para a correção UUP, atualize os clientes do ConfigMgr para corresponder. Todos os clientes que as atualizações UUP de destino tem de ser atualizados para evitar **desnecessariamente baixar cerca de 6 GB** de conteúdo não utilizado para o cliente.

#### <a name="configmgr-1810-uup-hotfix-kb4482615-from-1810-fast-ring"></a>Cadência rápida de 1810 ConfigMgr 1810 UUP correção (KB4482615)
Se estiver atualmente a uma cadência rápida de 1810 do ConfigMgr, em seguida, terá de atualizar do ConfigMgr com duas atualizações de manutenção, mas adiar a implantação de atualizações de cliente até que fez ambos, para que só precisa de atualizar os clientes de uma vez.

1. Uma correção para implementar até 1810 GA estarão disponível para em breve (prevê o início de Janeiro), espere até ver a atualização são apresentados no atualizações e manutenção.  

2. Atualização (apenas os servidores de site, não clientes) para "Correção do Gestor de configuração 1810 (KB4479288)" (pacote GUID 930FA45E-530F-4B08-B1BF-DE3F5267B03C)  

3. Atualizar novamente para o "Correção do Gestor de configuração 1810 (KB4482615)" (pacote GUID 86450B7D-3574-4CF7-8B11-486A2C1F62A6) – Esta correção permitirá UUP Pro não express.  

    1. Transferir a correção do Microsoft Download Center (ligação será fornecida uma vez publicado)  

    2. Depois de transferir esta correção, consulte a página de Web do Microsoft Docs seguinte para obter instruções de instalação: [Utilizar a ferramenta de registo de atualização para importar correções](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

    3. Para obter informações sobre como transferir ficheiros de suporte da Microsoft, clique no seguinte número de artigo para visualizar o artigo da Base de dados de Conhecimento Microsoft: [Como obter ficheiros de suporte da Microsoft a partir de serviços online](https://support.microsoft.com/help/119591/how-to-obtain-microsoft-support-files-from-online-services)  

4. Depois de atualizar para a correção UUP, atualize os clientes do ConfigMgr para corresponder. Todos os clientes que as atualizações UUP de destino tem de ser atualizados para evitar **desnecessariamente baixar cerca de 6 GB** de conteúdo não utilizado para o cliente.

#### <a name="1812-technical-preview"></a>Pré-visualização técnica 1812
Equivale a 1812 Technical Preview em cenários UUP suportados para a correção de UUP 1810 do ConfigMgr (KB4482615).

A apenas tenha em atenção é que a atualização de cliente de 1812 Technical Preview é dividido de 1810.1 TP ou 1811 TP. Para contornar este problema, terá de desinstalar o 1810.1 TP e 1811 clientes TP, em seguida, instalar o cliente TP 1812 corretamente. Todos os clientes que as atualizações UUP de destino tem de ser 1812 Technical Preview (ou posterior) para impedir **desnecessariamente baixar cerca de 6 GB** de conteúdo não utilizado para o cliente.


### <a name="3-update-windows-clients-to-supported-versions"></a>3. Atualizar clientes do Windows para versões suportadas

#### <a name="for-express-installation-file-sync"></a>Para a sincronização de ficheiros de instalação rápida
Para conteúdo express, suportados incluem as versões do Windows:

- **Windows 10 versão 1709** com [KB4338825](https://support.microsoft.com/help/4338825) (atualização cumulativa de segurança de Julho de 2017) ou posterior  

- **Windows 10 versão 1803** com [KB4284835](https://support.microsoft.com/help/4284835) (atualização cumulativa de segurança de Junho de 2017) ou posterior  

- **Windows 10 versão 1809** com ainda lançado a atualização de que não são de segurança cumulativa de Janeiro (ou a seguinte atualização cumulativa de segurança de Fevereiro) ou posterior

#### <a name="for-non-express-installation-file-sync"></a>Para a sincronização de ficheiros de instalação não express
Para o conteúdo não express, um patch adicional tem de ser aplicada. Este caminho se tornou disponível num formato não cumulativa no catálogo de 12/20 e estará disponível no formato cumulativo normal em Janeiro tardia.

**Windows 10 versão 1709** e **Windows 10 versão 1803** com ambos:
- Dezembro-Janeiro: Os clientes devem ter um nível de base de atualização cumulativa mais a atualização não cumulativa  
    - Atualização cumulativa  
        - 1709: [KB4338825](https://support.microsoft.com/help/4338825) (atualização cumulativa de segurança de Julho de 2017) através de 2019 Janeiro cumulativa atualização de segurança, inclusive  
        - versão 1803: [KB4284835](https://support.microsoft.com/help/4284835) (atualização cumulativa de segurança de Junho de 2017) através de 2019 Janeiro atualização cumulativa de segurança, inclusive  
    - Atualização cumulativa para o não: Esta atualização só está disponível no catálogo e não diretamente de sincronização para o WSUS. Para importar a atualização para o seu ambiente para poder implementá-la, consulte [importar atualizações a partir do catálogo Microsoft Update](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).  
        - 1709: [KB4483530](https://support.microsoft.com/help/4483530)  
        - versão 1803: [KB4483541](https://support.microsoft.com/help/4483541)  
- Fevereiro e muito mais: Para apenas a atualização cumulativa de ainda ser lançada atualização que não são de segurança cumulativa de Janeiro (ou a seguinte atualização cumulativa de segurança de Fevereiro) ou posterior   

**Windows 10 versão 1809** com ainda lançado a atualização de que não são de segurança cumulativa de Janeiro (ou a seguinte atualização cumulativa de segurança de Fevereiro) ou posterior


### <a name="4-enable-express-installation-on-clients-in-client-settings"></a>4. Ativar a instalação rápida nos clientes nas definições do cliente

A definição para ativar a instalação rápida do cliente tem de ser definido para atualizações UUP, independentemente se conteúdo express é ou não sincronizado. Esta definição ativa do ConfigMgr permitir que o WUA determinar o conteúdo necessário para transferir a clientes, em vez de ter o ConfigMgr transferir todo o conteúdo associado com a atualização UUP. Esta definição é necessária mesmo para cenários de não-express porque não existe conteúdo FOD e pacote de idiomas opcional, resultando num não-considerável extra dados que não são necessárias para todos os clientes associados com a atualização.

A ativação desta definição não afetará as transferências de conteúdos do servidor, comportamentos de download de único cliente. É importante que tem o ConfigMgr e versões de cliente do Windows articulada acima antes de ativar esta definição se não o tenha feito-ativar, como essas versões corrigir alguns problemas de compatibilidade com aprovação de atualizações diretamente no WSUS e ativar ConfigMgr para utilizar este canal para UUP das atualizações, mesmo que o conteúdo express não está sincronizado.

Para ativar a instalação rápida nos clientes:

1. Na consola do Configuration Manager, navegue até **Administration** \ **as definições de cliente**  

2. Abra as propriedades das definições de cliente que pretende utilizar ou criar um novo para implementar conforme apropriado.  

3. Sob **atualizações de Software** grupo, defina **ativar a instalação de ficheiros de instalação rápida nos clientes** para **Sim**

![Realce a definição no grupo de atualizações de Software de cliente](../media/uup-preview-client-settings.png)


### <a name="5-make-sure-your-adrs-are-set-as-desired"></a>5. Certifique-se de seu ADRs são definidas conforme pretendido 

Antes de ativar sincronização da UUP atualizações, considere os ADRs e qualquer outra infra-estrutura de atualização que tem no local. Se não pretender que estas atualizações para implementar automaticamente como parte de seu ADRs existente e planos de manutenção, certifique-se de que atualizar seu ADRs filtrá-las, consulte [como encontrar UUP sincronizado atualizações](#how-to-find-synced-uup-updates). Existente planos de manutenção irá implementar não UUP apenas por predefinição, mas pode atualizá-las para alterar este comportamento.

Considere também se estas atualizações irão afetar qualquer um dos seus relatórios de conformidade ou outra infraestrutura apenas, sincronizando-as e efetue quaisquer modificações de pretendido com antecedência. Por exemplo, se avaliar a compatibilidade em todos os produtos, agora verá o UUP e não UUP atualização cumulativa do Windows 10 como não conformes ou em conformidade, por conseguinte, a inclinação seus números.



## <a name="enable-uup-and-start-testing"></a>Ativar UUP e começar a testar

### <a name="select-products-and-classifications-to-sync"></a>Selecione os produtos e classificações para sincronizar

Quando estiver pronto para iniciar a sincronização de atualizações UUP e tentar-os e tenham recebido word da Microsoft que ativámos o WSUS ver o projeto-piloto, ative os novos produtos.

1. [Sincronizar atualizações de Software](/sccm/sum/get-started/synchronize-software-updates) para permitir que os novos produtos preencher  

2. Na consola do Configuration Manager, navegue até **Administration** \ **configuração do Site** \ **Sites**  

3. Selecione o seu site de nível superior (CAS ou autónomo primário)  

4. Open **configurar componentes do Site** \ **ponto de atualização de Software**  

5. Sobre o **produtos** separador, assim que o servidor WSUS é adicionado à pré-visualização, dois novos produtos devem aparecer. Esses produtos contêm o conteúdo UUP de pré-visualização.  

    - **Piloto do Windows 10 UUP**: Atualizações UUP de estação de trabalho do Windows  
    - **Windows Server 2016 UUP**: Atualizações do Windows Server UUP  

6. Sobre o **classificações** separador, certifique-se selecionar:  

    - **Atualizações de segurança**: Para ver as atualizações cumulativas UUP  
    - **Atualizações**: Para ver as atualizações de funcionalidades UUP  

7. Sincronizar atualizações de software para ver as novas atualizações UUP


### <a name="how-to-find-synced-uup-updates"></a>Como encontrar atualizações UUP sincronizadas

Depois de sincronizados atualizações UUP no seu ambiente, poderá ser útil para encontrá-los para testar. Existem duas formas fáceis de encontrar as pré-visualizar atualizações na consola do Configuration Manager.

- Uma vez que estas atualizações de pré-visualização estão em produtos separados, pode sempre utilizar o produto para filtrar ou encontrar estas atualizações. Filtro de produto foi adicionado para planos de manutenção para permitir que selecione se pretende implementar as atualizações de funcionalidade UUP ou não UUP.  

- Há uma nova coluna opcional, **Tag**, na **todas as atualizações de Software** e **todas as atualizações do Windows 10** nós da biblioteca de Software, bem como um filtro em ADRs. Este campo é definido como **UUP** para atualizações UUP e em branco para não UUP atualizações.  


### <a name="updates-available-during-preview"></a>Atualizações disponíveis durante a pré-visualização

- Atualizações cumulativas do Windows 10 1709
    - Atualização de segurança de Dezembro (12/11)
    - Atualização de segurança de Janeiro (1/8)
    - (1/15) de atualização de Janeiro não-segurança
    - Atualização de segurança de Fevereiro (2/12)  

- Atualizações cumulativas do Windows 10 1803
    - Atualização de segurança de Dezembro (12/11)
    - Atualização de segurança de Janeiro (1/8)
    - (1/15) de atualização de Janeiro não-segurança
    - Atualização de segurança de Fevereiro (2/12)  

- Atualizações cumulativas do Windows 10 1809
    - Atualização de segurança de Fevereiro (2/12)  

- Atualizações de funcionalidades de 10 1803 do Windows (a partir de 1709 ou versão 1803)   
    - Conformidade de atualização de segurança de Dezembro (12/11)
    - Conformidade de atualização de segurança de Janeiro (1/8)
    - Conformidade de atualização de segurança de Fevereiro (2/12)  

- Atualizações de funcionalidades de 10 1809 do Windows (a partir de 1709 ou versão 1803)
    - Conformidade de atualização de segurança (12/11) de Dezembro
    - Conformidade de atualização de segurança (1/8) de Janeiro
    - Conformidade de atualização de segurança de Fevereiro (2/12)  

Se necessário, Março e atualizações de segurança futuras continuará a ser publicado em todas estas áreas para enquanto UUP é ainda na pré-visualização (privada ou pública). Assim que concluirmos a pré-visualização, apenas as atualizações cumulativas do Windows 10 versão 1809 e atualizações de funcionalidades (a partir do Windows 10 versão 1803) serão suportadas em produção.


### <a name="scenarios-to-try"></a>Cenários para experimentar

#### <a name="feature-updates"></a>Atualizações de funcionalidade
- Atualização diretamente para o nível de conformidade de segurança à sua escolha  

- Atualização com FODs e pacotes de idiomas instalados antes da atualização, são preservadas durante a atualização  

- Opcionalmente, ative a sincronização de ficheiros de instalação rápida para atualizações de funcionalidades reduzir a quantidade de conteúdo de que cada cliente tem de transferir.  

    > [!Note]  
    > Este benefício de cliente impacta a maior download de servidor e a distribuição, como é o caso para ficheiros de instalação rápida para as atualizações cumulativas.  

#### <a name="cumulative-updates"></a>Atualizações cumulativas
Durante a pré-visualização, manter os clientes em conformidade com a atualização do tipo UUP para várias atualizações consecutivas para ter a noção do expectativas em curso.

#### <a name="content"></a>Conteúdo
A primeira atualização para cada versão principal (1709, 1803, 1809), arquitetura e a combinação do idioma aparecerá ser grande, em ambos os número de ficheiros e espaço em disco, em comparação com o que faria vê em atualizações não UUP antes. Este conteúdo extra é principalmente para todos os pacotes de idioma e FOD para as atualizações cumulativas. Para atualizações de funcionalidades, especialmente se express está ativado existe conteúdo adicional que seja grande para essa primeira atualização. 

No entanto, as atualizações subsequentes (atualizações cumulativas e as atualizações de funcionalidades mensais em níveis mais altos de conformidade) a quantidade de conteúdo novo que tem de ser transferidos e distribuída será muito mais pequena, como todos o FOD e conteúdo do pacote de idioma forma inteligente partilhado através de atualizações em vez de redownloaded ou redistribuído. Durante a pré-visualização, no 1709 e versão 1803, este download mensal será aproximadamente equivalente ao tamanho das atualizações cumulativas que vir em cenários de não-UUP. No entanto, 1809, a história é muito melhor do que o download incremental da atualização cumulativa é muito menor de mês a mês. 

Quando examinar o conteúdo total transferido e distribuídas por um período de 12 meses para não express, versão 1803 sem UUP deve ser aproximadamente equivalente ao 1809 com UUP, e após esse ponto de desequilíbrio o conteúdo total transferido e distribuídas por toda a tempo de vida da versão é mais pequeno no 1809 com UUP. Para o ponto de desequilíbrio express, é mais cedo tal como acontece com 1809, express é apenas para a atualização não cumulativa de atualizações de funcionalidades e, portanto, o conteúdo do servidor de grande custo de express é apenas uma vez por versão, em vez de mensal.

#### <a name="supported-content-channels"></a>Canais de conteúdo suportados
Para a pré-visualização, de teste com o que usar em seus ambientes empresariais reais. UUP oferecerá suporte a todos os canais de conteúdo, incluindo:
- Otimização da entrega do Windows
- Cache de elemento de rede do Configuration Manager
- BranchCache do Windows
- Implementar sem baixar para servidor (nenhum pacote de implantação) para transferir diretamente do MU, que se estiver a utilizar, recomendamos que EFETUE a utilizar em conjunto
- Fornecedores de conteúdo alternativos de terceiros

Para obter mais informações, consulte [entrega de atualização do Windows 10 otimizar](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).