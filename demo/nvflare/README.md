# Experimental Support of Federated XGBoost using NVFlare

This directory contains a demo of Federated Learning using
[NVFlare](https://nvidia.github.io/NVFlare/).

To run the demo, first build XGBoost with the federated learning plugin enabled (see the
[README](../../plugin/federated/README.md)).

Install NVFlare (note that currently NVFlare only supports Python 3.8):
```shell
pip install nvflare
```

Prepare the data:
```shell
./prepare_data.sh
```

Start the NVFlare federated server:
```shell
./poc/server/startup/start.sh
```

In another terminal, start the first worker:
```shell
./poc/site-1/startup/start.sh
```

And the second worker:
```shell
./poc/site-2/startup/start.sh
```

Then start the admin CLI, using `admin/admin` as username/password:
```shell
./poc/admin/startup/fl_admin.sh
```

In the admin CLI, run the following commands:
```shell
upload_app hello-xgboost
set_run_number 1
deploy_app hello-xgboost all
start_app all
```

Once the training finishes, the model file should be written into
`./poc/site-1/run_1/test.model.json` and `./poc/site-2/run_1/test.model.json`
respectively.

Finally, shutdown everything from the admin CLI:
```shell
shutdown client
shutdown server
```
