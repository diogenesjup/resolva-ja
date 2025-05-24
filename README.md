# Resolva Já

Resolva Já - Contrate profissionais qualificados perto de você.

Este aplicativo facilita a conexão entre clientes que precisam de serviços e profissionais qualificados para realizá-los. Ele atende a dois tipos principais de usuários:

*   **Clientes:** Pessoas que buscam profissionais para realizar serviços específicos.
*   **Profissionais:** Prestadores de serviço que buscam oportunidades de trabalho e clientes.

## Sobre o Projeto

O Resolva Já é uma aplicação móvel híbrida desenvolvida utilizando Ionic (tipo "custom") e Cordova, projetada para rodar em plataformas Android e iOS.

**Tecnologias Principais:**

*   **Frontend:** HTML5, CSS3, JavaScript (ECMAScript 6+), com o auxílio das bibliotecas jQuery e Bootstrap para a interface do usuário e interações.
*   **Build/Empacotamento:** Apache Cordova para empacotar os ativos web em uma aplicação nativa instalável.
*   **Configuração Ionic:** `ionic.config.json` define o projeto como do tipo "custom", indicando uma estrutura que não se baseia em frameworks como Angular, React ou Vue, mas sim em JavaScript puro ou outra biblioteca/framework para a lógica da interface.

**Arquitetura da Aplicação:**

A aplicação segue um modelo de Single Page Application (SPA):

*   `www/index.html`: É o ponto de entrada principal que serve como o "shell" da aplicação.
*   `www/app.js`: Inicializa o objeto principal da aplicação (`App`) com configurações e tokens.
*   `www/controllers/Controllers.js`: Contém a classe `App`, que atua como o controlador principal, gerenciando a lógica de negócios, o estado da aplicação e a navegação entre as diferentes seções (views).
*   `www/views/Views.js`: Responsável por gerar e renderizar dinamicamente o conteúdo HTML das diferentes telas (views) dentro da seção `#content` do `index.html`.
*   `www/models/Models.js`: Gerencia toda a comunicação com a API backend, realizando requisições AJAX para buscar e enviar dados.
*   `www/helpers/Helpers.js`: Provavelmente contém funções utilitárias para validação, formatação de dados, etc. (conforme comentários no código).
*   **Armazenamento Local:** O `localStorage` do navegador é usado extensivamente para armazenar dados da sessão, informações do usuário, tokens e outros dados necessários para o funcionamento offline ou para persistência entre sessões.

## Principais Funcionalidades

### Para Clientes (Contratantes)

*   **Cadastro e Login:** Registro simplificado e login (via SMS ou e-mail/senha).
*   **Navegação por Categorias de Serviço:** Explore diversas categorias para encontrar o serviço desejado.
*   **Solicitação de Orçamentos:** Publique detalhes do serviço que precisa, como descrição, requisitos, local e urgência.
*   **Gerenciamento de Solicitações:** Visualize, cancele ou encerre suas solicitações de orçamento.
*   **Edição de Perfil:** Mantenha suas informações de contato e perfil atualizadas.

### Para Profissionais (Prestadores de Serviço)

*   **Cadastro e Login:** Junte-se à plataforma para oferecer seus serviços.
*   **Seleção de Categorias de Atuação:** Especifique as áreas em que você atua.
*   **Visualização de Orçamentos:** Acesse uma lista de solicitações de serviço de clientes.
*   **Desbloqueio de Orçamentos:** Utilize "MOEDAS" (créditos da plataforma) para obter os detalhes de contato do cliente e enviar um orçamento.
*   **Compra de "MOEDAS":** Adquira pacotes de "MOEDAS" utilizando PIX ou Cartão de Crédito (integrado com Gerencianet).
*   **Cursos e Treinamentos:** Acesse módulos de aprendizado, com vídeos e testes, para aprimorar suas habilidades.
*   **Indique e Ganhe:** Programa de indicação para ganhar "MOEDAS" extras.
*   **Edição de Perfil:** Gerencie suas informações profissionais, portfólio e dados de contato.
*   **Alertas e Notificações:** Receba avisos sobre novas oportunidades e interações na plataforma.

## Estrutura do Projeto

Abaixo uma descrição dos principais arquivos e diretórios do projeto:

```
.
├── config.xml               # Configurações do Cordova (plugins, plataformas, metadados do app)
├── ionic.config.json        # Configuração do projeto Ionic (nome, tipo "custom")
├── package.json             # Dependências de desenvolvimento e scripts básicos
├── www/                     # Diretório raiz dos ativos web da aplicação
│   ├── app.js               # Ponto de partida do JavaScript, inicializa o objeto App
│   ├── index.html           # Arquivo HTML principal (shell da aplicação)
│   ├── controllers/
│   │   └── Controllers.js   # Classe App principal, com lógica de controle e navegação
│   ├── models/
│   │   └── Models.js        # Classes para interação com a API backend
│   ├── views/
│   │   └── Views.js         # Classes para renderização das diferentes telas (views)
│   ├── helpers/
│   │   └── Helpers.js       # Funções utilitárias (validação, máscaras, etc.)
│   ├── commom/
│   │   └── commom.js        # Inicialização de plugins externos e configurações comuns
│   ├── assets/              # Recursos estáticos
│   │   ├── css/             # Arquivos de estilo (Bootstrap, customizados)
│   │   ├── js/              # Bibliotecas JavaScript (jQuery, Bootstrap, plugins)
│   │   ├── images/          # Imagens e ícones
│   │   └── fonts/           # Fontes
│   └── ...                  # Outros arquivos e diretórios da aplicação web
├── platforms/               # Código específico da plataforma (Android, iOS) - gerado pelo Cordova
├── plugins/                 # Código dos plugins Cordova - gerado pelo Cordova
└── README.md                # Este arquivo
```

