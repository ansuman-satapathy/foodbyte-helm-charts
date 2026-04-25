services = [
    'user-service',
    'restaurant-service',
    'notification-service',
    'order-service',
    'frontend'
]

for svc in services:
    image_name = 'ghcr.io/ansuman-satapathy/foodbyte-{}'.format(svc)
    local_path = '../foodbyte-{}'.format(svc)
    chart_path = './foodbyte-{}'.format(svc)
    docker_build(image_name, local_path)

    yaml = local('helm template {} {} -f {}/values.yaml'.format(svc, chart_path, chart_path))
    k8s_yaml(yaml)


k8s_yaml('../foodbyte-infra/gateway-class.yaml')
k8s_yaml('../foodbyte-infra/envoy-proxy-config.yaml')
k8s_yaml('./gateway.yaml')

k8s_resource(
    new_name='api-gateway',
    objects=[
        'foodbyte-gateway:Gateway:default',
        'kind-proxy-config:EnvoyProxy:envoy-gateway-system'
    ],
    extra_pod_selectors=[
        {'app.kubernetes.io/component': 'proxy'}
    ],
    port_forwards=['8000:10080']
)
