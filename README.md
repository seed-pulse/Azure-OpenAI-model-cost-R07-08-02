# Azure-OpenAI-model-cost-R07-08-02


Azureスクリーンショット群より\*\*全API（gpt-4.1, gpt-4o, dall-e-3, text-embedding-3-large, sora）\*\*の
\*\*「エンドポイント」「デプロイ名」「モデル名」「リージョン」「レート制限」「廃止日」\*\*をテキスト抽出＆整理し、

* **config.py用の変数テンプレート**
* **マークダウン形式の一覧（GitHub用）**

として**両方出力**します！

---

# 1. config.py用テンプレート

```python
# Azure OpenAI API 設定まとめ

AZURE_OPENAI_CONFIG = {
    "gpt_4_1": {
        "endpoint": "https://chris-mdohqmzee-eastus2.cognitiveservices.azure.com/",
        "deployment": "gpt-4.1",
        "model": "gpt-4.1",
        "region": "East US 2",
        "rate_limit_tpm": 50000,
        "expires": "2026-04-11 9:00 AM",
    },
    "gpt_4o": {
        "endpoint": "https://chris-mdohqmzee-eastus2.cognitiveservices.azure.com/",
        "deployment": "gpt-4o",
        "model": "gpt-4o",
        "region": "East US 2",
        "rate_limit_tpm": 60000,
        "expires": "2026-03-01 9:00 AM",
    },
    "dall_e_3": {
        "endpoint": "https://chris-mdoqhju-swedencentral.cognitiveservices.azure.com/",
        "deployment": "dall-e-3",
        "model": "dall-e-3",
        "region": "Sweden Central",
        "rate_limit_tpm": None,
        "expires": "2025-09-30",
    },
    "text_embedding_3_large": {
        "endpoint": "https://chris-mdoqhju-swedencentral.cognitiveservices.azure.com/",
        "deployment": "text-embedding-3-large",
        "model": "text-embedding-3-large",
        "region": "Sweden Central",
        "rate_limit_tpm": 150000,
        "expires": "2026-04-30 9:00 AM",
    },
    "sora": {
        "endpoint": "https://chris-mdohqmzee-eastus2.cognitiveservices.azure.com/",
        "deployment": "sora",
        "model": "sora",
        "region": "East US 2",
        "rate_limit_tpm": 60000,
        "expires": "2025-09-15 9:00 AM",
    },
}
```

---

# 2. マークダウン形式（GitHub貼付用）

```markdown
# Azure OpenAI API 各モデル設定まとめ

| モデル名                   | エンドポイント                                                      | デプロイ名              | リージョン         | レート制限（TPM） | 廃止日                    |
|----------------------------|---------------------------------------------------------------------|------------------------|--------------------|------------------|---------------------------|
| **gpt-4.1**                | https://chris-mdohqmzee-eastus2.cognitiveservices.azure.com/        | gpt-4.1                | East US 2          | 50,000           | 2026-04-11 9:00 AM        |
| **gpt-4o**                 | https://chris-mdohqmzee-eastus2.cognitiveservices.azure.com/        | gpt-4o                 | East US 2          | 60,000           | 2026-03-01 9:00 AM        |
| **dall-e-3**               | https://chris-mdoqhju-swedencentral.cognitiveservices.azure.com/    | dall-e-3               | Sweden Central     | 不明              | 2025-09-30                |
| **text-embedding-3-large** | https://chris-mdoqhju-swedencentral.cognitiveservices.azure.com/    | text-embedding-3-large | Sweden Central     | 150,000          | 2026-04-30 9:00 AM        |
| **sora**                   | https://chris-mdohqmzee-eastus2.cognitiveservices.azure.com/        | sora                   | East US 2          | 60,000           | 2025-09-15 9:00 AM        |

---

## 🔖 参考：API呼び出し時のパラメータ

- **endpoint** … エンドポイントURL
- **deployment** … デプロイ名（API呼び分け時の指定名）
- **model** … モデル名（APIリクエストに必要な場合もあり）
- **region** … Azureリージョン
- **rate_limit_tpm** … 1分あたりの最大トークン/リクエスト数（TPM＝Tokens Per Minute）
- **expires** … モデル廃止予定日

> DALL-E-3のレート制限値は画像では明記されていませんでした（管理画面上で非公開のケースも多いため、API制限エラー時は個別調査推奨）

---

## 📝 注意点
- **APIキーは各エンドポイントの「Key Authentication」で管理**
- **リージョン違いに注意！（同じモデル名でもリージョンごとにエンドポイント/制限値が異なる場合あり）**
- **必ず最新のAzure Portalで“廃止日・制限値”を再確認のこと**

---

```

