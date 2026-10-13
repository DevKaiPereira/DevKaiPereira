<div align="center">
  <a href="https://github.com/DevKaiPereira">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="dark_mode.svg">
      <source media="(prefers-color-scheme: light)" srcset="light_mode.svg">
      <img alt="Perfil de Kaique Pereira" src="dark_mode.svg">
    </picture>
  </a>
</div>

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/dev-kaique/)
[![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/kaique_dev_/)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:kaiquesouzapereira63@gmail.com)

</div>
#!/usr/bin/env python3
"""Gera dark_mode.svg e light_mode.svg (perfil estilo neofetch).

Uso:
    python build_svg.py                # arte ASCII de exemplo
    python build_svg.py minha_foto.jpg # converte a sua foto em ASCII
    (para a foto: pip install pillow)
"""
import sys, os, json, math, urllib.request
from html import escape

USER = "DevKaiPereira"

# ------------------------- EDITE AQUI -------------------------
# ("kv", chave, valor) | ("title", texto) | ("blank",)
INFO = [
    ("title", "kaique@devkaipereira"),
    ("kv", "OS", "Windows 11, Linux"),
    ("kv", "Uptime", "2+ anos de experiência"),
    ("kv", "Host", "Brasil"),
    ("kv", "Kernel", "Full-Stack Developer"),
    ("kv", "IDE", "VSCode"),
    ("blank",),
    ("kv", "Languages.Programming", "TypeScript, JavaScript, Java"),
    ("kv", "Languages.Computer", "HTML, CSS, JSON, SQL"),
    ("kv", "Languages.Real", "Português, English"),
    ("blank",),
    ("kv", "Stack.Frontend", "React, HTML, CSS"),
    ("kv", "Stack.Backend", "Node.js, Express, Spring"),
    ("kv", "Stack.Database", "MySQL, MongoDB"),
    ("kv", "Tools", "Git, Docker, Maven"),
    ("blank",),
    ("title", "Contato"),
    ("kv", "Email.Personal", "kaiquesouzapereira63@gmail.com"),
    ("kv", "LinkedIn", "dev-kaique"),
    ("kv", "Instagram", "kaique_dev_"),
    ("blank",),
    ("title", "GitHub Stats"),
    ("stats",),
]
ASCII_COLS, ASCII_ROWS = 46, 32
# --------------------------------------------------------------

W, H = 985, 530
INFO_X, LINE_W, LH = 400, 56, 20  # LINE_W = largura em caracteres

THEMES = {
    "dark_mode":  dict(bg="#0d1117", fg="#c9d1d9", key="#ffa657", val="#a5d6ff", dots="#616e7c", ascii="#c9d1d9", add="#3fb950", dele="#f85149"),
    "light_mode": dict(bg="#f6f8fa", fg="#24292f", key="#953800", val="#0a3069", dots="#c2cfde", ascii="#24292f", add="#1a7f37", dele="#cf222e"),
}

def gh(path):
    req = urllib.request.Request(f"https://api.github.com{path}")
    req.add_header("Accept", "application/vnd.github+json")
    if os.environ.get("GITHUB_TOKEN"):
        req.add_header("Authorization", f"Bearer {os.environ['GITHUB_TOKEN']}")
    with urllib.request.urlopen(req, timeout=15) as r:
        return json.load(r)

def get_stats():
    s = dict(repos="—", stars="—", followers="—", commits="—")
    try:
        u = gh(f"/users/{USER}")
        s["repos"], s["followers"] = u["public_repos"], u["followers"]
        s["stars"] = sum(r["stargazers_count"] for r in gh(f"/users/{USER}/repos?per_page=100"))
        s["commits"] = f'{gh(f"/search/commits?q=author:{USER}")["total_count"]:,}'
    except Exception as e:
        print("Aviso: não consegui buscar stats ->", e)
    return s

def make_ascii(path, invert):
    ramp = " .:-=+*#%@"
    if invert:
        ramp = ramp[::-1]
    grid = []
    if path:
        from PIL import Image, ImageOps
        img = ImageOps.autocontrast(Image.open(path).convert("L").resize((ASCII_COLS, ASCII_ROWS)))
        px = img.load()
        for y in range(ASCII_ROWS):
            grid.append("".join(ramp[int(px[x, y] / 256 * len(ramp))] for x in range(ASCII_COLS)))
    else:  # arte de exemplo: esfera sombreada
        for y in range(ASCII_ROWS):
            row = ""
            for x in range(ASCII_COLS):
                dx, dy = (x - ASCII_COLS / 2) / (ASCII_COLS / 2), (y - ASCII_ROWS / 2) / (ASCII_ROWS / 2)
                d = math.hypot(dx, dy)
                if d > 1:
                    row += " "
                else:
                    z = math.sqrt(1 - d * d)
                    light = max(0, min(1, z * 0.6 + (-dx - dy) * 0.3 + 0.2))
                    row += ramp[int(light * (len(ramp) - 1))]
            grid.append(row)
    return grid

def build(name, t, photo, stats):
    out = [f'<svg xmlns="http://www.w3.org/2000/svg" width="{W}" height="{H}" viewBox="0 0 {W} {H}">',
           f'<style>text{{font-family:Consolas,"DejaVu Sans Mono","Courier New",monospace;white-space:pre}}'
           f'.a{{font-size:12px;fill:{t["ascii"]}}}.i{{font-size:16px;fill:{t["fg"]}}}'
           f'.k{{fill:{t["key"]}}}.v{{fill:{t["val"]}}}.d{{fill:{t["dots"]}}}.p{{fill:{t["add"]}}}.m{{fill:{t["dele"]}}}</style>',
           f'<rect width="100%" height="100%" rx="15" fill="{t["bg"]}"/>',
           '<text class="a" xml:space="preserve">']
    for i, line in enumerate(make_ascii(photo, name == "light_mode")):
        out.append(f'<tspan x="20" y="{28 + i * 15}">{escape(line)}</tspan>')
    out.append('</text><text class="i" xml:space="preserve">')

    y = 30
    def kv(k, v, vclass="v"):
        dots = "." * max(2, LINE_W - len(k) - len(v) - 2)
        return (f'<tspan x="{INFO_X}" y="{y}"><tspan class="k">{escape(k)}:</tspan> '
                f'<tspan class="d">{dots}</tspan> <tspan class="{vclass}">{escape(v)}</tspan></tspan>')

    for item in INFO:
        if item[0] == "title":
            out.append(f'<tspan x="{INFO_X}" y="{y}">{escape(item[1])} <tspan class="d">{"-" * max(2, LINE_W - len(item[1]) - 1)}</tspan></tspan>')
        elif item[0] == "kv":
            out.append(kv(item[1], item[2]))
        elif item[0] == "stats":
            out.append(kv("Repos", f'{stats["repos"]}')); y += LH
            out.append(kv("Stars", f'{stats["stars"]}')); y += LH
            out.append(kv("Followers", f'{stats["followers"]}')); y += LH
            out.append(kv("Commits", f'{stats["commits"]}')); y -= 0
        y += LH
    out.append('</text></svg>')
    open(f"{name}.svg", "w", encoding="utf-8").write("\n".join(out))
    print("gerado", f"{name}.svg")

if __name__ == "__main__":
    photo = sys.argv[1] if len(sys.argv) > 1 else None
    stats = get_stats()
    for n, t in THEMES.items():
        build(n, t, photo, stats)
