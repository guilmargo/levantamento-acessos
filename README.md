# Levantamento de recursos e acessos por cargo

Formulário para os gestores informarem, para cada cargo, os equipamentos, sistemas, SharePoint, e-mail, telefonia e outros acessos de que um novo colaborador precisa. As respostas ficam no Firebase (Firestore) do projeto `rh-pesquisa`.

- **Gestores:** abrem o site, escolhem setor e cargo, respondem as 6 categorias ("Precisa" ou "Não precisa") e enviam com nome e e-mail. Não precisam de login.
- **RH:** o link "Acesso do RH", no rodapé, envia um link de acesso por e-mail. Só `bianca.garcia@vaxxinova.com.br` consegue abrir o painel, ver as respostas e baixar o Excel.

## Configuração no Firebase (uma vez só)

1. **Firestore Database** → criar o banco (modo produção) se ainda não existir.
2. **Firestore Database → Regras** → colar o conteúdo de [`firestore.rules`](firestore.rules) e publicar.
3. **Authentication → Método de login** → ativar **E-mail/senha** e, dentro dele, **Link do e-mail (login sem senha)**.
4. **Authentication → Configurações → Domínios autorizados** → adicionar `guilmargo.github.io`.

## Estrutura dos dados

| Coleção | Conteúdo | Quem lê |
|---|---|---|
| `respostas/{cargo}` | itens por categoria, categorias "não precisa", nome e e-mail de quem respondeu, data | só o RH |
| `status/{cargo}` | se o cargo foi respondido e quantos itens | todos (mostra "Respondido/Pendente") |

A lista de setores e cargos fica em `index.html` (constante `AREAS`). O id de cada cargo segue a ordem da lista, então, para incluir cargos novos, acrescente no fim de cada setor ou no fim da lista, sem reordenar.
