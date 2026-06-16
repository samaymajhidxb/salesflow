import { useState, useEffect, useMemo } from "react";
import { BarChart, Bar, LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer, PieChart, Pie, Cell, Legend } from "recharts";

// ── Persistent Storage ────────────────────────────────────────────────────────
const STORAGE_KEY = "salesflow-inquiries";

const loadData = async () => {
  try {
    const result = await window.storage.get(STORAGE_KEY);
    return result ? JSON.parse(result.value) : [];
  } catch {
    return [];
  }
};

const saveData = async (data) => {
  try {
    await window.storage.set(STORAGE_KEY, JSON.stringify(data));
  } catch (e) {
    console.error("Storage error", e);
  }
};

// ── Constants ─────────────────────────────────────────────────────────────────
const TEAM = ["Alice Chen", "Ben Marsh", "Carla Torres", "David Kim", "Emma Ford"];
const STAGES = ["New", "Qualified", "Proposal", "Negotiation", "Closed Won", "Closed Lost"];
const PRIORITIES = ["Low", "Medium", "High"];
const STAGE_COLORS = {
  New: "#64748b", Qualified: "#3b82f6", Proposal: "#f59e0b",
  Negotiation: "#8b5cf6", "Closed Won": "#10b981", "Closed Lost": "#ef4444",
};
const PRIORITY_COLORS = { Low: "#64748b", Medium: "#f59e0b", High: "#ef4444" };
const FORECAST = [
  { month: "Jan", pipeline: 45000, closed: 28000, target: 35000 },
  { month: "Feb", pipeline: 52000, closed: 31000, target: 35000 },
  { month: "Mar", pipeline: 61000, closed: 42000, target: 40000 },
  { month: "Apr", pipeline: 58000, closed: 38000, target: 40000 },
  { month: "May", pipeline: 74000, closed: 48000, target: 45000 },
  { month: "Jun", pipeline: 82000, closed: 0, target: 50000 },
];

const SAMPLE_DATA = [
  { id: "1", company: "Vertex Corp", contact: "John Lee", value: 12000, assignee: "Alice Chen", stage: "Qualified", priority: "High", date: "2026-05-01", notes: "Interested in full package" },
  { id: "2", company: "Blue Oak Ltd", contact: "Sara Patel", value: 7500, assignee: "Ben Marsh", stage: "Proposal", priority: "Medium", date: "2026-05-05", notes: "Sent proposal v2" },
  { id: "3", company: "Neonix", contact: "Tom Hall", value: 32000, assignee: "Carla Torres", stage: "Negotiation", priority: "High", date: "2026-04-22", notes: "Final pricing discussion" },
  { id: "4", company: "PeakFlow", contact: "Mike Russo", value: 21000, assignee: "Emma Ford", stage: "Closed Won", priority: "High", date: "2026-04-15", notes: "Contract signed!" },
  { id: "5", company: "Drift Systems", contact: "Amy Wong", value: 5000, assignee: "David Kim", stage: "New", priority: "Low", date: "2026-05-10", notes: "Initial inquiry via email" },
];

const fmt = (n) => n >= 1000 ? `$${(n / 1000).toFixed(1)}k` : `$${n}`;

// ── Components ────────────────────────────────────────────────────────────────
const Badge = ({ label, color }) => (
  <span style={{ background: color + "22", color, border: `1px solid ${color}44`, padding: "2px 10px", borderRadius: 20, fontSize: 11, fontWeight: 700 }}>{label}</span>
);

const StatCard = ({ label, value, sub, color, icon }) => (
  <div style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, padding: "20px 22px", flex: 1, minWidth: 150 }}>
    <div style={{ display: "flex", justifyContent: "space-between" }}>
      <div>
        <div style={{ color: "#64748b", fontSize: 11, fontWeight: 700, letterSpacing: "0.08em", textTransform: "uppercase", marginBottom: 8 }}>{label}</div>
        <div style={{ color: "#f8fafc", fontSize: 26, fontWeight: 800 }}>{value}</div>
        {sub && <div style={{ color, fontSize: 12, marginTop: 4, fontWeight: 600 }}>{sub}</div>}
      </div>
      <div style={{ background: color + "18", borderRadius: 10, padding: 10, fontSize: 18, height: "fit-content" }}>{icon}</div>
    </div>
  </div>
);

