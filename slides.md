---
theme: seriph
background: /background.png
title: 伊予絣計測支援システムの開発
class: text-center
transition: slide-left
mdc: true
---

# 伊予絣計測支援システムの開発
## 〜伝統工芸の保持者を支えるPWAツールの提案〜

<div class="pt-12">
  <span @click="$slide.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white op-10">
    卒業研究発表会 <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-bot m-12 w-full flex justify-between pr-24 border-t border-gray-500/30 pt-4">
  <div class="text-left">
    <div class="text-sm opacity-60 italic">Kawahara e-Business College</div>
    <div class="text-xl">河原電子ビジネス専門学校</div>
  </div>

  <div class="text-right">
    <div class="text-sm opacity-60 italic">Presented by</div>
    <div class="text-2xl font-bold">村上 聖音</div>
  </div>
</div>

---

# 1. 研究の背景と動機
### 伝統工芸「伊予絣」の現状と課題

- **伊予絣の希少性と価値**
  - 現在、この全工程を一人で完結できる職人は極めて稀。
  - **「素材から着物まで」**: 染料の採取から機織りまで、気の遠くなるような工程数。
- **デジタル化への挑戦と挫折**
  - 既存の描画ソフト（IbisPaint等）を試行：**「機能が多すぎて、描画に集中できない」**
  - アナログの描き心地とデジタルの利便性の間にある、高い習得コストの壁。
- **職人の本音と「あと10枚」**
  - 「織りたいから、織る」という純粋な創作意欲。
  - 残された時間の中で、**「面倒な計算や計測」に邪魔されず、表現に没頭したい**というニーズ。

<v-click>
<div class="mt-4 p-4 bg-orange-50/10 rounded border-l-4 border-orange-500">
  <b>解決すべき課題：</b><br>
  職人が「幾何学模様」などの新しい表現に挑戦する際、アナログでは困難だった
  <b>精密な計測と計算の自動化</b>を行い、創作の自由度を最大化する。
</div>
</v-click>

<!--
【導入：職人の凄さ】  
私の祖母は、愛媛県指定無形文化財の保持者として伊予絣を織っています。
伊予絣の制作は、染料となる木の実を拾うところから始まり、藍を建て、糸を染め、機を織り、最終的に着物にするまで、気の遠くなるような全工程を一人で完結させます。  
現在、これを全てこなせる職人は極めて稀です。  

【転換：デジタルの壁】  
そんな祖母が「デジタルで絵を描いてみたい」と口にした際、既存のアイビスペイントなどの描画ソフトを試してもらいました。
しかし、多機能ゆえの操作の複雑さや、アナログとは異なる描き心地が壁となり、創作に集中できないという課題に直面しました。  

【核心：あと10枚の意味】  
祖母は「生きてるうちにあと10枚織れるかどうか」と言います。  
これは悲観的な意味ではなく、「残された時間で、いかに楽しみながら自分の表現を突き詰められるか」という前向きな挑戦の言葉です。  
趣味だからこそ、ズレを直すような「苦労」ではなく、新しい幾何学模様に挑むような「創作」に時間を使いたい。そのための計測と計算を、私の技術で肩代わりすること。それが本研究の出発点です。  

【解決すべき課題：祖母のスタイルと幾何学模様】  
これまでの祖母の作品は、身近な植物などをモチーフにした自然物の図案が中心で、手仕事ゆえの「揺らぎ」も、その「味」となりえました。  
しかし、今新しく挑戦しようとしているのは、正確なリピートが求められる「幾何学模様」です。幾何学模様は、同じパターンを何度も「繰り返す」必要があり、方眼紙の小さなマス目を数えながら行う設計作業では、一度の数え間違いや計算のズレが作品全体の調和を壊してしまいます。  
この「方眼紙のマス目を延々と数え、計算する」というアナログ作業のプレッシャーを、デジタルの正確な計測と自動計算で取り除くこと。それにより、職人が老化による衰えを気にせず、新しい表現に没頭できる自由を提供することが本システムの目的です。  
-->

