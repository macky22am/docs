---
title: Habilitar las GitHub Actions con la puerta de enlace de MinIO para el almacenamiento en NAS
intro: 'Puedes habilitar a las {% data variables.product.prodname_actions %} en {% data variables.product.prodname_ghe_server %} y utilizar la puerta de enlace de MinIO para el almacenamiento en NAS para almacenar artefactos que generan las ejecuciones del flujo de trabajo.'
permissions: 'Site administrators can enable {% data variables.product.prodname_actions %} and configure enterprise settings.'
versions:
  ghes: '*'
type: how_to
topics:
  - Actions
  - Enterprise
  - Infrastructure
  - Storage
redirect_from:
  - /admin/github-actions/enabling-github-actions-with-minio-gateway-for-nas-storage
shortTitle: Puerta de enlace de MinIO para el almacenamiento en NAS
---

{% warning %}

**Advertencia**: MinIO anunció la eliminación de MinIO Gateways. Desde el 1 de junio de 2022, tanto el soporte como las correcciones de errores para la implementación de la puerta de enlace de la NAS de MinIO estarán disponibles únicamente para los clientes con suscripciones de pago a través de su contrato de soporte LTS. Si quieres seguir utilizando MinIO Gateways con {% data variables.product.prodname_actions %}, te recomendamos migrarte al soporte LTS de MinIO. Para obtener más información, consulta el [programa para eliminar a MinIO Gateway para GCS, Azure, HDFS](https://github.com/minio/minio/issues/14331) en el repositorio minio/minio.

{% endwarning %}

## Prerrequisitos

Antes de que habilites las {% data variables.product.prodname_actions %}, asegúrate de que has completado los siguientes pasos:

* Para evitar la contención de recursos en el aplicativo, te recomendamos que hospedes a MinIO separado de {% data variables.product.product_location %}.
* Crea tu bucket para almacenar los artefactos del flujo de trabajo. Para configurar tu bucket y clave de acceso, consulta la [Documentación de MinIO](https://docs.min.io/docs/minio-gateway-for-nas.html). {% indented_data_reference reusables.actions.enterprise-s3-permission spaces=2 %}

{% data reusables.actions.enterprise-common-prereqs %}

## Habilitar las {% data variables.product.prodname_actions %} con la puerta de enlace de MinIO para almacenamiento en NAS

{% data reusables.enterprise_installation.ssh-into-instance %}
{% data reusables.actions.perform-blob-storage-precheck %}
{% data reusables.enterprise_site_admin_settings.access-settings %}
{% data reusables.enterprise_site_admin_settings.management-console %}
{% data reusables.enterprise_management_console.actions %}
{% data reusables.actions.enterprise-enable-checkbox %}
1. Debajo de "Almacenamiento de artefactos & bitácoras", selecciona **Amazon S3**, e ingresa los detalles de tu bucket de almacenamiento:

   * **URL de servicio de AWS**: La URL para tu servicio de MinIO. Por ejemplo, `https://my-minio.example:9000`.
   * **AWS S3 Bucket**: El nombre de tu bucket de S3.
   * **Clave de AWS S3 Access** y **Clave de AWS S3 Secret**: La `MINIO_ACCESS_KEY` y `MINIO_SECRET_KEY` que se utiliza para tu instancia de MinIO. Para obtener más información, consulta la [Documentación de MinIO](https://docs.min.io/docs/minio-gateway-for-nas.html).

   ![Botón radial para seleccionar el almacenamiento de Amazon S3 y los campos para la configuración de MinIO](/assets/images/enterprise/management-console/actions-minio-s3-storage.png)
1. Debajo de "Almacenamiento de artefactos & bitácoras", selecciona **Forzar el estilo de la ruta**. ![Casilla de verificación para forzar el estilo de ruta](/assets/images/enterprise/management-console/actions-minio-force-path-style.png)
{% data reusables.enterprise_management_console.save-settings %}

{% data reusables.actions.enterprise-postinstall-nextsteps %}
