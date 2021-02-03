#Quick-Start
---
You find a lot of examples in the examples.py - Please have a look there!
##### Quick Test if everything is working

```
from uqo.client.config import Config
from uqo.examples.examples import *

config = Config(configpath="config.json")
connection = config.create_connection()

ping(config)
```
If you execute this and get a "pong" as a result - you have set up everything properly.

##### Solving a  QUBO / Ising Model with QBSolv
For QUBO:
```
from uqo.client.config import Config
from uqo.Problem import Problem

config = Config(configpath="config.json")
connection = config.create_connection()

example_qubo = {(0, 0): -2, (1, 1): -2, (2, 2): -2, (3, 3): 3}
answer = Problem.Qubo(config, example_qubo).with_platform("qbsolv").solve(100)
```
For ISING:
```
from uqo.client.config import Config
from uqo.Problem import Problem

config = Config(configpath="config.json")
connection = config.create_connection()

example_ising_h, example_ising_J = {1: 1, 2: 2, 3: 3}, {(1, 2): 4, (1, 3): 5, (2, 3): 6}
answer = Problem.Ising(config, example_ising_h, example_ising_J).with_platform("qbsolv").solve(100)
```

Of course you can also add solver parameters:
```
from uqo.client.config import Config
from uqo.Problem import Problem

config = Config(configpath="config.json")
connection = config.create_connection()

test_dict = {"test_parameter": {(0, 1): 5, (1, 2): 3}}
answer = Problem.Qubo(config, example_qubo).with_platform("qbsolv").with_params(**test_dict).solve(100)
```
For more examples please check the examples.py