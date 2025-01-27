---
title: Executar a CLI do Azure em um contêiner do Docker
description: Como executar um contêiner do Docker hospedando a CLI do Azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 01/29/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-cli
ms.devlang: azurecli
ms.openlocfilehash: 346014c1890cd7aa5b4225df15078e55db908a33
ms.sourcegitcommit: 334a1da92a73e42e715e33470057f4194f10b2ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59289076"
---
# <a name="run-azure-cli-in-a-docker-container"></a>Executar a CLI do Azure em um contêiner do Docker

Você pode usar o Docker para executar um contêiner do Linux autônomo com a CLI do Azure pré-instalada. O Docker ajuda você a começar rapidamente com um ambiente isolado para executar a CLI. A imagem também pode ser usada como base para suas próprias implantações.

## <a name="run-in-a-docker-container"></a>Executar em um contêiner do Docker

> [!NOTE]
> A CLI do Azure migrou para o [Registro de Contêiner da Microsoft](https://azure.microsoft.com/services/container-registry). Ainda há suporte para marcas existentes no Hub do Docker, mas as novas versões só estarão disponíveis como mcr.microsoft.com/azure-cli.

Instalar a CLI usando `docker run`.

   ```bash
   docker run -it mcr.microsoft.com/azure-cli
   ```

> [!NOTE]
> Se você quiser acompanhar as chaves SSH do seu ambiente de usuário, use `-v ${HOME}/.ssh:/root/.ssh` para montar suas chaves SSH no ambiente.
>
> ```bash
> docker run -it -v ${HOME}/.ssh:/root/.ssh mcr.microsoft.com/azure-cli
> ```

A CLI está instalada na imagem como o comando `az` no `/usr/local/bin`. Para entrar, execute o comando [az login](/cli/azure/reference-index#az-login).

[!INCLUDE [interactive-login](includes/interactive-login.md)]

Para saber mais sobre os diferentes métodos de autenticação, confira [Entrar com a CLI do Azure](authenticate-azure-cli.md).

## <a name="update-docker-image"></a>Atualizar imagem do Docker

Atualizar com o Docker requer obter a nova imagem e recriar qualquer contêiner existente. Por esse motivo, você deve evitar o uso de um contêiner que hospede a CLI como um armazenamento de dados.

Atualizar sua imagem local com `docker pull`.

```bash
docker pull mcr.microsoft.com/azure-cli
```

## <a name="uninstall-docker-image"></a>Desinstalar imagem do Docker

[!INCLUDE [uninstall-boilerplate.md](includes/uninstall-boilerplate.md)]

Depois de parar qualquer contêiner executando a imagem da CLI, remova-o.

```bash
docker rmi mcr.microsoft.com/azure-cli
```

## <a name="next-steps"></a>Próximas etapas

Agora que você pronto para usar a CLI do Azure, faça um tour breve de seus recursos e comandos comuns.

> [!div class="nextstepaction"]
> [Introdução à CLI do Azure](get-started-with-azure-cli.md)
