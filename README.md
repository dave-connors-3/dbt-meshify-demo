# dbt-meshify-demo

This repo is intended to test out dbt-meshify in a jaffle shop sandbox environment! Set up your duckdb instance following the steps below (~10m) and try out the available commands. 

Full documentation for the dbt-meshify package is [here](https://dbt-labs.github.io/dbt-meshify/0.1/). 

Some example commands:

```
# create a group of all models tagged with "finance"
# leaf nodes and nodes with cross-group dependencies will be `public`
dbt-meshify operation create-group finance --owner name Monopoly Man --select +tag:finance

# add a contract to the marts models
dbt-meshify add-contract -s models/marts

# perform steps one and two in one go!
# contracts will be added to any public models from the grouping stage
dbt-meshify group finance --owner name Monopoly Man --select +tag:finance

# use the add-version operation to add a new version to a model
dbt-meshify operation add-version -s fct_orders
```
## Set up Project with Data

This project is optimized for running in a container. If you'd like to use it locally outside of container you'll need to follow the instructions below.

1. Create a python virtual environment and install the dependencies.

```console
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

2. Install meltano with [pipx](https://pypa.github.io/pipx/installation/). And install meltano's dependencies.

```console
pipx install meltano
meltano install
```

3. Run the EL pipeline.

```console
meltano run el
```

4. Install dbt dependencies and build the dbt project.

```console
dbt deps
dbt build
```

5. Install Evidence dependencies and run the Evidence server.

```console
cd reports
npm install
npm run dev
```

## Contributing

We welcome issues and PRs requesting or adding new features. The package that generates the synthetic data, [`jafgen`](https://pypi.org/project/jafgen/), is also under active development, and will add more types of source data to model as we go along. If you have tests, descriptions, new models, metrics, materializations types, or techniques you use this repo to demonstrate, which you feel would make for a more expansive baseline experience, we encourage you to consider contributing them back in so that this project becomes an even better collective tool for exploring and learning dbt over time.
