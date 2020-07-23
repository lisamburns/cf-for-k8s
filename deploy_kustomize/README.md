hack to deploy cf-for-k8s with kustomize/kubectl instead of kapp
1. generate rendered yaml with ytt as normal (cf-for-k8s-rendered.yml)
1. Move cf-for-k8s-rendered.yml to deploy_kustomize/cf-for-k8s-rendered.yml
1. kubectl apply -k .
1. It works!
1. How does ordering work without kapp annotations?
  1. Ordering works with kustomize because it applies namespaces first, then CRDs, then validating/mutating webhook configurations, then serviceaccounts.
  It applies the deployments last.
  1. Webhooks are still able to inject sidecars into every pod because k8s waits for the webhook server to come up before it creates pods for each deployment
