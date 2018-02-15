---
title: "Execute a CLI do Azure 2.0 em um Contêiner do Docker"
description: "Como executar um contêiner do Docker hospedando a CLI do Azure 2.0"
author: sptramer
ms.author: sttramer
manager: routlaw
ms.date: 01/29/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ms.openlocfilehash: 3a09eb6d83bb5401628bd952d199a03ecbb8216e
ms.sourcegitcommit: b93a19222e116d5880bbe64c03507c64e190331e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="run-azure-cli-20-in-a-docker-container"></a><span data-ttu-id="2f56e-103">Executar a CLI do Azure 2.0 em um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="2f56e-103">Run Azure CLI 2.0 in a Docker container</span></span>

<span data-ttu-id="2f56e-104">Você pode usar o Docker para executar um contêiner do Linux autônomo com a CLI do Azure 2.0 pré-instalada.</span><span class="sxs-lookup"><span data-stu-id="2f56e-104">You can use Docker to run a standalone Linux container with the Azure CLI 2.0 pre-installed.</span></span> <span data-ttu-id="2f56e-105">O Docker permite que você inicie rapidamente com um ambiente no qual você pode experimentar a CLI para decidir se é ideal para você ou usar nossa imagem como uma base para sua própria implantação.</span><span class="sxs-lookup"><span data-stu-id="2f56e-105">Docker lets you get started quickly with an environment where you can try out the CLI to decide if it's right for you, or use our image as a base for your own deployment.</span></span>

## <a name="run-in-a-docker-container"></a><span data-ttu-id="2f56e-106">Executar em um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="2f56e-106">Run in a Docker container</span></span>

<span data-ttu-id="2f56e-107">Instalar a CLI usando `docker run`.</span><span class="sxs-lookup"><span data-stu-id="2f56e-107">Install the CLI using `docker run`.</span></span>

   ```bash
   docker run -it microsoft/azure-cli
   ```

<span data-ttu-id="2f56e-108">A CLI está instalada na imagem como o comando `az` no `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="2f56e-108">The CLI is installed on the image as the `az` command in `/usr/local/bin`.</span></span>

> [!NOTE]
> <span data-ttu-id="2f56e-109">Se você quiser acompanhar as chaves SSH do seu ambiente de usuário, use `-v ${HOME}:/root` para montar $HOME como `/root`.</span><span class="sxs-lookup"><span data-stu-id="2f56e-109">If you want to pick up the SSH keys from your user environment, you can use `-v ${HOME}:/root` to mount $HOME as `/root`.</span></span>

> ```bash
> docker run -it -v ${HOME}:/root microsoft/azure-cli
> ```

## <a name="update-docker-image"></a><span data-ttu-id="2f56e-110">Atualizar imagem do Docker</span><span class="sxs-lookup"><span data-stu-id="2f56e-110">Update Docker image</span></span>

<span data-ttu-id="2f56e-111">Atualizar com o Docker requer obter a nova imagem e recriar qualquer contêiner existente.</span><span class="sxs-lookup"><span data-stu-id="2f56e-111">Updating with Docker requires both pulling the new image and re-creating any existing containers.</span></span> <span data-ttu-id="2f56e-112">Por esse motivo, você deve evitar o uso de um contêiner que hospeda a CLI como um armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="2f56e-112">For this reason you should try to avoid using a container that hosts the CLI as a data store.</span></span>

<span data-ttu-id="2f56e-113">Atualizar sua imagem local com `docker pull`.</span><span class="sxs-lookup"><span data-stu-id="2f56e-113">Update your local image with `docker pull`.</span></span>

```bash
docker pull microsoft/azure-cli
```

## <a name="uninstall-docker-image"></a><span data-ttu-id="2f56e-114">Desinstalar imagem do Docker</span><span class="sxs-lookup"><span data-stu-id="2f56e-114">Uninstall Docker image</span></span>

[!INCLUDE [uninstall-boilerplate.md](includes/uninstall-boilerplate.md)]

<span data-ttu-id="2f56e-115">Depois de parar qualquer contêiner executando a imagem da CLI, remova-o.</span><span class="sxs-lookup"><span data-stu-id="2f56e-115">After halting any containers running the CLI image, remove it.</span></span>

```bash
docker rmi microsoft/azure-cli
```