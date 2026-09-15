import React, { useState, useEffect, useRef, useMemo, useCallback } from "react";
import {
  Search, Bell, Plus, ChevronDown, Star, GitFork, Circle, Dot,
  GitBranch, Code2, BookOpen, History, AlertCircle, GitPullRequest,
  PlayCircle, Package, Lock, Globe, ChevronRight, X, Command,
  Settings, LogOut, User, Users, MapPin, Link as LinkIcon, Calendar,
  Copy, Check, Menu, TrendingUp, Activity, Folder, File, ChevronLeft,
  Clock, MessageSquare, GitCommit, ArrowUpRight, Sparkles, Terminal,
} from "lucide-react";

/* ----------------------------------------------------------------------
   Design tokens (see component-level <style> for animation primitives)
   Base:      zinc-950 / zinc-900 / zinc-800 borders
   Signature: violet-500 -> teal-400 duotone (logo, primary actions, graph)
   Text:      zinc-100 primary, zinc-400 secondary, zinc-600 tertiary
-------------------------------------------------------------------------*/

const LANG_COLORS = {
  TypeScript: "bg-blue-400",
  JavaScript: "bg-yellow-400",
  Rust: "bg-orange-500",
  Go: "bg-cyan-400",
  Python: "bg-emerald-400",
  Swift: "bg-orange-400",
  CSS: "bg-fuchsia-400",
};

const REPOS = [
  { id: 1, name: "aurora-runtime", desc: "A lightweight, edge-first runtime for streaming server components.", lang: "TypeScript", stars: "4.2k", forks: 312, issues: 18, updated: "2 hours ago", visibility: "public", pinned: true },
  { id: 2, name: "quill-cli", desc: "Ergonomic command-line scaffolding for monorepos and design systems.", lang: "Rust", stars: "1.8k", forks: 94, issues: 6, updated: "yesterday", visibility: "public", pinned: true },
  { id: 3, name: "lumen-design", desc: "The internal component library and motion primitives for Lumen products.", lang: "TypeScript", stars: "926", forks: 58, issues: 11, updated: "3 days ago", visibility: "private", pinned: true },
  { id: 4, name: "tidepool", desc: "Distributed job queue with exactly-once semantics, built on Go.", lang: "Go", stars: "3.1k", forks: 201, issues: 27, updated: "5 days ago", visibility: "public", pinned: false },
  { id: 5, name: "glyph-render", desc: "GPU-accelerated text shaping and layout engine.", lang: "Rust", stars: "612", forks: 33, issues: 4, updated: "1 week ago", visibility: "public", pinned: false },
  { id: 6, name: "orchard", desc: "Declarative infra provisioning with drift detection built in.", lang: "Python", stars: "2.4k", forks: 145, issues: 9, updated: "2 weeks ago", visibility: "public", pinned: false },
];

const TRENDING = [
  { name: "vercel/turborepo", lang: "Rust", stars: "1.2k today" },
  { name: "shadcn/ui", lang: "TypeScript", stars: "980 today" },
  { name: "astral-sh/ruff", lang: "Rust", stars: "740 today" },
];

const ACTIVITY = [
  { icon: GitCommit, text: "Pushed 3 commits to", target: "aurora-runtime", branch: "feat/edge-cache", time: "24m ago" },
  { icon: GitPullRequest, text: "Opened a pull request in", target: "quill-cli", branch: "#218", time: "2h ago" },
  { icon: Star, text: "Starred", target: "astral-sh/ruff", branch: null, time: "6h ago" },
  { icon: AlertCircle, text: "Closed an issue in", target: "tidepool", branch: "#94", time: "yesterday" },
  { icon: GitFork, text: "Forked", target: "shadcn/ui", branch: null, time: "2 days ago" },
];

const NOTIFICATIONS = [
  { id: 1, unread: true, type: "pr", title: "Review requested on quill-cli", detail: "maya-lin wants your review on #218", time: "12m" },
  { id: 2, unread: true, type: "issue", title: "New issue in aurora-runtime", detail: "Memory leak in edge cache invalidation", time: "1h" },
  { id: 3, unread: false, type: "mention", title: "You were mentioned", detail: "@you can you take a look at this?", time: "5h" },
  { id: 4, unread: false, type: "pr", title: "Pull request merged", detail: "feat/streaming-ssr was merged into main", time: "1d" },
];