---

# 2. 現状の課題：計測精度の維持と単位換算
### 「手書き図面」から「製作データ」への高い障壁

<div class="grid grid-cols-2 gap-10">

<div>

- **「方眼紙」の読み取りによる疲労**
  - 幾何学模様における、同一パターンの繰り返し箇所の特定。
  - 小さなマス目を凝視し、手動で計測する際の認知負荷。
- **伊予絣特有の「単位換算」**
  - 方眼紙上の「mm」を「往・羽」へ変換する複雑な計算。
  - 老化や疲労による、無意識の計算ミス。

</div>

<div>

<v-click>
<div class="p-4 bg-orange-500/10 border-l-4 border-orange-500 text-sm">
<b>セカンドオピニオンとしての必要性：</b><br>
「自分の計算は合っているか？」という不安を、デジタルによるダブルチェックで解消。ミスを未然に防ぎ、精神的な余裕を生む。
</div>

<div class="mt-4 text-xs opacity-70">
※本システムは職人の判断を否定するものではなく、<br>
「自信を持って次の工程に進めるための根拠」を提供する。
</div>
</v-click>

</div>

</div>

<!--
【現状の課題：繰り返しの精度と心理的負担】  
特に祖母が挑戦したい幾何学模様において、最大の壁は「繰り返しの正確さ」の維持です。現在は方眼紙に図案を描き、そのマス目を一つずつ数えて計算していますが、規則的な模様ゆえに一箇所の数え間違いが全体の歪みとして目立ってしまいます。  

高齢の職人にとって、小さな方眼紙のマス目を何百回と数え続けるのは、私たちが想像する以上に目と脳を消耗させる作業です。  
また、方眼紙上の寸法を伊予絣特有の単位である「行(ゆき)・羽は)」へ換算する作業も重なり、脳の疲労による「うっかりミス」が数日後の織り工程で発覚するというリスクも常に抱えています。  

【補足：本システムの提供目的】  
「もし間違えていたら、これまでの努力が無駄になる」という不安は、創作のブレーキになります。本システムは、スマホで撮るだけでその「数え作業」と「計算」を瞬時に行い、職人が「これで大丈夫だ」と確信を持って次の工程に進める、セカンドオピニオンとしての役割を担います。  
-->

---

# 3. 解決策：伊予絣計測支援ツール
### 運用負荷を最小化した、PWAによる計測アプローチ

<div class="grid grid-cols-2 gap-10">

<div>

- **デバイスを選ばない「PWA」構成**
  - インストール不要、GitHub Pagesで完結。
  - 上京後の保守性を考慮したサーバーレス設計。
- **直感的な「3ステップ」計測**
  1. **撮影**: 手書きの図面をタブレットで撮影。
  2. **補正**: 射影変換による歪み補正。
  3. **計測**: 任意の点を選択し「行・羽」を算出。
- **データ出力と保存**
  - PDF出力による現場での参照
  - JSONによる中断保存

</div>

<div>

<div class="p-3 bg-blue-500/10 border border-blue-500/50 rounded">
<p class="text-sm font-bold text-blue-400">🛠 技術的アプローチ</p>
<ul class="text-xs list-disc ml-4 space-y-1 mt-2">
<li><b>射影変換の実装</b>：斜めからの撮影でも、方眼紙の四隅を指定することで正確な平面座標を復元。</li>
<li><b>低負荷・高レスポンス</b>：クライアントサイド（JS）のみで計算を完結させ、低スペックなタブレットでも動作を担保。</li>
</ul>
</div>

</div>

</div>

<v-click>
<div class="mt-2 p-4 bg-green-500/10 border-l-4 border-green-500 text-sm">
<b>こだわりの設計思想：</b><br>
自動認識による「過剰な自動化」をあえて避け、職人が測りたい場所を確実に測れる
<b>「セミオート」な使い心地</b>と、永続的な利用に耐えるシンプルな構成を両立。
</div>
</v-click>

