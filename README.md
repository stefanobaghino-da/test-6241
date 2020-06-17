### Instructions

Open two terminals.

Terminal 1

```
daml build
```

Terminal 2

- Got to `daml` repo.

```
bazel build //ledger/sandbox:sandbox-binary_deploy.jar
bazel run //ledger/sandbox:sandbox-binary -- --ledgerid test-6241 --sql-backend-jdbcurl "jdbc:postgresql://localhost/sandbox?user=sandbox&password=sandbox" --metrics-reporter=graphite "$PRJ_DIR"/stefanobaghino-da/test-6241/.daml/dist/test-6241-0.0.1.dar
```

Terminal 1

```
for i in {1..100}; do
  echo ">>> Run $i/100"
  daml script --dar .daml/dist/test-6241-0.0.1.dar --script-name Test:oops --ledger-host localhost --ledger-port 6865 --wall-clock-time
done
```

Watch the metrics.

