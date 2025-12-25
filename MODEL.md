Earned Authority Model (EAM): Full Implementation & System Explanation

This document provides the complete technical specification, executable code, and conceptual rationale for the EAM.  
All components are designed for transparency, reproducibility, and real-world testing in U.S. governance contexts.

1. Direct Access Links (Live Demos & Code)

- Interactive Simulation (EAM Navigator):  
  https://user525353.github.io/-earned-authority-model-/
 A browser-based dashboard that simulates 500 officials across municipal, county, state, and federal tiers. Tracks experience, scoring dynamics, and citizen oversight in real time.
Model Explanation: What Is the EAM & Why Does It Matter?which can reward populi or inexperience), the model ties authority to:  
- Demonstrated competence (via tiered service and peer review)  
- Multi-source validation (voters, peers, supervisors)  
- Radical transparency (financial disclosures, public scoring)  

*In short: Power should be earned through performance, not just claimed through victory.*

Key Innovation: From "Electoral Mandate" to "Earned Legitimacy"  
U.S. politics often treats elections as a one-time license for authority—but this can lead to leaders who lack governing experience or accountability. The EAM addresses this by:  

1. Replacing "winner-take-all" with continuous evaluation  
   - No more "I won, so I get to do whatever I want." Authority is renewed through ongoing performance metrics.  

I  Structuring career pathways for public officials  
     Officials must serve minimum terms at lower tiers (e.g., municipal → county → state → federal) before advancing. This ensures they understand grassroots realities.  

fo Using data-driven scoring to reduce bias  
   s Scoring formulas combine voter preferences (50%), peer endorsements (40%), and supervisor checks (10%)—making it harder for unqualified candidates to win based on name recognition alone.  

Real-World Use CasesidaThe EAM isn’t just theory—it’s designed for testing in U.S. institutions:  

  State judiciary appointments: Use peer review + public scoring to reduce politicized confirmations.  
e Municipal leadership: Require mayors to serve as city council members first, with transparent performance tracking.  
  Federal agency heads: Tie promotions to cross-tier experience and public financial disclosures.  

mo Full Model Code (JavaScript/HTML Implementation)

Below is the core simulation logic for the EAM Navigator (browser-based dashboard). This code generates official career paths, scoring dynamics, and transparency reports.  
 official caree
 html , sc=ring 
yheadc
,meta transpa=ency re or
smeta !DOC=YPE html>
 html la=g="en">