<!--
【解決策：システムの概要と構成】  
課題を解決するために開発したのが、ブラウザから手軽に利用できるPWA「伊予絣計測支援ツール」です。  
このシステムは、私の「上京」という個人的なライフイベントを背景とした、明確な設計思想を持っています。それは「クラウドを一切介さず、サーバーレスで完結させること」です。GitHub Pagesのみで動作させることで、将来にわたる保守コストを極限まで抑え、祖母がいつでも使い続けられる環境を優先しました。  

【技術的アプローチ：射影変換と計測】  
システムの核となるのは、ホモグラフィ変換を用いた座標補正です。タブレットで図面を撮影した際、どうしても発生する「斜めの歪み」を、画面上の四隅を指定するだけで真上からの正確な図面データへと補正します。  
計測に関しても、あえてOpenCVによる全自動認識は採用しませんでした。低スペックなタブレットでの動作安定性を重視し、かつ「熟練の職人が必要な箇所だけを確認したい」というニーズに応えるため、タップした任意の座標を「行(ゆき)・羽(は)」という伊予絣の単位へ瞬時に換算するインターフェースにこだわりました。  

【運用と今後】  
計測結果はPDFとして出力して現場で持ち歩くことができるほか、JSON形式での保存機能により、大規模な図面の計測も途中で中断して再開することが可能です。  
「高度なAI」を載せることよりも、祖母の生活に寄り添い、確実に、かつ長く使い続けられる「道具」としての完成度を追求しました。  
-->

---

# 4. 実行画面：直感的な計測プロセス
### 職人の「測りたい」に即座に応えるUI

<div class="grid grid-cols-3 gap-4">

<div class="text-center">
<p class="text-xs font-bold mb-2">① 歪み補正（射影変換）</p>
<img src="/calibration.png" class="h-60 rounded border border-white/10 object-contain mx-auto bg-black/20" />
<p class="text-[10px] mt-2 opacity-70">四隅を指定し、方眼紙を正対させる</p>
</div>

<div class="text-center">
<p class="text-xs font-bold mb-2">② 任意地点の計測</p>
<img src="/measurement.png" class="h-60 rounded border border-white/10 object-contain mx-auto bg-black/20" />
<p class="text-[10px] mt-2 opacity-70">タップした箇所の「行・羽」を算出</p>
</div>

<div class="text-center">
<p class="text-xs font-bold mb-2">③ 計測データの活用</p>
<img src="/output.png" class="h-60 rounded border border-white/10 object-contain mx-auto bg-black/20" />
<p class="text-[10px] mt-2 opacity-70">現場へ持ち出し、または作業再開</p>
</div>

</div>

<div class="flex justify-between items-start">
  <div class="p-3 bg-blue-500/10 border-l-4 border-blue-500 text-xs">
    <b>技術スタック：</b> React / TypeScript / Canvas API / jsPDF
    <span class="pl-4">GitHub Pagesによる静的配信で、永続的な利用を実現</span>
  </div>
  
  <div class="text-right">
    <div class="bg-white p-1 rounded inline-block">
      <a href="https://ca01971172.github.io/iyo-kasuri-calc/" target="_blank">
      <img src="https://api.qrserver.com/v1/create-qr-code/?size=60x60&data=https://ca01971172.github.io/iyo-kasuri-calc/" width="60" height="60" />
      </a>
    </div>
  </div>
</div>

<!--
【実演への繋ぎ：システムの動き】  
実際の操作画面についてご説明します。 システムは非常にシンプルで、まずは図面を撮影し、その画像の四隅をタップして指定します。  
これにより、斜めに撮られた写真であっても、数学的な補正、いわゆる射影変換を行い、正確な平面データとして復元します。