const Modal = ({ onClose, onSave, initial }) => {
  const blank = { company: "", contact: "", value: "", assignee: TEAM[0], stage: "New", priority: "Medium", date: new Date().toISOString().split("T")[0], notes: "" };
  const [form, setForm] = useState(initial ? { ...initial, value: String(initial.value || "") } : blank);
  const set = (k, v) => setForm(f => ({ ...f, [k]: v }));
  const inp = { background: "#0f172a", border: "1px solid #334155", borderRadius: 8, color: "#f1f5f9", padding: "9px 12px", width: "100%", fontSize: 13, outline: "none", boxSizing: "border-box" };
  const lbl = { color: "#94a3b8", fontSize: 11, fontWeight: 600, letterSpacing: "0.06em", textTransform: "uppercase", marginBottom: 5, display: "block" };
  return (
    <div style={{ position: "fixed", inset: 0, background: "#00000099", zIndex: 999, display: "flex", alignItems: "center", justifyContent: "center" }}>
      <div style={{ background: "#1e293b", border: "1px solid #334155", borderRadius: 18, padding: 32, width: 480, maxWidth: "95vw" }}>
        <div style={{ color: "#f8fafc", fontSize: 18, fontWeight: 800, marginBottom: 24 }}>{initial ? "Edit Inquiry" : "New Inquiry"}</div>
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
          {[["Company", "company"], ["Contact", "contact"]].map(([l, k]) => (
            <div key={k}><label style={lbl}>{l}</label><input style={inp} value={form[k]} onChange={e => set(k, e.target.value)} /></div>
          ))}
          <div><label style={lbl}>Deal Value ($)</label><input type="number" style={inp} value={form.value} onChange={e => set("value", e.target.value)} /></div>
          <div><label style={lbl}>Date</label><input type="date" style={inp} value={form.date} onChange={e => set("date", e.target.value)} /></div>
          <div><label style={lbl}>Assignee</label>
            <select style={inp} value={form.assignee} onChange={e => set("assignee", e.target.value)}>
              {TEAM.map(t => <option key={t}>{t}</option>)}
            </select>
          </div>
          <div><label style={lbl}>Stage</label>
            <select style={inp} value={form.stage} onChange={e => set("stage", e.target.value)}>
              {STAGES.map(s => <option key={s}>{s}</option>)}
            </select>
          </div>
          <div><label style={lbl}>Priority</label>
            <select style={inp} value={form.priority} onChange={e => set("priority", e.target.value)}>
              {PRIORITIES.map(p => <option key={p}>{p}</option>)}
            </select>
          </div>
        </div>
        <div style={{ marginTop: 16 }}><label style={lbl}>Notes</label>
          <textarea style={{ ...inp, minHeight: 60, resize: "vertical" }} value={form.notes} onChange={e => set("notes", e.target.value)} />
        </div>
        <div style={{ display: "flex", gap: 10, marginTop: 24, justifyContent: "flex-end" }}>
          <button onClick={onClose} style={{ background: "#334155", color: "#94a3b8", border: "none", borderRadius: 8, padding: "9px 20px", cursor: "pointer", fontWeight: 600 }}>Cancel</button>
          <button onClick={() => onSave(form)} style={{ background: "#3b82f6", color: "#fff", border: "none", borderRadius: 8, padding: "9px 20px", cursor: "pointer", fontWeight: 700 }}>Save</button>
        </div>
      </div>
    </div>
  );
};

