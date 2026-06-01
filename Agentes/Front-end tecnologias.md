
O familiagaucha-frontend usa principalmente:
Angular 20 como framework frontend.
TypeScript 5.8.
SCSS para estilos.

GovBR-DS:
@govbr-ds/core
@govbr-ds/webcomponents
Web Components via GovBR-DS.
RxJS e Zone.js, padrão do Angular.
Font Awesome para ícones.
Ng Select (@ng-select/ng-select) para selects avançados.
Chart.js para gráficos.
ngx-markdown, marked e PrismJS para renderização/highlight de Markdown e código.
lottie-web para animações Lottie.
Elastic APM RUM (@elastic/apm-rum) para monitoramento frontend.
Na parte de build/deploy:
Node.js 20 no build.
Angular CLI / @angular/build.
Docker com build multi-stage.
Nginx Alpine para servir o app Angular em produção.
Kubernetes/AKS com manifests em aks-desenvolvimento, aks-sit, aks-uat e aks-producao.
Azure Container Registry (sharedservicesquadsacr.azurecr.io).
Azure Pipelines para build e push da imagem Docker.

Também há ferramentas de qualidade/convenção:
Prettier
Husky
lint-staged
Commitizen / commitlint
markdownlint

### Instruções

- TypeScript Strict Mode
- Single quotes, no semicolons
- Use functional patterns where possible