次に、その図面上の「知りたい点」をタップするだけで、伊予絣の単位である「行」と「羽」が瞬時に計算されます。これまでは方眼紙のマス目を一つずつ数えていた作業が、たった一回のタップで完結します。  

さらに、これらのデータはPDFとして書き出しが可能です。これにより、タブレットを汚しやすい染めや織りの現場にも、紙のデータとして持ち込むことができます。  

【デモ開始】  
それでは、実際にどのように動作するのか、ブラウザ上で実演いたします。
-->

---

# 5. 計測精度の検証
### 職人の「正解」に対する算出結果の比較

<div class="grid grid-cols-3 gap-2 items-start mt-2">
  <div class="flex flex-col gap-1 items-center">
    <span class="text-[9px] font-bold text-blue-400">職人の図面と手計算メモ</span>
    <img src="/grandma_zumen.png" class="h-32 rounded border border-white/10 shadow-sm" />
    <img src="/grandma_memo.png" class="h-32 rounded border border-white/10 shadow-sm" />
    <span class="text-[8px] opacity-60">区間ごとの「差分」記録</span>
  </div>

  <div class="flex flex-col gap-1 items-center relative">
    <span class="text-[9px] font-bold text-green-400">アプリの計測画面</span>
    <img src="/app_result.png" class="h-66 rounded border border-white/10 mx-auto object-contain bg-black/10" />
    <span class="text-[8px] opacity-60 text-center">起点からの「絶対値」表示</span>
  </div>

  <div class="flex flex-col gap-1">
    <span class="text-[9px] font-bold text-orange-400 text-center">精度照合表（差分換算）</span>
    <div class="bg-orange-500/5 p-2 rounded border border-orange-500/20 shadow-lg">
      <table class="text-[11px] w-full border-collapse">
        <thead>
          <tr class="border-b border-orange-500/30 font-bold text-center text-orange-300">
            <td class="pb-1">区間</td><td class="pb-1">職人</td><td class="pb-1">アプリ</td>
          </tr>
        </thead>
        <tbody class="text-center">
          <tr class="border-b border-white/5"><td>1</td><td>37羽 (38羽)</td><td>37羽</td></tr>
          <tr class="border-b border-white/5"><td>2</td><td>6羽</td><td>5羽</td></tr>
          <tr class="border-b border-white/5"><td>3</td><td>15羽</td><td>15羽</td></tr>
          <tr class="border-b border-white/5"><td>4</td><td>2羽</td><td>3羽</td></tr>
        </tbody>
      </table>
      <div class="text-[8px] mt-2 opacity-80 leading-tight border-t border-white/10 pt-1">
        ※アプリ値を差分に換算して比較。<br>
        職人の「帳尻合わせ（±2羽）」の範囲内で完全に一致。
      </div>
    </div>
  </div>
</div>

<v-click>
<div class="mt-3 p-2 bg-blue-500/10 border-l-4 border-blue-500 text-[11px] leading-snug">
<b>検証結果：</b>
記録形式は異なりますが、数値を揃えると極めて高い精度で一致。
職人からも「現場の微調整で吸収できる誤差であり、計算の根拠として十分信頼できる」との評価を得ました。
</div>
</v-click>

<!--
【精度検証：現場での実用性】  
「デジタルでどこまで正確に測れるのか」を検証しました。 スライド左側は祖母が手計算で書き記した「正解」のメモ、右側が本システムでの計測結果です。

比較の結果、数値はほぼ一致しました。 実際、熟練の職人であっても、織る際の糸の張り具合などで「±2羽」程度の帳尻合わせは現場で日常的に行われます。  
祖母からも「この精度があれば、自分の計算ミスを恐れずに自信を持って作業を始められる」という、職人視点での実用性に対する高い評価をいただくことができました。
-->

---

# 6. 画像処理による歪み補正
### 「真正面から撮れない」という現場の物理的制約を解決

