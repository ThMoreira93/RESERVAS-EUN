GMAT - Configuração Segura

Este projeto foi ajustado para não expor chaves sensíveis no código versionado.

Passos rápidos

1. Copie `config.example.js` para `config.js` e preencha com seus valores reais.
2. Publique o site (Firebase Hosting, GitHub Pages, Nginx, etc.). Em `firebase.json`, `config.js` já está ignorado.
3. Aplique as regras do Firestore:
   firebase deploy --only firestore:rules
4. (Opcional) Crie índices:
   firebase deploy --only firestore:indexes

Regras do Firestore

As regras em `firestore.rules` permitem:
- Criar `pedidos` sem autenticação (formulário público)
- Ler `pedidos` publicamente (consulta por número/colaborador)
- Atualizar/apagar `pedidos` somente por administradores (`usuarios/{uid}.role == 'admin'`)
- Usuário autenticado lê apenas seu próprio doc em `usuarios/{uid}`; mudanças apenas por admin

Ajuste conforme sua necessidade de privacidade.

Restringindo a API Key do Firebase

- No Google Cloud Console, restrinja a chave por:
  - Aplicativos (HTTP referrers): adicione seus domínios
  - APIs permitidas: habilite apenas Firebase/Firestore/Identity Toolkit
- Considere rotacionar a chave exposta anteriormente.

Desenvolvimento local

- `config.js` está no `.gitignore`. Não faça commit.
- Sirva os arquivos estáticos com qualquer servidor ou `firebase emulators:start` se desejar simular.