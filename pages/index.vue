<template>
  <div class="container">
    <div class="categories">
      <div
        v-for="(category, index) in categories"
        :key="category"
        class="category-link"
      >
        <p v-if="index !== 0" class="divide">
          /
        </p>
        <nuxt-link
          class="category"
          :to="{ name: 'category-name', params: { name: category } }"
        >
          {{ category }}
        </nuxt-link>
      </div>
    </div>
    <div class="columns is-multiline is-vcentered">
      <div
        v-for="(article, index) in newsData"
        :key="article.publishedAt"
        :class="[
          'column',
          index === 0 || index === 6 || index === 13 || index === 19
            ? 'is-two-thirds-desktop is-two-thirds-tablet'
            : 'is-one-thirds-desktop is-one-third-tablet'
        ]"
      >
        <a :href="article.url">
          <div class="card">
            <div class="card-image">
              <figure
                :class="[
                  'image',
                  index === 0 || index === 6 || index === 13 || index === 19
                    ? 'is-3by1'
                    : 'is-3by2'
                ]"
              >
                <img :src="article.urlToImage" alt="Placeholder image" />
              </figure>
            </div>
            <div class="card-content">
              <div class="content">
                <p class="content-title subtitle">{{ article.title }}</p>
                <time :datetime="article.publishedAt">{{
                  article.publishedAt
                }}</time>
              </div>
            </div>
          </div>
        </a>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data: function() {
    return {
      categories: [
        'business',
        'entertainment',
        'general',
        'health',
        'science',
        'sports',
        'technology'
      ]
    }
  },
  async asyncData(context) {
    const url =
      'http://localhost:3000/api/v2/top-headlines?' +
      'country=jp&' +
      'apiKey=43e584e514174783ac4c7b0975951259'
    const newsData = await context.app.$axios.$get(url, {
      headers: {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': '*'
      },
      data: {}
    })
    // const newsData = {
    //   status: 'ok',
    //   totalResults: 30,
    //   articles: [
    //     {
    //       source: { id: null, name: 'Yahoo.co.jp' },
    //       author: null,
    //       title:
    //         '吉本興業、宮迫博之との契約解消を正式発表 会見の予定は「ございません」（オリコン） - Yahoo!ニュース',
    //       description:
    //         '吉本興業は19日、詐欺グループの会合に闇営業で参加し、所属する吉本興業から活動停止 - Yahoo!ニュース(オリコン)',
    //       url: 'https://headlines.yahoo.co.jp/hl?a=20190719-00000353-oric-ent',
    //       urlToImage:
    //         'https://lpt.c.yimg.jp/amd/20190719-00000353-oric-000-view.jpg',
    //       publishedAt: '2019-07-19T04:14:50Z',
    //       content: 'Impress Watch7/11() 18:33'
    //     },
    //     {
    //       source: { id: null, name: 'Asahi.com' },
    //       author: '朝日新聞デジタル',
    //       title: '元SMAPの3人、ジャニーさんへの追悼文を連名で発表 - 朝日新聞',
    //       description:
    //         'ジャニーズ事務所のアイドルグループ「ＳＭＡＰ」の元メンバーで、現在は別の事務所で活動している稲垣吾郎さん（４５）、草彅剛さん（４５）、香取慎吾さん（４２）の３人が１９日、ジャニーズ事務所の創業者で今…',
    //       url: 'https://www.asahi.com/articles/ASM7M45K6M7MUCVL00Z.html',
    //       urlToImage:
    //         'https://www.asahicom.jp/articles/images/c_AS20190719001625_comm.jpg',
    //       publishedAt: '2019-07-19T04:11:23Z',
    //       content:
    //         'Copyright © The Asahi Shimbun Company. All rights reserved. No reproduction or republication without written permission.'
    //     },
    //     {
    //       source: { id: null, name: 'F1-gate.com' },
    //       author: null,
    //       title:
    //         'マックス・フェルスタッペン、F1の給油復活案を支持 - F1-Gate.com',
    //       description:
    //         'レッドブル・ホンダのマックス・フェルスタッペンは、F1に給油の復活することで燃料とタイヤをセーブすることに囚われることなく“全開”の戦い...',
    //       url: 'https://f1-gate.com/verstappen/f1_50733.html',
    //       urlToImage:
    //         'https://f1-gate.com/media/img2019/20190719-max-verstappen.jpg',
    //       publishedAt: '2019-07-19T03:24:23Z',
    //       content: null
    //     },
    //     {
    //       source: { id: 'reuters', name: 'Reuters' },
    //       author: 'Reuters Editorial',
    //       title:
    //         '正午のドルは107円半ば、ＦＲＢ幹部発言に困惑 - ロイター (Reuters Japan)',
    //       description:
    //         '正午のドルは前日ＮＹ市場終盤の水準から小幅ドル高の１０７円半ば。朝方にＮＹ連銀が、前日のウィリアムズ総裁の講演内容は学術的なもので、連邦公開市場委員会（ＦＯＭＣ）の政策に関するものではないとのコメントを発表し、ドルの買い戻しが進んだ。',
    //       url: 'https://jp.reuters.com/article/tokyo-frx-mid-19-idJPKCN1UE08T',
    //       urlToImage:
    //         'https://s1.reutersmedia.net/resources/r/?m=02&d=20190719&t=2&i=1409568154&w=1200&r=LYNXNPEF6I071',
    //       publishedAt: '2019-07-19T03:24:00Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'Newsweekjapan.jp' },
    //       author: null,
    //       title:
    //         '河野外相談話「韓国は日韓請求権協定に違反、必要な措置を講じる」 - Newsweekjapan',
    //       description:
    //         '河野太郎外務相は19日、談話を発表し、韓国が日韓請求権協定に違反しているとして「...',
    //       url:
    //         'https://www.newsweekjapan.jp/stories/world/2019/07/post-12573.php',
    //       urlToImage:
    //         'https://www.newsweekjapan.jp/stories/assets_c/2019/07/newsweek_20190719_122618-thumb-470xauto-164189.jpeg',
    //       publishedAt: '2019-07-19T03:22:28Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'As-web.jp' },
    //       author: null,
    //       title:
    //         'ホンダF1山本MDインタビュー：フェラーリを上回る速さを示したイギリスGP。「パワーサーキットでここまで戦えたのは非常にポジティブ」 - オートスポーツweb',
    //       description:
    //         'F1第9戦オーストリアGPでの初優勝の興奮さめやらぬ翌週の第10戦イギリスGPで、レッドブルとホンダのスタッフは親睦をかねた耐久カート大会を開催。マックス・フェルスタッペン、ピエール・ガスリーの両ドライバーがサプライズで飛び入り参加するなどして、大盛り上がりだった。 ホンダの山本雅史マネージングディレクターも予定を1日繰り上げてイギリスに飛び、クリスチャン・ホーナー代表と組んで総合6位に入る活躍を見せた。そして本番のF1でも、惜しくも表彰台には上がれなかったものの、「十分にポジティブなレースだった」と満足そうだっ…',
    //       url: 'https://www.as-web.jp/f1/503914',
    //       urlToImage:
    //         'https://cdn-image.as-web.jp/2019/07/19115455/AP-1ZXTTXCMD1W11_news.jpg',
    //       publishedAt: '2019-07-19T03:08:30Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'Minkabu.jp' },
    //       author: 'FISCO 株・企業報',
    //       title:
    //         '金融庁と財務省、FATF承認の「仮想通貨SWIFT」創設へ＝ロイター報道【フィスコ・ビットコインニュース】 - みんなの仮想通貨',
    //       description:
    //         '財務省・金融庁が主導する形で、暗号資産版の「SWIFT」を創設する計画が、国際機関である金融活動作業部会（FATF）で承認されたことがわかった。ロイターが報じた。主な目的は、国内外の取引所経由で仮想通貨を送金する際の個人...',
    //       url: 'https://cc.minkabu.jp/news/3241',
    //       urlToImage: 'https://cc.minkabu.jp/logo.png',
    //       publishedAt: '2019-07-19T03:00:04Z',
    //       content: ''
    //     },
    //     {
    //       source: { id: null, name: 'Asahi.com' },
    //       author: '朝日新聞デジタル',
    //       title:
    //         '身柄確保の男、隣人とトラブル 胸ぐらつかみ「殺すぞ」 - 朝日新聞',
    //       description:
    //         '捜査関係者によると、京都アニメーションの爆発火災で、身柄を確保された男はさいたま市見沼区のアパートに住んでいた。関係者によると、２０１６年夏ごろに入居したとみられる。同じアパートに住む４０代男性によ…',
    //       url: 'https://www.asahi.com/articles/ASM7M2W6SM7MPTIL008.html',
    //       urlToImage:
    //         'https://www.asahicom.jp/articles/images/c_AS20190719000826_comm.jpg',
    //       publishedAt: '2019-07-19T02:56:26Z',
    //       content:
    //         'Copyright © The Asahi Shimbun Company. All rights reserved. No reproduction or republication without written permission.'
    //     },
    //     {
    //       source: { id: null, name: 'Sankei.com' },
    //       author: '産経ニュース',
    //       title:
    //         '京アニ火災 屋上へ逃げ切れず 十数段の階段で１９人を発見 - 産経ニュース',
    //       description:
    //         'アニメ制作会社「京都アニメーション」（本社・京都府宇治市）の京都市伏見区桃山町因幡にある３階建てのスタジオが全焼し、３３人が死亡した火災で、建物の３階から屋上に…',
    //       url:
    //         'https://www.sankei.com/affairs/news/190719/afr1907190024-n1.html',
    //       urlToImage:
    //         'https://www.sankei.com/images/news/190719/afr1907190024-p1.jpg',
    //       publishedAt: '2019-07-19T02:50:00Z',
    //       content:
    //         'PR\r\nPR\r\nPR\r\n©2019 The Sankei Shimbun All rights reserved.'
    //     },
    //     {
    //       source: { id: null, name: 'Nikkei.com' },
    //       author: '日本経済新聞社',
    //       title:
    //         '外相、韓国大使に抗議 元徴用工問題「極めて無礼」 - 日本経済新聞',
    //       description:
    //         '河野太郎外相は19日午前、韓国最高裁が日本企業に賠償を命じた元徴用工訴訟を巡り、南官杓（ナム・グァンピョ）駐日韓国大使を外務省に呼んだ。日本が求めた日韓請求権協定に基づく仲裁手続きに韓国が応じなかっ',
    //       url: 'https://www.nikkei.com/article/DGXMZO47520060Z10C19A7MM0000/',
    //       urlToImage:
    //         'https://article-image-ix.nikkei.com/https%3A%2F%2Fimgix-proxy.n8s.jp%2FDSXMZO4752013019072019MM0001-PB1.jpg?auto=format%2Ccompress&ch=Width%2CDPR&fit=max&ixlib=java-1.1.1&s=da69864bf2cfcbc0e2fef30432bafbe9',
    //       publishedAt: '2019-07-19T01:49:00Z',
    //       content:
    //         '2019/7/19 10:49 (2019/7/19 13:21)\r\n19\r\n19\r\n19652\r\n7\r\n10125718\r\nICJ\r\n19ICJ'
    //     },
    //     {
    //       source: { id: null, name: 'Pronews.jp' },
    //       author: null,
    //       title: 'ハッセルブラッド、「X1D II 50C」体験会を開催 - PRONEWS',
    //       description:
    //         'ハッセルブラッドは、新製品「X1DII50C」の体験会を東京・原宿にあるハッセルブラッドストア東京にて開催中だ。開催日は毎週火曜日から土曜日の14:00から約1時間程度。予約不要で参加費は無料。同体験会では、スタッフによる製品プレゼンテーションの後、参加者がX1DII50Cの実機を手に取って試すことができる。なお、会場にあるX1DII50Cはサンプル機のため、実際の製品とは仕様等が変更となる場合があるとしている。▶「X1DII50C」体験会...',
    //       url: 'https://www.pronews.jp/news/20190719100025.html',
    //       urlToImage:
    //         'https://www.pronews.jp/pronewscore/wp-content/uploads/2019/07/190719_x1d-ii-top-white_top.jpg',
    //       publishedAt: '2019-07-19T01:13:37Z',
    //       content: 'X9XCD 3,5-4,5/35-75201910585,000...'
    //     },
    //     {
    //       source: { id: null, name: 'Dwango.jp' },
    //       author: 'ドワンゴジェイピーnews',
    //       title:
    //         'あいみょん 体を縛られ吊るされ…不気味で“クセになる”MV完成 - ドワンゴジェイピーnews',
    //       description:
    //         'シンガーソングライター あいみょんが7月24日（水）に発売する8thシングル『真夏の夜の匂いがする』のMusic Videoが公開された。石原さとみ主演のTBS系火曜ドラマ「Heaven？～ご苦楽レストラン～」主題歌となっている本楽曲。今回のMusic Videoは『マリーゴールド』『今夜このまま』『ハルノヒ』のMusic Videoを手掛けた山田智和氏が監督を務めている。撮影の舞台となった...',
    //       url: 'https://news.dwango.jp/music/39391-1907',
    //       urlToImage:
    //         'https://news-img.dwango.jp/uploads/medium/file/000/161/103/161103/md_k6dxz7lcbupd3ihr7hu.JPG',
    //       publishedAt: '2019-07-19T01:00:00Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'Aviationwire.jp' },
    //       author: 'Tadayuki YOSHIKAWA',
    //       title:
    //         'ボーイング、737MAXの補償49億ドル 運航再開は10月以降に - Aviation Wire',
    //       description: null,
    //       url: 'https://www.aviationwire.jp/archives/178844',
    //       urlToImage:
    //         'https://www.aviationwire.jp/wp-content/uploads/2016/02/160129_0570_737M_boe-720.jpg',
    //       publishedAt: '2019-07-19T00:29:00Z',
    //       content:
    //         '718737 MAX4952602420194-62\r\n737 MAX49PHOTO: Tadayuki YOSHIKAWA/Aviation Wire\r\n7374-617737 MAX10-124FAA\r\n73720204257\r\n4-6737 MAX56\r\nBoeing\r\n LCC737MAXA320neo1979737MAX11974777XNMA19624737BCF19620IAG737MAX200CEO19619737FAA737MAX3121964737 MAXMCAS19518737MAX1719… [+60 chars]'
    //     },
    //     {
    //       source: { id: null, name: 'Yahoo.co.jp' },
    //       author: null,
    //       title:
    //         'アメリカ軍がホルムズ海峡でイラン無人機を電子攻撃で撃墜（JSF） - Yahoo!ニュース - Yahoo!ニュース',
    //       description:
    //         '7月18日、アメリカのトランプ大統領はホルムズ海峡でアメリカ軍艦に接近して来たイランの無人機を撃墜したことを明らかにしました。火器は使わず、電子攻撃による攻撃です。',
    //       url: 'https://news.yahoo.co.jp/byline/obiekt/20190719-00134800/',
    //       urlToImage:
    //         'https://rpr.c.yimg.jp/amd/20190719-00134800-roupeiro-000-2-view.jpg',
    //       publishedAt: '2019-07-18T23:39:00Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'Golfdigest.co.jp' },
    //       author: 'GDO編集部',
    //       title:
    //         '3度の3パットも首位とは5打差 松山英樹はバーディで締めくくり - ゴルフダイジェスト・オンライン',
    //       description:
    //         '◇メジャー第4戦◇全英オープン 初日（18日）◇ロイヤルポートラッシュ（北アイルランド）◇7344yd（パー71） 天候次第で何が起こるか分からないのがリンクスコース。松山英樹は首位と5打差、イーブンパー42位で終えた初日を「悪くはない」と受け止めた。 序盤はグリーン上で苦しんだ。前日、雨風の中で最終調整を終え、「一番荒れているときに回ってしまって、そのイメージが少し残った」と、パッティングが強めに入ってしまう傾向。「思ったよりスピードがあった」と、1、4、6番でファーストパットをそれぞれ1～1.5mオーバーさせ…',
    //       url: 'https://news.golfdigest.co.jp/news/pga/article/100687/1/',
    //       urlToImage: 'https://i.gimg.jp/cmsimg/214952.jpg',
    //       publishedAt: '2019-07-18T22:34:27Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'Nikkei.com' },
    //       author: '日本経済新聞社',
    //       title:
    //         '米、他国船舶は護衛せず 有志連合で米政府高官（写真＝ＡＰ） - 日本経済新聞',
    //       description:
    //         '【ワシントン=永沢毅】米国防総省高官は18日、ホルムズ海峡近辺を航行する船舶の安全確保のための有志連合構想を巡り「米国は他国の船を護衛しない」との原則を明らかにした。自国の船を護衛するかどうかは参加',
    //       url: 'https://www.nikkei.com/article/DGXMZO47519040Z10C19A7000000/',
    //       urlToImage:
    //         'https://article-image-ix.nikkei.com/https%3A%2F%2Fimgix-proxy.n8s.jp%2FDSXMZO4751902019072019000001-PB1.jpg?auto=format%2Ccompress&ch=Width%2CDPR&fit=max&ixlib=java-1.1.1&s=ad10250409e13f645b405ef5f7772a95',
    //       publishedAt: '2019-07-18T22:30:00Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'Atmarkit.co.jp' },
    //       author: null,
    //       title:
    //         'トヨタが考える東京五輪のラストワンマイルモビリティ、最高速度は時速19km (1/2) - ＠IT MONOist',
    //       description:
    //         'トヨタ自動車は「東京2020オリンピック・パラリンピック競技大会」をサポートするために開発した専用モビリティ「APM」を発表。高齢者や障害者、妊娠中の女性や幼児などの来場者が、競技会場のセキュリティゲートから観客席入り口までといった“ラストワンマイル”の移動を快適に行えるようにする車両として開発された。',
    //       url:
    //         'https://monoist.atmarkit.co.jp/mn/articles/1907/19/news042.html',
    //       urlToImage:
    //         'https://image.itmedia.co.jp/mn/articles/1907/19/cover_news042.jpg',
    //       publishedAt: '2019-07-18T22:30:00Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'Ismedia.jp' },
    //       author: null,
    //       title:
    //         '北朝鮮も中国も…アメリカの外交は結局「トランプ再選」の策略だった（海野 素央） @gendai_biz - 現代ビジネス',
    //       description:
    //         '先月末、日本で主要20カ国・地域首脳会議（G20サミット）が開催されている最中、米国では2日間にわたり、2020年米大統領選挙に向けた民主党候補による最初のテレビ討論会が行われていました。',
    //       url: 'https://gendai.ismedia.jp/articles/-/65925',
    //       urlToImage:
    //         'https://gendai.ismedia.jp/mwimgs/7/b/-/img_7b4dd9fdfa82f11b1d174f879f39399d45000.jpg',
    //       publishedAt: '2019-07-18T21:10:12Z',
    //       content: null
    //     },
    //     {
    //       source: { id: null, name: 'Nikkei.com' },
    //       author: '日本経済新聞社',
    //       title: 'サンマ漁獲、数量制限で合意 中国の乱獲に歯止め - 日本経済新聞',
    //       description:
    //         '日本や中国、台湾など8カ国・地域がサンマの資源管理を話し合う「北太平洋漁業委員会」の年次会合が18日閉幕した。資源保護のため、漁獲枠を年55万6250トン、うち公海を年33万トンに設定することで各国',
    //       url: 'https://www.nikkei.com/article/DGXMZO47516640Z10C19A7EA1000/',
    //       urlToImage:
    //         'https://article-image-ix.nikkei.com/https%3A%2F%2Fimgix-proxy.n8s.jp%2FDSXMZO4482470015052019000002-PB1.jpg?auto=format%2Ccompress&ch=Width%2CDPR&fit=max&ixlib=java-1.1.1&s=978421a8586dc535cdf8598ea640551a',
    //       publishedAt: '2019-07-18T15:16:00Z',
    //       content:
    //         '2019/7/19 0:16\r\n33\r\n818556250332\r\nEEZ201844\r\n2020163\r\n2019/5/13 2:00\r\n42019/7/5 17:38'
    //     },
    //     {
    //       source: { id: null, name: 'Coconutsjapan.com' },
    //       author: null,
    //       title:
    //         '嵐・松本潤、ツアーに麺を持参「本当申し訳ない」驚きの理由にスタジオ歓声 #VS嵐 が話題 - COCONUTS',
    //       description:
    //         '7月18日に放送のバラエティ番組「VS嵐」（フジテレビ系）。ゲストは７月１９日公開の映画「東京喰種 トーキョーグール【S】」の出演陣、プラスワンゲストは、お笑い芸人のかまいたちのお二人でした。この放送で嵐メンバー５人全員が明かした食へのこだわりに注目が集まっています。 大野「忍びの国」で経験した恥ずかしい3分間？ 番組では、映画「東京喰種 トーキョーグール【S】」が、多くのCG撮影をとり入れている',
    //       url:
    //         'https://coconutsjapan.com/entertainment/vsarashi-matsumotozyun-tokyoguru/15981/',
    //       urlToImage:
    //         'https://i2.wp.com/coconutsjapan.com/wp-content/uploads/2018/08/clouds-3562230_640.jpg?fit=640%2C426&ssl=1',
    //       publishedAt: '2019-07-18T14:00:00Z',
    //       content: null
    //     }
    //   ]
    // }
    return {
      newsData: newsData.articles
    }
  }
}
</script>

<style lang="sass" scoped>
.container
  margin: 0 auto
  padding: 2rem
  min-height: 100vh
.categories
  Width: 100%
  display: flex
  justify-content: flex-start
  font-size: 1.4rem
  .category-link
    display: inline-flex
    .category
      padding-right: 0.7rem
      padding-bottom: 0.7rem
    .divide
      padding-right: 0.7rem
.card-image
  overflow: hidden
  .image
    img
      object-fit: cover
.content-title
  height: 50px
  font-weight: bold
  overflow: hidden
  text-overflow: ellipsis
</style>