<div class="flex flex-col gap-4">

  <div class="flex items-center gap-4">
    <div class="w-24 text-[10px] font-bold leading-tight text-blue-400">パターン1：<br>ほぼ正面からの撮影</div>
    <div class="flex-1 flex items-center justify-center gap-2 bg-black/5 p-2 rounded">
      <img src="/front_raw.png" class="h-32 rounded border border-white/10" />
      <carbon:arrow-right class="text-xl opacity-50" />
      <img src="/front_processed.png" class="h-32 rounded border border-blue-500/50 shadow-lg shadow-blue-500/20" />
    </div>
  </div>

  <div class="flex items-center gap-4">
    <div class="w-24 text-[10px] font-bold leading-tight text-green-400">パターン2：<br>極端な斜めからの撮影</div>
    <div class="flex-1 flex items-center justify-center gap-2 bg-black/5 p-2 rounded">
      <img src="/slant_raw.png" class="h-32 rounded border border-white/10" />
      <carbon:arrow-right class="text-xl opacity-50" />
      <img src="/slant_processed.png" class="h-32 rounded border border-green-500/50 shadow-lg shadow-green-500/20" />
    </div>
  </div>

</div>

<div class="mt-6 p-3 bg-gray-500/10 border border-white/10 rounded text-[12px] leading-relaxed">
<b>技術的必然性：射影変換（Homography Matrix）の適用</b><br>
手持ち撮影において「完全に真正面から、かつ影を落とさず撮る」ことは物理的に不可能です。
方眼紙の四隅から変換行列を算出し、画像を理想的な平面へ再投影することで、
<b>「どのような角度から撮っても正確に測れる」</b>という現場での可用性を担保しました。
</div>

<!--
【画像処理：物理的制約の解決】  
次に、現場での実用性を高めるための「画像処理」の工夫です。 手描きの図面をタブレットで撮影する際、自分の影を入れずに「完全に真正面」から撮ることは、手持ち撮影では物理的に不可能です。

そこで、数学的な座標補正である「射影変換」を実装しました。 スライド右側の例のように、照明の反射や自分の影を避けるためにあえて「斜め」から撮影した場合でも、システム側で正確な正方形のグリッドとして復元します。  
ユーザーに「綺麗に撮る努力」を強いるのではなく、技術側で制約を解決することで、暗い織り場や狭い作業机でも迷わず使える道具を目指しました。
-->
---

# 7. 技術的工夫と実証評価
### 現場の「使いやすさ」と「納得感」の両立

<div class="grid grid-cols-2 gap-10">

<div>

#### 🛠 ユーザビリティの追求
- **デジタル・ルーペの搭載**
  - タップ時に指で隠れる箇所を拡大表示。
  - 高齢者でもストレスなくミリ単位の指定が可能。
- **「確認用」としての数値提示**
  - 自動認識に頼り切らず、職人の目視確認を補完。
- **現場への橋渡し（PDF）**
  - 水や染料を扱う織り場へ「紙」として持ち出せる運用。

</div>

<div>

#### 📈 ユーザー（祖母）の評価
- **ポジティブな反応**
  - 「マス目を凝視しなくて良いのが何より楽」
  - 「自分の計算ミスを恐れず、安心して織り始められる」
- **今後の改善点**
  - 端末の操作自体への習熟（デジタル・ディバイド）。
  - 屋内照明による撮影精度のバラつきへの対応。

</div>

</div>

<v-click>
<div class="mt-8 p-4 bg-orange-500/10 border-l-4 border-orange-500 text-sm">
<b>結論：</b><br>
職人の技術を「置き換える」のではなく、計算・計測の不安を「取り除く」ことで、
<b>幾何学模様という新たな挑戦を心理的に支える</b>ツールの有効性が示された。
</div>
</v-click>

