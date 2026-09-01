# k8sHealth Roadmap

Kubernetes health plugin. Feature parity with monokit1 `k8sHealth/`.

## Scaffolding

- [X] Plugin skeleton from pluginTemplate (go.mod, justfile, Containerfile, test harness)
- [X] Example config `config/k8s.yml`
- [ ] Config struct + `k8s.yml` case wired into monokit_lib
- [ ] Containerfile: kind/k3s test fixture
- [ ] Podman integration tests
- [ ] In-cluster deployment manifests (namespace, RBAC, ConfigMap, PVC, CronJob, kustomization)

## Features

- [ ] Kubeconfig discovery and client creation
- [ ] Node health check (conditions, readiness, master detection)
- [ ] Pod health check (phase + per-container restarts/waiting reasons)
- [ ] RKE2 ingress-nginx health check (skipped on kubeadm)
- [ ] cert-manager health check (Certificate CR conditions + notAfter expiry; auto-detect namespace)
- [ ] kube-vip health check
  - [ ] Floating-IP discovery from pod args (or configured floating-ips / ingress-floating-ips)
  - [ ] Master-node count check
  - [ ] RKE2 server endpoint vs floating IP match
  - [ ] ICMP ping of floating IPs
- [ ] Cluster API certificate expiry check
- [ ] Kubeconfig client-certificate expiry check (warn-days, alarm + Redmine issue per entry)
- [ ] etcd cluster status (etcdctl discovery, TLS args for RKE2 and kubeadm, member list/leader)
- [ ] etcd backup/snapshot check (RKE2 snapshot discovery, etcdctl snapshot status verify, BoltDB header validation, max-age)
- [ ] Kubernetes end-of-life check (endoflife.date, warn-days)
- [ ] Namespace compliance checks (topology spread, replica count vs workers, image pull policy)
- [ ] Master taint compliance check
- [ ] RKE2 info + version news on change (master nodes only)
- [ ] Orphaned alarm cleanup for deleted pods/containers
- [ ] Alarm interval + recovery window (`alarm.interval` / `alarm.up_interval`) handling —
      needs the per-call interval override in lib
- [ ] `alarm.enabled` master switch that gates every alarm the plugin raises
- [ ] Cluster name resolution: config override, else derived from the monokit identifier
- [ ] Master-node detection via the API, used to gate the master-only checks
      (etcd backup, RKE2 info/version news)
- [ ] Health summary box output (depends on the lib renderer)
- [ ] Health data POST to the server API (depends on base client/server API)
- [ ] Continuous mode alongside one-shot mode with cron?
