# Mapa Colaborativo - União da Vitória / Porto União

</div>

O **Mapa Colaborativo** é um sistema interativo de reporte de problemas urbanos desenvolvido para web, focado na região de União da Vitória (PR) e Porto União (SC).

> **Nota sobre a versão:** O projeto foi **originalmente desenvolvido com o Supabase** como backend (PostgreSQL + Auth + Storage + RPC + PostGIS + Realtime). Devido à **pausa automática dos projetos gratuitos do Supabase** após ~7 dias sem atividade, a aplicação foi **migrada para uma versão 100% client-side**, com toda a lógica rodando no navegador e persistência via `localStorage`. Isso eliminou a dependência de servidor e permitiu hospedagem estática gratuita no **GitHub Pages**.

## Funcionalidades

O sistema é dividido em dois grandes módulos: **Área do Usuário** e **Mapa Interativo**.

### Área do Usuário
* **Cadastro e Login:** Autenticação com usuário e senha (hash **SHA-256** via `crypto.subtle`, armazenado em `localStorage`).
* **Sessão Persistente:** Controle de usuário logado com opção de sair. Sair em uma aba encerra a sessão em todas as abas abertas.
* **Perfil Simplificado:** Exibição do nome do usuário logado no cabeçalho do mapa.

### Mapa Interativo
* **Reportar Ocorrências:** Clique no mapa para cadastrar problemas (buraco, enchente, acidente, falta de iluminação) com título, descrição e foto.
* **Visualização de Ocorrências:** Marcadores coloridos por categoria, com **clustering** para melhor organização visual.
* **Áreas de Risco:** Camada especial que destaca zonas de risco — calculadas **no navegador** (cluster por categoria + convex hull com raio de 300 m e mínimo de 3 pontos).
* **Busca de Endereços:** Pesquisa com geocoding limitada à região de União da Vitória / Porto União.
* **Minha Localização:** Botão para centralizar o mapa na posição atual do usuário (GPS).
* **Boneco Arrastável:** Ferramenta que calcula e mostra em tempo real as **3 ocorrências mais próximas**, com linhas coloridas, setas indicativas e distâncias em metros/km.
* **Sincronização entre Abas:** Alterações em uma aba refletem automaticamente nas outras via evento `storage`.
* **Upload de Foto com Compressão:** Fotos são redimensionadas no client (máx. 800 px, JPEG 0.7) antes de serem salvas em base64.

### Demonstração

**[Acessar o sistema online →](https://guspelepe.github.io/SUPABASE/)**  

---

## Tecnologias Utilizadas

* **Linguagens e Estrutura:**
  * HTML5, CSS3 e JavaScript (Vanilla)
  * **Sem backend** — aplicação 100% estática
* **Armazenamento Local:**
  * `localStorage` (usuários, ocorrências, sessão e fotos em base64)
  * Hash de senhas via `crypto.subtle` (SHA-256)
  * Compressão de imagens no client via `<canvas>`
* **Mapa e Visualização:**
  * Leaflet
  * Leaflet MarkerCluster
  * Leaflet Control Geocoder
  * Leaflet Polyline Decorator
* **Fontes:** System UI / Sans-serif

## Acesso para Testes

O sistema **não requer servidor nem banco de dados**. O banco de dados local é populado conforme o uso.

**Para testar o sistema:**
1. Acesse a página de cadastro e crie um novo usuário (usuário com no mínimo 3 caracteres e senha com no mínimo 4).
2. Faça login com o usuário criado.
3. Explore o mapa, reporte ocorrências e teste as ferramentas (áreas de risco, boneco arrastável, busca, GPS).

**Dica:** Para compartilhar dados de teste entre abas, mantenha todas abertas no mesmo navegador/perfil — o sistema sincroniza automaticamente via evento `storage`.
