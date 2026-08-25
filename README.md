
<div align="center">

# 🌱 ClimaConecta ☁️

**Monitoramento do desmatamento na Amazônia brasileira utilizando arquitetura Serverless na AWS.**

[![AWS](https://img.shields.io/badge/AWS-Serverless-orange?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Python](https://img.shields.io/badge/Python-3.9+-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-brightgreen?style=for-the-badge)](#)

<p align="center">
  <a href="#-visão-geral">Visão Geral</a> •
  <a href="#-arquitetura-da-solução">Arquitetura</a> •
  <a href="#-estrutura-do-repositório">Estrutura</a> •
  <a href="#-tecnologias">Tecnologias</a> •
  <a href="#-implantação-e-uso">Implantação</a> •
  <a href="#-limitações-e-roadmap">Limitações</a> •
  <a href="#-como-contribuir">Contribuição</a> •
  <a href="#-autor">Autor</a>
</p>

</div>

---

## 🔭 Visão Geral

O **ClimaConecta** é uma solução baseada em computação em nuvem projetada para processar, analisar e visualizar dados públicos sobre o desmatamento na Amazônia Legal, utilizando dados históricos e alertas emitidos pelo **INPE** (programas **PRODES** e **DETER**).

Através de uma abordagem orientada a eventos (*event-driven*), o projeto demonstra como ferramentas modernas de nuvem podem transformar dados ambientais brutos em gráficos informativos de forma automatizada, barata e escalável.

### 💡 Por que este projeto existe?
> O acesso a dados ambientais brutos é frequentemente complexo e intimidador para o público geral. O ClimaConecta foi concebido como uma prova de conceito (PoC) para **democratizar o acesso a informações críticas sobre a conservação ambiental**, provando que arquiteturas em nuvem modernas e econômicas podem ser aplicadas a iniciativas de impacto socioambiental (ESG).

## 📐 Arquitetura da Solução

O fluxo de dados da aplicação funciona de maneira 100% desacoplada e sob demanda:

```text
[ Dados INPE ] ──(Upload Manual)──► [ Amazon S3: /dados ]
                                            │
                                    (S3 Event Trigger)
                                            ▼
                                   [ AWS Lambda ]
                            (Processamento Pandas + Matplotlib)
                                            │
                                            ▼
                               [ Amazon S3: /graficos ]
                                            │
                                            ▼
                           [ Interface Web Estática (S3) ]
```

1. **Ingestão:** Os dados brutos do INPE são depositados no bucket S3.
2. **Gatilho (Trigger):** O upload dispara um evento que aciona automaticamente a função Lambda.
3. **ETL e Visualização:** O Lambda processa as métricas via **Pandas** e renderiza novos gráficos via **Matplotlib**.
4. **Publicação:** Os gráficos gerados são gravados de volta no S3 e exibidos diretamente no dashboard HTML.

---

## 📁 Estrutura do Repositório

```bash
climaconecta/
├── lambda/      # Código-fonte da função AWS Lambda, requisitos e guia de Layers
├── s3/          # Estrutura de pastas simulada do bucket S3 e referências
├── site/        # Interface web estática (HTML/CSS) consumidora dos dados
└── README.md    # Documentação principal do projeto
```

---

## 🛠️ Tecnologias

| Componente | Tecnologia | Finalidade no Projeto |
| :--- | :--- | :--- |
| **Computação** | [AWS Lambda](https://aws.amazon.com/lambda/) | Execução de código serverless para ETL e geração de gráficos |
| **Armazenamento** | [Amazon S3](https://aws.amazon.com/s3/) | Armazenamento de dados brutos, gráficos gerados e hospedagem web |
| **Linguagem** | [Python 3.9+](https://www.python.org/) | Linguagem central de script e manipulação analítica |
| **Bibliotecas** | Pandas & Matplotlib | Processamento tabular de dados e renderização dos gráficos |
| **Frontend** | HTML5 / CSS3 Moderno | Visualização limpa e responsiva das métricas geradas |

---

## ⚙️ Implantação e Uso

### Pré-requisitos
- Conta ativa na [Amazon Web Services (AWS)](https://aws.amazon.com/).
- [AWS CLI](https://aws.amazon.com/cli/) instalado e configurado localmente (opcional, caso queira via terminal).
- Python 3.9+ instalado em sua máquina local para testes.

### 1. Configurando o S3
1. Crie um bucket no S3 (ex: `climaconecta-storage`).
2. Recrie a hierarquia descrita na pasta [`s3/`](./s3):
   - `dados/` (entrada dos dados brutos)
   - `graficos/` (saída das imagens processadas)
3. Habilite a funcionalidade de **Hospedagem de Site Estático** se for hospedar o dashboard diretamente pelo S3.

### 2. Configurando a Função Lambda
1. Crie uma função Lambda com runtime **Python 3.9+**.
2. Associe uma **Lambda Layer** com as bibliotecas `pandas` e `matplotlib` (instruções completas em [`lambda/`](./lambda)).
3. Anexe uma política IAM à função com permissões mínimas: `s3:GetObject` na pasta `dados/` e `s3:PutObject` na pasta `graficos/`.
4. Configure o **S3 Event Notification** para acionar o Lambda em todo evento `s3:ObjectCreated:*` na pasta `dados/`.

### 3. Visualizando os Resultados
Suba os arquivos da pasta [`site/`](./site) no diretório raiz do bucket web e acesse o endpoint fornecido pelo S3 para visualizar o painel em funcionamento.

---

## ⚠️ Limitações do Ambiente & Roadmap

> **Nota Acadêmica:** Por ter sido concebido em ambiente restrito de laboratório educacional, foram tomadas decisões arquiteturais para simplificar a infraestrutura:
- **Coleta de Dados:** Ocorre manualmente via download de relatórios do INPE.
- **Distribuição (CDN):** O uso do **Amazon CloudFront** não foi incluído para simplificar os custos e o ciclo de testes no laboratório.

### 🗺️ Próximos Passos (Roadmap)
- [ ] Implementar **Amazon EventBridge + Lambda** para automação de scrapers/consumo de APIs públicas do INPE.
- [ ] Configurar **Amazon CloudFront** associado a certificado SSL via **AWS Certificate Manager (ACM)**.
- [ ] Substituir gráficos estáticos por uma API REST com **Amazon API Gateway** retornando JSON para renderização com Chart.js.

---

## 🤝 Como Contribuir

Contribuições para o aprimoramento da arquitetura ou interface são muito bem-vindas!

1. Faça um **Fork** do repositório.
2. Crie uma branch para a sua funcionalidade:
   ```bash
   git checkout -b feature/minha-melhoria
   ```
3. Commit suas alterações:
   ```bash
   git commit -m "feat: adiciona script para ingestao automatica via API"
   ```
4. Submeta a branch:
   ```bash
   git push origin feature/minha-melhoria
   ```
5. Abra um **Pull Request**.

---

## 📄 Licença

Este projeto está sob a licença **MIT**. Consulte o arquivo [LICENSE](LICENSE) para obter detalhes.

---

## 👨‍💻 Autor

<table align="center">
  <tr>
    <td align="center">
      <a href="https://github.com/erickfanka">
        <img src="https://avatars.githubusercontent.com/erickfanka" width="120px;" alt="Foto de Erick Fanka" style="border-radius: 50%;" />
      </a>
      <br />
      <strong>Erick Fanka</strong>
    </td>
    <td>
      <strong>Medalhista WorldSkills | Cloud Computing | AWS | Python | Redes </strong><br />
      <a href="https://www.linkedin.com/in/erick-fanka">
        <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
      </a>
      <a href="https://github.com/erickfanka">
        <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
      </a>
    </td>
  </tr>
</table>
