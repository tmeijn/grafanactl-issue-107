# Grafanactl issue 107 reproduction

This repository is used to reproduce the issue described in [Grafanactl issue 107](https://github.com/grafana/grafana/issues/107).

## Steps to reproduce

1. Clone this repository.
2. Run the following command to start the Grafana server:

   ```bash
   docker compose up -d
   ```

3. Open your web browser and navigate to `http://localhost:3001` and ensure the Grafana UI is displayed.
4. Open a terminal and run the following command to serve the dashboard:

   ```bash
   grafanactl --config grafanactl-config.yaml config check && grafanactl -v --config grafanactl-config.yaml resources serve ./dashboard/
   ```

5. Open your web browser and navigate to `http://localhost:8080` and confirm the test dashboard is displayed.
6. Click on the test dashboard. You should get a 404 error.

## Testing grafanctl build from PR 115

Ref: https://github.com/grafana/grafana/pull/115

1. Build the `grafanactl` binary from the PR branch:

    ```bash
       git clone https://github.com/borissmidt/grafanactl.git
       cd grafanactl
       git checkout fix-the-dashboard-serving
       go install ./cmd/grafanactl
    ```

2. Verify the version of `grafanactl`:

    ```bash
    grafanactl --version # Should be "grafanactl version SNAPSHOT built from  on"
    ```

    NOTE: If using `mise` ensure you comment out `grafanactl` in `mise.toml` so that it isn't active anymore.

3. Open a terminal and run the following command to serve the dashboard:

   ```bash
   grafanactl --config grafanactl-config.yaml config check && grafanactl -v --config grafanactl-config.yaml resources serve ./dashboard/
   ```
