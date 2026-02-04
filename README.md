FOR THE WINDOWS :
https://www.npmjs.com/package/opencode-windows-fixed-cache

```
npm i opencode-windows-fixed-cache
```


`opencode.json` : enable `provider.options.enableMeta`


```
    "provider": {
        "anthropic": {
            "name": "fox.anthropic.claude",
            "npm": "@ai-sdk/anthropic",
            "options": {
                "baseURL": "https://code.newcli.com/claude/aws/v1",
                "apiKey": "sk-ant-oat01-x-xxx-xx",
                "setCacheKey": true,
                "enableMeta":true
            },
```
