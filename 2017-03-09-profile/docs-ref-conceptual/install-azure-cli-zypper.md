---
title: Instalar a CLI do Azure 2.0 com o zypper
description: Como instalar a CLI do Azure 2.0 com o zypper
keywords: cli do azure, instalar cli do azure, zypper cli do azure, opensuse cli do azure, sle cli do azure
author: sptramer
ms.author: sttramer
manager: routlaw
ms.date: 11/01/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: c01679ccb77880f1f628f4e48683d8ff030a568b
ms.sourcegitcommit: 905939cc44764b4d1cc79a9b36c0793f7055a686
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="install-azure-cli-20-with-zypper"></a>Instalar CLI do Azure 2.0 com zypper

Se você estiver executando uma distribuição que vem com o `zypper`, como o OpenSUSE ou SLE, há um pacote disponível para a CLI do Azure que pode ser instalado em seu sistema.

> [!NOTE]
> Você deve ter o Python 2.7.x ou Python 3.x para usar a CLI. Se a distribuição não tiver um pacote para cada um, [instale o Python](https://www.python.org/downloads/).

## <a name="install"></a>Instalar 

1. Instale `curl`:

   ```bash
   sudo zypper refresh
   sudo zypper install -y curl
   ```

2. Importe a chave de repositório da Microsoft:

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. Crie informações sobre o repositório do `azure-cli` local:

   ```bash
   sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/azure-cli.repo'
   ```

4. Atualize o índice de pacote do `zypper` e instale:

   ```bash
   sudo zypper refresh
   sudo zypper install -y azure-cli
   ```

É possível executar a CLI com o comando `az`.

## <a name="update"></a>Atualização

Você pode atualizar o pacote com o comando `zypper update`.

```bash
sudo zypper refresh
sudo zypper update azure-cli
```

## <a name="uninstall"></a>Desinstalar

Se você decidiu desinstalar a CLI do Azure, lamentamos sua saída. Antes de desinstalar, use o comando `az feedback` para nos fornecer algumas razões por ter escolhido desinstalar e como poderíamos melhorar a experiência da CLI. Queremos assegurar que a CLI do Azure não tenha bugs e seja amigável o máximo possível. Você também pode [registrar um problema do github](https://github.com/Azure/azure-cli/issues).

1. Remova o pacote do seu sistema.

    ```bash
    sudo zypper remove -y azure-cli
    ```

2. Se você não pretende reinstalar a CLI, remova as informações do repositório.

  ```bash
  sudo rm /etc/zypp/repos.d/azure-cli.repo
  ```

3. Se você removeu as informações do repositório, remova também a chave de assinatura do Microsoft GPG.

  ```bash
  MSFT_KEY=`rpm -qa gpg-pubkey /* --qf "%{version}-%{release} %{summary}\n" | grep Microsoft | awk '{print $1}'`
  sudo rpm -e --allmatches gpg-pubkey-$MSFT_KEY
  ```
