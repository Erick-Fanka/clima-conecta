# 🔒 Política de Segurança

> *Política padrão para todos os repositórios de **Erick Fanka***
> **Nota:** Estes repositórios são mantidos para fins **educacionais e de estudo**. Embora sigamos boas práticas de segurança, não garantimos a ausência de vulnerabilidades.

---

---

## 📋 Como Reportar Vulnerabilidades

### **1. Via GitHub (Recomendado)**
- Abra uma **Issue** com o título no formato:
  ```markdown
  [SECURITY] Descrição breve da vulnerabilidade
  ```
- **Inclua no relato:**
  - Descrição detalhada do problema
  - Passos para reproduzir
  - Impacto potencial
  - Sugestão de correção (opcional)

### **2. Via Email (Casos Críticos)**
- Envie para: **erickfanka@gmail.com**
- Use para relatar problemas que **não devem ser públicos** inicialmente.

**⏳ Tempo de Resposta:**
- Relatos serão avaliados em até **48 horas úteis**
- Correções serão implementadas conforme prioridade

---

---

## 🛡️ **Princípios de Segurança Adotados**

Todos os projetos seguem estes pilares:

| Princípio | Descrição |
|-----------|-----------|
| **🔐 Mínimo Privilégio** | Apenas permissões estritamente necessárias são concedidas |
| **🔑 Gerenciamento de Credenciais** | **Nunca** armazenamos senhas, chaves ou tokens em arquivos de código |
| **🔒 Configurações Seguras por Padrão** | Serviços são configurados com as opções mais restritivas |
| **🔄 Atualizações Regulares** | Dependências e pacotes são mantidos atualizados |

---

---
## 💡 **Boas Práticas para Contribuidores**

### ❌ **Nunca faça:**
- Comitar **senhas, chaves de API, tokens ou dados sensíveis**
- Armazenar credenciais em arquivos de configuração (`.env`, `.json`, `.yaml`, etc.)
- Usar contas com privilégios excessivos em ambientes de teste

### ✅ **Sempre faça:**
- Use **variáveis de ambiente** para credenciais
- Teste em **ambientes isolados** (Docker, virtualenv, etc.)
- Revise suas alterações antes do **commit**
- Mantenha **dependências atualizadas**

---

---
## 👤 **Autor**

**Erick Fanka**
🎓 Estudante de Cloud Computing | 🏆 Competidor WorldSkills
[🔗 LinkedIn](https://www.linkedin.com/in/erick-fanka) | [🐙 GitHub](https://github.com/Erick-Fanka)