<!--
【技術的な工夫：操作性の配慮】  
ここでは、単なるシステムの仕組みではなく、実際に祖母が使う上での「工夫」についてお話しします。
タブレットを操作する際、自分の指で計測地点が隠れてしまうことが大きなストレスになります。そこで、タップ箇所を拡大表示する「ルーペ機能」を実装し、視力に頼りすぎない操作性を確保しました。  
また、このツールは「全自動」ではありません。あえて職人の目視と連携させることで、職人自身の「納得感」を大切にした設計にしています。

【実証実験と評価】  
実際に、伊予絣の保持者である祖母にこのプロトタイプを使ってもらいました。 最も大きな反響は「安心感」でした。「今まで小さなマス目を数えるのが苦痛で、間違えたらどうしようという不安が常にあったが、このツールで二重チェックできるのが嬉しい」という声をいただきました。

【考察】  
実証を通じて見えてきたのは、デジタル技術の役割は、熟練の技を自動化することではなく、職人が「自分の判断に自信を持って、次の挑戦に進めるようにすること」だという点です。これこそが、伝統工芸と現代技術が共存する一つの形ではないかと考えています。
-->

---

# 8. 今後の展望と結論
### 伝統と技術の橋渡しとして

<div class="grid grid-cols-2 gap-10">

<div>

#### 🚀 今後の展望（ロードマップ）
- **AIによる計測（打点）の完全自動化**
  - 現在は手動で行っている「点の選択」を自動化。
  - 職人が図面を読み解くスピードを加速させる。
- **実寸（cm）換算機能の統合**
  - 「羽数：長さ」の比例計算をシステム内で完結。
  - 絣括り（糸を縛る作業）にそのまま使える数値を算出。
- **デジタル・アーカイブ化**
  - 熟練者の頭の中にある図案をデジタル資産として残し、次世代へ継承する基盤作り。

</div>

<div>

#### 🏁 結び
- **技術の役割**
  - 高度なAIを載せることよりも、職人が「あと10枚」に没頭できる環境を優先。
- **伝統への貢献**
  - デジタルを「敵」や「代用品」ではなく、技を支える「新しい道具」として提示。

</div>

</div>

<div class="mt-4 text-center italic text-lg text-orange-400">
" 技術は、職人が新しい挑戦に踏み出すための『自信』を支えるものである。 "
</div>

<!--
【今後の展望：さらなる負荷軽減と汎用性】  
最後に、今後の展望についてお話しします。  
本システムは現在、ユーザーが画面上の点を選択する「セミオート」の形式をとっています。今後は画像処理やAIを導入することで、図面を認識して自動的に計測ポイントを特定する「完全自動計測」へのアップデートを目指しています。

また、職人の計算工程を詳しく解析したところ、「図面上の羽数」から「糸を縛るための実寸（cm）」を導き出す比例計算に多大な時間を費やしていることが分かりました。  
今後は、織り機の密度に合わせた「長さ換算機能」を統合することで、図面をタップするだけで、そのまま糸のマスキング作業に使える数値を算出できる、より現場に即したツールへと進化させていきたいと考えています。

【結び：本研究の結論】  
本研究を通じて確信したのは、伝統工芸におけるデジタルの役割は、熟練の技を自動化して奪うことではないということです。  
本当の価値は、職人が抱える「ミスへの不安」や「身体的な消耗」といったノイズを取り除き、職人が本来向き合うべき「表現の追求」に没頭できる環境を作ること。つまり、職人の『自信』を支える新しい道具になることだと考えています。

【最後の挨拶】  
祖母が「あと10枚」を織り上げるその時、このツールがその挑戦を少しでも支えることができれば、エンジニアとしてこれ以上の喜びはありません。

ご清聴ありがとうございました。
-->

---
layout: center
class: text-center
---

# Thank you!
### 研究の総括と質疑応答

<div class="grid grid-cols-2 gap-8 mt-8 text-left">

