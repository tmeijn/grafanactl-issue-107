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
   grafanactl --config grafanactl-config.yaml config check && grafanactl --config grafanactl-config.yaml resources serve ./dashboard/
   ```

5. Open your web browser and navigate to `http://localhost:8080` and confirm the test dashboard is displayed.
6. Click on the test dashboard. You should get a 404 error.