const FILE_TREE = [
  { type: "folder", name: "src", children: [
    { type: "folder", name: "runtime", children: [
      { type: "file", name: "scheduler.ts" },
      { type: "file", name: "cache.ts" },
    ]},
    { type: "file", name: "index.ts" },
    { type: "file", name: "server.ts" },
  ]},
  { type: "folder", name: "examples", children: [
    { type: "file", name: "edge.ts" },
  ]},
  { type: "file", name: "package.json" },
  { type: "file", name: "README.md" },
];

const CODE_SAMPLES = {
  "scheduler.ts": `import { Task, Priority } from "./types";

export class Scheduler {
  private queue: Task[] = [];

  // Insert respecting priority, highest first
  enqueue(task: Task, priority: Priority = "normal") {
    const weight = priority === "high" ? 0 : 1;
    this.queue.splice(weight, 0, task);
    return this.queue.length;
  }

  async run() {
    while (this.queue.length) {
      const task = this.queue.shift();
      if (!task) continue;
      await task.execute();
    }
  }
}`,
  "cache.ts": `const store = new Map<string, { value: unknown; ttl: number }>();

export function set(key: string, value: unknown, ttlMs = 60_000) {
  store.set(key, { value, ttl: Date.now() + ttlMs });
}

export function get(key: string) {
  const entry = store.get(key);
  if (!entry) return null;
  if (Date.now() > entry.ttl) {
    store.delete(key);
    return null;
  }
  return entry.value;
}`,
  "index.ts": `export { Scheduler } from "./runtime/scheduler";
export * as cache from "./runtime/cache";

// Public entrypoint for the aurora runtime
export const version = "2.4.0";`,
  "server.ts": `import { createServer } from "node:http";

const server = createServer((req, res) => {
  res.writeHead(200, { "content-type": "text/plain" });
  res.end("aurora runtime online");
});

server.listen(3000);`,
  "edge.ts": `// Minimal edge handler example
export default {
  fetch(request: Request) {
    return new Response("hello from the edge");
  },
};`,
  "package.json": `{
  "name": "aurora-runtime",
  "version": "2.4.0",
  "license": "MIT",
  "type": "module"
}`,
  "README.md": `# aurora-runtime

A lightweight, edge-first runtime for streaming server components.

## Install

npm install aurora-runtime`,
};

function highlight(line) {
  const escaped = line
    .replace(/&/g, "&amp;")
    .replace(/</g, "&lt;")
    .replace(/>/g, "&gt;");
  const tokens = [
    { re: /(\/\/.*$)/g, cls: "text-zinc-500" },
    { re: /(".*?"|`.*?`)/g, cls: "text-teal-300" },
    { re: /\b(import|export|from|const|let|class|async|await|return|new|while|if|continue|default|function|extends|private|public)\b/g, cls: "text-violet-400" },
    { re: /\b(string|number|unknown|void|Request|Response|Task|Priority)\b/g, cls: "text-blue-300" },
    { re: /\b(\d+_?\d*)\b/g, cls: "text-amber-300" },
  ];
  let result = escaped;
  tokens.forEach(({ re, cls }) => {
    result = result.replace(re, (m) => `§${cls}§${m}§`);
  });
  const parts = result.split("§");
  const out = [];
  for (let i = 0; i < parts.length; i++) {
    if (i % 3 === 0) {
      if (parts[i]) out.push(<span key={i}>{parts[i]}</span>);
    } else if (i % 3 === 1) {
      const cls = parts[i];
      const text = parts[i + 1];
      out.push(<span key={i} className={cls}>{text}</span>);
      i++;
    }
  }
  return out;
}

function useReducedMotion() {
  const [reduced, setReduced] = useState(false);
  useEffect(() => {
    const mq = window.matchMedia("(prefers-reduced-motion: reduce)");
    setReduced(mq.matches);
    const handler = () => setReduced(mq.matches);
    mq.addEventListener?.("change", handler);
    return () => mq.removeEventListener?.("change", handler);
  }, []);
  return reduced;
}

/* ---------------------------------- UI atoms ---------------------------------- */

