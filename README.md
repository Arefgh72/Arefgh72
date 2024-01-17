import requests
import json

def get_config():
    url = "https://api.github.com/repos/NimaParsayi/cloudflare-vless/contents/config.json"
    headers = {
        "Accept": "application/vnd.github.v3+json"
    }
    response = requests.get(url, headers=headers)
    response.raise_for_status()
    content = json.loads(response.content)
    return content["content"]

config = get_config()
config = base64.b64decode(config).decode("utf-8")

with open("config.json", "w") as f:
    f.write(config)