## API Backend

A aplicação depende de uma API backend para todas as suas operações dinâmicas, como autenticação, gerenciamento de dados de usuários, serviços, orçamentos, pagamentos, etc. A classe `Models.js` (`www/models/Models.js`) é responsável por todas as interações com esta API.

As URLs base da API para os diferentes ambientes são configuradas em `www/controllers/Controllers.js`:

*   **Homologação (Desenvolvimento/Testes):**
    *   API: `https://servidorseguro.cloud/resolva-ja/apiservicekeys/`
    *   CDN: `https://servidorseguro.cloud/resolva-ja/cdn/`
    *   DOM (para algumas referências): `https://servidorseguro.cloud/resolva-ja/app/www/`
*   **Produção:**
    *   API: `https://resolvaja.tec.br/apiservicekeys/`
    *   CDN: `https://resolvaja.tec.br/cdn/`
    *   DOM (para algumas referências): `https://resolvaja.tec.br/app/www/`
*   **API de Pagamento (Produção):**
    *   `https://resolvaja.tec.br/pay/`

_Nota: Os tokens de acesso e outras chaves sensíveis para a API e serviços de terceiros (como Gerencianet) são gerenciados dentro do código da aplicação._

## Dependências

### Frontend

*   **jQuery:** Biblioteca JavaScript para manipulação do DOM, eventos e AJAX.
*   **Bootstrap:** Framework CSS para design responsivo e componentes de interface.
*   **SweetAlert2:** Para modais e alertas personalizados.
*   **WOW.js:** Para animações ao rolar a página.
*   **jQuery TouchSwipe:** Para detecção de gestos de swipe.
*   **jQuery Form:** Para submissão de formulários AJAX.
*   **Inputmask:** Para aplicar máscaras de entrada em campos de formulário.

### Cordova Plugins

Listados em `package.json` e/ou `config.xml`:

*   `cordova-plugin-android-permissions`: Para gerenciar permissões no Android.
*   `cordova-plugin-inappbrowser`: Para abrir links em um navegador dentro do app.
*   `cordova-plugin-statusbar`: Para controlar a barra de status do dispositivo.
*   `cordova-plugin-ionic-webview`: Para usar o WebView moderno do Ionic, melhorando performance e compatibilidade.
*   `cordova-plugin-whitelist` (e `cordova-plugin-navigation-whitelist` ou similar, implícito pelo uso de `allow-navigation`): Para controlar quais URLs o WebView pode acessar.

## Configuração e Build (Cordova Geral)

Como o arquivo `package.json` não especifica scripts de build detalhados, os seguintes são comandos Cordova CLI genéricos que podem ser usados para configurar e construir o projeto.

**Pré-requisitos:**

*   Node.js e npm: [https://nodejs.org/](https://nodejs.org/)
*   Cordova CLI: Instale globalmente via npm: `npm install -g cordova`
*   SDK da plataforma desejada (ex: Android Studio para Android, Xcode para iOS).

**Passos:**

1.  **Clonar o repositório (se aplicável):**
    ```bash
    git clone <url-do-repositorio>
    cd <diretorio-do-projeto>
    ```

2.  **Instalar dependências do projeto:**
    (O `package.json` lista `cordova-android` como devDependency. Outras dependências de build podem ser necessárias dependendo do ambiente.)
    ```bash
    npm install
    ```

3.  **Adicionar Plataformas (se não estiverem presentes na pasta `platforms`):**
    ```bash
    cordova platform add android
    # ou
    cordova platform add ios
    ```
    *Nota: O arquivo `config.xml` já especifica a engine android `^13.0.0`.*

4.  **Preparar os recursos da plataforma:**
    Este comando copia os ativos web para a pasta da plataforma específica.
    ```bash
    cordova prepare android
    # ou
    cordova prepare ios
    ```

5.  **Construir a Aplicação:**
    ```bash
    cordova build android
    # ou
    cordova build ios
    ```
    Para construir em modo de release para Android:
    ```bash
    cordova build android --release
    ```
    (Será necessário assinar o APK gerado).

6.  **Executar a Aplicação:**
    *   **Em um emulador ou dispositivo conectado:**
        ```bash
        cordova run android
        # ou
        cordova run ios
        ```
    *   **Abrir no IDE da plataforma (para build e execução manual):**
        *   Android Studio: Importe o projeto da pasta `platforms/android`.
        *   Xcode: Abra o arquivo `.xcworkspace` na pasta `platforms/ios`.

**Observações:**

*   O `android-minSdkVersion` está configurado como `29` e `android-targetSdkVersion` como `34`.
*   Certifique-se de que as variáveis de ambiente para os SDKs das plataformas (ex: `ANDROID_HOME` ou `ANDROID_SDK_ROOT`) estejam configuradas corretamente.

## Autor

*   **Empresa:** Resolva Já Tecnologia
*   **Desenvolvedor Principal:** Diógenes Junior
*   **Contato:** <diogenesjunior.ti@gmail.com>
*   **Website:** [https://resolvaja.tec.br/](https://resolvaja.tec.br/) (Conforme `config.xml`)