function Avatar({ size = 32, seed = "you" }) {
  const hue = useMemo(() => {
    let h = 0;
    for (const c of seed) h = (h * 31 + c.charCodeAt(0)) % 360;
    return h;
  }, [seed]);
  return (
    <div
      className="rounded-full flex items-center justify-center text-[11px] font-semibold text-white shrink-0 ring-1 ring-white/10"
      style={{
        width: size,
        height: size,
        background: `linear-gradient(135deg, hsl(${hue} 70% 55%), hsl(${(hue + 60) % 360} 70% 45%))`,
      }}
    >
      {seed.slice(0, 2).toUpperCase()}
    </div>
  );
}

function Badge({ children, tone = "default" }) {
  const tones = {
    default: "bg-zinc-800/80 text-zinc-300 border-zinc-700",
    violet: "bg-violet-500/10 text-violet-300 border-violet-500/30",
    teal: "bg-teal-500/10 text-teal-300 border-teal-500/30",
    amber: "bg-amber-500/10 text-amber-300 border-amber-500/30",
  };
  return (
    <span className={`inline-flex items-center gap-1 rounded-full border px-2 py-0.5 text-[11px] font-medium ${tones[tone]}`}>
      {children}
    </span>
  );
}

function Button({ children, variant = "default", size = "md", className = "", icon: Icon, ...props }) {
  const base = "relative inline-flex items-center justify-center gap-1.5 font-medium rounded-lg transition-all duration-200 ease-out active:scale-[0.97] focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-violet-400/60 focus-visible:ring-offset-2 focus-visible:ring-offset-zinc-950 disabled:opacity-50 disabled:pointer-events-none";
  const variants = {
    default: "bg-zinc-100 text-zinc-900 hover:bg-white shadow-sm shadow-black/20",
    primary: "text-white bg-gradient-to-r from-violet-600 to-violet-500 hover:from-violet-500 hover:to-violet-400 shadow-lg shadow-violet-900/40",
    ghost: "bg-transparent text-zinc-300 hover:bg-zinc-800/70 hover:text-white",
    outline: "bg-zinc-900/60 text-zinc-200 border border-zinc-700 hover:border-zinc-500 hover:bg-zinc-800/60",
  };
  const sizes = {
    sm: "text-xs px-2.5 py-1.5",
    md: "text-sm px-3.5 py-2",
    lg: "text-sm px-5 py-2.5",
  };
  return (
    <button className={`${base} ${variants[variant]} ${sizes[size]} ${className}`} {...props}>
      {Icon && <Icon size={size === "sm" ? 13 : 15} strokeWidth={2.25} />}
      {children}
    </button>
  );
}

function IconButton({ icon: Icon, className = "", active = false, ...props }) {
  return (
    <button
      className={`relative h-9 w-9 flex items-center justify-center rounded-lg text-zinc-400 hover:text-zinc-100 hover:bg-zinc-800/70 transition-all duration-200 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-violet-400/60 ${active ? "text-zinc-100 bg-zinc-800/70" : ""} ${className}`}
      {...props}
    >
      <Icon size={18} strokeWidth={2} />
    </button>
  );
}

function FadeUp({ children, delay = 0, className = "" }) {
  return (
    <div
      className={`animate-[fadeUp_0.6s_cubic-bezier(0.16,1,0.3,1)_both] ${className}`}
      style={{ animationDelay: `${delay}ms` }}
    >
      {children}
    </div>
  );
}

/* ---------------------------------- Contribution graph ---------------------------------- */

function useContributionData() {
  return useMemo(() => {
    const weeks = 26;
    const days = 7;
    const grid = [];
    let seed = 42;
    const rand = () => {
      seed = (seed * 9301 + 49297) % 233280;
      return seed / 233280;
    };
    for (let w = 0; w < weeks; w++) {
      const col = [];
      for (let d = 0; d < days; d++) {
        const r = rand();
        const level = r > 0.75 ? Math.ceil(r * 4) : r > 0.5 ? 1 : 0;
        col.push({ level: Math.min(level, 4), count: Math.round(level * r * 8) });
      }
      grid.push(col);
    }
    return grid;
  }, []);
}

