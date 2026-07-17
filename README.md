[Uploading language_game_mockup.html…]()
# LingoQuest
LingoQuest is a gamified AI English WeChat Mini-Program. It turns learning into an RPG adventure with voice PK, streaks, and GPT-powered feedback for effortless practice.

<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{--g1:#FF6B35;--g2:#F7C59F;--g3:#1B4332;--g4:#52B788;--g5:#E9C46A;--g6:#264653}
body{font-family:var(--font-sans)}
.phone{width:340px;margin:0 auto;background:var(--color-background-secondary);border-radius:32px;border:1.5px solid var(--color-border-secondary);overflow:hidden;min-height:640px;display:flex;flex-direction:column}
.statusbar{height:28px;background:#1a1a2e;display:flex;align-items:center;justify-content:space-between;padding:0 20px}
.statusbar span{color:#fff;font-size:11px}
.screen{flex:1;overflow:hidden;position:relative}
.page{display:none;flex-direction:column;height:100%;overflow-y:auto}
.page.active{display:flex}

.home-header{background:#1a1a2e;padding:16px 16px 12px;color:#fff}
.home-header .greeting{font-size:12px;color:#aaa;margin-bottom:2px}
.home-header .username{font-size:16px;font-weight:500}
.xp-bar-wrap{margin-top:10px;background:#333;border-radius:6px;height:8px;overflow:hidden}
.xp-bar{height:100%;background:var(--g1);border-radius:6px;width:62%}
.xp-label{display:flex;justify-content:space-between;margin-top:4px}
.xp-label span{font-size:10px;color:#888}

.streak-row{display:flex;gap:8px;padding:12px 16px}
.streak-card{flex:1;background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:12px;padding:10px 8px;text-align:center}
.streak-card .num{font-size:20px;font-weight:500;color:var(--g1)}
.streak-card .lbl{font-size:10px;color:var(--color-text-secondary);margin-top:2px}

.section-title{font-size:13px;font-weight:500;color:var(--color-text-secondary);padding:4px 16px 8px;letter-spacing:.5px}

.task-list{padding:0 16px;display:flex;flex-direction:column;gap:8px}
.task-item{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:14px;padding:12px 14px;display:flex;align-items:center;gap:12px;cursor:pointer;transition:background .15s}
.task-item:active{background:var(--color-background-secondary)}
.task-icon{width:40px;height:40px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0}
.task-icon.word{background:#FFF0E8}
.task-icon.listen{background:#E8F5E9}
.task-icon.talk{background:#E8EEF8}
.task-body{flex:1}
.task-name{font-size:14px;font-weight:500;color:var(--color-text-primary)}
.task-sub{font-size:11px;color:var(--color-text-secondary);margin-top:2px}
.task-prog{margin-top:6px;background:var(--color-background-secondary);border-radius:4px;height:4px;overflow:hidden}
.task-prog .bar{height:100%;border-radius:4px}
.bar.w0{background:#FF6B35;width:0%}
.bar.w40{background:#FF6B35;width:40%}
.bar.w100{background:#52B788;width:100%}
.task-badge{font-size:10px;font-weight:500;padding:3px 8px;border-radius:8px}
.badge-done{background:#E8F5E9;color:#1B4332}
.badge-go{background:#FFF0E8;color:#8B3A00}

.voice-btn-wrap{padding:16px;margin-top:4px}
.voice-btn{width:100%;background:#1a1a2e;color:#fff;border:none;border-radius:14px;padding:14px;font-size:14px;font-weight:500;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px}
.mic-ring{width:16px;height:16px;border-radius:50%;border:2px solid var(--g1);display:flex;align-items:center;justify-content:center}
.mic-dot{width:6px;height:6px;border-radius:50%;background:var(--g1)}

.map-container{background:#1a1a2e;flex:1;padding:16px;position:relative;overflow:hidden}
.map-title{color:#fff;font-size:15px;font-weight:500;margin-bottom:16px}
.map-path{position:relative;padding-bottom:20px}
.map-node{display:flex;flex-direction:column;align-items:center;margin-bottom:32px;position:relative}
.map-node::after{content:'';position:absolute;bottom:-28px;left:50%;width:2px;height:24px;background:#333;transform:translateX(-50%)}
.map-node:last-child::after{display:none}
.node-circle{width:56px;height:56px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:22px;border:2.5px solid transparent;cursor:pointer}
.node-done{background:#52B788;border-color:#1B4332}
.node-active{background:#FF6B35;border-color:#8B3A00;box-shadow:0 0 0 4px rgba(255,107,53,.25)}
.node-locked{background:#2a2a3e;border-color:#333}
.node-label{color:#ccc;font-size:11px;margin-top:6px;text-align:center;max-width:70px}
.node-label.done{color:#52B788}
.node-label.active{color:#FF6B35}
.map-nodes-row{display:flex;justify-content:space-around;margin-bottom:12px}

.arena-header{background:#1a1a2e;padding:16px;color:#fff}
.arena-title{font-size:15px;font-weight:500;margin-bottom:12px}
.rank-row{display:flex;gap:8px}
.rank-card{flex:1;background:#252535;border-radius:10px;padding:10px 8px;text-align:center}
.rank-card .rn{font-size:18px;font-weight:500;color:var(--g5)}
.rank-card .rl{font-size:10px;color:#888}
.leaderboard{padding:12px 16px;flex:1}
.lb-item{display:flex;align-items:center;gap:12px;padding:10px 0;border-bottom:0.5px solid var(--color-border-tertiary)}
.lb-rank{width:24px;font-size:13px;font-weight:500;color:var(--color-text-secondary);text-align:center}
.lb-rank.top{color:var(--g5)}
.lb-avatar{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:500;color:#fff;flex-shrink:0}
.lb-name{flex:1;font-size:13px;color:var(--color-text-primary)}
.lb-score{font-size:13px;font-weight:500;color:var(--g1)}

.bag-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:10px;padding:16px}
.bag-card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:14px;padding:14px;text-align:center;cursor:pointer}
.bag-emoji{font-size:28px;margin-bottom:6px}
.bag-name{font-size:12px;font-weight:500;color:var(--color-text-primary)}
.bag-count{font-size:11px;color:var(--color-text-secondary);margin-top:2px}

.profile-header{background:#1a1a2e;padding:20px 16px;color:#fff;text-align:center}
.avatar-big{width:64px;height:64px;border-radius:50%;background:var(--g1);margin:0 auto 8px;display:flex;align-items:center;justify-content:center;font-size:26px}
.prof-name{font-size:16px;font-weight:500}
.prof-sub{font-size:12px;color:#aaa;margin-top:2px}
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;padding:12px 16px}
.cal-day{aspect-ratio:1;border-radius:4px;background:var(--color-background-secondary)}
.cal-day.done{background:#52B788}
.cal-day.today{background:var(--g1)}
.achievement-list{padding:0 16px;display:flex;flex-direction:column;gap:8px}
.ach-item{display:flex;align-items:center;gap:12px;background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:12px;padding:10px 14px}
.ach-icon{font-size:20px;width:36px;text-align:center}
.ach-body .ach-name{font-size:13px;font-weight:500;color:var(--color-text-primary)}
.ach-body .ach-desc{font-size:11px;color:var(--color-text-secondary)}

.navbar{height:58px;background:var(--color-background-primary);border-top:0.5px solid var(--color-border-tertiary);display:flex;align-items:stretch}
.nav-item{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;cursor:pointer;border:none;background:transparent;padding:0;transition:opacity .15s}
.nav-item .nav-icon{width:20px;height:20px;border-radius:6px;background:var(--color-background-secondary);display:flex;align-items:center;justify-content:center;font-size:11px}
.nav-item.active .nav-icon{background:#1a1a2e}
.nav-item .nav-lbl{font-size:9px;color:var(--color-text-secondary)}
.nav-item.active .nav-lbl{color:#1a1a2e;font-weight:500}
</style>

<h2 class="sr-only">语言学习小程序游戏设计原型，包含首页、任务、地图、竞技场、背包和我的页面</h2>

<div style="padding:12px 0">
<div class="phone">
  <div class="statusbar">
    <span>9:41</span>
    <span>LingoQuest</span>
    <span>●●●</span>
  </div>

  <div class="screen">

    <div class="page active" id="page-home">
      <div class="home-header">
        <div class="greeting">早上好 👋</div>
        <div class="username">小明同学</div>
        <div class="xp-bar-wrap"><div class="xp-bar"></div></div>
        <div class="xp-label"><span>Lv.12 词语骑士</span><span>620 / 1000 XP</span></div>
      </div>
      <div class="streak-row">
        <div class="streak-card"><div class="num">🔥 14</div><div class="lbl">连续打卡天</div></div>
        <div class="streak-card"><div class="num">⭐ 3</div><div class="lbl">今日星星</div></div>
        <div class="streak-card"><div class="num">🎯 2/3</div><div class="lbl">今日完成</div></div>
      </div>
      <div class="section-title">今日任务 · 预计 10 分钟</div>
      <div class="task-list">
        <div class="task-item">
          <div class="task-icon word">🃏</div>
          <div class="task-body">
            <div style="display:flex;justify-content:space-between;align-items:center">
              <div class="task-name">单词关 · 消消乐</div>
              <span class="task-badge badge-done">已完成</span>
            </div>
            <div class="task-sub">今日单词：20个</div>
            <div class="task-prog"><div class="bar w100"></div></div>
          </div>
        </div>
        <div class="task-item">
          <div class="task-icon listen">🔊</div>
          <div class="task-body">
            <div style="display:flex;justify-content:space-between;align-items:center">
              <div class="task-name">听力关 · 听音选图</div>
              <span class="task-badge badge-done">已完成</span>
            </div>
            <div class="task-sub">完成 5/5 题</div>
            <div class="task-prog"><div class="bar w100"></div></div>
          </div>
        </div>
        <div class="task-item" style="border:1.5px solid #FF6B35">
          <div class="task-icon talk">💬</div>
          <div class="task-body">
            <div style="display:flex;justify-content:space-between;align-items:center">
              <div class="task-name">对话关 · 剧情选择</div>
              <span class="task-badge badge-go">进行中</span>
            </div>
            <div class="task-sub">场景：咖啡店对话</div>
            <div class="task-prog"><div class="bar w40"></div></div>
          </div>
        </div>
      </div>
      <div class="voice-btn-wrap">
        <button class="voice-btn" onclick="alert('🎤 语音练习启动！\n\n可识别发音并打分，支持：\n· 跟读练习\n· 自由对话\n· 发音评测')">
          <div class="mic-ring"><div class="mic-dot"></div></div>
          开始语音练习
        </button>
      </div>
    </div>

    <div class="page" id="page-map">
      <div class="map-container">
        <div class="map-title">冒险地图 · 英语王国</div>
        <div style="display:flex;flex-direction:column;align-items:center">
          <div class="map-node">
            <div class="node-circle node-done">🏠</div>
            <div class="node-label done">新手村</div>
          </div>
          <div class="map-node">
            <div class="node-circle node-done">🌲</div>
            <div class="node-label done">迷雾森林</div>
          </div>
          <div class="map-node" style="margin-bottom:32px">
            <div class="node-circle node-active">⚔️</div>
            <div class="node-label active">龙穴关卡</div>
          </div>
          <div class="map-node">
            <div class="node-circle node-locked">🏰</div>
            <div class="node-label">冰雪城堡</div>
          </div>
          <div class="map-node">
            <div class="node-circle node-locked">🌋</div>
            <div class="node-label">火焰山脉</div>
          </div>
          <div class="map-node" style="margin-bottom:0">
            <div class="node-circle node-locked">👑</div>
            <div class="node-label">英语王都</div>
          </div>
        </div>
      </div>
    </div>

    <div class="page" id="page-arena">
      <div class="arena-header">
        <div class="arena-title">竞技场 · 每日PK</div>
        <div class="rank-row">
          <div class="rank-card"><div class="rn">🥈 银牌</div><div class="rl">当前段位</div></div>
          <div class="rank-card"><div class="rn">142</div><div class="rl">全国排名</div></div>
          <div class="rank-card"><div class="rn">+38</div><div class="rl">今日积分</div></div>
        </div>
      </div>
      <div class="leaderboard">
        <div class="section-title" style="padding-left:0">好友排行榜</div>
        <div class="lb-item">
          <div class="lb-rank top">🥇</div>
          <div class="lb-avatar" style="background:#FF6B35">王</div>
          <div class="lb-name">王小花</div>
          <div class="lb-score">2,840</div>
        </div>
        <div class="lb-item">
          <div class="lb-rank top">🥈</div>
          <div class="lb-avatar" style="background:#52B788">李</div>
          <div class="lb-name">李大明</div>
          <div class="lb-score">2,610</div>
        </div>
        <div class="lb-item" style="background:var(--color-background-secondary);border-radius:8px;padding:10px 8px;border:1.5px solid #FF6B35;margin-top:4px">
          <div class="lb-rank top">🥉</div>
          <div class="lb-avatar" style="background:#264653">明</div>
          <div class="lb-name">小明（我）</div>
          <div class="lb-score">2,480</div>
        </div>
        <div class="lb-item">
          <div class="lb-rank">4</div>
          <div class="lb-avatar" style="background:#E9C46A;color:#333">张</div>
          <div class="lb-name">张三丰</div>
          <div class="lb-score">2,210</div>
        </div>
      </div>
      <div style="padding:0 16px 16px">
        <button class="voice-btn" onclick="alert('⚔️ 发起语音PK挑战！\n\n随机匹配一位好友\n用语音朗读来决胜负')">
          <div class="mic-ring"><div class="mic-dot"></div></div>
          语音PK 开战
        </button>
      </div>
    </div>

    <div class="page" id="page-bag">
      <div class="home-header" style="padding-bottom:14px">
        <div class="username">我的背包</div>
        <div style="color:#aaa;font-size:11px;margin-top:4px">收集到 38 / 120 张单词卡</div>
      </div>
      <div class="bag-grid">
        <div class="bag-card"><div class="bag-emoji">📗</div><div class="bag-name">基础词卡</div><div class="bag-count">20 张</div></div>
        <div class="bag-card"><div class="bag-emoji">🔮</div><div class="bag-name">魔法道具</div><div class="bag-count">5 个</div></div>
        <div class="bag-card"><div class="bag-emoji">⚡</div><div class="bag-name">复习加速</div><div class="bag-count">×3</div></div>
        <div class="bag-card"><div class="bag-emoji">🛡️</div><div class="bag-name">错误保护</div><div class="bag-count">×2</div></div>
        <div class="bag-card"><div class="bag-emoji">🌟</div><div class="bag-name">稀有词卡</div><div class="bag-count">3 张</div></div>
        <div class="bag-card" style="border:1px dashed var(--color-border-secondary);background:transparent"><div class="bag-emoji" style="opacity:.3">🔒</div><div class="bag-name" style="color:var(--color-text-secondary)">待解锁</div><div class="bag-count">Lv.15</div></div>
      </div>
    </div>

    <div class="page" id="page-me">
      <div class="profile-header">
        <div class="avatar-big">🧑</div>
        <div class="prof-name">小明同学</div>
        <div class="prof-sub">词语骑士 · 连续打卡 14 天</div>
      </div>
      <div class="section-title" style="margin-top:12px">本月打卡记录</div>
      <div class="cal-grid">
        <div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div>
        <div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div><div class="cal-day done"></div>
        <div class="cal-day today"></div><div class="cal-day"></div><div class="cal-day"></div><div class="cal-day"></div><div class="cal-day"></div><div class="cal-day"></div><div class="cal-day"></div>
      </div>
      <div class="section-title" style="margin-top:4px">我的成就</div>
      <div class="achievement-list">
        <div class="ach-item"><div class="ach-icon">🔥</div><div class="ach-body"><div class="ach-name">坚持不懈</div><div class="ach-desc">连续打卡 14 天</div></div></div>
        <div class="ach-item"><div class="ach-icon">📖</div><div class="ach-body"><div class="ach-name">博学多才</div><div class="ach-desc">掌握 500 个单词</div></div></div>
        <div class="ach-item"><div class="ach-icon">🎤</div><div class="ach-body"><div class="ach-name">初级演说家</div><div class="ach-desc">完成 10 次语音练习</div></div></div>
      </div>
      <div style="height:12px"></div>
    </div>

  </div>

  <div class="navbar">
    <button class="nav-item active" onclick="go('home',this)">
      <div class="nav-icon" style="font-size:13px">🏠</div>
      <span class="nav-lbl">首页</span>
    </button>
    <button class="nav-item" onclick="go('map',this)">
      <div class="nav-icon" style="font-size:13px">🗺</div>
      <span class="nav-lbl">地图</span>
    </button>
    <button class="nav-item" onclick="go('arena',this)">
      <div class="nav-icon" style="font-size:13px">⚔️</div>
      <span class="nav-lbl">竞技场</span>
    </button>
    <button class="nav-item" onclick="go('bag',this)">
      <div class="nav-icon" style="font-size:13px">🎒</div>
      <span class="nav-lbl">背包</span>
    </button>
    <button class="nav-item" onclick="go('me',this)">
      <div class="nav-icon" style="font-size:13px">👤</div>
      <span class="nav-lbl">我的</span>
    </button>
  </div>
</div>
</div>

<script>
function go(id,el){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  el.classList.add('active');
}
</script>

## AI Integration
- **GPT-5.6 API**: Powers real-time speaking feedback, grammar correction, and dynamic RPG quest generation based on user proficiency.
- **Codex**: Used to auto-generate personalized vocabulary quizzes and parse user error patterns for adaptive difficulty adjustment.
