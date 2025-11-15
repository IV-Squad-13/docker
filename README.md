# F microsserviços

# Repostório para Arquivos Relacionados a Dockerização

## Link para Imagens

- [Monolito](https://hub.docker.com/repository/docker/yuri000/monolito_api/general)
```
docker pull yuri000/monolito_api:latest
```

- [Discovery](https://hub.docker.com/repository/docker/yuri000/squad-13/tags/discovery/sha256:d8c410a3c07b2ac50e071e49b8a239aa660da86315396efd0c5635c1b7824cd4)
```
docker pull yuri000/squad13:discovery
```

- [Gateway](https://hub.docker.com/repository/docker/yuri000/squad-13/tags/gateway/sha256:2c7535eff6ddf7b5785fdb4a1d867fef771d7e8a8857ddc7e0f59dedb4a83bbe)
```
docker pull yuri000/squad13:gateway
```

## Configuração de Variáveis de Ambiente

### Setup Inicial

As credenciais e configurações sensíveis estão em um arquivo `.env` (não commitado):

```bash
# 1. Copie o template
cp .env.example .env

# 2. Edite com suas credenciais
nano .env
```

### Variáveis Necessárias

```bash
POSTGRES_URL=jdbc:postgresql://host:porta/database
POSTGRES_USER=usuario
POSTGRES_PASSWORD=senha
MONGO_URI=mongodb+srv://user:pass@host/db
SERVER_PORT=13000
ALLOWED_ORIGIN=*
SECRET=sua-chave-secreta
```

**⚠️ SEGURANÇA:**
- O arquivo `.env` está no `.gitignore` e **NÃO** deve ser commitado
- Use `.env.example` como template
- GitHub Push Protection está ativo para prevenir vazamento de credenciais