function ContributionGraph() {
  const data = useContributionData();
  const [hovered, setHovered] = useState(null);
  const levelColor = [
    "bg-zinc-800/70",
    "bg-teal-900/70",
    "bg-teal-700/80",
    "bg-teal-500/90",
    "bg-teal-300",
  ];
  const total = data.flat().reduce((s, c) => s + c.count, 0);

  return (
    <div className="relative">
      <div className="flex items-baseline justify-between mb-3">
        <p className="text-sm text-zinc-400">
          <span className="text-zinc-100 font-semibold">{total}</span> contributions in the last 6 months
        </p>
        <div className="hidden sm:flex items-center gap-1 text-[11px] text-zinc-500">
          <span>Less</span>
          {levelColor.map((c, i) => (
            <span key={i} className={`h-2.5 w-2.5 rounded-[3px] ${c}`} />
          ))}
          <span>More</span>
        </div>
      </div>
      <div className="flex gap-[3px] overflow-x-auto pb-1">
        {data.map((col, wi) => (
          <div key={wi} className="flex flex-col gap-[3px]">
            {col.map((cell, di) => {
              const isHovered = hovered && hovered.w === wi && hovered.d === di;
              return (
                <div
                  key={di}
                  onMouseEnter={() => setHovered({ w: wi, d: di, ...cell })}
                  onMouseLeave={() => setHovered(null)}
                  className={`h-2.5 w-2.5 rounded-[3px] ${levelColor[cell.level]} transition-transform duration-150 ease-out cursor-pointer ${isHovered ? "scale-[1.6] ring-1 ring-teal-200/60" : ""}`}
                  style={{ animation: `popIn 0.4s cubic-bezier(0.16,1,0.3,1) both`, animationDelay: `${(wi * 7 + di) * 3}ms` }}
                />
              );
            })}
          </div>
        ))}
      </div>
      {hovered && (
        <div className="absolute -top-9 left-0 bg-zinc-800 text-zinc-100 text-xs px-2.5 py-1.5 rounded-md shadow-xl border border-zinc-700 animate-[fadeUp_0.15s_ease-out_both] pointer-events-none">
          <span className="font-semibold">{hovered.count}</span> contributions
        </div>
      )}
    </div>
  );
}

/* ---------------------------------- Repository card ---------------------------------- */

function RepositoryCard({ repo, onOpen, delay = 0 }) {
  return (
    <FadeUp delay={delay}>
      <button
        onClick={() => onOpen(repo)}
        className="group w-full text-left rounded-xl border border-zinc-800 bg-zinc-900/40 p-4 transition-all duration-300 ease-out hover:-translate-y-[3px] hover:border-violet-500/40 hover:shadow-[0_8px_30px_-10px_rgba(124,111,243,0.35)] focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-violet-400/60"
      >
        <div className="flex items-start justify-between gap-2">
          <div className="flex items-center gap-2 min-w-0">
            <BookOpen size={15} className="text-zinc-500 shrink-0" />
            <span className="font-mono text-[14px] text-violet-300 group-hover:text-violet-200 transition-colors truncate">
              {repo.name}
            </span>
          </div>
          <Badge tone={repo.visibility === "private" ? "amber" : "default"}>
            {repo.visibility === "private" ? <Lock size={10} /> : <Globe size={10} />}
            {repo.visibility}
          </Badge>
        </div>
        <p className="mt-2 text-[13px] text-zinc-400 leading-relaxed line-clamp-2">{repo.desc}</p>
        <div className="mt-4 flex items-center gap-4 text-[12px] text-zinc-500">
          <span className="flex items-center gap-1.5">
            <span className={`h-2.5 w-2.5 rounded-full ${LANG_COLORS[repo.lang] || "bg-zinc-500"}`} />
            {repo.lang}
          </span>
          <span className="flex items-center gap-1"><Star size={12} /> {repo.stars}</span>
          <span className="flex items-center gap-1"><GitFork size={12} /> {repo.forks}</span>
          <span className="hidden sm:flex items-center gap-1"><AlertCircle size={12} /> {repo.issues}</span>
          <span className="ml-auto text-zinc-600">{repo.updated}</span>
        </div>
      </button>
    </FadeUp>
  );
}

/* ---------------------------------- Command palette ---------------------------------- */