// ── Main App ──────────────────────────────────────────────────────────────────
export default function SalesTracker() {
  const [tab, setTab] = useState("dashboard");
  const [inquiries, setInquiries] = useState([]);
  const [loading, setLoading] = useState(true);
  const [showModal, setShowModal] = useState(false);
  const [editItem, setEditItem] = useState(null);
  const [filterStage, setFilterStage] = useState("All");
  const [filterAssignee, setFilterAssignee] = useState("All");
  const [search, setSearch] = useState("");
  const [toast, setToast] = useState(null);

  useEffect(() => {
    loadData().then(data => {
      setInquiries(data.length ? data : SAMPLE_DATA);
      setLoading(false);
    });
  }, []);

  const showToast = (msg, color = "#10b981") => {
    setToast({ msg, color });
    setTimeout(() => setToast(null), 2500);
  };

  const handleSave = async (form) => {
    const obj = { ...form, value: Number(form.value) || 0 };
    let updated;
    if (editItem) {
      updated = inquiries.map(i => i.id === editItem.id ? { ...obj, id: editItem.id } : i);
      showToast("Deal updated ✓");
    } else {
      updated = [{ ...obj, id: Date.now().toString() }, ...inquiries];
      showToast("New deal added ✓");
    }
    setInquiries(updated);
    await saveData(updated);
    setShowModal(false);
    setEditItem(null);
  };

  const handleDelete = async (id) => {
    if (!window.confirm("Delete this inquiry?")) return;
    const updated = inquiries.filter(i => i.id !== id);
    setInquiries(updated);
    await saveData(updated);
    showToast("Deleted", "#ef4444");
  };

  const filtered = useMemo(() => inquiries.filter(i =>
    (filterStage === "All" || i.stage === filterStage) &&
    (filterAssignee === "All" || i.assignee === filterAssignee) &&
    ((i.company || "").toLowerCase().includes(search.toLowerCase()) ||
      (i.contact || "").toLowerCase().includes(search.toLowerCase()))
  ), [inquiries, filterStage, filterAssignee, search]);

  const activeDeals = inquiries.filter(i => !i.stage?.startsWith("Closed"));
  const wonDeals    = inquiries.filter(i => i.stage === "Closed Won");
  const closedDeals = inquiries.filter(i => i.stage?.startsWith("Closed"));
  const pipeline    = activeDeals.reduce((s, i) => s + Number(i.value || 0), 0);
  const wonVal      = wonDeals.reduce((s, i) => s + Number(i.value || 0), 0);
  const winRate     = closedDeals.length ? Math.round(wonDeals.length / closedDeals.length * 100) : 0;
  const stageData   = STAGES.map(s => ({ name: s, value: inquiries.filter(i => i.stage === s).reduce((a, b) => a + Number(b.value || 0), 0) })).filter(x => x.value > 0);
  const teamData    = TEAM.map(t => ({ name: t.split(" ")[0], value: inquiries.filter(i => i.assignee === t).reduce((a, b) => a + Number(b.value || 0), 0) }));

  const selStyle = { background: "#0f172a", border: "1px solid #334155", borderRadius: 8, color: "#94a3b8", padding: "9px 12px", fontSize: 13, outline: "none" };
  const tabs = [
    { id: "dashboard", label: "Dashboard", icon: "▦" },
    { id: "inquiries", label: "Inquiries", icon: "◎" },
    { id: "forecast",  label: "Forecast",  icon: "↗" },
    { id: "team",      label: "Team",      icon: "◉" },
  ];

  if (loading) return (
    <div style={{ minHeight: "100vh", background: "#020817", display: "flex", alignItems: "center", justifyContent: "center", flexDirection: "column", gap: 16 }}>
      <div style={{ width: 40, height: 40, border: "3px solid #1e293b", borderTop: "3px solid #3b82f6", borderRadius: "50%", animation: "spin .8s linear infinite" }} />
      <style>{`@keyframes spin{to{transform:rotate(360deg)}}`}</style>
      <div style={{ color: "#64748b", fontSize: 14 }}>Loading SalesFlow…</div>
    </div>
  );

  return (
    <div style={{ minHeight: "100vh", background: "#020817", color: "#f1f5f9", fontFamily: "'DM Sans', sans-serif", display: "flex" }}>
      <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet" />

      {/* Toast */}
      {toast && (
        <div style={{ position: "fixed", top: 24, right: 24, zIndex: 9999, background: toast.color, color: "#fff", padding: "10px 20px", borderRadius: 10, fontWeight: 700, fontSize: 13, boxShadow: "0 4px 20px #0008" }}>
          {toast.msg}
        </div>
      )}

      {/* Sidebar */}
      <div style={{ width: 220, minHeight: "100vh", background: "#0a1628", borderRight: "1px solid #1e293b", display: "flex", flexDirection: "column", padding: "24px 0", flexShrink: 0 }}>
        <div style={{ padding: "0 24px 20px" }}>
          <div style={{ color: "#3b82f6", fontSize: 10, fontWeight: 700, letterSpacing: ".2em", textTransform: "uppercase", marginBottom: 6 }}>SalesFlow</div>
          <div style={{ color: "#f8fafc", fontSize: 22, fontWeight: 800, lineHeight: 1.2 }}>Sales<br />Tracker</div>
        </div>
        <div style={{ margin: "0 16px 20px", background: "#0d2a1a", border: "1px solid #10b98133", borderRadius: 8, padding: "7px 12px", display: "flex", alignItems: "center", gap: 8 }}>
          <div style={{ width: 8, height: 8, borderRadius: "50%", background: "#10b981", animation: "pulse 2s infinite" }} />
          <style>{`@keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}`}</style>
          <span style={{ color: "#10b981", fontSize: 11, fontWeight: 700 }}>Data Saved Locally</span>
        </div>
        <nav style={{ flex: 1 }}>
          {tabs.map(t => (
            <button key={t.id} onClick={() => setTab(t.id)} style={{ display: "flex", alignItems: "center", gap: 12, width: "100%", padding: "12px 24px", background: tab === t.id ? "#1e3a5f" : "none", color: tab === t.id ? "#60a5fa" : "#64748b", border: "none", borderLeft: tab === t.id ? "3px solid #3b82f6" : "3px solid transparent", cursor: "pointer", fontSize: 13, fontWeight: 600, textAlign: "left" }}>
              <span style={{ fontSize: 15 }}>{t.icon}</span>{t.label}
            </button>
          ))}
        </nav>
        <div style={{ padding: "20px 24px 0", borderTop: "1px solid #1e293b" }}>
          <div style={{ color: "#64748b", fontSize: 11, marginBottom: 4 }}>{inquiries.length} total records</div>
          <div style={{ color: "#f1f5f9", fontSize: 13, fontWeight: 700 }}>Management</div>
          <div style={{ color: "#3b82f6", fontSize: 11 }}>Admin View</div>
        </div>
      </div>

      {/* Main */}
      <div style={{ flex: 1, padding: "32px 36px", overflowY: "auto" }}>

        {/* DASHBOARD */}
        {tab === "dashboard" && (
          <div>
            <h1 style={{ fontSize: 26, fontWeight: 800, margin: "0 0 4px" }}>Sales Overview</h1>
            <div style={{ color: "#64748b", fontSize: 13, marginBottom: 28 }}>{inquiries.length} records · auto-saved</div>
            <div style={{ display: "flex", gap: 16, flexWrap: "wrap", marginBottom: 28 }}>
              <StatCard label="Pipeline" value={fmt(pipeline)} sub="Active deals" color="#3b82f6" icon="💰" />
              <StatCard label="Won Revenue" value={fmt(wonVal)} sub="Closed won" color="#10b981" icon="✅" />
              <StatCard label="Active Deals" value={activeDeals.length} sub="In progress" color="#f59e0b" icon="📋" />
              <StatCard label="Win Rate" value={`${winRate}%`} sub="Of closed" color="#8b5cf6" icon="🏆" />
            </div>
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20, marginBottom: 20 }}>
              <div style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, padding: 24 }}>
                <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".08em", marginBottom: 16 }}>Pipeline by Stage</div>
                {stageData.length === 0
                  ? <div style={{ color: "#475569", textAlign: "center", padding: "40px 0", fontSize: 13 }}>No deals yet</div>
                  : <ResponsiveContainer width="100%" height={190}>
                    <BarChart data={stageData} barSize={26}>
                      <CartesianGrid strokeDasharray="3 3" stroke="#1e293b" />
                      <XAxis dataKey="name" tick={{ fill: "#64748b", fontSize: 10 }} />
                      <YAxis tick={{ fill: "#64748b", fontSize: 10 }} tickFormatter={v => `$${v / 1000}k`} />
                      <Tooltip contentStyle={{ background: "#1e293b", border: "1px solid #334155", borderRadius: 8, color: "#f1f5f9" }} formatter={v => [`$${v.toLocaleString()}`, "Value"]} />
                      <Bar dataKey="value" radius={[6, 6, 0, 0]}>{stageData.map((s, i) => <Cell key={i} fill={STAGE_COLORS[s.name] || "#3b82f6"} />)}</Bar>
                    </BarChart>
                  </ResponsiveContainer>
                }
              </div>
              <div style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, padding: 24 }}>
                <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".08em", marginBottom: 16 }}>Forecast vs Target</div>
                <ResponsiveContainer width="100%" height={190}>
                  <LineChart data={FORECAST}>
                    <CartesianGrid strokeDasharray="3 3" stroke="#1e293b" />
                    <XAxis dataKey="month" tick={{ fill: "#64748b", fontSize: 11 }} />
                    <YAxis tick={{ fill: "#64748b", fontSize: 10 }} tickFormatter={v => `$${v / 1000}k`} />
                    <Tooltip contentStyle={{ background: "#1e293b", border: "1px solid #334155", borderRadius: 8, color: "#f1f5f9" }} />
                    <Legend wrapperStyle={{ fontSize: 11, color: "#94a3b8" }} />
                    <Line type="monotone" dataKey="closed" stroke="#10b981" strokeWidth={2.5} dot={{ r: 3 }} name="Closed" />
                    <Line type="monotone" dataKey="pipeline" stroke="#3b82f6" strokeWidth={2} strokeDasharray="5 3" dot={false} name="Pipeline" />
                    <Line type="monotone" dataKey="target" stroke="#f59e0b" strokeWidth={1.5} strokeDasharray="3 3" dot={false} name="Target" />
                  </LineChart>
                </ResponsiveContainer>
              </div>
            </div>
            <div style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, padding: 24 }}>
              <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".08em", marginBottom: 16 }}>Recent Deals</div>
              <table style={{ width: "100%", borderCollapse: "collapse" }}>
                <thead><tr style={{ borderBottom: "1px solid #1e293b" }}>
                  {["Company", "Assignee", "Value", "Stage", "Priority"].map(h => <th key={h} style={{ color: "#475569", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".06em", textAlign: "left", padding: "0 12px 10px 0" }}>{h}</th>)}
                </tr></thead>
                <tbody>{inquiries.slice(0, 5).map(i => (
                  <tr key={i.id} style={{ borderBottom: "1px solid #0f172a" }}>
                    <td style={{ padding: "10px 12px 10px 0" }}><div style={{ color: "#f1f5f9", fontWeight: 600, fontSize: 13 }}>{i.company}</div><div style={{ color: "#64748b", fontSize: 11 }}>{i.contact}</div></td>
                    <td style={{ color: "#94a3b8", fontSize: 13, padding: "10px 12px 10px 0" }}>{(i.assignee || "").split(" ")[0]}</td>
                    <td style={{ color: "#10b981", fontWeight: 700, fontSize: 13, padding: "10px 12px 10px 0" }}>{fmt(Number(i.value || 0))}</td>
                    <td style={{ padding: "10px 12px 10px 0" }}><Badge label={i.stage} color={STAGE_COLORS[i.stage] || "#64748b"} /></td>
                    <td><Badge label={i.priority} color={PRIORITY_COLORS[i.priority] || "#64748b"} /></td>
                  </tr>
                ))}</tbody>
              </table>
            </div>
          </div>
        )}

        {/* INQUIRIES */}
        {tab === "inquiries" && (
          <div>
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 24 }}>
              <div><h1 style={{ fontSize: 26, fontWeight: 800, margin: 0 }}>Inquiries & Deals</h1>
                <div style={{ color: "#64748b", fontSize: 13, marginTop: 4 }}>{filtered.length} records</div></div>
              <button onClick={() => { setEditItem(null); setShowModal(true); }} style={{ background: "#3b82f6", color: "#fff", border: "none", borderRadius: 10, padding: "10px 20px", cursor: "pointer", fontWeight: 700, fontSize: 13 }}>+ New Inquiry</button>
            </div>
            <div style={{ display: "flex", gap: 12, flexWrap: "wrap", marginBottom: 20 }}>
              <input placeholder="Search…" value={search} onChange={e => setSearch(e.target.value)} style={{ background: "#0f172a", border: "1px solid #334155", borderRadius: 8, color: "#f1f5f9", padding: "9px 14px", fontSize: 13, outline: "none", width: 200 }} />
              <select value={filterStage} onChange={e => setFilterStage(e.target.value)} style={selStyle}><option>All</option>{STAGES.map(x => <option key={x}>{x}</option>)}</select>
              <select value={filterAssignee} onChange={e => setFilterAssignee(e.target.value)} style={selStyle}><option>All</option>{TEAM.map(x => <option key={x}>{x}</option>)}</select>
            </div>
            <div style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, overflow: "hidden" }}>
              <table style={{ width: "100%", borderCollapse: "collapse" }}>
                <thead><tr style={{ background: "#0a1628", borderBottom: "1px solid #1e293b" }}>
                  {["Company", "Contact", "Value", "Assignee", "Stage", "Priority", "Date", "Notes", ""].map(h => <th key={h} style={{ color: "#475569", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".06em", textAlign: "left", padding: "12px 14px" }}>{h}</th>)}
                </tr></thead>
                <tbody>
                  {filtered.map((i, idx) => (
                    <tr key={i.id} style={{ borderBottom: "1px solid #1e293b", background: idx % 2 === 0 ? "#0f172a" : "#0a1628" }}>
                      <td style={{ padding: "12px 14px", color: "#f1f5f9", fontWeight: 700, fontSize: 13 }}>{i.company}</td>
                      <td style={{ padding: "12px 14px", color: "#94a3b8", fontSize: 13 }}>{i.contact}</td>
                      <td style={{ padding: "12px 14px", color: "#10b981", fontWeight: 700, fontSize: 13 }}>{fmt(Number(i.value || 0))}</td>
                      <td style={{ padding: "12px 14px", color: "#94a3b8", fontSize: 13 }}>{(i.assignee || "").split(" ")[0]}</td>
                      <td style={{ padding: "12px 14px" }}><Badge label={i.stage} color={STAGE_COLORS[i.stage] || "#64748b"} /></td>
                      <td style={{ padding: "12px 14px" }}><Badge label={i.priority} color={PRIORITY_COLORS[i.priority] || "#64748b"} /></td>
                      <td style={{ padding: "12px 14px", color: "#64748b", fontSize: 12 }}>{i.date}</td>
                      <td style={{ padding: "12px 14px", color: "#64748b", fontSize: 12, maxWidth: 140, overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap" }}>{i.notes}</td>
                      <td style={{ padding: "12px 14px", whiteSpace: "nowrap" }}>
                        <button onClick={() => { setEditItem(i); setShowModal(true); }} style={{ background: "#1e3a5f", color: "#60a5fa", border: "none", borderRadius: 6, padding: "4px 10px", cursor: "pointer", fontSize: 11, fontWeight: 700, marginRight: 6 }}>Edit</button>
                        <button onClick={() => handleDelete(i.id)} style={{ background: "#3b1a1a", color: "#f87171", border: "none", borderRadius: 6, padding: "4px 10px", cursor: "pointer", fontSize: 11, fontWeight: 700 }}>Del</button>
                      </td>
                    </tr>
                  ))}
                  {filtered.length === 0 && <tr><td colSpan={9} style={{ textAlign: "center", padding: 40, color: "#475569" }}>No records found</td></tr>}
                </tbody>
              </table>
            </div>
          </div>
        )}

        {/* FORECAST */}
        {tab === "forecast" && (
          <div>
            <h1 style={{ fontSize: 26, fontWeight: 800, margin: "0 0 4px" }}>Sales Forecast</h1>
            <div style={{ color: "#64748b", fontSize: 13, marginBottom: 28 }}>Pipeline vs closed vs target — 2026</div>
            <div style={{ display: "flex", gap: 16, flexWrap: "wrap", marginBottom: 28 }}>
              <StatCard label="May Pipeline" value="$74k" sub="Strongest month" color="#3b82f6" icon="📈" />
              <StatCard label="May Closed" value="$48k" sub="+7% vs target" color="#10b981" icon="✅" />
              <StatCard label="H1 Target" value="$245k" sub="On track" color="#f59e0b" icon="🎯" />
              <StatCard label="Forecast Acc." value="91%" sub="Last 3 months" color="#8b5cf6" icon="🔮" />
            </div>
            <div style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, padding: 28, marginBottom: 20 }}>
              <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".08em", marginBottom: 20 }}>Monthly Performance</div>
              <ResponsiveContainer width="100%" height={260}>
                <BarChart data={FORECAST} barGap={4}>
                  <CartesianGrid strokeDasharray="3 3" stroke="#1e293b" />
                  <XAxis dataKey="month" tick={{ fill: "#64748b", fontSize: 12 }} />
                  <YAxis tick={{ fill: "#64748b", fontSize: 11 }} tickFormatter={v => `$${v / 1000}k`} />
                  <Tooltip contentStyle={{ background: "#1e293b", border: "1px solid #334155", borderRadius: 8, color: "#f1f5f9" }} formatter={v => [`$${v.toLocaleString()}`]} />
                  <Legend wrapperStyle={{ fontSize: 12, color: "#94a3b8" }} />
                  <Bar dataKey="pipeline" fill="#3b82f633" stroke="#3b82f6" strokeWidth={1.5} radius={[4, 4, 0, 0]} name="Pipeline" />
                  <Bar dataKey="closed" fill="#10b981" radius={[4, 4, 0, 0]} name="Closed" />
                  <Bar dataKey="target" fill="#f59e0b44" stroke="#f59e0b" strokeWidth={1.5} radius={[4, 4, 0, 0]} name="Target" />
                </BarChart>
              </ResponsiveContainer>
            </div>
            <div style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, padding: 28 }}>
              <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".08em", marginBottom: 16 }}>Stage Distribution</div>
              <div style={{ display: "flex", alignItems: "center", gap: 32 }}>
                <ResponsiveContainer width={200} height={200}>
                  <PieChart>
                    <Pie data={stageData.length > 0 ? stageData : [{ name: "Empty", value: 1 }]} dataKey="value" cx="50%" cy="50%" outerRadius={85} innerRadius={50}>
                      {(stageData.length > 0 ? stageData : [{ name: "Empty" }]).map((x, i) => <Cell key={i} fill={STAGE_COLORS[x.name] || "#1e293b"} />)}
                    </Pie>
                    <Tooltip contentStyle={{ background: "#1e293b", border: "1px solid #334155", borderRadius: 8, color: "#f1f5f9" }} formatter={v => [`$${v.toLocaleString()}`]} />
                  </PieChart>
                </ResponsiveContainer>
                <div style={{ flex: 1 }}>
                  {stageData.length === 0 ? <div style={{ color: "#475569", fontSize: 13 }}>Add deals to see distribution</div> :
                    stageData.map(x => (
                      <div key={x.name} style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "8px 0", borderBottom: "1px solid #1e293b" }}>
                        <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                          <div style={{ width: 10, height: 10, borderRadius: 3, background: STAGE_COLORS[x.name] }} />
                          <span style={{ color: "#94a3b8", fontSize: 13 }}>{x.name}</span>
                        </div>
                        <span style={{ color: "#f1f5f9", fontWeight: 700, fontSize: 13 }}>{fmt(x.value)}</span>
                      </div>
                    ))}
                </div>
              </div>
            </div>
          </div>
        )}

        {/* TEAM */}
        {tab === "team" && (
          <div>
            <h1 style={{ fontSize: 26, fontWeight: 800, margin: "0 0 4px" }}>Team Performance</h1>
            <div style={{ color: "#64748b", fontSize: 13, marginBottom: 28 }}>Individual breakdowns for management</div>
            <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill,minmax(260px,1fr))", gap: 16, marginBottom: 28 }}>
              {TEAM.map(member => {
                const deals = inquiries.filter(i => i.assignee === member);
                const w = deals.filter(i => i.stage === "Closed Won");
                const act = deals.filter(i => !i.stage?.startsWith("Closed"));
                const cl = deals.filter(i => i.stage?.startsWith("Closed"));
                const rate = cl.length ? Math.round(w.length / cl.length * 100) : 0;
                return (
                  <div key={member} style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, padding: 22 }}>
                    <div style={{ display: "flex", alignItems: "center", gap: 14, marginBottom: 14 }}>
                      <div style={{ width: 42, height: 42, borderRadius: 12, background: "#1e3a5f", display: "flex", alignItems: "center", justifyContent: "center", color: "#60a5fa", fontWeight: 800, fontSize: 16 }}>{member[0]}</div>
                      <div><div style={{ color: "#f1f5f9", fontWeight: 700, fontSize: 14 }}>{member}</div>
                        <div style={{ color: "#64748b", fontSize: 11 }}>Sales Rep · {deals.length} deals</div></div>
                    </div>
                    <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10 }}>
                      {[["Active", act.length, "#3b82f6"], ["Win Rate", `${rate}%`, "#10b981"],
                        ["Pipeline", fmt(act.reduce((s, i) => s + Number(i.value || 0), 0)), "#f59e0b"],
                        ["Won", fmt(w.reduce((s, i) => s + Number(i.value || 0), 0)), "#8b5cf6"]].map(([l, v, c]) => (
                          <div key={l} style={{ background: "#0a1628", borderRadius: 8, padding: "10px 12px" }}>
                            <div style={{ color: "#475569", fontSize: 10, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".06em" }}>{l}</div>
                            <div style={{ color: c, fontSize: 18, fontWeight: 800, marginTop: 4 }}>{v}</div>
                          </div>
                        ))}
                    </div>
                  </div>
                );
              })}
            </div>
            <div style={{ background: "#0f172a", border: "1px solid #1e293b", borderRadius: 14, padding: 24 }}>
              <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".08em", marginBottom: 16 }}>Team Pipeline Comparison</div>
              <ResponsiveContainer width="100%" height={220}>
                <BarChart data={teamData} barSize={32}>
                  <CartesianGrid strokeDasharray="3 3" stroke="#1e293b" />
                  <XAxis dataKey="name" tick={{ fill: "#64748b", fontSize: 12 }} />
                  <YAxis tick={{ fill: "#64748b", fontSize: 11 }} tickFormatter={v => `$${v / 1000}k`} />
                  <Tooltip contentStyle={{ background: "#1e293b", border: "1px solid #334155", borderRadius: 8, color: "#f1f5f9" }} formatter={v => [`$${v.toLocaleString()}`, "Value"]} />
                  <Bar dataKey="value" fill="#3b82f6" radius={[6, 6, 0, 0]} />
                </BarChart>
              </ResponsiveContainer>
            </div>
          </div>
        )}
      </div>

      {showModal && <Modal onClose={() => { setShowModal(false); setEditItem(null); }} onSave={handleSave} initial={editItem} />}
    </div>
  );
}
