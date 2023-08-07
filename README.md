# gh-rate-limit

This is an extension for [GitHub CLI](https://cli.github.com/) that just shows you your existing rate limits and when it resets

It is exactly the same as doing
```
curl -fSsL -H "Authorization: token $(github_pat)" -X GET \
  https://api.github.com/rate_limit \
  | jq --raw-output '.resources | to_entries[] | {name: .key} + .value | "\(.name)  \(.remaining)/\(.limit)  \(.reset | strflocaltime("%H:%M:%S") )"' \
  | column -t
```

Marginally useful but not very interesting; it uses JQ because I haven't yet worked out how to get a go template to format a seconds in epoch.

## Installation

Prerequisites:
 * [GitHub CLI](https://cli.github.com/) is already installed and authenticated
 * [`jq`](https://stedolan.github.io/jq/) is installed

To install this extension:

```
gh extension install quotidian-ennui/gh-rate-limit
```

## Usage

```
bsh ❯ gh rate-limit
core                         4897/5000    14:46:20
search                       30/30        13:59:42
graphql                      4999/5000    14:46:43
integration_manifest         5000/5000    14:58:42
source_import                100/100      13:59:42
code_scanning_upload         1000/1000    14:58:42
actions_runner_registration  10000/10000  14:58:42
scim                         15000/15000  14:58:42
dependency_snapshots         100/100      13:59:42
code_search                  10/10        13:59:42

bsh ❯ gh rate-limit -u
core                         107/5000  14:46:20
search                       0/30      14:09:03
graphql                      1/5000    14:46:43
integration_manifest         0/5000    15:08:03
source_import                0/100     14:09:03
code_scanning_upload         0/1000    15:08:03
actions_runner_registration  0/10000   15:08:03
scim                         0/15000   15:08:03
dependency_snapshots         0/100     14:09:03
code_search                  0/10      14:09:03
```

## License

See [LICENSE](./LICENSE)
