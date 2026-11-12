## Trino on a single Parquet file

This setup uses Trino's Hive connector backed by:
- a file-based metastore (no external Hive Metastore Service required), and
- the native local filesystem driver (`fs.native-local.enabled=true`),

so the entire benchmark can be reproduced on a single VM with nothing
beyond Docker installed.

The ClickBench `hits.parquet` file stores `EventTime`, `ClientEventTime`
and `LocalEventTime` as Unix-epoch `BIGINT` values, and `EventDate` as a
`UINT16` count of days since 1970-01-01 (read directly as `DATE`).
`create.sql` registers the parquet file directly as the external table
`hits`, and `queries.sql` applies `from_unixtime(EventTime)` where
timestamp operations are needed.