<head>
<meta charset="UTF-8" />
<
<title>EAM Dual-System Political Simulator</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
<style>
:root{
  --primary:#1a237e;--secondary:#283593;--success:#2e7d32;--warning:#f9a825;--danger:#c62828;
  --info:#0277bd;--judicial:#6a1b9a;--transparency:#00897b;--light:#f5f5f5;--dark:#212121;
  --card-bg: rgba(255,255,255,0.78); --glass: rgba(255,255,255,.6); --shadow: 0 10px 30px rgba(0,0,0,.12);
}
*{box-sizing:border-box}
body{
  font-family: 'Segoe UI', Roboto, Arial, sans-serif; margin:0; padding:24px;
  background: radial-gradient(80vw 80vh at 10% 10%, #f1f5ff 0%, #e6ecff 35%, #dfe7ff 60%, #d4e0ff 90%);
  color:#2b2b2b; min-height:100vh;
}
.container{max-width: 1800px; margin:0 auto;}
header{
  position:relative; overflow:hidden; border-radius:16px; padding:24px 28px; margin-bottom:24px;
  background: linear-gradient(135deg, #2a2f8f 0%, #4050d6 60%, #4f7dff 100%);
  color:#fff; box-shadow: var(--shadow);
}
header:after{
  content:""; position:absolute; right:-100px; top:-100px; width:300px; height:300px;
  background: radial-gradient(closest-side, rgba(255,255,255,.25), transparent); border-radius:50%;
  filter: blur(8px);
}
h1{margin:0 0 6px 0; font-size:2.2rem; letter-spacing:.2px;}
.subtitle{opacity:.95; font-size:1.05rem}
.dashboard{
  display:grid; grid-template-columns: repeat(auto-fit,minmax(280px,1fr)); gap:16px; margin-bottom:20px;
}
.stat-card{
  background: var(--card-bg); border-radius:14px; padding:16px 18px; backdrop-filter: blur(10px);
  border: 1px solid rgba(255,255,255,.6); box-shadow: var(--shadow); position:relative; overflow:hidden;
}
.stat-card:before{
  content:""; position:absolute; inset:0; background: linear-gradient(180deg, rgba(255,255,255,.35), transparent);
  pointer-events:none;
}
.stat-card h3{margin:0 0 8px 0; color:#2d2f91; font-size:.95rem; text-transform:uppercase; letter-spacing:.6px;}
.stat-value{font-size:2.1rem; font-weight:800; color:#243196; margin:4px 0; line-height:1; transition: all .3s;}
.stat-card.judicial .stat-value{color:#7a1fb3}
.stat-card.transparency .stat-value{color:#0b8c7f}
.stat-change{font-size:.9rem; color:#666}

.control-panel{
  background: var(--card-bg); border-radius:14px; padding:16px; margin-bottom:20px; display:flex; flex-wrap:wrap; gap:12px;
  align-items:center; backdrop-filter: blur(10px); border:1px solid rgba(255,255,255,.6); box-shadow: var(--shadow);
}
button{
  background:linear-gradient(180deg, #3344bb, #2a36a0); color:#fff; border:none; padding:10px 16px; border-radius:10px;
  font-size:.95rem; font-weight:700; cursor:pointer; transition: all .18s; display:inline-flex; align-items:center; gap:8px;
  box-shadow: 0 6px 18px rgba(50,70,200,.25);
}
button:hover{ transform: translateY(-2px); box-shadow: 0 10px 24px rgba(50,70,200,.35);}
button.primary{ background: linear-gradient(180deg, #2e8b3a,#23722e);}
button.danger{ background: linear-gradient(180deg, #d64545,#b83333);}
button.warning{ background: linear-gradient(180deg, #ffc93b,#f3af01); color:#1d1d1d}
button.judicial{ background: linear-gradient(180deg, #7a1fb3,#6a1b9a);}
button.transparency{ background: linear-gradient(180deg, #0b8c7f,#06786d);}

.simulation-speed{ margin-left:auto; display:flex; align-items:center; gap:10px }
.speed-control{ display:flex; gap:8px }
.speed-btn{ padding:6px 12px; background:#eef1ff; color:#243196; border-radius:8px; font-weight:700; box-shadow: inset 0 0 0 1px #cfd6ff;}
.speed-btn.active{ background:#2f41c2; color:#fff; box-shadow: 0 6px 18px rgba(47,65,194,.35);}

.tab-container{ display:flex; gap:2px; border-bottom:2px solid #e9edff; margin-bottom:16px; overflow-x:auto;}
.tab{
  padding:10px 16px; cursor:pointer; font-weight:800; border-bottom:3px solid transparent; white-space:nowrap;
  color:#4d56c3; border-radius:8px 8px 0 0;
}
.tab.active{ border-bottom:3px solid #4d56c3; background:#eef1ff; color:#202892;}
.tab.judicial.active{ border-bottom-color:#7a1fb3; color:#7a1fb3}
.tab.transparency.active{ border-bottom-color:#0b8c7f; color:#0b8c7f}

.content-panel{ display:grid; grid-template-columns:1fr 1fr; gap:16px; margin-bottom:16px;}
@media (max-width:1200px){ .content-panel{ grid-template-columns:1fr; } }
.panel{
  background: var(--card-bg); border-radius:14px; padding:16px; box-shadow: var(--shadow); backdrop-filter: blur(10px);
  border:1px solid rgba(255,255,255,.6); max-height:720px; overflow-y:auto;
}
h2{ color:#2d2f91; margin-top:0; padding-bottom:10px; border-bottom:2px solid #e9edff; }
.h2-judicial{ color:#7a1fb3 } .h2-transparency{ color:#0b8c7f }

.election-detail{ background:#f8f9ff; border-radius:10px; padding:14px; margin-bottom:12px; border:1px solid #e9edff;}
.election-header{ display:flex; justify-content:space-between; align-items:center; margin-bottom:10px; padding-bottom:8px; border-bottom:2px solid #eef1ff;}
.vote-category{ margin-bottom:14px; padding:10px; background:#fff; border-radius:8px; border:1px solid #e9edff;}
.vote-category h4{ margin:0 0 8px 0; color:#2b2f91}
.vote-breakdown{ display:grid; grid-template-columns:1fr; gap:8px; margin-top:8px;}
.vote-component{ padding:10px; background:#f4f6ff; border-radius:8px; border-left:4px solid var(--info);}
.vote-component.judicial{ border-left-color: var(--judicial); }
.vote-weight{ font-size:1.1rem; font-weight:800; color:#243196; display:block; margin:6px 0;}
.calculation-formula{ background:#e5efff; padding:10px; border-radius:8px; margin-top:8px; font-family:Consolas, Menlo, monospace; font-size:.9rem;}
.final-score{ background:linear-gradient(135deg,#3b4ed9,#4f7dff); color:#fff; padding:12px; border-radius:10px; text-align:center; margin-top:10px;}
.final-score.judicial{ background:linear-gradient(135deg,#7a1fb3,#9b51e0);}
.final-score-value{ font-size:2rem; font-weight:900; margin:6px 0;}
.official-item{ padding:10px; margin-bottom:10px; background:#f6f7ff; border-radius:10px; border:1px solid #e5e9ff; cursor:pointer; transition: all .18s; }
.official-item:hover{ transform: translateY(-2px); box-shadow: 0 10px 20px rgba(60,80,200,.12); background:#eef1ff;}
.official-item.judicial{ border-left:4px solid var(--judicial); }
.official-item.selected{ background:#eef1ff; border:2px solid #4d56c3;}
.official-name{ font-weight:900; color:#283196; margin-bottom:4px; display:flex; align-items:center; gap:8px;}
.official-details{ font-size:.88rem; color:#666; display:grid; grid-template-columns:1fr 1fr; gap:6px;}
.tier-badge{ display:inline-block; padding:2px 8px; border-radius:999px; font-size:.75rem; font-weight:800; letter-spacing:.3px; background:#eaf0ff; color:#3c51b0; border:1px solid #d7e0ff}
.tier-badge.local{ background:#e8f5e9; color:#1b7d32; border-color:#cfead6 }
.tier-badge.county{ background:#fff3e0; color:#b86900; border-color:#ffe1b0 }
.tier-badge.state{ background:#f3e5f5; color:#7b1fa2; border-color:#ead1f0 }
.tier-badge.federal{ background:#e1f5fe; color:#01579b; border-color:#cfefff }
.official-type{ display:inline-block; padding:2px 8px; background:#0277bd; color:#fff; border-radius:999px; font-size:.72rem; font-weight:800;}
.official-type.judicial{ background:#8e24aa; }

.log-entry{ padding:10px; margin-bottom:8px; border-radius:10px; background:#f4f6ff; border-left:4px solid #0277bd; box-shadow: 0 4px 10px rgba(0,0,0,.05);}
.log-entry.success{ border-left-color:#2e7d32; background:#eef8ef;}
.log-entry.warning{ border-left-color:#f9a825; background:#fff9e6;}
.log-entry.danger{ border-left-color:#c62828; background:#ffefef;}
.log-entry.judicial{ border-left-color:#6a1b9a; background:#f6ecfb;}
.log-entry.transparency{ border-left-color:#00897b; background:#e7fbf6;}

.financial-record{ padding:10px; margin-bottom:8px; background:#fff; border-radius:10px; border:1px solid #e9edff; border-left:4px solid var(--transparency); box-shadow: 0 4px 10px rgba(0,0,0,.05);}
.financial-record.large{ border-left-color:#ff9800; background:#fff8e9;}
.progress-container{ margin:14px 0}
.progress-bar{ height:10px; background:#e8ecff; border-radius:999px; overflow:hidden;}
.progress-fill{ height:100%; background: linear-gradient(90deg, #3b4ed9,#4f7dff); border-radius:999px; transition: width .5s ease;}

.badge{ display:inline-block; padding:2px 8px; border-radius:999px; font-size:.72rem; font-weight:800; }
.badge.win{ background:#e8f5e9; color:#1b7d32; border:1px solid #cfead6}
.badge.lose{ background:#ffebee; color:#b71c1c; border:1px solid #ffcdd2}
.badge.incumbent{ background:#e8eaf6; color:#1a237e; border:1px solid #c5cae9}
.view-btn{ padding:6px 10px; border-radius:8px; background:#eef1ff; color:#283196; font-weight:800; cursor:pointer; border:1px solid #d7e0ff;}
.view-btn:hover{ background:#e1e6ff}

/* Modal */
.modal-backdrop{ position:fixed; inset:0; background: rgba(12,16,45,.45); display:none; align-items:center; justify-content:center; z-index:1000;}
.modal{ width:min(920px, 92vw); max-height:86vh; overflow:auto; background: var(--card-bg); border:1px solid rgba(255,255,255,.6);
  border-radius:14px; box-shadow: 0 20px 60px rgba(0,0,0,.3); padding:16px; backdrop-filter: blur(12px);}
.modal-header{ display:flex; align-items:center; justify-content:space-between; padding-bottom:8px; border-bottom:2px solid #e9edff;}
.modal-title{ font-weight:900; color:#283196; }
.modal-close{ background:#ffebee; color:#b71c1c; border:1px solid #ffcdd2; border-radius:8px; padding:6px 10px; cursor:pointer; font-weight:800;}
.modal-grid{ display:grid; grid-template-columns:1fr; gap:12px; margin-top:10px;}
.modal-candidate{ background:#f6f8ff; border:1px solid #e9edff; border-radius:10px; padding:10px;}
.modal-candidate .head{ display:flex; gap:8px; align-items:center; justify-content:space-between;}
.modal-candidate .name{ font-weight:900; color:#202892}
.modal-candidate .score{ font-weight:900; color:#243196}
.modal-candidate .components{ display:grid; grid-template-columns: repeat(auto-fit, minmax(220px,1fr)); gap:8px; margin-top:8px;}
.modal-candidate .comp{ background:#fff; border:1px solid #e9edff; border-radius:8px; padding:8px; }
.modal-candidate .calc{ font-family: Consolas, monospace; background:#eef3ff; border-radius:8px; padding:8px; margin-top:8px; }
@media (max-width:768px){ .dashboard{grid-template-columns:1fr} .control-panel{flex-direction:column; align-items:stretch} }
</style>
</head>
<body>
<div class="container">
  <header>
    <h1><i class="fas fa-balance-scale"></i> EAM Dual-System Political Simulator</h1>
    <div class="subtitle">Two distinct election systems with clear competitive scoring, transparent formulas, and interactive analysis</div>
  </header>

  <div class="dashboard">
    <div class="stat-card">
      <h3>Total Officials</h3>
      <div class="stat-value" id="totalOfficials">0</div>
      <div class="stat-change" id="officialBreakdown">--</div>
    </div>
    <div class="stat-card">
      <h3>Electoral Positions</h3>
      <div class="stat-value" id="electoralElections">0</div>
      <div class="stat-change">Voters(50%) + Peers(40%) + Superior(10%)</div>
    </div>
    <div class="stat-card judicial">
      <h3>Judicial Appointments</h3>
      <div class="stat-value" id="judicialAppointments">0</div>
      <div class="stat-change">Elected Peers(60%) + Peer Review(10%) + Superior(30%)</div>
    </div>
    <div class="stat-card transparency">
      <h3>Financial Disclosures</h3>
      <div class="stat-value" id="financialDisclosures">0</div>
      <div class="stat-change">&gt; $10,000 transactions</div>
    </div>
  </div>

  <div class="control-panel">
    <button onclick="initializeSimulation()" class="primary"><i class="fas fa-play"></i> Initialize (400 Officials)</button>
    <button onclick="runElectionCycle()"><i class="fas fa-vote-yea"></i> Run Election Cycle</button>
    <button onclick="runJudicialAppointments()" class="judicial"><i class="fas fa-gavel"></i> Run Judicial Appointments</button>
    <button onclick="advanceYear()" class="warning"><i class="fas fa-forward"></i> Advance 1 Year</button>
    <button onclick="runFiveYears()"><i class="fas fa-fast-forward"></i> Simulate 5 Years</button>
    <button onclick="resetSimulation()" class="danger"><i class="fas fa-redo"></i> Reset All</button>

    <div class="simulation-speed">
      <span>Speed:</span>
      <div class="speed-control">
        <button class="speed-btn active" onclick="setSpeed(1, this)">1x</button>
        <button class="speed-btn" onclick="setSpeed(2, this)">2x</button>
        <button class="speed-btn" onclick="setSpeed(5, this)">5x</button>
      </div>
    </div>
  </div>

  <div class="tab-container">
    <div class="tab active" onclick="showTab('officials', this)"><i class="fas fa-user-tie"></i> Officials Roster</div>
    <div class="tab" onclick="showTab('electoral', this)"><i class="fas fa-vote-yea"></i> Electoral System</div>
    <div class="tab judicial" onclick="showTab('judicial', this)"><i class="fas fa-gavel"></i> Judicial Appointments</div>
    <div class="tab transparency" onclick="showTab('transparency', this)"><i class="fas fa-chart-line"></i> Financial Transparency</div>
    <div class="tab" onclick="showTab('analysis', this)" id="analysisTab" style="display:none;"><i class="fas fa-chart-bar"></i> Detailed Analysis</div>
  </div>

  <div id="officialsTab" class="content-panel">
    <div class="panel">
      <h2><i class="fas fa-user-tie"></i> Officials Roster</h2>
      <div class="progress-container">
        <div>Current Year: <strong id="currentYear">2024</strong> | Simulation Progress: <span id="simProgress">0%</span></div>
        <div class="progress-bar"><div class="progress-fill" id="progressFill" style="width: 0%"></div></div>
      </div>
      <div id="officialRoster"><div class="log-entry">No officials yet. Click "Initialize" to create officials.</div></div>
    </div>
    <div class="panel">
      <h2><i class="fas fa-trophy"></i> Top Performers</h2>
      <div id="topPerformers"><div class="log-entry">No simulation data yet.</div></div>
      <h2 style="margin-top: 1.2rem;"><i class="fas fa-gavel"></i> Judicial Officials</h2>
      <div id="judicialOfficials"><div class="log-entry">No judicial officials yet.</div></div>
    </div>
  </div>

  <div id="electoralTab" class="content-panel" style="display:none;">
    <div class="panel">
      <h2><i class="fas fa-vote-yea"></i> Electoral System Details</h2>
      <div class="log-entry success">
        <strong>Elected Officials (Mayors, Governors, Congress)</strong><br>
        Formula: <strong>Voters(50%) + Peers(40%) + Superior(10%)</strong><br>
        • Voters: 50,000–1,200,000 simulated voters (tier-based)<br>
        • Peers: 15–100 fellow officials<br>
        • Superior: Single vote (1 or 0)<br>
        • <strong>NO minimum thresholds</strong> – highest score wins
      </div>
      <h3>Recent Electoral Elections</h3>
      <div id="electoralElectionsList"><div class="log-entry">No electoral elections yet.</div></div>
    </div>
    <div class="panel">
      <h2><i class="fas fa-calculator"></i> Score Calculation Example</h2>
      <div id="electoralExample"><!-- demo block --></div>
    </div>
  </div>

  <div id="judicialTab" class="content-panel" style="display:none;">
    <div class="panel">
      <h2 class="h2-judicial"><i class="fas fa-gavel"></i> Judicial Appointment System</h2>
      <div class="log-entry judicial">
        <strong>Judicial Positions (Judges, Prosecutors, Police Chiefs)</strong><br>
        Formula: <strong>Elected Peers(60%) + Peer Review(10%) + Superior(30%)</strong><br>
        • Peer Review influences peers (35%) and superior (60%), but cannot veto
      </div>
      <h3>Recent Judicial Appointments</h3>
      <div id="judicialAppointmentsList"><div class="log-entry">No judicial appointments yet.</div></div>
    </div>
    <div class="panel">
      <h2 class="h2-judicial"><i class="fas fa-calculator"></i> Judicial Score Calculation</h2>
      <div id="judicialExample"><!-- demo block --></div>
    </div>
  </div>

  <div id="transparencyTab" class="content-panel" style="display:none;">
    <div class="panel">
      <h2 class="h2-transparency"><i class="fas fa-chart-line"></i> Financial Transparency System</h2>
      <div class="log-entry transparency">
        <strong>All transactions &gt; $10,000 automatically disclosed</strong><br>
        • 72-hour disclosure • Open JSON/CSV • Categories: travel, real estate, etc.
      </div>
      <h3>Recent Financial Disclosures</h3>
      <div id="financialDisclosuresList"><div class="log-entry">No financial disclosures yet.</div></div>
    </div>
    <div class="panel">
      <h2 class="h2-transparency"><i class="fas fa-home"></i> Housing Subsidy System</h2>
      <div class="log-entry">
        <strong>Eligibility:</strong> No property • <strong>Amount:</strong> 30% base • <strong>Payment:</strong> 5 years
      </div>
      <h3>Compensation Structure</h3>
      <div id="compensationDetails"><!-- demo block --></div>
    </div>
  </div>

  <div id="analysisTab" class="content-panel" style="display:none;">
    <div class="panel">
      <h2 id="analysisTitle">Detailed Election Analysis</h2>
      <div id="officialDetail"><div class="log-entry">Click on any official to see detailed election analysis.</div></div>
    </div>
    <div class="panel">
      <h2><i class="fas fa-history"></i> Election History</h2>
      <div id="electionHistory"><div class="log-entry">No election history available.</div></div>
    </div>
  </div>
</div>

<!-- Modal for election details -->
<div id="detailModal" class="modal-backdrop" onclick="closeModal(event)">
  <div class="modal" onclick="event.stopPropagation()">
    <div class="modal-header">
      <div class="modal-title" id="modalTitle">Election Details</div>
      <button class="modal-close" onclick="closeModal()">Close</button>
    </div>
    <div id="modalBody" class="modal-grid"></div>
  </div>
</div>

<script>
const CONFIG = {
  totalOfficials: 400,
  judicialRatio: 0.25,
  termLength: 5,
  currentYear: 2024,
  electoralWeights: { voters: 0.50, peers: 0.40, superior: 0.10 },
  judicialWeights: { electedPeers: 0.60, peerReview: 0.10, superior: 0.30 },
  peerReviewInfluence: { onElectedPeers: 0.35, onSuperior: 0.60 },
  disclosureThreshold: 10000,
  housingSubsidyRate: 0.30,
  tiers: {
    LOCAL:{ name:'Local', electoralPositions:['Mayor','City Councilor','City Clerk'], judicialPositions:['Municipal Judge','City Prosecutor','Police Chief'], basePeers:{electoral:15,judicial:20}, voterRange:[50000,120000]},
    COUNTY:{ name:'County', electoralPositions:['County Executive','County Commissioner','County Clerk'], judicialPositions:['County Judge','District Attorney','Sheriff'], basePeers:{electoral:25,judicial:30}, voterRange:[120000,300000]},
    STATE:{ name:'State', electoralPositions:['Governor','State Senator','State Representative'], judicialPositions:['State Judge','State Attorney General','State Police Commissioner'], basePeers:{electoral:40,judicial:50}, voterRange:[500000,1200000]},
    FEDERAL:{ name:'Federal', electoralPositions:['U.S. Senator','U.S. Representative','Cabinet Secretary'], judicialPositions:['Federal Judge','U.S. Attorney','FBI Director'], basePeers:{electoral:100,judicial:100}, voterRange:[2000000,5000000]}
  },
  simulationSpeed: 1
};
let simulationState = {
  officials: [], elections: [], judicialAppointments: [], financialDisclosures: [],
  currentYear: CONFIG.currentYear, selectedOfficial: null,
  stats: { totalElections:0, electoralElections:0, judicialAppointments:0, incumbentWins:0, challengerWins:0, financialDisclosures:0, avgTenure:0, termExpirations:0 }
};
function clamp01(x){ return Math.max(0, Math.min(1, x)); }
function rand(seed){ const x = Math.sin(seed) * 10000; return x - Math.floor(x); } // deterministic PRNG helper

class Official{
  constructor(id, firstName, lastName, startYear, isJudicial=false){
    this.id=id; this.firstName=firstName; this.lastName=lastName; this.fullName=`${firstName} ${lastName}`;
    this.isJudicial=isJudicial; this.tier=this.assignInitialTier(); this.position='';
    this.experience={LOCAL:0,COUNTY:0,STATE:0,FEDERAL:0}; this.totalExperience=0;
    this.careerHistory=[]; this.electionHistory=[];
    this.termStartYear=startYear; this.termsServed=1; this.yearsInCurrentTerm=0; this.isTermExpired=false;
    this.constituentAppeal=0.4+Math.random()*0.4; this.peerRespect=0.3+Math.random()*0.5;
    this.superiorFavor=0.2+Math.random()*0.6; this.ambition=0.5+Math.random()*0.5; this.incumbencyFactor=1.0;
    this.legalCompetence=isJudicial?0.5+Math.random()*0.5:0; this.ethicsScore=isJudicial?0.6+Math.random()*0.4:0;
    this.ownsProperty=Math.random()<0.7; this.baseSalary=0; this.housingSubsidy=0; this.totalCompensation=0; this.transactions=[];
    this.electionsWon=0; this.electionsLost=0; this.reElectionsWon=0; this.promotions=0;
    this.initializeCareer(startYear);
  }
  assignInitialTier(){ const r=Math.random(); if(r<0.6)return'LOCAL'; if(r<0.85)return'COUNTY'; if(r<0.95)return'STATE'; return'FEDERAL'; }
  initializeCareer(startYear){
    const tierConfig=CONFIG.tiers[this.tier];
    const positionPool=this.isJudicial?tierConfig.judicialPositions:tierConfig.electoralPositions;
    this.position=positionPool[Math.floor(Math.random()*positionPool.length)];
    this.experience[this.tier]=1+Math.floor(Math.random()*3);
    this.totalExperience=this.experience[this.tier];
    this.termStartYear=startYear-this.experience[this.tier];
    this.yearsInCurrentTerm=this.experience[this.tier];
    this.calculateCompensation();
    this.careerHistory.push({year:this.termStartYear,tier:this.tier,position:this.position,event:'Initial election/appointment'});
  }
  calculateCompensation(){
    const regionalMedian=120000+Math.random()*80000;
    const salaryMultiplier=2.0+Math.random();
    this.baseSalary=Math.round(regionalMedian*salaryMultiplier);
    this.housingSubsidy=this.ownsProperty?0:Math.round(this.baseSalary*CONFIG.housingSubsidyRate);
    this.totalCompensation=this.baseSalary+this.housingSubsidy;
  }
  advanceYear(){
    this.totalExperience++; this.experience[this.tier]++; this.yearsInCurrentTerm++;
    this.isTermExpired=(simulationState.currentYear-this.termStartYear)>=CONFIG.termLength;
    this.calculateCompensation();
  }
  assumeOffice(termStartYear, position=null, tier=null){
    this.termStartYear=termStartYear; this.yearsInCurrentTerm=0; this.isTermExpired=false;
    if(position) this.position=position; if(tier){ this.tier=tier; this.termsServed++; }
    if(this.termsServed>1){ this.incumbencyFactor=Math.min(1.5, 1.0 + (this.termsServed*0.1)); }
  }
  addElectionRecord(record){ this.electionHistory.unshift({year:simulationState.currentYear, data:record}); if(this.electionHistory.length>20) this.electionHistory.pop(); }
  addTransaction(amount, category, description){
    const tx={ date:new Date().toISOString().split('T')[0], amount, category, description, disclosed: amount>CONFIG.disclosureThreshold };
    this.transactions.unshift(tx);
    if(tx.disclosed){ simulationState.financialDisclosures.push({officialId:this.id, officialName:this.fullName, ...tx}); simulationState.stats.financialDisclosures++; }
    if(this.transactions.length>20) this.transactions.pop();
  }
}

const ElectionEngine = {
  runElectoralElections(){
    const expiring = simulationState.officials.filter(o=>o.isTermExpired && !o.isJudicial);
    const created=[];
    expiring.forEach(inc=>{ const e=this.createElectoralElection(inc); if(e) created.push(e); });
    created.forEach(election=>{
      election.candidateResults = election.candidates.map(c=> this.calculateElectoralScore(election, c, election.position.tier));
      election.candidateResults.sort((a,b)=> b.finalScore - a.finalScore);
      election.winnerId = election.candidateResults[0].candidateId;

      election.candidateResults.forEach(res=>{
        const who = simulationState.officials.find(o=>o.id===res.candidateId);
        if(!who) return;
        const record = { electionId:election.id, type:'electoral', position:election.position, result:res, isWinner: res.candidateId===election.winnerId, seed:election.seed, params:election.params };
        who.addElectionRecord(record);
        if(record.isWinner){
          who.electionsWon++; if(res.isIncumbent){ who.reElectionsWon++; simulationState.stats.incumbentWins++; } else { simulationState.stats.challengerWins++; }
          who.assumeOffice(simulationState.currentYear, election.position.title, election.position.tier);
        }else{
          who.electionsLost++;
        }
      });

      simulationState.stats.electoralElections++; simulationState.stats.totalElections++;
      SimulationUI.logEvent(`[Electoral Election] ${election.candidateResults[0].candidateName} won ${election.position.title} with ${election.candidateResults[0].finalScore.toFixed(2)} points.`, 'success');
    });
    simulationState.elections.push(...created);
    return created;
  },

  runJudicialAppointments(){
    const expiring = simulationState.officials.filter(o=>o.isTermExpired && o.isJudicial);
    const created=[];
    expiring.forEach(inc=>{ const a=this.createJudicialAppointment(inc); if(a) created.push(a); });
    created.forEach(app=>{
      app.candidateResults = app.candidates.map(c=> this.calculateJudicialScore(app, c, app.position.tier));
      app.candidateResults.sort((a,b)=> b.finalScore - a.finalScore);
      app.winnerId = app.candidateResults[0].candidateId;

      app.candidateResults.forEach(res=>{
        const who = simulationState.officials.find(o=>o.id===res.candidateId);
        if(!who) return;
        const record = { electionId:app.id, type:'judicial', position:app.position, result:res, isWinner: res.candidateId===app.winnerId, seed:app.seed, params:app.params };
        who.addElectionRecord(record);
        if(record.isWinner){
          who.electionsWon++; if(res.isIncumbent){ who.reElectionsWon++; simulationState.stats.incumbentWins++; } else { simulationState.stats.challengerWins++; }
          who.assumeOffice(simulationState.currentYear, app.position.title, app.position.tier);
        }else{
          who.electionsLost++;
        }
      });

      simulationState.stats.judicialAppointments++; simulationState.stats.totalElections++;
      SimulationUI.logEvent(`[Judicial Appointment] ${app.candidateResults[0].candidateName} appointed ${app.position.title} with ${app.candidateResults[0].finalScore.toFixed(2)} points.`, 'judicial');
    });
    simulationState.judicialAppointments.push(...created);
    return created;
  },

  createElectoralElection(inc){
    const seed = Date.now() + Math.floor(Math.random()*1e6);
    const params = { tier:inc.tier };
    const candidates=[{
      candidateId: inc.id, candidateName: inc.fullName, isIncumbent:true,
      constituentAppeal:inc.constituentAppeal, peerRespect:inc.peerRespect, superiorFavor:inc.superiorFavor, totalExperience:inc.totalExperience
    }];
    const challengers = this.findChallengers(inc);
    challengers.forEach(ch=> candidates.push({
      candidateId: ch.id, candidateName: ch.fullName, isIncumbent:false,
      constituentAppeal:ch.constituentAppeal, peerRespect:ch.peerRespect, superiorFavor:ch.superiorFavor, totalExperience:ch.totalExperience
    }));
    return { id:`elec_${seed}`, seed, params, position:{tier:inc.tier, title:inc.position, type:'electoral'}, candidates, type:'electoral', isCompetitive:candidates.length>1, timestamp:new Date() };
  },

  createJudicialAppointment(inc){
    const seed = Date.now() + Math.floor(Math.random()*1e6);
    const params = { tier:inc.tier };
    const candidates=[{
      candidateId: inc.id, candidateName: inc.fullName, isIncumbent:true,
      peerRespect:inc.peerRespect, superiorFavor:inc.superiorFavor, legalCompetence:inc.legalCompetence, ethicsScore:inc.ethicsScore, totalExperience:inc.totalExperience
    }];
    const challengers = simulationState.officials.filter(o=> o.isJudicial && o.id!==inc.id && !o.isTermExpired && o.tier===inc.tier && Math.random()<o.ambition*0.3).slice(0,3);
    challengers.forEach(ch=> candidates.push({
      candidateId:ch.id, candidateName:ch.fullName, isIncumbent:false,
      peerRespect:ch.peerRespect, superiorFavor:ch.superiorFavor, legalCompetence:ch.legalCompetence, ethicsScore:ch.ethicsScore, totalExperience:ch.totalExperience
    }));
    return { id:`jud_${seed}`, seed, params, position:{tier:inc.tier, title:inc.position, type:'judicial'}, candidates, type:'judicial', isCompetitive:candidates.length>1, timestamp:new Date() };
  },

  findChallengers(inc){
    return simulationState.officials.filter(o=> !o.isJudicial && o.id!==inc.id && !o.isTermExpired && o.tier===inc.tier && o.experience[o.tier]>=2 && Math.random()<o.ambition*0.4).slice(0,3);
  },

  calculateElectoralScore(election, candidate, tier){
    const t=CONFIG.tiers[tier];
    const s1 = rand(election.seed + candidate.candidateId);
    const s2 = rand(election.seed + candidate.candidateId*7);
    const s3 = rand(election.seed + candidate.candidateId*11);

    const totalVoters = t.voterRange[0] + s1 * (t.voterRange[1]-t.voterRange[0]);
    let voterSupport = candidate.constituentAppeal * (0.6 + s2 * 0.4);
    if(candidate.isIncumbent) voterSupport *= 1.1;
    const vPct = clamp01(voterSupport);

    const peerCount = t.basePeers.electoral;
    let peerSupport = candidate.peerRespect * (0.5 + s3 * 0.5);
    if(candidate.isIncumbent) peerSupport *= 1.15;
    const pPct = clamp01(peerSupport);

    let superiorSupport = candidate.isIncumbent ? 1 : (candidate.superiorFavor > 0.5 ? 1 : 0);
    const sPct = clamp01(superiorSupport);

    const votes=Math.round(vPct*totalVoters);
    const voterScore=vPct*CONFIG.electoralWeights.voters;
    const peerScore=pPct*CONFIG.electoralWeights.peers;
    const superiorScore=sPct*CONFIG.electoralWeights.superior;
    const finalScore=(voterScore+peerScore+superiorScore)*100;

    return {
      candidateId:candidate.candidateId, candidateName:candidate.candidateName, isIncumbent:candidate.isIncumbent,
      components:{
        voters:{ support:vPct, weight:CONFIG.electoralWeights.voters, score:voterScore*100, details:`${(vPct*100).toFixed(1)}% (${votes.toLocaleString()} of ${Math.round(totalVoters).toLocaleString()})` },
        peers:{ support:pPct, weight:CONFIG.electoralWeights.peers, score:peerScore*100, details:`${(pPct*100).toFixed(1)}% of ${peerCount} peers` },
        superior:{ support:sPct, weight:CONFIG.electoralWeights.superior, score:superiorScore*100, details: sPct===1?'Supported (1 vote)':'Not supported' }
      },
      finalScore,
      calculation:`(${(vPct*100).toFixed(1)}% × 0.50) + (${(pPct*100).toFixed(1)}% × 0.40) + (${(sPct*100).toFixed(0)}% × 0.10) = ${finalScore.toFixed(2)}`
    };
  },

  calculateJudicialScore(appointment, candidate, tier){
    const t=CONFIG.tiers[tier];
    const s1 = rand(appointment.seed + candidate.candidateId);
    const s2 = rand(appointment.seed + candidate.candidateId*5);
    const s3 = rand(appointment.seed + candidate.candidateId*13);

    const peerReviewers = 70 + Math.floor(s1 * 31);
    const R = clamp01((candidate.legalCompetence * 0.7 + candidate.ethicsScore * 0.3) * (0.7 + s2 * 0.3));
    const peerReviewComponent = R * CONFIG.judicialWeights.peerReview;

    const electedPeerCount = t.basePeers.judicial;
    let P_raw = clamp01(candidate.peerRespect * (0.5 + s3 * 0.5));
    if(candidate.isIncumbent) P_raw = clamp01(P_raw*1.2);
    const alphaP = CONFIG.peerReviewInfluence.onElectedPeers;
    const P_eff = clamp01(P_raw*(1-alphaP) + R*alphaP);
    const electedPeerComponent = P_eff * CONFIG.judicialWeights.electedPeers;

    let S_raw = candidate.isIncumbent ? 1 : (candidate.superiorFavor > 0.4 ? 1 : 0);
    const alphaS = CONFIG.peerReviewInfluence.onSuperior;
    const S_eff = clamp01(S_raw*(1-alphaS) + R*alphaS);
    const superiorComponent = S_eff * CONFIG.judicialWeights.superior;

    const finalScore=(peerReviewComponent + electedPeerComponent + superiorComponent)*100;

    return {
      candidateId:candidate.candidateId, candidateName:candidate.candidateName, isIncumbent:candidate.isIncumbent,
      components:{
        peerReview:{ support:R, weight:CONFIG.judicialWeights.peerReview, score:peerReviewComponent*100, details:`${Math.round(R*100)}% from ${peerReviewers} anonymous peers`, influence:'Affects peers/superior; no veto' },
        electedPeers:{ support:P_eff, weight:CONFIG.judicialWeights.electedPeers, score:electedPeerComponent*100, details:`${(P_eff*100).toFixed(1)}% of ${electedPeerCount} elected peers (raw ${(P_raw*100).toFixed(1)}%)`, influence:`Influenced ${Math.round(alphaP*100)}% by peer review` },
        superior:{ support:S_eff, weight:CONFIG.judicialWeights.superior, score:superiorComponent*100, details:`${(S_eff*100).toFixed(1)}% effective support (raw ${(S_raw*100).toFixed(0)}%)`, influence:`Influenced ${Math.round(alphaS*100)}% by peer review` }
      },
      finalScore,
      calculation:`(${(R*100).toFixed(0)}% × 0.10) + (${(P_eff*100).toFixed(1)}% × 0.60) + (${(S_eff*100).toFixed(0)}% × 0.30) = ${finalScore.toFixed(2)}`
    };
  }
};

const SimulationEngine = {
  initialize(){
    simulationState={ officials:[], elections:[], judicialAppointments:[], financialDisclosures:[], currentYear:CONFIG.currentYear, selectedOfficial:null,
      stats:{ totalElections:0, electoralElections:0, judicialAppointments:0, incumbentWins:0, challengerWins:0, financialDisclosures:0, avgTenure:0, termExpirations:0 } };

    const fns=['James','Mary','John','Patricia','Robert','Jennifer','Michael','Linda','William','Elizabeth','David','Barbara','Richard','Susan','Joseph'];
    const lns=['Smith','Johnson','Williams','Brown','Jones','Garcia','Miller','Davis','Rodriguez','Martinez','Hernandez','Lopez','Wilson','Anderson'];

    for(let i=0;i<CONFIG.totalOfficials;i++){
      const first=fns[Math.floor(Math.random()*fns.length)];
      const last=lns[Math.floor(Math.random()*lns.length)];
      const start=CONFIG.currentYear - Math.floor(Math.random()*10);
      const isJudicial=Math.random()<CONFIG.judicialRatio;
      const o=new Official(i+1, first, last, start, isJudicial);

      if(Math.random()<0.10){ o.termStartYear=CONFIG.currentYear - CONFIG.termLength; o.isTermExpired=true; }

      simulationState.officials.push(o);

      if(Math.random()<0.3){
        const amount=Math.round(5000+Math.random()*20000);
        const cats=['travel','equipment','conference','other'];
        o.addTransaction(amount, cats[Math.floor(Math.random()*cats.length)], 'Initial expense');
      }
    }
    SimulationUI.logEvent(`[System] Initialized ${simulationState.officials.length} officials (${Math.round(CONFIG.judicialRatio*100)}% judicial).`,'success');
    SimulationUI.updateAllDisplays();
  },
  advanceYear(){
    simulationState.currentYear++;
    SimulationUI.logEvent(`[Year] Advanced to ${simulationState.currentYear}.`,'warning');
    simulationState.officials.forEach(o=>o.advanceYear());
    const exp=simulationState.officials.filter(o=>o.isTermExpired).length;
    simulationState.stats.termExpirations=exp;
    if(exp>0) SimulationUI.logEvent(`[Year] ${exp} officials have terms expiring.`,'warning');

    const retired=simulationState.officials.filter(o=>o.totalExperience>20 && Math.random()<0.05);
    simulationState.officials=simulationState.officials.filter(o=>!retired.includes(o));
    if(retired.length>0) SimulationUI.logEvent(`[Year] ${retired.length} officials retired.`,'info');

    const totalTenure=simulationState.officials.reduce((s,o)=>s+o.totalExperience,0);
    simulationState.stats.avgTenure=(totalTenure/simulationState.officials.length).toFixed(1);
    SimulationUI.updateAllDisplays();
  },
  runElectionCycle(){
    const res = ElectionEngine.runElectoralElections();
    SimulationUI.logEvent(`[Elections] ${res.length} electoral elections completed.`,'success');
    SimulationUI.updateAllDisplays();
  },
  runJudicialAppointments(){
    const res = ElectionEngine.runJudicialAppointments();
    SimulationUI.logEvent(`[Appointments] ${res.length} judicial appointments completed.`,'judicial');
    SimulationUI.updateAllDisplays();
  }
};

const SimulationUI = {
  logEvent(msg,type='info'){ console.log(`[${type.toUpperCase()}] ${msg}`); },
  updateAllDisplays(){
    this.updateDashboard(); this.updateOfficialRoster(); this.updateTopPerformers();
    this.updateJudicialOfficials(); this.updateElectoralElections(); this.updateJudicialAppointments();
    this.updateFinancialDisclosures();
  },
  animateNumber(el, to){
    const from = Number(el.textContent.replace(/,/g,'')) || 0;
    const duration=400; const start=performance.now();
    const step=(t)=>{
      const p=Math.min(1,(t-start)/duration); const v = Math.round(from + (to-from)*p);
      el.textContent = v.toLocaleString();
      if(p<1) requestAnimationFrame(step);
    };
    requestAnimationFrame(step);
  },
  updateDashboard(){
    const off=simulationState.officials;
    const electoral=off.filter(o=>!o.isJudicial).length;
    const judicial=off.filter(o=>o.isJudicial).length;

    this.animateNumber(document.getElementById('totalOfficials'), off.length);
    document.getElementById('officialBreakdown').innerHTML = `${electoral} electoral, ${judicial} judicial`;

    this.animateNumber(document.getElementById('electoralElections'), simulationState.stats.electoralElections);
    this.animateNumber(document.getElementById('judicialAppointments'), simulationState.stats.judicialAppointments);
    this.animateNumber(document.getElementById('financialDisclosures'), simulationState.stats.financialDisclosures);

    document.getElementById('currentYear').textContent = simulationState.currentYear;
    const progressPct = Math.min(100, (off.length / CONFIG.totalOfficials) * 100);
    document.getElementById('simProgress').textContent = progressPct.toFixed(1)+'%';
    document.getElementById('progressFill').style.width = progressPct + '%';
  },
  updateOfficialRoster(){
    const container=document.getElementById('officialRoster');
    const sample=[...simulationState.officials].sort(()=>0.5-Math.random()).slice(0,10);
    container.innerHTML='';
    sample.forEach(o=>{
      const isSelected= simulationState.selectedOfficial && simulationState.selectedOfficial.id===o.id;
      const div=document.createElement('div');
      div.className=`official-item ${o.isJudicial?'judicial':''} ${isSelected?'selected':''}`;
      div.onclick=()=>this.showOfficialDetail(o);
      div.innerHTML=`
        <div class="official-name">
          <span class="tier-badge ${o.tier.toLowerCase()}">${o.tier}</span>
          ${o.fullName}
          <span class="official-type ${o.isJudicial?'judicial':''}">${o.isJudicial?'Judicial':'Electoral'}</span>
          ${o.isTermExpired?'<span class="badge" style="background:#ffefef;color:#b71c1c;border:1px solid #ffcdd2">Term Expired</span>':''}
        </div>
        <div class="official-details">
          <div>${o.position}</div>
          <div>${o.totalExperience} yrs</div>
          <div>Salary: $${o.baseSalary.toLocaleString()}</div>
          <div>Property: ${o.ownsProperty?'Yes':'No'}</div>
          <div>Record: ${o.electionsWon}-${o.electionsLost}</div>
          <div>Terms: ${o.termsServed}</div>
        </div>
      `;
      container.appendChild(div);
    });
  },
  updateTopPerformers(){
    const top=[...simulationState.officials].sort((a,b)=>b.totalExperience-a.totalExperience).slice(0,5);
    const c=document.getElementById('topPerformers'); c.innerHTML='';
    top.forEach(o=>{
      const div=document.createElement('div');
      div.className=`official-item ${o.isJudicial?'judicial':''}`;
      div.onclick=()=>this.showOfficialDetail(o);
      div.innerHTML=`
        <div class="official-name">
          <span class="tier-badge ${o.tier.toLowerCase()}">${o.tier}</span>${o.fullName}
        </div>
        <div class="official-details">
          <div>${o.position}</div><div>${o.totalExperience} yrs exp</div><div>Comp: $${o.totalCompensation.toLocaleString()}</div>
        </div>
      `;
      c.appendChild(div);
    });
  },
  updateJudicialOfficials(){
    const list=simulationState.officials.filter(o=>o.isJudicial).sort((a,b)=>b.legalCompetence-a.legalCompetence).slice(0,5);
    const c=document.getElementById('judicialOfficials'); c.innerHTML='';
    list.forEach(o=>{
      const div=document.createElement('div'); div.className='official-item judicial'; div.onclick=()=>this.showOfficialDetail(o);
      div.innerHTML=`
        <div class="official-name">
          <span class="tier-badge ${o.tier.toLowerCase()}">${o.tier}</span>${o.fullName}
        </div>
        <div class="official-details">
          <div>${o.position}</div><div>Competence: ${Math.round(o.legalCompetence*100)}%</div><div>Ethics: ${Math.round(o.ethicsScore*100)}%</div>
        </div>
      `;
      c.appendChild(div);
    });
  },
  updateElectoralElections(){
    const c=document.getElementById('electoralElectionsList');
    const recent = simulationState.elections.slice(-5).reverse();
    c.innerHTML='';
    if(recent.length===0){ c.innerHTML='<div class="log-entry">No electoral elections yet.</div>'; return; }
    recent.forEach(e=>{
      const w = e.candidateResults && e.candidateResults[0];
      if(!w) return;
      const div=document.createElement('div'); div.className='log-entry success';
      div.innerHTML=`
        <strong>${e.position.title} (${e.position.tier})</strong> 
        <span class="badge win">Winner</span> ${w.candidateName} — <strong>${w.finalScore.toFixed(2)}</strong> pts
        <br>
        <small>Competitive: ${e.isCompetitive?'Yes':'No'} | Seed: ${e.seed}</small>
        <div style="margin-top:8px;">
          <button class="view-btn" onclick="openElectionModal('${e.id}', 'electoral')"><i class="fas fa-eye"></i> View Details</button>
        </div>
      `;
      c.appendChild(div);
    });
  },
  updateJudicialAppointments(){
    const c=document.getElementById('judicialAppointmentsList');
    const recent = simulationState.judicialAppointments.slice(-5).reverse();
    c.innerHTML='';
    if(recent.length===0){ c.innerHTML='<div class="log-entry">No judicial appointments yet.</div>'; return; }
    recent.forEach(a=>{
      const w=a.candidateResults && a.candidateResults[0];
      if(!w) return;
      const div=document.createElement('div'); div.className='log-entry judicial';
      div.innerHTML=`
        <strong>${a.position.title} (${a.position.tier})</strong> 
        <span class="badge win">Appointed</span> ${w.candidateName} — <strong>${w.finalScore.toFixed(2)}</strong> pts
        <br>
        <small>Peer review influence applied | Seed: ${a.seed}</small>
        <div style="margin-top:8px;">
          <button class="view-btn" onclick="openElectionModal('${a.id}', 'judicial')"><i class="fas fa-eye"></i> View Details</button>
        </div>
      `;
      c.appendChild(div);
    });
  },
  updateFinancialDisclosures(){
    const c=document.getElementById('financialDisclosuresList');
    const recent=simulationState.financialDisclosures.slice(-6).reverse();
    c.innerHTML='';
    if(recent.length===0){ c.innerHTML='<div class="log-entry">No financial disclosures yet.</div>'; return; }
    recent.forEach(r=>{
      const div=document.createElement('div'); div.className='financial-record large';
      div.innerHTML=`
        <strong>${r.officialName}</strong><br>
        Amount: $${r.amount.toLocaleString()} • Category: ${r.category}<br>
        Date: ${r.date} • ${r.description}<br>
        <small>Auto-disclosed &gt; $${CONFIG.disclosureThreshold.toLocaleString()}</small>
      `;
      c.appendChild(div);
    });
  },
  showOfficialDetail(official){
    simulationState.selectedOfficial=official; showTab('analysis', document.getElementById('analysisTab'));
    document.getElementById('analysisTitle').textContent = `${official.fullName} - Detailed Analysis`;
    const detail=document.getElementById('officialDetail');
    const history=document.getElementById('electionHistory');

    let d=`
      <div class="election-detail ${official.isJudicial?'judicial':''}">
        <div class="election-header">
          <h4>Official Profile</h4>
          <span class="official-type ${official.isJudicial?'judicial':''}">${official.isJudicial?'Judicial Official':'Electoral Official'}</span>
        </div>
        <div class="vote-category">
          <h4>Career Information</h4>
          <div class="vote-breakdown">
            <div class="vote-component ${official.isJudicial?'judicial':''}">
              <strong>Position:</strong> ${official.position}<br>
              <strong>Tier:</strong> ${official.tier}<br>
              <strong>Total Experience:</strong> ${official.totalExperience} years<br>
              <strong>Terms Served:</strong> ${official.termsServed}
            </div>
            <div class="vote-component ${official.isJudicial?'judicial':''}">
              <strong>Current Term:</strong> Year ${official.yearsInCurrentTerm+1}/5<br>
              <strong>Term Status:</strong> ${official.isTermExpired?'EXPIRED':'Active'}<br>
              <strong>Election Record:</strong> ${official.electionsWon}-${official.electionsLost}<br>
              <strong>Re-elections Won:</strong> ${official.reElectionsWon}
            </div>
          </div>
        </div>
        <div class="vote-category">
          <h4>Attributes</h4>
          <div class="vote-breakdown">
            <div class="vote-component ${official.isJudicial?'judicial':''}">
              <strong>Peer Respect:</strong> ${Math.round(official.peerRespect*100)}%<br>
              <strong>Superior Favor:</strong> ${Math.round(official.superiorFavor*100)}%<br>
              <strong>Ambition:</strong> ${Math.round(official.ambition*100)}%
            </div>`;
    if(official.isJudicial){
      d+=`<div class="vote-component judicial">
             <strong>Legal Competence:</strong> ${Math.round(official.legalCompetence*100)}%<br>
             <strong>Ethics Score:</strong> ${Math.round(official.ethicsScore*100)}%
          </div>`;
    }else{
      d+=`<div class="vote-component">
             <strong>Constituent Appeal:</strong> ${Math.round(official.constituentAppeal*100)}%
          </div>`;
    }
    d+=`</div></div>
        <div class="vote-category">
          <h4>Compensation & Finances</h4>
          <div class="vote-breakdown">
            <div class="vote-component ${official.isJudicial?'judicial':''}">
              <strong>Base Salary:</strong> $${official.baseSalary.toLocaleString()}<br>
              <strong>Housing Subsidy:</strong> $${official.housingSubsidy.toLocaleString()}<br>
              <strong>Total Compensation:</strong> $${official.totalCompensation.toLocaleString()}
            </div>
            <div class="vote-component ${official.isJudicial?'judicial':''}">
              <strong>Property Ownership:</strong> ${official.ownsProperty?'Yes':'No'}<br>
              <strong>Transactions:</strong> ${official.transactions.length} recorded<br>
              <strong>Large Disclosures:</strong> ${official.transactions.filter(t=>t.disclosed).length}
            </div>
          </div>
        </div>
      </div>`;
    detail.innerHTML=d;

    if(official.electionHistory.length===0){
      history.innerHTML='<div class="log-entry">No election history available.</div>';
    }else{
      let h='';
      official.electionHistory.forEach(rec=>{
        const r=rec.data.result, type=rec.data.type==='electoral'?'Election':'Appointment';
        h+=`
          <div class="election-detail ${type==='Appointment'?'judicial':''}">
            <div class="election-header">
              <h4>${type} for ${rec.data.position.title} (Year ${rec.year})</h4>
              <span class="badge ${rec.data.isWinner?'win':'lose'}">${rec.data.isWinner?'WINNER':'Runner-up'}</span>
              ${r.isIncumbent?'<span class="badge incumbent">Incumbent</span>':''}
            </div>
            <div class="vote-category">
              <h4>Score Components</h4>
              <div class="vote-breakdown">
        `;
        if(type==='Election'){
          h+=`
            <div class="vote-component"><strong>Voters (50%):</strong><br>${r.components.voters.details}<br>Score: ${r.components.voters.score.toFixed(2)} pts</div>
            <div class="vote-component"><strong>Peers (40%):</strong><br>${r.components.peers.details}<br>Score: ${r.components.peers.score.toFixed(2)} pts</div>
            <div class="vote-component"><strong>Superior (10%):</strong><br>${r.components.superior.details}<br>Score: ${r.components.superior.score.toFixed(2)} pts</div>
          `;
        }else{
          h+=`
            <div class="vote-component judicial"><strong>Peer Review (10%):</strong><br>${r.components.peerReview.details}<br>Score: ${r.components.peerReview.score.toFixed(2)} pts<br><small>${r.components.peerReview.influence}</small></div>
            <div class="vote-component judicial"><strong>Elected Peers (60%):</strong><br>${r.components.electedPeers.details}<br>Score: ${r.components.electedPeers.score.toFixed(2)} pts<br><small>${r.components.electedPeers.influence}</small></div>
            <div class="vote-component judicial"><strong>Superior (30%):</strong><br>${r.components.superior.details}<br>Score: ${r.components.superior.score.toFixed(2)} pts<br><small>${r.components.superior.influence}</small></div>
          `;
        }
        h+=`</div></div>
            <div class="calculation-formula"><strong>Calculation:</strong> ${r.calculation}</div>
            <div class="final-score ${type==='Appointment'?'judicial':''}">
              <div>FINAL SCORE</div>
              <div class="final-score-value">${r.finalScore.toFixed(2)}</div>
              <div>${rec.data.isWinner?'WINNER':'Runner-up'}</div>
            </div>
          </div>
        `;
      });
      history.innerHTML=h;
    }
    this.updateOfficialRoster();
  }
};

// Tabs and global functions
function showTab(name, el){
  document.querySelectorAll('.content-panel').forEach(p=>p.style.display='none');
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  const panel=document.getElementById(name+'Tab'); if(panel) panel.style.display='grid';
  if(el) el.classList.add('active');
  if(name==='analysis') document.getElementById('analysisTab').style.display='block';
}
function initializeSimulation(){ SimulationEngine.initialize(); }
function runElectionCycle(){ SimulationEngine.runElectionCycle(); }
function runJudicialAppointments(){ SimulationEngine.runJudicialAppointments(); }
function advanceYear(){ SimulationEngine.advanceYear(); }
function runFiveYears(){
  SimulationUI.logEvent(`[System] Running 5-year simulation...`,'warning');
  for(let i=0;i<5;i++) SimulationEngine.advanceYear();
  SimulationUI.logEvent(`[System] 5-year simulation complete.`,'success');
  SimulationUI.updateAllDisplays();
}
function resetSimulation(){
  if(confirm('Reset the entire simulation? All data will be lost.')){
    simulationState={ officials:[], elections:[], judicialAppointments:[], financialDisclosures:[], currentYear:CONFIG.currentYear, selectedOfficial:null,
      stats:{ totalElections:0, electoralElections:0, judicialAppointments:0, incumbentWins:0, challengerWins:0, financialDisclosures:0, avgTenure:0, termExpirations:0 } };
    document.getElementById('analysisTab').style.display='none';
    showTab('officials', document.querySelector('.tab'));
    SimulationUI.updateAllDisplays();
    SimulationUI.logEvent('[System] Simulation reset.','warning');
  }
}
function setSpeed(speed, el){
  CONFIG.simulationSpeed=speed;
  document.querySelectorAll('.speed-btn').forEach(b=>b.classList.remove('active'));
  if(el) el.classList.add('active');
  SimulationUI.logEvent(`[System] Simulation speed: ${speed}x.`,'info');
}

// Modal controls
function openElectionModal(id, kind){
  const modal=document.getElementById('detailModal');
  const title=document.getElementById('modalTitle');
  const body=document.getElementById('modalBody'); body.innerHTML='';

  const src = kind==='electoral' ? simulationState.elections : simulationState.judicialAppointments;
  const item = src.find(x=>x.id===id);
  if(!item){ return; }

  title.textContent = `${kind==='electoral'?'Election':'Judicial Appointment'} — ${item.position.title} (${item.position.tier}) — Seed ${item.seed}`;
  const results = (item.candidateResults||[]).slice().sort((a,b)=>b.finalScore-a.finalScore);
  results.forEach((r, idx)=>{
    const div=document.createElement('div'); div.className='modal-candidate';
    const rankBadge = idx===0?'<span class="badge win">WINNER</span>':'<span class="badge lose">Runner</span>';
    div.innerHTML = `
      <div class="head">
        <div class="name">${idx+1}. ${r.candidateName} ${r.isIncumbent?'<span class="badge incumbent">Incumbent</span>':''}</div>
        <div class="score">${r.finalScore.toFixed(2)} pts ${idx===0?rankBadge:''}</div>
      </div>
      <div class="components">
        ${kind==='electoral' ? `
          <div class="comp"><strong>Voters (50%)</strong><br>${r.components.voters.details}<br>Score: ${r.components.voters.score.toFixed(2)}</div>
          <div class="comp"><strong>Peers (40%)</strong><br>${r.components.peers.details}<br>Score: ${r.components.peers.score.toFixed(2)}</div>
          <div class="comp"><strong>Superior (10%)</strong><br>${r.components.superior.details}<br>Score: ${r.components.superior.score.toFixed(2)}</div>
        ` : `
          <div class="comp"><strong>Peer Review (10%)</strong><br>${r.components.peerReview.details}<br>Score: ${r.components.peerReview.score.toFixed(2)}<br><small>${r.components.peerReview.influence}</small></div>
          <div class="comp"><strong>Elected Peers (60%)</strong><br>${r.components.electedPeers.details}<br>Score: ${r.components.electedPeers.score.toFixed(2)}<br><small>${r.components.electedPeers.influence}</small></div>
          <div class="comp"><strong>Superior (30%)</strong><br>${r.components.superior.details}<br>Score: ${r.components.superior.score.toFixed(2)}<br><small>${r.components.superior.influence}</small></div>
        `}
      </div>
      <div class="calc"><strong>Calculation:</strong> ${r.calculation}</div>
    `;
    body.appendChild(div);
  });

  modal.style.display='flex';
}
function closeModal(e){ document.getElementById('detailModal').style.display='none'; }

document.addEventListener('DOMContentLoaded', ()=>{
  SimulationUI.logEvent('[System] EAM Dual-System Simulator loaded.','info');
  SimulationUI.logEvent('[System] Electoral: Voters(50%) + Peers(40%) + Superior(10%)','info');
  SimulationUI.logEvent('[System] Judicial: Elected Peers(60%) + Peer Review(10%) + Superior(30%)','judicial');
  SimulationUI.logEvent('[System] Pure competition: Highest score wins, no thresholds.','success');
});
</script>
</body>
</html>


  
