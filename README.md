## 说明

> 此项目用于启用第三方CC的aws缓存渠道

### 配置参数

在 `opencode.json` 的 provider `options` 中配置以下参数：

| 参数 | 类型 | 说明 |
|------|------|------|
| `enableMeta` | `boolean` | 启用后会在请求 header 中注入 `x-opencode-session`，并在请求 body 的 `metadata` 字段中注入 `user_id`、`project_id`、`session_id` |
| `enableFast` | `boolean` | 启用后会在请求 body 中设置 `service_tier: "priority"`，用于开启优先级加速（适用于 OpenAI 和 Claude） |
| `setCacheKey` | `boolean` | 启用缓存 key |
| `baseURL` | `string` | 自定义 API 地址 |
| `apiKey` | `string` | API 密钥 |

### 配置示例

```json
{
  "anthropic": {
    "name": "fox.anthropic.claude",
    "npm": "@ai-sdk/anthropic",
    "options": {
      "baseURL": "https://code.newcli.com/claude/aws/v1",
      "apiKey": "sk-ant-oat01-x-x-x",
      "setCacheKey": true,
      "enableMeta": true,
      "enableFast": true
    },
    "models": {
      "claude-sonnet-4-5": {
        "id": "claude-sonnet-4-5",
        "name": "Claude Sonnet 4.5 (Antigravity)",
        "limit": {
          "context": 200000,
          "output": 64000
        },
        "modalities": {
          "input": [
            "text",
            "image",
            "pdf"
          ],
          "output": [
            "text"
          ]
        }
      },
      "claude-sonnet-4-5-thinking": {
        "name": "Claude Sonnet 4.5 Thinking (Antigravity)",
        "limit": {
          "context": 200000,
          "output": 64000
        },
        "modalities": {
          "input": [
            "text",
            "image",
            "pdf"
          ],
          "output": [
            "text"
          ]
        },
        "variants": {
          "low": {
            "thinkingConfig": {
              "thinkingBudget": 8192
            }
          },
          "max": {
            "thinkingConfig": {
              "thinkingBudget": 32768
            }
          }
        }
      },
      "claude-opus-4-5": {
        "name": "Claude Opus 4.5 (Antigravity)",
        "limit": {
          "context": 200000,
          "output": 64000
        },
        "modalities": {
          "input": [
            "text",
            "image",
            "pdf"
          ],
          "output": [
            "text"
          ]
        },
        "variants": {
          "low": {
            "thinkingConfig": {
              "thinkingBudget": 8192
            }
          },
          "max": {
            "thinkingConfig": {
              "thinkingBudget": 32768
            }
          }
        }
      },
      "claude-opus-4-6": {
        "id": "claude-opus-4-6",
        "name": "Claude Opus 4.6 (Antigravity)",
        "limit": {
          "context": 200000,
          "output": 128000
        },
        "modalities": {
          "input": [
            "text",
            "image",
            "pdf"
          ],
          "output": [
            "text"
          ]
        }
      },
      "claude-opus-4-5-thinking": {
        "name": "Claude Opus 4.5 Thinking (Antigravity)",
        "limit": {
          "context": 200000,
          "output": 64000
        },
        "modalities": {
          "input": [
            "text",
            "image",
            "pdf"
          ],
          "output": [
            "text"
          ]
        },
        "variants": {
          "low": {
            "thinkingConfig": {
              "thinkingBudget": 8192
            }
          },
          "max": {
            "thinkingConfig": {
              "thinkingBudget": 32768
            }
          }
        }
      }
    }
  }
}
```
