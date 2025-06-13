# 🚀 EvoAPI MCP Server

Um servidor MCP (Model Context Protocol) para integração com Evolution API, permitindo interação com WhatsApp através de agentes de IA.

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://python.org)
[![MCP](https://img.shields.io/badge/MCP-1.6+-green.svg)](https://modelcontextprotocol.io)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![smithery badge](https://smithery.ai/badge/@fellipesaraiva88/evoapi-mcp)](https://smithery.ai/server/@fellipesaraiva88/evoapi-mcp)

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Instalação](#instalação)
- [Configuração](#configuração)
- [Uso](#uso)
- [API Reference](#api-reference)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Contribuição](#contribuição)
- [Licença](#licença)

## 🎯 Sobre o Projeto

O **EvoAPI MCP Server** é uma ponte entre agentes de IA (como Claude) e a Evolution API, permitindo que assistentes virtuais interajam com WhatsApp de forma programática. O projeto oferece funcionalidades completas para:

- 📱 Gerenciamento de grupos do WhatsApp
- 💬 Envio de mensagens para grupos e contatos individuais
- 📜 Recuperação de histórico de mensagens
- 🔒 Segurança com variáveis de ambiente

## ✨ Funcionalidades

### 🛠️ Ferramentas MCP Disponíveis

- **`get_groups`**: Lista todos os grupos do WhatsApp disponíveis
- **`get_group_messages`**: Recupera mensagens de um grupo em período específico
- **`send_message_to_group`**: Envia mensagens para grupos
- **`send_message_to_phone`**: Envia mensagens para números individuais

### 🔧 Funcionalidades Auxiliares

- **Exportação CSV**: Exporta dados de grupos para análise
- **Controle de Grupos**: Gerenciamento avançado de grupos
- **Histórico de Mensagens**: Acesso completo ao histórico de conversas

## 🚀 Instalação

### Instalando via Smithery

Para instalar evoapi-mcp para Claude Desktop automaticamente via [Smithery](https://smithery.ai/server/@fellipesaraiva88/evoapi-mcp):

```bash
npx -y @smithery/cli install @fellipesaraiva88/evoapi-mcp --client claude
```

### Pré-requisitos

- Python 3.11+
- UV (gerenciador de pacotes Python)
- Evolution API configurada

### Passo a Passo

1. **Instale o UV globalmente:**
```bash
pip install uv
```

2. **Clone o repositório:**
```bash
git clone https://github.com/seu-usuario/evoapi-mcp.git
cd evoapi-mcp
```

3. **Instale as dependências:**
```bash
# Se não existir pyproject.toml
uv init

# Instale as dependências
uv add mcp[cli] evolutionapi python-dotenv

# Ou se já existir pyproject.toml
uv sync
```

## ⚙️ Configuração

### 1. Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto:

```env
# Evolution API Configuration
EVO_API_URL=https://sua-evolution-api.com
EVO_API_TOKEN=seu_token_aqui
EVO_INSTANCE_NAME=sua_instancia
EVO_INSTANCE_TOKEN=token_da_instancia
```

### 2. Configuração do Claude Desktop

Edite o arquivo de configuração do Claude:

```bash
# Windows
code $env:AppData\Claude\claude_desktop_config.json

# Linux/Mac
code ~/.config/claude/claude_desktop_config.json
```

Adicione a configuração do servidor MCP:

```json
{
  "mcpServers": {
    "evolution_api": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\caminho\\para\\evoapi_mcp",
        "run",
        "evoapi_mcp.py"
      ]
    }
  }
}
```

## 📖 Uso

### Integração com Claude

Após a configuração, você pode usar os seguintes comandos no Claude:

```
Liste meus grupos do WhatsApp
```

```
Envie uma mensagem "Olá pessoal!" para o grupo "Família"
```

```
Mostre as mensagens do grupo X das últimas 24 horas
```

### Uso Programático

```python
from evoapi_mcp import get_groups, send_message_to_group

# Listar grupos
grupos = get_groups()
print(grupos)

# Enviar mensagem
resultado = send_message_to_group("123@g.us", "Olá!")
print(resultado)
```

## 📚 API Reference

### `get_groups() -> str`
Retorna lista formatada de todos os grupos disponíveis.

**Retorno:**
```
Grupo ID: 123456789@g.us, Nome: Família
Grupo ID: 987654321@g.us, Nome: Trabalho
```

### `get_group_messages(group_id: str, start_date: str, end_date: str) -> str`
Recupera mensagens de um grupo em período específico.

**Parâmetros:**
- `group_id`: ID do grupo (formato: `123@g.us`)
- `start_date`: Data inicial (`YYYY-MM-DD HH:MM:SS`)
- `end_date`: Data final (`YYYY-MM-DD HH:MM:SS`)

### `send_message_to_group(group_id: str, message: str) -> str`
Envia mensagem para um grupo específico.

**Parâmetros:**
- `group_id`: ID do grupo
- `message`: Conteúdo da mensagem

### `send_message_to_phone(cellphone: str, message: str) -> str`
Envia mensagem para número individual.

**Parâmetros:**
- `cellphone`: Número no formato internacional (`5511999999999`)
- `message`: Conteúdo da mensagem

## 🏗️ Estrutura do Projeto

```
evoapi_mcp/
├── 📁 docs/              # Documentação adicional
├── 📄 evoapi_mcp.py      # Servidor MCP principal
├── 📄 group_controller.py # Controlador de grupos
├── 📄 group.py           # Modelo de grupo
├── 📄 message_sandeco.py # Modelo de mensagem
├── 📄 send_sandeco.py    # Cliente de envio
├── 📄 export_groups_csv.py # Exportação CSV
├── 📄 pyproject.toml     # Configuração do projeto
├── 📄 .env.example       # Exemplo de variáveis
├── 📄 .gitignore         # Arquivos ignorados
└── 📄 README.md          # Este arquivo
```

## 🔒 Segurança

- ✅ Todas as credenciais são gerenciadas via variáveis de ambiente
- ✅ Nenhum dado sensível é hardcoded no código
- ✅ Conformidade com boas práticas de segurança
- ✅ Auditoria de segurança realizada e aprovada

## 🧪 Testes

Execute os testes para validar a instalação:

```bash
# Teste de importações
python -c "from evoapi_mcp import get_groups; print('✅ Importações OK')"

# Teste de configuração
python -c "from group_controller import GroupController; gc = GroupController(); print(f'✅ Controller: {gc.base_url}')"
```

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add: nova funcionalidade'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📋 Roadmap

- [ ] Suporte para envio de mídia (imagens, vídeos)
- [ ] Webhooks para recebimento de mensagens
- [ ] Interface web para gerenciamento
- [ ] Suporte para múltiplas instâncias
- [ ] Logs avançados e monitoramento

## 📄 Licença

Distribuído sob a licença MIT. Veja `LICENSE` para mais informações.

## 👥 Autores

- **Seu Nome** - *Desenvolvimento inicial* - [@seu-github](https://github.com/seu-usuario)

## 🙏 Agradecimentos

- [Evolution API](https://github.com/EvolutionAPI/evolution-api) - API base para WhatsApp
- [Model Context Protocol](https://modelcontextprotocol.io) - Protocolo MCP
- [FastMCP](https://github.com/pydantic/fastmcp) - Framework MCP

---

<div align="center">

**[⬆ Voltar ao topo](#-evoapi-mcp-server)**

Feito com ❤️ para a comunidade

</div>