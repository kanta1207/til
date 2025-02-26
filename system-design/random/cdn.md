# CDN サービス（Cloudflare CDN, AWS CloudFront） と Edge Computing サービス（Cloudflare Workers, AWS Lambda&AWS CloudFront Functions）

まず基本的な用語を説明します：

## 基本用語解説

**CDN (Content Delivery Network)**

コンテンツ配信ネットワーク
簡単に言うと「世界中にサーバーを置いて、ユーザーに近いサーバーからコンテンツを届けるしくみ」
例：Netflix の動画を見るとき、アメリカのサーバーから直接配信されるのではなく、日本にあるサーバーから配信される

**Edge Computing**

エッジコンピューティング
コンピュータの計算をエッジデバイス（ユーザーの端末）で行うこと

**エッジロケーション**

CDN が世界中に配置しているサーバー
「エッジ」は「端」という意味で、ユーザーに近い場所という意味
例：東京、大阪、シンガポール、など世界中の主要都市にあるサーバー

**キャッシュ**

データの一時保存
よく使うデータをユーザーの近くのサーバーに保存しておくこと
例：人気の動画を各地のサーバーに保存しておいて、すぐに見られるようにする

**Cloudflare のサービス**

1. Cloudflare CDN (Basic Service)

   - コンテンツ配信
   - キャッシュ
   - 基本的なセキュリティ

2. Cloudflare Workers (Separate Service), runs on Cloudflare CDN
   - Edge computing platform
   - Runs on the same infrastructure
   - Can interact with the CDN but is not a CDN itself

**AWS のサービス**

1. AWS CloudFront (Basic Service)

   - コンテンツ配信
   - キャッシュ
   - 基本的なセキュリティ

2. AWS Lambda & AWS CloudFront Functions (Edge Computing Service)
   - Edge computing platform
   - Runs on the same infrastructure
   - Can interact with the CDN but is not a CDN itself

### Real-world Analogy:

Think of a convenience store network:

**Cloudflare CDN = Store network**

- Products are placed in local stores for easy access
- Basic "placement" and "sales" only

**Cloudflare Workers = Adding a "kitchen" to each store**

- Not just storing products
- Can heat up meals
- Brew coffee
- Process products

Use Cases:

Simple CDN Usage

Image delivery
Video delivery
HTML file delivery

Cloudflare Workers Capabilities

Content modification based on country
API response customization
User-specific content display
Real-time data aggregation and analysis