---

**どちらの形式も、そのままコピペ・運用・GitHub貼付が可能です。**
さらに細かい仕様や、各モデルごとのサンプル呼び出しコードも即展開できますので、
ご要望あればご指示ください！

--------------


**Azure OpenAI API各モデルの利用料金（Price）は、モデル・リージョン・従量単価によって細かく異なります。**
ただし**公式ポータルやドキュメントで“常に変動・頻繁に更新”されるため、ここでは2025年8月時点の「おおよその目安」と、確認方法・参考リンクをセットでお伝えします。**

---

## 【Azure OpenAI 料金体系の基本ポイント】

* **課金単位：**

  * gpt-4.1/gpt-4o：**1000トークンごと**
  * DALL·E-3, Sora：**画像/動画1回ごと**
  * Embedding：**1000トークンごと**
* **リージョンごとに金額が異なる**（例：East US 2とSweden Centralで異なる）
* **APIバージョン・プレビュー/GAによっても変化あり**
* **料金はUSD（米ドル）建てが基本、クレジット消化もUSD換算**

---

## 【2025年8月時点の主要モデル「おおよその目安」】

| モデル名                       | East US 2 / Sweden Central等 | 主な料金単価（目安）                                             | 備考                       |
| -------------------------- | --------------------------- | ------------------------------------------------------ | ------------------------ |
| **gpt-4.1**                | East US 2                   | \$5.00 / 1M input tokens<br>\$15.00 / 1M output tokens | 標準英語ベース。日本語も同等で換算可       |
| **gpt-4o**                 | East US 2                   | \$5.00 / 1M input tokens<br>\$15.00 / 1M output tokens | gpt-4.1と同等（OpenAI公式より安価） |
| **dall-e-3**               | Sweden Central              | \$0.04 ～ \$0.08 / 画像1枚                                 | 解像度・用途で変動あり              |
| **text-embedding-3-large** | Sweden Central              | \$0.13 / 1,000 tokens                                  | 最新embedding              |
| **sora**                   | East US 2                   | 未公開/変動（テスト段階・都度公式参照）                                   | 動画生成は数ドル/分級の可能性あり        |

---

## 【公式価格表へのアクセス方法】

