---
title: "Fortinetが「FortiGateデバイスの認証情報を使った攻撃キャンペーンの分析」を公開｜ゆぅさんのセキュリティ教室 第25回"
emoji: "🛡"
type: "tech"
topics: ["security", "セキュリティ", "jpcert", "脆弱性"]
published: true
---

> 本稿は note 公開記事のクロスポストです。原典: [note の記事](https://note.com/yuusan_security/n/n62d26251aba1)

> **毎週きりがなく流れてくるセキュリティ情報に、「結局なに?」と詰まって、ひとりで抱えていませんか。この連載は、情報に溺れそうな人を置き去りにしません。今週も、あなたの隣で一緒に読み解きます。**

> **現場担当者の朝、コーヒーを入れる前に最初に確認したこと。それは Fortinetが「FortiGateデバイスの認証情報を使った攻撃キャンペーンの分析」を公開 の続報でした。**

このニュース、顧客や上司に「結局なに?」 と聞かれて答えに詰まった経験ありませんか? 本稿は、この情報を **3 つの軸 (背景・目的・期待される効果) × 3 ペルソナ (現場 / 管理者 / 経営者)** で翻訳し、明日から取れる行動に落とし込みます。完全版 PDF (14 頁) の核心を、本稿 1 本で読めるよう再構成しました。

---

## 📚 この記事で学べる 5 つのこと

1. **Fortinetが「FortiGateデバイスの認証情報を使った攻撃キャンペーンの分析」を公開** の本質を「背景・目的・期待される効果」 の 3 軸で構造化して理解できます
2. 現場担当者 / 管理者 / 経営者 別の「即答テンプレ」 が手に入ります
3. 立場ごとに明日から取れる **実務行動** とその順番
4. 顧客提案 / 経営報告に転用できる **言葉の選び方**
5. 同じ Claude Code 環境で「自分でも作れる型」 として習得可能

---

## 1️⃣ 背景: なぜ今このセキュリティ情報が公開されたのか

Fortinetは2026年6月20日、PSIRTブログに「FortiGateデバイスの認証情報を使った攻撃キャンペーンの分析」を公開した（原典によれば米国時間2026年6月19日に掲載されたブログの抄訳）。原典は、FortiBleedと呼ばれる認証情報窃取キャンペーンについて、過去のインシデント（FG-IR-26-060、FG-IR-25-647）に関連する認証情報の再利用と、多要素認証（MFA）が有効化されていないデバイスへのブルートフォース攻撃が組み合わされていると説明している。時系列を整理すると、Fortinetの公開より前に外部の報告が先行していた。Recorded Futureによれば、研究者が2026年6月13日にデータセットを公表し、194カ国の約73,932件のFortiGateファイアウォールのURLの認証情報を含むとされる。CISAはFortinetの米国での公開の前日にあたる2026年6月18日に注意喚起を出し、約74,000台が侵害されたと述べている。台数は報告元ごとに異なり、Fortinetの原典は台数を示していない。Fortinetの公開は、こうした外部報告を受けて、製品ベンダーとして事実関係と対策を示したものと考えられる。

---

## 2️⃣ 目的: Fortinet が誰に何を届けたいのか

原典は「これはフォーティネット製品の新たな脆弱性ではなく」と明記し、この活動が最近公表されたインシデントやアドバイザリとも関連していないと述べている。想定読者は影響を受けた可能性のあるFortiGateを使う組織で、Fortinetは対象の顧客へ順次連絡していると説明している。そのうえで直ちに取るべき対応として、すべての管理者・VPNセッションの終了と認証情報のリセット、すべての管理者・VPNユーザーでのMFA有効化、管理者認証情報のハッシュ方式としてPBKDF2をサポートする7.4、7.6、8.0の最新バージョンへのアップグレード、設定の検証（「forticloud」「fortiuser」「fortinet-support」「fortinet-tech-support」など見覚えのないアカウントの確認）、ログの確認、外部からの管理アクセスの制限を挙げている。侵害の証拠が見つかった場合はデバイスを侵害されたものとして扱い、AD/LDAP統合のアカウントも侵害されたものとして扱うよう求めている。「新たな脆弱性ではない」と先に示すことで、利用者の関心をパッチ待ちではなく運用上の対策に向けさせる意図があると考えられる。

---

## 3️⃣ 期待される効果: 業務にどう活かすか

短期的には、FortiGateを使う組織が侵害の有無を確かめ、認証情報のリセットとMFA有効化を進めるきっかけになると考えられる。中期的には、PBKDF2に対応したバージョンへの移行が進むことが期待される。ただしArctic Wolfは、旧バージョンからアップグレードしても、各管理者がアップグレード後にログインするまで管理者パスワードは旧方式のハッシュのまま残ると説明しており、アップグレード後の全管理者のログイン（またはパスワード更新）までを作業に含める必要がある。構造的には、原典が「新たな脆弱性ではない」と明言したことで、パスワードの使い回し、MFA未設定、管理画面のインターネット公開といった運用上の弱点が問題の中心であることが共有され、境界機器の認証管理を見直す動きにつながると考えられる。

---

## 🖼 図解で一望する

本稿の要点を図にまとめました。社内共有にそのままお使いください。

![インフォグラフィック 1/4 (標準・縦)](JPCERT_WR_20260624_01_インフォグラフィック_標準_縦.png)

![インフォグラフィック 2/4 (簡易・縦)](JPCERT_WR_20260624_01_インフォグラフィック_簡易_縦.png)

![インフォグラフィック 3/4 (詳細・横)](JPCERT_WR_20260624_01_インフォグラフィック_詳細_横.png)

![インフォグラフィック 4/4 (詳細・正方形)](JPCERT_WR_20260624_01_インフォグラフィック_詳細_正方形.png)

---

## 4️⃣ 3 ペルソナ別 実務シナリオ翻訳

同じ脅威情報も、立場が違えば「最初に取るべき行動」 が変わります。**本稿の核心は、ここから先の「誰に何を伝えるか」 の翻訳設計** にあります。

### ペルソナ① 現場担当者

**この立場の方が抱える懸念**: 自組織のFortiGateがFortiBleedの影響を受けていないか、侵害の痕跡をどう調べればよいかが気になる。

**明日から取れる 4 つの行動**:
1. 原典の「設定を検証する」に従い、「forticloud」「fortiuser」「fortinet-support」「fortinet-tech-support」など見覚えのないアカウントや、ファイアウォール・VPN設定の不正な変更がないか確認する。
2. 原典の「ログを確認する」に従い、不明なIPアドレスからの予期しない管理者アクセスや、想定外のVPNユーザー作成・パスワードリセット・VPN接続がないか調べる。
3. すべての管理者セッションとVPNセッションを終了し、管理者・VPNのパスワードをリセットしたうえで、すべてのアカウントでMFAを有効化する。
4. PBKDF2をサポートするバージョンへアップグレードし、全管理者がアップグレード後に一度ログインする（またはパスワードを更新する）ところまでを手順に含める。外部からの管理アクセスは信頼されたホストに限定するか無効化する。

**この情報から学べること**: 原典が示すとおり、今回の問題は新たな脆弱性ではなく、認証情報の再利用とMFA未設定という運用上の弱点にある。アップグレードしただけではハッシュの移行が終わらない場合がある（Arctic Wolfの説明）ことを、作業手順を組む段階で押さえておくことが重要である。

### ペルソナ② 管理者

**この立場の方が抱える懸念**: 自組織のFortiGateの侵害状況を把握し、対策の優先順位を決めてチームに指示を出せるかが気になる。

**明日から取れる 4 つの行動**:
1. 現場担当者に、原典の手順に沿った侵害調査（見覚えのないアカウント・設定変更・ログ）の実施と報告期限を指示する。
2. 認証情報リセットとMFA有効化の対象（管理者・VPNユーザー）と実施順を決め、VPN利用者への事前連絡と切替手順を用意する。
3. FortiOSのバージョンと外部管理アクセスの設定を棚卸しし、アップグレード後の全管理者ログインまで含めた計画を立てる。
4. 調査結果と対策の進み具合（MFA有効化率、アップグレード率、外部管理アクセスの制限状況）をまとめ、経営層へ報告する。

**この情報から学べること**: 原典は「新たな脆弱性ではない」と明記しており、パッチ適用だけでは対策が終わらないことを意味する。認証管理・アクセス制御・ログ確認という運用面の改善を、進み具合の数字で追える形にすることが管理者の役割になる。過去のインシデントの認証情報が再利用されたことは、インシデント後の認証情報リセットが徹底されていたかを振り返るきっかけにもなる。

### ペルソナ③ 経営者

**この立場の方が抱える懸念**: 各国の機関が注意喚起を出している大規模な攻撃に対し、自組織が影響を受けていないか、経営として何を判断すべきかが気になる。

**明日から取れる 4 つの行動**:
1. 管理者から侵害調査の結果と対策の進み具合の報告を受け、侵害が確認された場合はインシデント対応体制の立ち上げと外部専門家の関与を判断する。
2. MFA導入・アップグレード・外部管理アクセスの制限に必要な予算と人員を承認し、完了までの期限を管理者と合意する。
3. 侵害が確認された場合に備え、取引先・顧客への影響と情報開示の要否を法務・広報と協議しておく。
4. 今回を機に、ネットワーク境界機器全般の認証管理方針（MFA必須、管理画面を公開しない）を見直すよう指示する。

**この情報から学べること**: この攻撃は新たな脆弱性ではなく設定・運用の弱点を突くものであり、製品を入れ替えるだけでは防げない。MFA導入や認証管理の強化といった運用改善への投資を、製品購入と同じ重さで判断する必要がある。過去のインシデントの認証情報が再利用された事実は、インシデント後の後始末（認証情報のリセット）まで含めて対応を完了させる重要性を示している。

---

## 📎 本文の日付・数値の出典

本文に出てくる日付・数値は、下記の公開情報で確認したものだけを載せています。

発行元: **Fortinet** ／ 一次情報: https://www.fortinet.com/jp/blog/psirt-blogs/analysis-of-reported-credential-compromise-of-fortigate-devices

- 「2026年6月20日」 — [Fortinet PSIRT ブログ](https://www.fortinet.com/jp/blog/psirt-blogs/analysis-of-reported-credential-compromise-of-fortigate-devices) 該当箇所: 投稿者欄「Carl Windsor | 2026年6月20日土曜日」
- 「米国時間2026年6月19日」 — [Fortinet PSIRT ブログ](https://www.fortinet.com/jp/blog/psirt-blogs/analysis-of-reported-credential-compromise-of-fortigate-devices) 該当箇所: 「米国時間2026年6月19日に掲載されたフォーティネットブログの抄訳です。」
- 「FG-IR-26-060、FG-IR-25-647」 — [Fortinet PSIRT ブログ](https://www.fortinet.com/jp/blog/psirt-blogs/analysis-of-reported-credential-compromise-of-fortigate-devices) 該当箇所: 状況分析「過去のインシデント（FG-IR-26-060、FG-IR-25-647）に関連する認証情報を再利用する」
- 「7.4、7.6、8.0」 — [Fortinet PSIRT ブログ](https://www.fortinet.com/jp/blog/psirt-blogs/analysis-of-reported-credential-compromise-of-fortigate-devices) 該当箇所: 「7.4、7.6、または8.0の最新バージョンへアップグレードする：これらのバージョンでは、管理者認証情報のハッシュ方式としてPBKDF2がサポートされています。」
- 「2026年6月13日」 — [Recorded Future](https://www.recordedfuture.com/blog/critical-fortibleed-campaign) 該当箇所: Timeline "June 13, 2026: Researcher Volodymyr Diachenko publicly reports the FortiBleed dataset"
- 「194カ国の約73,932件」 — [Recorded Future](https://www.recordedfuture.com/blog/critical-fortibleed-campaign) 該当箇所: "valid administrative and SSL VPN credentials for approximately 73,932 FortiGate firewall URLs across 194 countries"
- 「2026年6月18日」 — [CISA](https://www.cisa.gov/news-events/alerts/2026/06/18/cisa-urges-hardening-fortinet-devices-after-reports-credential-exposure) 該当箇所: アラート表題 "CISA Urges Hardening Fortinet Devices After Reports of Credential Exposure"（公開日 June 18, 2026）
- 「約74,000台」 — [CISA](https://www.cisa.gov/news-events/alerts/2026/06/18/cisa-urges-hardening-fortinet-devices-after-reports-credential-exposure) 該当箇所: アラート本文 "approximately 74,000 internet-accessible Fortinet devices"（FortiBleed による侵害）

---

## 🎬 動画解説

本稿の 3 軸 × 3 ペルソナの要点を、動画でも解説しています。

https://youtu.be/FzYlzSujIj8
---

## この記事について

本稿は note で公開した記事の技術版クロスポストです（原典: [note の記事](https://note.com/yuusan_security/n/n62d26251aba1)）。
JPCERT/CC Weekly Report 等の公的情報を **背景・目的・期待される効果の3軸 × 現場/管理者/経営者の3ペルソナ** に翻訳する週次連載の1本です。

## 関連リソース

- 毎週の3軸分析を続けて読む: https://www.intect-i.jp/go/dojo/?utm_source=zenn&utm_medium=social&utm_campaign=dojo
- 実践教材・レポート(BOOTH): https://www.intect-i.jp/go/booth/?utm_source=zenn&utm_medium=social&utm_campaign=booth
- 無料ツール WR-Analysis: https://www.intect-i.jp/tools/wr-analysis/?utm_source=zenn&utm_medium=social&utm_campaign=wr_analysis
- 法人・事業者の方へ（研修の中身を14分で見る・無料/登録不要）: https://www.intect-i.jp/for-business/?utm_source=zenn&utm_medium=sns_biz
