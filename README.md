# gh-approve-deploy

This is an extension for [GitHub CLI](https://cli.github.com/) that just shows you your existing rate limits and when
it resets

It is exactly the same as doing
```
curl -fSsL -H "Authorization: token $(github_pat)" -X GET \
  https://api.github.com/rate_limit \
  | jq '.rate | { "limit": .limit, "remaining" : .remaining  , "resets" : .reset | strflocaltime("%H:%M:%S") }'
```

Marginally useful but not very interesting.

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
{
  "limit": 5000,
  "remaining": 4964,
  "resets": "09:28:51"
}
```

## License

See [LICENSE](./LICENSE)