* **Azure OpenAI Service 価格公式（随時更新・一番確実）**

  * [Azure OpenAI Service 価格表（日本語公式）](https://azure.microsoft.com/ja-jp/pricing/details/cognitive-services/openai-service/)
  * [OpenAI Pricing（英語・詳細）](https://openai.com/pricing)

* **API管理画面やAzure Portalでも「課金額・請求履歴」から月次推移が確認可能**

---

### 【注意点・ポイント】

* **実際の請求額は「無料クレジット」や「プロモ枠」を差し引いて反映されます**
* **日本語（マルチバイト文字）も「1トークン＝約4文字」計算なので、OpenAIのトークン換算方法と同様**
* **画像生成・動画生成系（DALL-E-3, Sora）は用途やオプションで課金単価が変動**
* **利用上限や無料枠を超えると自動で課金切替（管理画面で確認・通知も可能）**

---

## 📝 **GitHub用：料金表Markdownサンプル**

```markdown
## Azure OpenAI 各モデル料金目安（2025年8月時点）

| モデル                   | リージョン     | 主な料金単価（目安）               | 備考                       |
|--------------------------|----------------|------------------------------------|----------------------------|
| **gpt-4.1**              | East US 2      | $5.00 / 1M input tokens<br>$15.00 / 1M output tokens | 日本語も同等（4文字＝1トークン換算） |
| **gpt-4o**               | East US 2      | $5.00 / 1M input tokens<br>$15.00 / 1M output tokens | gpt-4.1と同等              |
| **dall-e-3**             | Sweden Central | $0.04 ～ $0.08 / 画像1枚           | 画像サイズ/品質で変動      |
| **text-embedding-3-large**| Sweden Central| $0.13 / 1,000 tokens               |                           |
| **sora**                 | East US 2      | 未公開（要公式確認・高額の可能性） | 動画生成/解像度/長さで変動  |

> 最新料金・利用明細は [Azure OpenAI公式価格表](https://azure.microsoft.com/ja-jp/pricing/details/cognitive-services/openai-service/) を必ず参照してください。

---

**注意：上記は目安です。実利用前に必ず最新情報を公式でご確認ください。**
```


---------------


**各APIの「月間最大利用額」や「単発リクエストごとの見積もり計算式」、
GitHub用Markdownテンプレ**として整理して出します。

---

# 1. 月間最大利用額の目安（レート上限でフル利用した場合）

例：**gpt-4.1**

* 最大レート：**50,000トークン/分**
* 1日あたり：50,000トークン × 60分 × 24h = **72,000,000トークン/日**
* 1ヶ月（30日）あたり：72,000,000 × 30 = **2,160,000,000トークン/月**

---

## 【gpt-4.1, gpt-4o の場合】

* **入力課金：\$5.00 / 1,000,000トークン**
* **出力課金：\$15.00 / 1,000,000トークン**

| モデル     | 月間最大トークン        | 入力料金     | 出力料金     | 月額合計（理論最大） |
| ------- | --------------- | -------- | -------- | ---------- |
| gpt-4.1 | 2,160,000,000   | \$10,800 | \$32,400 | \$43,200   |
| gpt-4o  | 2,592,000,000\* | \$12,960 | \$38,880 | \$51,840   |

※gpt-4oは60,000tpmの場合で計算（4.1より20%高い）

---

## 【text-embedding-3-large】

* **150,000トークン/分** × 60 × 24 × 30 = **6,480,000,000トークン/月**
* \$0.13 / 1,000トークン

→ 6,480,000,000 ÷ 1,000 × \$0.13 = **\$842,400/月**

---

## 【dall-e-3（画像生成）】

* **1枚あたり \$0.04〜\$0.08**
* 仮に1日1,000枚 × 30日 = **30,000枚/月**
* \$0.04 × 30,000 = **\$1,200/月**（最安の場合）

---

## 【sora（動画生成）】

* 料金未公開（参考：OpenAI公式で動画1分＝\$1〜\$10程度の想定あり）
* 1日30本 × 30日 = 900本（用途による）
* \$5/本 × 900 = **\$4,500/月**（仮定値、公式参照必須）

---

# 2. APIコスト計算式

### gpt-4.1/gpt-4o

* **入力コスト**（USD） = 入力トークン数 / 1,000,000 × \$5.00
* **出力コスト**（USD） = 出力トークン数 / 1,000,000 × \$15.00

### text-embedding-3-large

* **コスト（USD）** = トークン数 / 1,000 × \$0.13

### dall-e-3

* **コスト（USD）** = 画像生成枚数 × \$0.04 〜 \$0.08

### sora

* **コスト（USD）** = 動画生成本数 × \$1 〜 \$10（長さ/画質による）

---

# 3. マークダウン表・サンプル（GitHub貼付用）

```markdown
## Azure OpenAI API 料金・利用量見積もり（2025年8月時点）

### 1. 月間最大理論コスト（レート上限フル活用時の目安）

| モデル                   | 月間最大トークン/回数 | 入力料金      | 出力/画像/動画料金 | 月額合計    |
|--------------------------|----------------------|---------------|-------------------|------------|
| **gpt-4.1**              | 2,160,000,000        | $10,800       | $32,400           | $43,200    |
| **gpt-4o**               | 2,592,000,000        | $12,960       | $38,880           | $51,840    |
| **text-embedding-3-large**| 6,480,000,000       | $842,400      | –                 | $842,400   |
| **dall-e-3**             | 30,000枚             | –             | $1,200            | $1,200     |
| **sora**                 | 900本                | –             | $4,500（仮定値）   | $4,500     |

> ※あくまで理論最大。実際は用途やAPI制限、無料枠で大幅に安くなる場合が多いです。

---

### 2. APIコスト計算式（サンプル）

- **gpt-4.1/gpt-4o**  
  - 入力コスト: `入力トークン数 / 1,000,000 × $5.00`
  - 出力コスト: `出力トークン数 / 1,000,000 × $15.00`

- **text-embedding-3-large**  
  - コスト: `トークン数 / 1,000 × $0.13`

- **dall-e-3**  
  - コスト: `画像生成枚数 × $0.04 〜 $0.08`

- **sora**  
  - コスト: `動画生成本数 × $1 〜 $10（公式都度確認）`

---

### 3. 公式料金ページ・最新リンク

- [Azure OpenAI 公式価格表](https://azure.microsoft.com/ja-jp/pricing/details/cognitive-services/openai-service/)
- [OpenAI Pricing](https://openai.com/pricing)

---

#### ⚠️ **注意**
- 「レート制限値」いっぱいまで使い切ることはほぼ稀です（実運用は通常1〜10%未満の利用が大半）。
- **実際の請求額は「Azure無料枠」や「プロモクレジット」で変動します。**
- **ご利用前に必ず「最新の料金・クレジット残高」をAzure Portalでご確認ください。**

---
```

---

**この表はそのままGitHubや資料にコピペして活用できます。**
さらに「自分の実利用に合わせた計算式例」や「警告アラート設計」なども要望があればすぐ展開しますので、
気軽にリクエストください！