<div class="p-5 bg-blue-500/5 rounded border border-blue-500/20">
<p class="text-sm font-bold text-blue-400 mb-3">✅ 本研究で実現したこと（振り返り）</p>
<ul class="text-[12px] space-y-2 opacity-90">
<li><b>心理的障壁の除去:</b> ミスを恐れず新しい幾何学模様に挑める「二重チェック」体制。</li>
<li><b>身体的負担の解消:</b> マス目の凝視から解放される「デジタル・ルーペ」の実装。</li>
<li><b>永続的な支援:</b> 開発者が離れた後も使い続けられる「完全サーバーレス設計」。</li>
</ul>
</div>

<div class="p-5 bg-orange-500/5 rounded border border-orange-500/20">
<p class="text-sm font-bold text-orange-400 mb-3">🚀 次のステップ（今後の展望）</p>
<ul class="text-[12px] space-y-2 opacity-90">
<li><b>実測値（cm）計算の自動化:</b> 「羽数：長さ」の比例計算を統合し、設計・仕立てまでをカバー。</li>
<li><b>AIによる図面認識:</b> 手動打点データを教師データとし、完全自動計測へのアップグレード。</li>
<li><b>現場環境への適応:</b> 低照度下での画像補正アルゴリズムの強化。</li>
</ul>
</div>

</div>

<div class="mt-10 flex flex-col items-center">
  <div class="bg-white p-1 rounded mb-2 shadow-lg">
      <a href="https://ca01971172.github.io/iyo-kasuri-calc/" target="_blank">
        <img src="https://api.qrserver.com/v1/create-qr-code/?size=80x80&data=https://ca01971172.github.io/iyo-kasuri-calc/" width="80" height="80" />
      </a>
  </div>
  <p class="text-[10px] opacity-60">実機デモURL:
    <a href="https://ca01971172.github.io/iyo-kasuri-calc/" target="_blank">https://ca01971172.github.io/iyo-kasuri-calc/</a>
  </p>
</div>

<!--
### 質疑応答用・想定問答集（要点メモ）

**Q1. 精度について（スマホで大丈夫？）**
- 環境による誤差は否定できない。
- **位置付け:** 熟練技術の代替ではなく「計算ミスを防ぐセカンドオピニオン」。
- **解決する苦痛:** ミリ単位のズレより「根本的な数え間違い」による手戻りの不安。
- **スタンス:** デジタルが目安を出し、職人が最終判断する「人と技術の協調」。

**Q2. 全自動にしなかった理由は？（OpenCV等）**
- **技術面:** ブラウザ上での安定性や実装コストを考慮。
- **運用面:** 職人の作業フローを尊重。
- **発見:** 職人は全座標ではなく「重要なポイント」を選んで思考している。
- **結論:** 押し付けの全自動より、測りたい場所を選べる「半自動」が道具として最適。

**Q3. 現場環境で使えるの？（汚れ・暗さ）**
- **工程の精査:** 手が汚れるのは染色時のみ。設計・括り・織りの段階では操作可能。
- **ハイブリッド運用:** 現場が厳しい場合はPDFで書き出し「紙」として持ち込み。
- **利便性:** アナログの良さとデジタルの正確さを使い分けられる設計。

**Q4. 尺計算への対応は？**
- **現状:** 保持者の計算式を解析し、ボトルネックが「羽数→実寸(cm)」の比例計算と判明。
- **今後:** 織機ごとの密度定数（例：430羽/39.5cm）をプリセット。
- **展望:** タップ一つで「糸を縛る位置（cm）」まで一撃で算出する機能を統合予定。

**Q5. N=1（祖母だけ）でいいの？**
- **希少性:** 保持者はわずか2名。手法も道具も「自分流」が基本の世界。
- **戦略:** 汎用性を求めて薄めるより「最高峰の一人を完璧に救う」ことに特化。
- **価値:** このN=1の深い成功体験こそが、文化財保護におけるDXの最短距離。
-->
