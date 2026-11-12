# sam-atelier-img-2

[sam-atelier](https://github.com/polos0117/sam-atelier) 의 **둘째** 그림 저장소다(2026-11-12 부터 열림). 앞 저장소는 [sam-atelier-img](https://github.com/polos0117/sam-atelier-img)(0 번)에 있다.
Pages 로 `https://polos0117.github.io/sam-atelier-img-2/img/<파일>` 에서 읽는다. 게임의 초상(`sam-atelier/images/`)과는 따로다.

## 왜 하나 더 두나

GitHub Pages 사이트 한 개는 1 GB 까지다. 첫 저장소 `sam-atelier-img` 가 GitHub 크기로 약 1.0 GB 가 되어(2026-11-12) **새 그림은 여기에 올린다.**
앞 저장소의 그림은 지우지도 옮기지도 않는다 — 옛 주소가 그대로 산다.

어느 그림이 어느 저장소에 있는지는 등록기가 `sam-atelier` 의 `data/img.json` 에 `"where": {"<파일>": 1}` 로 적고(0 번은 적지 않는다),
화면(`lib/img.js` 의 `BASES`)이 그 번호로 주소를 고른다.

## 규칙

- **새 그림은 여기에만 올린다.** 첫 저장소는 닫혔다 — 그쪽에 새 이름이 올라오면 등록이 전부 멈춘다.
  이미 있는 이름을 고쳐 그리는 교체만 그 파일이 있는 저장소에 덮어쓴다(`data/img.json` 의 `where`, 없으면 0 번).
- 같은 이름을 두 저장소에 두지 않는다(등록이 멈춘다).
- 새 그림의 기록(`records/<장수>/`)도 여기에 둔다. 한 장수의 기록이 두 저장소에 나뉘어도 도구(계획기 · `casual-check`)가 둘 다 읽는다.
- **자동화 상태는 첫 저장소에 그대로** — 잠금(`records/automation/claims/`) · GPT 세션 설계 주문(`free/<장수>/`) · 교체 장부(`records/replacement.json`) · 배경(`backgrounds/`). 여러 세션이 한 곳을 보게.
- **생성 원본 PNG 는 올리지 않는다** — webp(품질 90, method 6, 1024×1536)로, 기록엔 원본 sha256 만.
- 파일 이름 규칙 · 자리는 앞 저장소와 같다 — [IMAGE_RULES.md](https://github.com/polos0117/sam-atelier/blob/main/IMAGE_RULES.md).

```
img/<장수>_<세계>_<화풍>_f.webp           세계 그림. 1024×1536 (2:3). 세계는 samguk · fantasy · mecha
img/<장수>_<세계>_<화풍>_f_casualN.webp   일상컷 N — 그 세계 그림을 참고 그림으로
img/thumb/<같은 이름>                      목록용(긴 변 512). 워크플로가 만든다
records/<장수>/<세계>.<화풍>-ui.json       생성 기록(+ 올릴 때 generation)
records/<장수>/<세계>-casualN.<화풍>-ui.json
```

## 올린 뒤에 할 일

없다. `img/` 에 webp 를 올리면 `썸네일` 워크플로가 `img/thumb/` 를 만들어 되커밋하고, 코드 저장소의 `그림 등록` 을 깨운다 — 이 저장소의 Actions 비밀 `CODE_REPO_TOKEN`(Fine-grained token, 저장소 sam-atelier 하나, Contents: Read and write)이 있을 때. 없으면 코드 저장소가 한 시간마다 스스로 돈다.

## 처음 한 번

1. 공개(Public) 저장소로 만든다 — Pages 무료 요금제는 공개 저장소만 낸다.
2. Settings → Pages → Source: Deploy from a branch, `main` / `(root)`.
3. Settings → Secrets and variables → Actions → `CODE_REPO_TOKEN`.

`.nojekyll` 은 Pages 가 파일을 있는 그대로 내보내게 한다. 워크플로의 「크기」 단계가 900 MB 를 넘으면 경고를 띄운다 — 그때 `sam-atelier-img-3` 을 같은 방법으로 준비한다.
