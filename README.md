# RTC Reward Action

Automatically award **RTC tokens** when a pull request is merged. Turn any GitHub repo into a bounty platform!

## Usage

```yaml
# .github/workflows/rtc-reward.yml
name: RTC Reward on PR Merge

on:
  pull_request:
    types: [closed]

jobs:
  reward:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
      - uses: alex-agent/rtc-reward-action@v1
        with:
          node-url: https://50.28.86.131
          amount: 5
          wallet-from: project-fund
          admin-key: ${{ secrets.RTC_ADMIN_KEY }}
```

## How Contributors Provide Their Wallet

### Option 1: PR Body
Include your RTC wallet in the PR description:
```
## Changes
Fixed bug in foo.py

## RTC Wallet
RTCa1b2c3d4e5f6789012345678901234567890abcd
```

### Option 2: `.rtc-wallet` File
Add a `.rtc-wallet` file to the repo root (one time setup):
```
RTCa1b2c3d4e5f6789012345678901234567890abcd
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `node-url` | Yes | `https://50.28.86.131` | RustChain node endpoint |
| `amount` | Yes | `5` | RTC amount per merged PR |
| `wallet-from` | Yes | - | Source wallet for transfers |
| `admin-key` | Yes | - | Admin signing key (use secrets!) |
| `dry-run` | No | `false` | Test mode - no real transfers |

## Dry Run Mode

Test your setup without spending RTC:
```yaml
with:
  dry-run: true
  amount: 5
```

## Setup Checklist

- [ ] Create a RustChain wallet for your project
- [ ] Store admin key in `Settings > Secrets > RTC_ADMIN_KEY`
- [ ] Add this action to `.github/workflows/rtc-reward.yml`
- [ ] Contributors add their RTC wallet to PRs

## About RTC

RTC is the native token of [RustChain](https://rustchain.org), a blockchain that rewards vintage hardware. 1 RTC ≈ $0.10 USD.

## License

MIT
