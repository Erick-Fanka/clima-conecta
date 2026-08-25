# ClimaConecta - AWS Lambda ⚡

Processamento de dados do INPE (PRODES e DETER), geração de gráficos e armazenamento no Amazon S3.

---

## Arquitetura

```
INPE (PRODES/DETER) → Lambda → Gráficos → S3 → Site
```

## Componentes

| Arquivo | Função |
|---|---|
| `lambda_function.py` | Função principal da Lambda |
| `layer.zip` | Layer com dependências (~70 MB) |

## Setup da Layer

| Passo | Comando |
|---|---|
| Clonar o repositório | `git clone https://github.com/Erick-Fanka/clima-conecta.git` |
| Enviar layer para o S3 | `aws s3 cp lambda/layer.zip s3://seu-bucket/` |
| Criar a Layer na AWS | Usar o arquivo do S3 no console da Lambda |

> **Nota:** O arquivo `layer.zip` (~70 MB) não pode ser visualizado no GitHub, mas pode ser baixado normalmente.