function CommandPalette({ open, onClose }) {
  const inputRef = useRef(null);
  const [query, setQuery] = useState("");
  const recent = ["aurora-runtime", "shadcn/ui", "maya-lin"];
  const results = query
    ? [...REPOS.filter((r) => r.name.includes(query.toLowerCase())), ...TRENDING.filter((t) => t.name.includes(query.toLowerCase()))]
    : [];

  useEffect(() => {
    if (open) setTimeout(() => inputRef.current?.focus(), 60);
    else setQuery("");
  }, [open]);

  useEffect(() => {
    const handler = (e) => e.key === "Escape" && onClose();
    if (open) window.addEventListener("keydown", handler);
    return () => window.removeEventListener("keydown", handler);
  }, [open, onClose]);

  if (!open) return null;

  return (
    <div className="fixed inset-0 z-[100] flex items-start justify-center pt-[12vh] px-4">
      <div
        className="absolute inset-0 bg-zinc-950/70 backdrop-blur-sm animate-[fadeIn_0.2s_ease-out_both]"
        onClick={onClose}
      />
      <div className="relative w-full max-w-xl rounded-2xl border border-zinc-800 bg-zinc-900/95 backdrop-blur-xl shadow-2xl shadow-black/60 overflow-hidden animate-[scaleIn_0.22s_cubic-bezier(0.16,1,0.3,1)_both]">
        <div className="flex items-center gap-3 px-4 border-b border-zinc-800">
          <Search size={17} className="text-zinc-500 shrink-0" />
          <input
            ref={inputRef}
            value={query}
            onChange={(e) => setQuery(e.target.value)}
            placeholder="Search repositories, people, and more…"
            className="w-full bg-transparent py-3.5 text-sm text-zinc-100 placeholder:text-zinc-500 outline-none"
          />
          <kbd className="hidden sm:inline text-[10px] text-zinc-500 border border-zinc-700 rounded px-1.5 py-0.5">ESC</kbd>
        </div>
        <div className="max-h-80 overflow-y-auto py-2">
          {!query && (
            <div className="px-4 py-1.5 text-[11px] uppercase tracking-wide text-zinc-600">Recent</div>
          )}
          {!query &&
            recent.map((r) => (
              <button key={r} className="w-full flex items-center gap-3 px-4 py-2.5 text-sm text-zinc-300 hover:bg-zinc-800/70 transition-colors">
                <Clock size={14} className="text-zinc-500" />
                <span className="font-mono">{r}</span>
              </button>
            ))}
          {query && results.length === 0 && (
            <p className="px-4 py-6 text-sm text-zinc-500 text-center">No results for “{query}”</p>
          )}
          {query &&
            results.map((r, i) => (
              <button key={i} className="w-full flex items-center gap-3 px-4 py-2.5 text-sm text-zinc-200 hover:bg-zinc-800/70 transition-colors">
                <BookOpen size={14} className="text-zinc-500" />
                <span className="font-mono">{r.name}</span>
              </button>
            ))}
        </div>
      </div>
    </div>
  );
}

/* ---------------------------------- Notifications dropdown ---------------------------------- */

function NotificationsPanel({ open, onClose }) {
  const iconFor = { pr: GitPullRequest, issue: AlertCircle, mention: MessageSquare };
  if (!open) return null;
  return (
    <div className="absolute right-0 top-11 w-[340px] max-w-[90vw] rounded-xl border border-zinc-800 bg-zinc-900/95 backdrop-blur-xl shadow-2xl shadow-black/60 overflow-hidden animate-[scaleIn_0.18s_cubic-bezier(0.16,1,0.3,1)_both] origin-top-right z-50">
      <div className="flex items-center justify-between px-4 py-3 border-b border-zinc-800">
        <span className="text-sm font-semibold text-zinc-100">Notifications</span>
        <button onClick={onClose} className="text-zinc-500 hover:text-zinc-200">
          <X size={15} />
        </button>
      </div>
      <div className="max-h-96 overflow-y-auto">
        {NOTIFICATIONS.map((n, i) => {
          const Icon = iconFor[n.type];
          return (
            <div
              key={n.id}
              className="flex gap-3 px-4 py-3 border-b border-zinc-800/60 last:border-0 hover:bg-zinc-800/50 transition-colors cursor-pointer animate-[fadeUp_0.3s_ease-out_both]"
              style={{ animationDelay: `${i * 40}ms` }}
            >
              <div className={`h-8 w-8 rounded-full flex items-center justify-center shrink-0 ${n.unread ? "bg-violet-500/15 text-violet-300" : "bg-zinc-800 text-zinc-500"}`}>
                <Icon size={14} />
              </div>
              <div className="min-w-0 fl
