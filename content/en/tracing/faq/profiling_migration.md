---
title: Preparing Your Beta Continuous Profiling for GA
kind: faq
---

**You must migrate your current setup as the agentless mode will no longer be supported when Continuous Profiling is generally available.**

As we get closer to Continuous Profiling general availability, we have made changes so onboarding your services is even easier than before. Notably, will now send profiles through the Datadog Agent, removing the need for an API key or an upload endpoint. In summary we made the following changes:

- Deprecated having to specify an API key: `DD_PROFILING_API_KEY`, `DD_API_KEY`, `DD_PROFILING_API_KEY_FILE`.
- Deprecated having to specify the uploading endpoint: `DD_SITE`.
- Added support to send profiles directly through the agent.
- Added support for including container-id header during profile collection so you can automatically get container tags.

## Migrating from Agentless to the Agent Setup

{{< tabs >}}
{{% tab "Java" %}}

Perform following steps to migrate your services to send profiles directly through the agent:

1. Upgrade your agent to version [7.20.2][1]+ or [6.20.2][1]+

2. Upgrade the tracing library to [version 0.55][2]+

3. Delete `DD_PROFILING_API_KEY_FILE` or `DD_PROFILING_API_KEY` environment variable alongside the API key file as they were deprecated in version 0.55.

  **Note** If you used `-Ddd.profiling.api-key-file` flag, you no longer need to specify this during your service invocation due to deprecation in version 0.55.

4. Ensure `Ddd.profiling.enabled` flag or `DD_PROFILING_ENABLED` environment variable to `true`. Update to your service invocation should look like:

    ```diff
    java -javaagent:dd-java-agent.jar -Ddd.profiling.enabled=true -jar <YOUR_SERVICE>.jar <YOUR_SERVICE_FLAGS>
    ```

**NOTE** The following environment variables have been deprecated:

| Arguments                       | Environment variable        | Description                                      |
| ------------------------------- | --------------------------- | ------------------------------------------------ |
| `-Ddd.profiling.proxy.host`     | DD_PROFILING_PROXY_HOST     | Host for your proxy (`my-proxy.example.com`).    |
| `-Ddd.profiling.proxy.port`     | DD_PROFILING_PROXY_PORT     | Port used by your proxy. Default port is `8080`. |
| `-Ddd.profiling.proxy.username` | DD_PROFILING_PROXY_USERNAME | Username used by your proxy.                     |
| `-Ddd.profiling.proxy.password` | DD_PROFILING_PROXY_PASSWORD | Password used by your proxy.                     |


[1]: https://app.datadoghq.com/account/settings#agent/overview
[2]: https://app.datadoghq.com/apm/install
{{% /tab %}}

{{% tab "Python" %}}

| Arguments                       | Environment variable        | Description                                      |
| ------------------------------- | --------------------------- | ------------------------------------------------ |
| `-Ddd.profiling.proxy.host`     | DD_PROFILING_PROXY_HOST     | Host for your proxy (`my-proxy.example.com`).    |
| `-Ddd.profiling.proxy.port`     | DD_PROFILING_PROXY_PORT     | Port used by your proxy. Default port is `8080`. |
| `-Ddd.profiling.proxy.username` | DD_PROFILING_PROXY_USERNAME | Username used by your proxy.                     |
| `-Ddd.profiling.proxy.password` | DD_PROFILING_PROXY_PASSWORD | Password used by your proxy.                     |

{{% /tab %}}

{{% tab "Go" %}}

| Arguments                       | Environment variable        | Description                                      |
| ------------------------------- | --------------------------- | ------------------------------------------------ |
| `-Ddd.profiling.proxy.host`     | DD_PROFILING_PROXY_HOST     | Host for your proxy (`my-proxy.example.com`).    |
| `-Ddd.profiling.proxy.port`     | DD_PROFILING_PROXY_PORT     | Port used by your proxy. Default port is `8080`. |
| `-Ddd.profiling.proxy.username` | DD_PROFILING_PROXY_USERNAME | Username used by your proxy.                     |
| `-Ddd.profiling.proxy.password` | DD_PROFILING_PROXY_PASSWORD | Password used by your proxy.                     |

{{% /tab %}}
{{< /tabs >}}


### Troubleshooting

We could have a troubleshooting section too

[1]:
