# Flexflow MT5

To run the Flexflow MT5 experiment, first build the Docker container with `docker build -t flexflow_mt5 .` (running the command in this folder) and then run with `docker run -it --entrypoint bash --gpus all flexflow_mt5:latest`.

Next, follow the instructions from [this link](https://github.com/flexflow/FlexFlow/blob/master/examples/python/pytorch/mt5/MT5.md#mt5-in-flexflow).