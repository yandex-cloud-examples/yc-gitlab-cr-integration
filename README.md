# Хранение Docker-образов из Yandex Managed Service for GitLab в Yandex Container Registry

В GitLab интегрирован сервис [Container Registry](https://docs.gitlab.com/ee/user/packages/container_registry/). Он позволяет хранить Docker-образы для каждого проекта в GitLab.

Вместо GitLab Container Registry вы можете использовать [Yandex Container Registry](https://yandex.cloud/ru/docs/container-registry/). Этот сервис позволяет хранить Docker-образы в облаке и распространять их между управляемыми сервисами Yandex Cloud, например, [Yandex Managed Service for Kubernetes](https://yandex.cloud/ru/docs/managed-kubernetes/) или [Yandex Managed Service for GitLab](https://yandex.cloud/ru/docs/managed-gitlab/).

Использование Yandex Container Registry для хранения образов из проектов GitLab обладает несколькими преимуществами:

* GitLab Container Registry хранит образы и теги на диске [инстанса GitLab](https://yandex.cloud/ru/docs/managed-gitlab/concepts/#instance). Когда место на диске заканчивается, возникает ошибка с HTTP-кодом 500, инстанс становится недоступным. Восстановить его можно только через обращение в техническую поддержку.

  Yandex Container Registry хранит образы и теги в [реестрах](https://yandex.cloud/ru/docs/container-registry/concepts/registry), для которых выделяются отдельные [квоты](https://yandex.cloud/ru/docs/container-registry/concepts/limits). Поэтому накопление Docker-образов и тегов не влияет на место на диске инстанса.

* Образы в Yandex Container Registry остаются доступными, даже если Managed Service for GitLab недоступен.

* Yandex Container Registry поддерживает [сканер уязвимостей Docker-образов](https://yandex.cloud/ru/docs/container-registry/concepts/vulnerability-scanner). С его помощью можно обнаружить уязвимости и устранить их до развертывания приложения. Подробнее о сканировании см. в [блоге Yandex Cloud](https://yandex.cloud/ru/blog/posts/2023/04/vulnerability-scanner-and-yandex-container-registry).


Подготовка инфраструктуры для Managed Service for GitLab и Yandex Container Registry через Terraform описана в [практическом руководстве](https://yandex.cloud/ru/docs/managed-gitlab/tutorials/image-storage), необходимый для настройки конфигурационный файл [container-registry-and-gitlab.tf](container-registry-and-gitlab.tf) расположен в этом репозитории.