# ultimos &nbsp; [![bluebuild build badge](https://github.com/matehuos/ultimos/actions/workflows/build.yml/badge.svg)](https://github.com/matehuos/ultimos/actions/workflows/build.yml)

**ultimos** é um projeto de hobby que serve como um laboratório para meus interresses em infraestrutura, cloud e DevOps. Ele foca na construção de um sistema operacional desktop customizado e nativo em nuvem, criando um ambiente atômico e confiável.

## 🛠️ Ferramentas e Tecnologias Base
Para viabilizar a arquitetura deste projeto, utilizo ferramentas que simplificam a criação de sistemas operacionais imutáveis:
- **[BlueBuild](https://blue-build.org/):** Utilizado como o framework principal e sistema de build. Ele orquestra a montagem do sistema e automatiza o pipeline, facilitando a aplicação de práticas de Infraestrutura como Código (IaC).
- **Bazzite-gnome (Imagem Base):** O projeto não começa do zero. Utilizo o Bazzite (baseado no Fedora Silverblue) com interface GNOME como base. A imagem é customizada com a adição de WMs e outros pacotes.


## 🚀 Motivação
Este repositório tem o único propósito de ganhar experiência prática com ferramentas e conceitos modernos de **DevOps** e **Engenharia de Plataforma**:
- **Infraestrutura como Código (IaC):** Configuração e geração declarativa do sistema operacional.
- **Automação CI/CD:** Pipelines para builds automatizados e publicação em registry OCI utilizando GitHub Actions.
- **Cloud-Native & SO Imutável:** Uso do `recipe.yml` para entregar o sistema como uma imagem de contêiner atômica e inicializável.
- **Segurança da Cadeia:** Imagens e verificação usando o `cosign` do Sigstore.

## 📦 Pacotes Principais
- **Hyprland** e ferramentas
- Niri
- Noctalia Shell v5
- Faugus Game Launcher



---

## 💻 Instalação

Para atualizar (rebase) uma instalação atômica existente do Fedora/BazziteOS para a build mais recente deste projeto:

1. **Faça o rebase para a imagem não assinada** (para instalar as chaves de assinatura e políticas adequadas):
   ```bash
   rpm-ostree rebase ostree-unverified-registry:ghcr.io/matehuos/ultimos:latest
   systemctl reboot
   ```
2. **Faça o rebase para a imagem assinada** (para garantir que futuras atualizações sejam seguras e verificadas):
   ```bash
   rpm-ostree rebase ostree-image-signed:docker://ghcr.io/matehuos/ultimos:latest
   systemctl reboot
   ```

*Nota: A tag `latest` sempre apontará para a versão mais recente que corresponda à versão principal do Bazzite especificada na receita (`recipe.yml`), evitando atualizações acidentais de versão principal.*

## 🛡️ Verificação de Segurança

As imagens geradas aqui são assinadas com segurança usando o [cosign](https://github.com/sigstore/cosign) do [Sigstore](https://www.sigstore.dev/). Para verificar a assinatura e a integridade da imagem, baixe o arquivo `cosign.pub` deste repositório e execute:

```bash
cosign verify --key cosign.pub ghcr.io/matehuos/ultimos
```
