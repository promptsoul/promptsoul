<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Nimbus</title>
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>

<style>
html{scroll-behavior:smooth}
body{font-family:Inter,system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif}
@keyframes fadeUp{from{opacity:0;transform:translateY(14px)}to{opacity:1;transform:translateY(0)}}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
@keyframes scaleIn{from{opacity:0;transform:scale(.96) translateY(-4px)}to{opacity:1;transform:scale(1) translateY(0)}}
@keyframes popIn{from{opacity:0;transform:scale(.4)}to{opacity:1;transform:scale(1)}}
@keyframes toastIn{from{opacity:0;transform:translate(-50%,12px)}to{opacity:1;transform:translate(-50%,0)}}
@keyframes drift{0%,100%{transform:translate(0,0) scale(1)}50%{transform:translate(40px,30px) scale(1.08)}}
@keyframes drift2{0%,100%{transform:translate(0,0) scale(1)}50%{transform:translate(-30px,20px) scale(1.06)}}
@keyframes growBar{from{width:0}to{width:var(--w)}}
.animate-fadeup{animation:fadeUp .5s ease both}
.animate-fadein{animation:fadeIn .4s ease both}
.animate-scalein{animation:scaleIn .2s ease both}
.animate-pop{animation:popIn .3s cubic-bezier(.2,.8,.2,1) both}
.animate-toast{animation:toastIn .3s ease both}
.drift{animation:drift 10s ease-in-out infinite}
.drift2{animation:drift2 12s ease-in-out infinite}
.grow-bar{animation:growBar 1s ease both}
::-webkit-scrollbar{width:8px;height:8px}
::-webkit-scrollbar-track{background:#09090b}
::-webkit-scrollbar-thumb{background:#27272a;border-radius:8px}
::-webkit-scrollbar-thumb:hover{background:#3f3f46}
</style>
</head>

<body class="bg-zinc-950 text-zinc-100 min-h-screen">

<div class="fixed inset-0 overflow-hidden pointer-events-none">
  <div class="absolute -top-32 -left-32 w-96 h-96 rounded-full bg-violet-600/10 blur-3xl drift"></div>
  <div class="absolute top-1/3 -right-40 w-[28rem] h-[28rem] rounded-full bg-teal-500/5 blur-3xl drift2"></div>
</div>

<header class="sticky top-0 z-40 border-b border-zinc-800/80 bg-zinc-950/85 backdrop-blur-xl">
  <div class="mx-auto max-w-7xl px-4 sm:px-6 h-14 flex items-center justify-between">
    <div class="flex items-center gap-6">
      <button onclick="navigate('dashboard')" class="flex items-center gap-2.5 group">
        <div class="h-7 w-7 rounded-lg bg-gradient-to-br from-violet-500 to-teal-300 flex items-center justify-center shadow-lg shadow-violet-500/10">
          <svg viewBox="0 0 24 24" fill="none" class="w-4 h-4 text-white">
            <path d="M5 12h14M12 5l7 7-7 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
        <span class="font-semibold tracking-tight">Nimbus</span>
      </button>

      <nav id="navLinks" class="hidden md:flex items-center gap-1"></nav>
    </div>

    <div class="flex items-center gap-2">
      <button onclick="openCommand()" class="hidden sm:flex items-center gap-2 rounded-lg border border-zinc-800 bg-zinc-900/70 px-3 py-1.5 text-xs text-zinc-500 hover:text-zinc-300 hover:border-zinc-700 transition">
        <i data-lucide="search" class="w-3.5 h-3.5"></i>
        <span>Search</span>
        <kbd class="ml-3 rounded border border-zinc-700 px-1.5 py-0.5 text-[10px]">⌘K</kbd>
      </button>

      <button onclick="openCommand()" class="sm:hidden p-2 text-zinc-400 hover:text-zinc-100">
        <i data-lucide="search" class="w-4 h-4"></i>
      </button>

      <div class="relative">
        <button id="bellBtn" onclick="togglePanel('notifications')" class="p-2 text-zinc-400 hover:text-zinc-100 rounded-md hover:bg-zinc-800/70 transition relative">
          <i data-lucide="bell" class="w-4 h-4"></i>
          <span class="absolute top-1.5 right-1.5 h-1.5 w-1.5 rounded-full bg-violet-400"></span>
        </button>
        <div id="notifications" class="hidden absolute right-0 top-11 w-80 sm:w-96 rounded-xl border border-zinc-800 bg-zinc-900 shadow-2xl shadow-black/40 overflow-hidden animate-scalein"></div>
      </div>

      <div class="relative">
        <button onclick="togglePanel('profileMenu')" class="flex items-center gap-2 p-1 rounded-lg hover:bg-zinc-800/70 transition">
          <div class="h-7 w-7 rounded-full bg-gradient-to-br from-violet-500 to-teal-300 flex items-center justify-center text-[10px] font-bold text-zinc-950">JI</div>
          <i data-lucide="chevron-down" class="hidden sm:block w-3.5 h-3.5 text-zinc-500"></i>
        </button>
        <div id="profileMenu" class="hidden absolute right-0 top-10 w-56 rounded-xl border border-zinc-800 bg-zinc-900 shadow-2xl shadow-black/40 overflow-hidden animate-scalein"></div>
      </div>

      <button onclick="toggleMobile()" class="md:hidden p-2 text-zinc-400 hover:text-zinc-100">
        <i data-lucide="menu" class="w-4 h-4"></i>
      </button>
    </div>
  </div>

  <div id="mobileNav" class="hidden md:hidden border-t border-zinc-800/80 px-4 py-2 flex-col gap-1"></div>
</header>

<main id="app" class="relative z-10"></main>

<div id="toast" class="hidden fixed bottom-6 left-1/2 -translate-x-1/2 z-50 rounded-lg border border-zinc-700 bg-zinc-900 px-4 py-2.5 text-sm shadow-2xl animate-toast">
  <div class="flex items-center gap-2">
    <i data-lucide="check-circle-2" class="w-4 h-4 text-teal-400"></i>
    <span id="toastText"></span>
  </div>
</div>

<div id="commandModal" class="hidden fixed inset-0 z-50 items-start justify-center pt-[12vh] bg-black/60 backdrop-blur-sm">
  <div class="w-[min(640px,calc(100%-2rem))] rounded-xl border border-zinc-800 bg-zinc-900 shadow-2xl overflow-hidden animate-scalein">
    <div class="flex items-center gap-3 px-4 border-b border-zinc-800">
      <i data-lucide="search" class="w-4 h-4 text-zinc-500"></i>
      <input id="commandInput" oninput="renderCommand()" placeholder="Search repositories, people, commands..." class="w-full bg-transparent py-4 outline-none text-sm">
      <kbd class="rounded border border-zinc-700 px-1.5 py-0.5 text-[10px] text-zinc-500">ESC</kbd>
    </div>
    <div id="commandResults" class="max-h-80 overflow-auto py-2"></div>
    <div class="border-t border-zinc-800 px-4 py-2 text-[11px] text-zinc-600 flex justify-between">
      <span>Navigate with your keyboard</span>
      <span>Enter to select</span>
    </div>
  </div>
</div>

<script>
const REPOS=[
  {
    id:1,
    name:"aurora-runtime",
    desc:"High-performance runtime primitives for edge applications.",
    lang:"TypeScript",
    stars:2840,
    forks:318,
    issues:12,
    visibility:"public",
    pinned:true,
    updated:"2 hours ago"
  },
  {
    id:2,
    name:"nebula-cli",
    desc:"A fast, composable CLI for modern cloud workflows.",
    lang:"Rust",
    stars:1732,
    forks:141,
    issues:7,
    visibility:"public",
    pinned:true,
    updated:"5 hours ago"
  },
  {
    id:3,
    name:"vector-store",
    desc:"Embedded vector storage with predictable latency.",
    lang:"Go",
    stars:921,
    forks:83,
    issues:5,
    visibility:"private",
    pinned:true,
    updated:"1 day ago"
  },
  {
    id:4,
    name:"infra-modules",
    desc:"Reusable infrastructure modules for production systems.",
    lang:"HCL",
    stars:412,
    forks:39,
    issues:3,
    visibility:"public",
    pinned:false,
    updated:"2 days ago"
  },
  {
    id:5,
    name:"observability-kit",
    desc:"Opinionated observability primitives for distributed systems.",
    lang:"TypeScript",
    stars:768,
    forks:72,
    issues:8,
    visibility:"public",
    pinned:false,
    updated:"3 days ago"
  },
  {
    id:6,
    name:"scheduler",
    desc:"Priority-aware task scheduler for concurrent workloads.",
    lang:"Python",
    stars:621,
    forks:54,
    issues:4,
    visibility:"private",
    pinned:false,
    updated:"4 days ago"
  }
];

const TRENDING=[
  {name:"shadcn/ui",lang:"TypeScript",stars:"42.8k"},
  {name:"bun",lang:"Zig",stars:"78.4k"},
  {name:"astro",lang:"TypeScript",stars:"49.2k"},
  {name:"ruff",lang:"Rust",stars:"41.1k"},
  {name:"turso",lang:"Rust",stars:"15.7k"}
];

const ACTIVITY=[
  {icon:"git-commit-horizontal",text:"pushed to",target:"aurora-runtime",branch:"main",time:"12 minutes ago"},
  {icon:"git-pull-request",text:"opened pull request in",target:"nebula-cli",branch:"#216",time:"1 hour ago"},
  {icon:"circle-alert",text:"opened issue in",target:"vector-store",branch:"#94",time:"2 hours ago"},
  {icon:"star",text:"starred",target:"shadcn/ui",time:"4 hours ago"},
  {icon:"git-merge",text:"merged pull request in",target:"aurora-runtime",branch:"#208",time:"Yesterday"},
  {icon:"git-branch",text:"created branch in",target:"scheduler",branch:"perf/priority-queue",time:"Yesterday"}
];

const NOTIFICATIONS=[
  {
    type:"git-pull-request",
    title:"maya-lin requested your review",
    detail:"feat: streaming SSR for edge handlers",
    time:"12m",
    unread:true
  },
  {
    type:"circle-alert",
    title:"New issue assigned to you",
    detail:"Docs: clarify TTL default for cache.set",
    time:"2h",
    unread:true
  },
  {
    type:"at-sign",
    title:"devon-park mentioned you",
    detail:"in aurora-runtime#211",
    time:"5h",
    unread:false
  },
  {
    type:"git-merge",
    title:"Pull request merged",
    detail:"fix: race condition in scheduler.run",
    time:"Yesterday",
    unread:false
  }
];

const FILE_TREE=[
  {
    name:"src",
    type:"folder",
    children:[
      {name:"index.ts",type:"file"},
      {name:"scheduler.ts",type:"file"},
      {name:"cache.ts",type:"file"},
      {name:"runtime.ts",type:"file"}
    ]
  },
  {
    name:"tests",
    type:"folder",
    children:[
      {name:"runtime.test.ts",type:"file"},
      {name:"scheduler.test.ts",type:"file"}
    ]
  },
  {name:"package.json",type:"file"},
  {name:"README.md",type:"file"},
  {name:"tsconfig.json",type:"file"}
];

const CODE={
"index.ts":`import { Runtime } from "./runtime";
import { Scheduler } from "./scheduler";
import { Cache } from "./cache";

export class Aurora {
  private runtime: Runtime;
  private scheduler: Scheduler;
  private cache: Cache;

  constructor() {
    this.runtime = new Runtime();
    this.scheduler = new Scheduler();
    this.cache = new Cache();
  }

  async start() {
    await this.runtime.initialize();
    this.scheduler.start();
    return this;
  }

  async shutdown() {
    await this.scheduler.stop();
    await this.runtime.close();
  }
}

export default Aurora;`,

"scheduler.ts":`import type { Task, Priority } from "./types";

export class Scheduler {
  private queue: Task[] = [];
  private running = false;

  enqueue(task: Task, priority: Priority = "normal") {
    this.queue.push({ ...task, priority });
    this.queue.sort((a, b) => b.priority - a.priority);
  }

  async start() {
    this.running = true;

    while (this.running) {
      const task = this.queue.shift();

      if (!task) {
        await new Promise(r => setTimeout(r, 10));
        continue;
      }

      await task.run();
    }
  }

  async stop() {
    this.running = false;
  }
}`,

"cache.ts":`export interface CacheOptions {
  ttl?: number;
  maxSize?: number;
}

export class Cache<T> {
  private values = new Map<string, T>();

  constructor(private options: CacheOptions = {}) {}

  set(key: string, value: T) {
    this.values.set(key, value);

    if (this.options.maxSize &&
        this.values.size > this.options.maxSize) {
      const first = this.values.keys().next().value;
      this.values.delete(first);
    }
  }

  get(key: string) {
    return this.values.get(key);
  }

  clear() {
    this.values.clear();
  }
}`,

"runtime.ts":`export class Runtime {
  private initialized = false;

  async initialize() {
    if (this.initialized) return;

    await this.loadConfig();
    await this.connect();

    this.initialized = true;
  }

  private async loadConfig() {
    // Load runtime configuration
  }

  private async connect() {
    // Establish runtime connections
  }

  async close() {
    this.initialized = false;
  }
}`,

"runtime.test.ts":`import { Runtime } from "../src/runtime";

describe("Runtime", () => {
  it("initializes once", async () => {
    const runtime = new Runtime();

    await runtime.initialize();
    await runtime.initialize();

    expect(true).toBe(true);
  });
});`,

"scheduler.test.ts":`import { Scheduler } from "../src/scheduler";

describe("Scheduler", () => {
  it("starts and stops", async () => {
    const scheduler = new Scheduler();

    scheduler.start();
    await scheduler.stop();

    expect(true).toBe(true);
  });
});`,

"package.json":`{
  "name": "aurora-runtime",
  "version": "2.4.0",
  "private": false,
  "scripts": {
    "test": "vitest",
    "build": "tsc",
    "lint": "eslint ."
  },
  "dependencies": {
    "typescript": "^5.6.0"
  }
}`,

"README.md":`# Aurora Runtime

High-performance runtime primitives
for edge applications.

## Installation

npm install aurora-runtime

## Usage

import Aurora from "aurora-runtime";

const app = await new Aurora().start();

await app.shutdown();`,

"tsconfig.json":`{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "strict": true,
    "declaration": true,
    "outDir": "dist"
  },
  "include": ["src/**/*.ts"]
}`
};

const LANG_COLORS={
  TypeScript:"#3178c6",
  Rust:"#dea584",
  Go:"#00add8",
  Python:"#3572A5",
  Shell:"#89e051",
  Dockerfile:"#384d54"
};

function esc(s){
  return String(s)
    .replace(/&/g,"&amp;")
    .replace(/</g,"&lt;")
    .replace(/>/g,"&gt;");
}

function icon(name,cls="w-4 h-4"){
  return `<i data-lucide="${name}" class="${cls}"></i>`;
}

function badge(text,type="default"){
  const styles={
    default:"bg-zinc-800/70 text-zinc-400 border-zinc-700",
    violet:"bg-violet-500/10 text-violet-300 border-violet-500/20",
    teal:"bg-teal-500/10 text-teal-300 border-teal-500/20",
    amber:"bg-amber-500/10 text-amber-300 border-amber-500/20"
  };

  return `<span class="inline-flex items-center gap-1 rounded-full border px-1.5 py-0.5 text-[10px] ${styles[type]||styles.default}">${text}</span>`;
}

function button(label,kind="outline",ico="",extra=""){
  const styles={
    outline:"border border-zinc-700 bg-zinc-900/60 text-zinc-200 hover:bg-zinc-800 hover:border-zinc-600",
    primary:"bg-zinc-100 text-zinc-950 hover:bg-white",
    ghost:"text-zinc-400 hover:text-zinc-100 hover:bg-zinc-800/70"
  };

  return `<button class="inline-flex items-center justify-center gap-1.5 font-medium rounded-lg text-xs px-2.5 py-1.5 transition ${styles[kind]} ${extra}">
    ${ico?icon(ico,"w-3.5 h-3.5"):""}${label}
  </button>`;
}

function avatar(name,size=32){
  const initials=name==="jordan"?"JI":name.slice(0,2).toUpperCase();

  return `<div style="width:${size}px;height:${size}px" class="rounded-full bg-gradient-to-br from-violet-500 to-teal-300 flex items-center justify-center text-[${Math.max(8,Math.round(size/3))}px] font-bold text-zinc-950 shrink-0">${initials}</div>`;
}

function card(r,i=0){
  return `
  <div onclick="openRepo(${r.id})"
       class="group rounded-xl border border-zinc-800 bg-zinc-900/40 p-4 hover:bg-zinc-900/70 hover:border-zinc-700 transition cursor-pointer animate-fadeup"
       style="animation-delay:${i*60}ms">

    <div class="flex items-start justify-between gap-3">
      <div class="flex items-center gap-2 min-w-0">
        ${icon("book-open","w-4 h-4 text-zinc-500 shrink-0")}
        <h3 class="font-mono text-[13.5px] font-medium truncate group-hover:text-violet-300 transition">${r.name}</h3>
      </div>

      ${badge(r.visibility,r.visibility==="private"?"amber":"default")}
    </div>

    <p class="text-[12.5px] text-zinc-500 leading-relaxed mt-2.5 min-h-[38px]">${r.desc}</p>

    <div class="flex items-center gap-4 mt-4 text-[11px] text-zinc-500">
      <span class="flex items-center gap-1">
        <span class="h-2 w-2 rounded-full" style="background:${LANG_COLORS[r.lang]||"#71717a"}"></span>
        ${r.lang}
      </span>

      <span class="flex items-center gap-1">
        ${icon("star","w-3 h-3")}
        ${r.stars.toLocaleString()}
      </span>

      <span class="flex items-center gap-1">
        ${icon("git-fork","w-3 h-3")}
        ${r.forks}
      </span>

      <span class="ml-auto">${r.updated}</span>
    </div>
  </div>`;
}

function graph(){
  let cells="";

  for(let i=0;i<52*7;i++){
    const v=Math.random();

    let level=0;
    if(v>.78) level=1;
    if(v>.91) level=2;
    if(v>.97) level=3;
    if(v>.992) level=4;

    const classes=[
      "bg-zinc-800/70",
      "bg-teal-900/70",
      "bg-teal-700/80",
      "bg-teal-500/90",
      "bg-teal-300"
    ];

    cells+=`<span class="h-2.5 w-2.5 rounded-[3px] ${classes[level]} hover:ring-1 hover:ring-teal-300/50 transition"></span>`;
  }

  let s="";

  for(let week=0;week<52;week++){
    s+=`<div class="grid grid-rows-7 gap-[3px]">${Array.from({length:7},(_,d)=>cells[(week*7+d)*65]).join("")}</div>`;
  }

  return `
  <div class="overflow-x-auto">
    <div class="min-w-[720px]">
      <div class="flex items-center justify-between mb-2">
        <span class="text-[11px] text-zinc-500">1,847 contributions in the last year</span>
        <span class="text-[11px] text-zinc-600">Less ${[0,1,2,3,4].map(i=>`<span class="inline-block h-2.5 w-2.5 rounded-[3px] ml-1 ${["bg-zinc-800/70","bg-teal-900/70","bg-teal-700/80","bg-teal-500/90","bg-teal-300"][i]}"></span>`).join("")} More</span>
      </div>

      <div class="flex gap-[3px] overflow-x-auto pb-1">
        ${s}
      </div>
    </div>
  </div>`;
}

function renderNav(){
  document.getElementById("navLinks").innerHTML=[
    ["Overview","dashboard"],
    ["Repositories","repos"],
    ["Profile","profile"]
  ].map(x=>`
    <button onclick="navigate('${x[1]}')"
      class="px-3 py-1.5 text-[13px] font-medium rounded-md ${state.view===x[1]?"text-zinc-100":"text-zinc-400 hover:text-zinc-100"}">
      ${x[0]}
      ${state.view===x[1]?'<span class="block h-[2px] mt-1 rounded-full bg-gradient-to-r from-violet-400 to-teal-300"></span>':""}
    </button>
  `).join("");
}

function dashboard(){
  const pinned=REPOS.filter(r=>r.pinned);

  return `
  <div class="mx-auto max-w-7xl px-4 sm:px-6 py-8 space-y-10">

    <div class="flex flex-col sm:flex-row sm:items-end sm:justify-between gap-4 animate-fadeup">
      <div>
        <h1 class="text-2xl sm:text-[28px] font-semibold tracking-tight">Good afternoon, Jordan</h1>
        <p class="text-zinc-500 text-sm mt-1">Here's what's happening across your work today.</p>
      </div>

      <div class="flex gap-2">
        ${button("New branch","outline","git-branch")}
        ${button("New repository","primary","plus")}
      </div>
    </div>

    <div class="grid grid-cols-2 lg:grid-cols-4 gap-3">
      ${
        [
          ["Repositories","28","book-open"],
          ["Open pull requests","6","git-pull-request"],
          ["Open issues","14","circle-alert"],
          ["Followers","1,204","users"]
        ].map((x,i)=>`
          <div class="rounded-xl border border-zinc-800 bg-zinc-900/40 p-4 animate-fadeup" style="animation-delay:${80+i*60}ms">
            <div class="flex items-center justify-between">
              ${icon(x[2],"w-4 h-4 text-zinc-500")}
              ${icon("trending-up","w-3.5 h-3.5 text-teal-400")}
            </div>
            <p class="text-2xl font-semibold mt-2 tracking-tight">${x[1]}</p>
            <p class="text-[12px] text-zinc-500 mt-0.5">${x[0]}</p>
          </div>
        `).join("")
      }
    </div>

    <div class="grid lg:grid-cols-3 gap-6">

      <div class="lg:col-span-2 space-y-6">

        <div class="rounded-xl border border-zinc-800 bg-zinc-900/40 p-5 animate-fadeup">
          <div class="flex items-center gap-2 mb-4">
            ${icon("activity","w-4 h-4 text-zinc-400")}
            <h2 class="text-sm font-semibold text-zinc-200">Contribution activity</h2>
          </div>
          ${graph()}
        </div>
