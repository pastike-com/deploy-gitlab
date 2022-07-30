.gitlab-ci.yml

```yaml
variables:
  SERVICE_NAME: deploy-gitlab    # Имя сервиса. По умолчанию: имя проекта GitLab ($CI_PROJECT_NAME)
  REGISTRY: ''                   # Хост с registry. По умолчанию пусто.
  REGISTRY_NAMESPACE: pastikecom # Пространство имен в registry, в котором хранятся образы проекта. По умолчанию: `pastikecom`
  DOCKERFILE: Dockerfile         # Позволяет указать путь к Dockerfile, из которого надо собрать образ. По умолчанию: Dockerfile
  VALUES_FILE: values.yaml       # Путь к файлу values.yaml. По умолчанию : `values.yaml`
  CHART_NAME: 'pastike-com/base' # Используемый helm-chart. По умолчанию: `pastike-com/base`
  CHART_VERSION: 0.1.0           # Версия helm-chart. По умолчанию: `0.1.0`
  DEPLOYMENT_NAME: deploy-gitlab # Имя релиза (приложения в группе сервиса). По умолчанию : значение переменной SERVICE_NAME
  DEPLOY_NAMESPACE: pastike-com  # Пространство, в которое происходит деплой. По умолчанию: `pastike-com`

include:
  - 'https://raw.githubusercontent.com/pastike-com/deploy-gitlab/main/default.yaml'

stages:
  - build
  - deploy

build:
  extends: .build

deploy:
  extends: .deploy:k8s
```
