# Experimental Berlin Discourse Kubernetes Setup
This is the setup for the Experimental Berlin Kubernetes cluster.

The cluster consists of three main components, a Postgresql cluster administrated by a
[Postgres operator](https://github.com/zalando-incubator/postgres-operator) instance,
Redis instances and Discourse itself.

## How To
1. Deploy Postgres operator:
    1. `kubectl apply -f manifests/postgres-operator/operator-service-account-rbac.yaml`
    2. `kubectl apply -f manifests/postgres-operator/postgres-operator.yaml`
    3. `kubectl apply -f manifests/postgres-operator/postgres-operator-configuration.yaml`
    4. `kubectl apply -f manifests/postgres-operator/cluster.yaml`
2. Wait for Postgres database to be operational
3. Deploy Redis: `kubectl apply -f manifests/redis.yaml`
4. Deploy Discourse: `kubectl apply -f manifests/discourse.yaml`
5. Apply Discourse migrations (not sure why this step is necessary...):
    1. `./kubectl exec -ti web-server-0 /bin/bash`
    2. `cd /var/www/discourse`
    3. `bundle exec rake db:migrate`
6. Deploy ingress controller: `kubectl apply -f manifests/ingress-controller.yaml`