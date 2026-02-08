---
title: "GitOps with Meshery"
description: "Integrating your CI/CD pipelines with Meshery's GitHub Actions"
weight: 15
aliases:
  - /guides/infrastructure-management/gitops-with-meshery
---

<h1>GitOps with Meshery</h1>

## ![Kanvas Icon](/images/kanvas-icon-color.svg) Kanvas Snapshot GitHub Action

- See your deployment before you merge
- Connect Kanvas to your GitHub repo and see changes pull request-to-pull request
- Get snapshots of your infrastructure directly in your PRs

### Using Meshery's SnapShot GitHub Action
See your deployment before you merge. Connect Kanvas to your GitHub repo and see changes pull request-to-pull request. Get snapshots of your infrastructure directly in your PRs.

See [Extension: Kanvas Snapshot](/extensions/snapshot) for more details.

## ![Performance Logo](/images/smp-dark-text-side.svg) Meshery Performance Analysis GitHub Action

- See your performance regressions before you merge
- Connect Performance Management to your GitHub repo and see changes pull request-to-pull request
- Red light performance regressions
- Baseline and analyze the performance of your services is key to efficient operation of any application
  - Meshery is the canonical implementation of the Cloud Native Performance specification
- Define your performance profiles upfront. See statistical analysis with microservice latency and throughput quartiles
- Meshery includes your choice of load generator, so that you can measure your way
- Meshery packages all these features into an easy-to-use GitHub Action

Measuring and managing the performance of your infrastructure is key to efficient operation. You can choose from multiple load generators and use a highly configurable set of load profiles with variable tunable facets to run a performance test. Meshery packages all these features into an easy-to-use GitHub Action.

### Using Meshery's Performance Analysis GitHub Action

The [Meshery Performance Analysis GitHub Action](https://github.com/marketplace/actions/performance-testing-with-meshery) is available in the GitHub Marketplace. You can create your own performance profiles to run repeatable tests with Meshery. You can configure this action to trigger with each of your releases, on every pull request or any GitHub workflow trigger event. A sample configuration of the action is shown below.

```yaml
name: Meshery SMP Action
on:
  push:
    branches:
      'master'

jobs:
  performance-test:
    name: Performance Test
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v2
        with:
          ref: 'perf'

      - name: Deploy k8s-minikube
        uses: manusa/actions-setup-minikube@v2.4.1
        with:
          minikube version: 'v1.21.0'
          kubernetes version: 'v1.20.7'
          driver: docker

      - name: Run Performance Test
        uses: layer5io/meshery-smp-action@master
        with:
          provider_token: ${{ secrets.PROVIDER_TOKEN }}
          platform: docker
          profile_name: soak-test
```

You can also define your test configuration in an SMP compatible configuration file as shown below.

```yaml
smp_version: v0.0.1
id:
name: Istio Performance Test
labels: {}
clients:
- internal: false
  load_generator: fortio
  protocol: 1
  connections: 2
  rps: 10
  headers: {}
  cookies: {}
  body: ""
  content_type: ""
  endpoint_urls:
  - http://localhost:2323/productpage
duration: "30m"
```

See this sample GitHub workflow ([action.yml](https://github.com/layer5io/meshery-smp-action/blob/master/action.yml)) for more configuration details.

![performance management dashboard](/images/service-mesh-performance-profile-test-results.png)

The results from the tests are updated on the Performance Management dashboard in Meshery. To learn more about interpreting the test results, check out [this guide](/guides/performance-management/interpreting-performance-test-results). You can always checkout the [Meshery User Guides](/guides) to dive deep into these features.

[Cloud Native Performance](https://smp-spec.io) standardizes infrastructure measurement, characterizing any deployment's performance by capturing the details of infrastructure capacity, configuration and workload metadata.