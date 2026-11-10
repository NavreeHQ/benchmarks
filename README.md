# Navree benchmarks

The benchmark app of [Navree](https://github.com/NavreeHQ/navree), the harness that measures it, the specification it follows and Navree's own results. [navree.com/performance](https://navree.com/performance/) shows these numbers; everything needed to reproduce them is here.

| Path | What it is |
|---|---|
| `SPEC.md` | The contract: the machine, the database, the five endpoints and the rules of the measurement |
| `frameworks/navree/` | The benchmark API as an ordinary Navree application, built from the published `navree` crate |
| `db/init.sql` | The seeded database every run starts from |
| `wrk/` | The load generator's image and its request scripts |
| `tools/` | `conformance.mjs`, which checks an app against the spec, and the fixtures it shares with the harness |
| `run.mjs` | The harness: builds the app, checks conformance, measures and writes the results |
| `results/` | Navree's results: `navree.json`, a repeat run in `extra/`, the machine in `env.json` and the run's log |

## Run it

You need Docker, Node.js 24 and a machine with at least 24 CPUs for the default CPU split (`--app-cpus`, `--pg-cpus` and `--load-cpus` change it).

```sh
node run.mjs --smoke --only navree     # build, conformance, 5 seconds per test: a quick check
node run.mjs --only navree             # the real measurement: 3 runs of 15 seconds per test
```

The harness starts PostgreSQL, the app and the load generator in containers on one Docker network, one app at a time, recreates the database before each run, and writes `results/navree.json`. See `SPEC.md` for every number that matters and `frameworks/navree/README.md` for how the app is built.

## License

Free and open source under either of the [MIT license](LICENSE-MIT) or the [Apache License 2.0](LICENSE-APACHE), at your option.
