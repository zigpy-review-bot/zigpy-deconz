# ZHA test build for zigpy/zigpy-deconz#281

Home Assistant's ZHA integration from **2026.11.0b0**, unchanged except for the manifest: it additionally installs zigpy-deconz from the PR branch `zigpy-bot/gp-endpoint-slots` (zigpy/zigpy-deconz#281), which fixes ZHA failing to start on ConBee II / RaspBee II with `No available endpoint slots exist` (zigpy/zigpy-deconz#280).

This is a temporary test build. Remove it again once you're done testing, and before updating Home Assistant.

## Install (Home Assistant OS, Terminal & SSH app)

```sh
git clone --depth 1 -b zigpy-bot/zha-test-pr281 https://github.com/zigpy-review-bot/zigpy-deconz.git /tmp/zha-test
mkdir -p /homeassistant/custom_components
cp -r /tmp/zha-test/custom_components/zha /homeassistant/custom_components/
```

Then restart Home Assistant (a full restart). The log warns that a custom integration `zha` is loaded, which is expected. Home Assistant installs the zigpy-deconz test build on every start, so GitHub has to be reachable.

## Remove

```sh
rm -r /homeassistant/custom_components/zha
```

Then restart Home Assistant.

## What's in it

- `custom_components/zha/`: `homeassistant/components/zha` from the 2026.11.0b0 tag, plus `translations/en.json` generated with `python -m script.translations develop --integration zha`.
- `manifest.json`: a `version` (required for custom integrations), a changed `name`, and one more requirement: `zigpy-deconz @ git+https://github.com/zigpy/zigpy-deconz.git@zigpy-bot/gp-endpoint-slots`.
