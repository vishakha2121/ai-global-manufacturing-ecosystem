
---

## 🛠️ Tech Stack

### Backend
| Tech | Purpose |
|------|---------|
| **Python 3.10+** | Core language |
| **FastAPI** | REST API framework |
| **SQLAlchemy** | ORM |
| **Pydantic** | Schema validation |
| **SQLite** | Database (no server setup) |
| **Google Gemini API** | AI reasoning |
| **Uvicorn** | ASGI server |
| **python-dotenv** | Env variable loading |

### Frontend
| Tech | Purpose |
|------|---------|
| **React 18** | UI library |
| **Vite** | Build tool |
| **Tailwind CSS** | Styling |
| **React Router** | Routing |
| **Axios** | HTTP client |
| **Recharts** | Charts |
| **React Leaflet** | Global map |
| **Lucide React** | Icons |

### Dev Tools
| Tool | Purpose |
|------|---------|
| Git | Version control |
| GitHub | Remote repo |
| VS Code | Editor |

---

## 📁 Project Structure


---

## ✨ Key Features

### 🎯 Core Features
- ✅ **Multi-Agent Coordination** — 6 AI agents working together
- ✅ **Gemini-Powered Decisions** — cloud LLM reasoning
- ✅ **Digital Twin Simulation** — virtual replica of supply network
- ✅ **Supply Network Optimization** — production + shipping + energy
- ✅ **Real-time Dashboard** — live KPIs, charts, activity feed
- ✅ **Global Factory Map** — interactive world map
- ✅ **Agent Decision Logs** — full audit trail

### 📊 Module Features

#### 🏭 Factory Module
- List all factories with location, capacity, status
- Factory detail view with production stats
- Digital Twin visualization per factory
- Assign orders to optimal factory

#### 🚚 Shipping Module
- Shipment list with status tracking
- Route optimization (shortest / cheapest)
- Real-time ETA estimation
- Shipment tracker with map view

#### ⚡ Energy Module
- Energy consumption per factory
- Cost tracking and trend charts
- Renewable vs non-renewable mix
- Peak-hour recommendations

#### 📦 Inventory Module
- Stock levels per factory per product
- Auto-reorder alerts
- Inventory turnover metrics
- Stock heatmap visualization

#### 🛒 Procurement Module
- Raw material purchase records
- Supplier management
- Purchase order tracking
- Cost optimization

#### 🤖 Agent Module
- Agent status cards (active / idle / thinking)
- Decision log viewer
- Gemini response viewer
- Manual agent trigger

---

## 🏗️ System Architecture


---

## 🤖 Agent Ecosystem

| Agent | Responsibility | Trigger |
|-------|---------------|---------|
| **Coordinator Agent** 🧠 | Orchestrates all other agents, decides priority | New order / manual |
| **Factory Agent** 🏭 | Picks best factory for production | New order |
| **Shipping Agent** 🚚 | Picks fastest / cheapest route | Order assigned |
| **Energy Agent** ⚡ | Suggests energy savings, picks cheap hours | Scheduled / threshold |
| **Inventory Agent** 📦 | Detects low stock, triggers reorder | Threshold breach |
| **Procurement Agent** 🛒 | Decides raw material purchase | Low raw material |

### Gemini Prompt Strategy

Each agent uses a **structured prompt** with:
- Current state (JSON)
- Constraints (cost, time, capacity)
- Expected output format (JSON)

Example (Factory Agent):


---

## 🛠️ Tech Stack

### Backend
| Tech | Purpose |
|------|---------|
| **Python 3.10+** | Core language |
| **FastAPI** | REST API framework |
| **SQLAlchemy** | ORM |
| **Pydantic** | Schema validation |
| **SQLite** | Database (no server setup) |
| **Google Gemini API** | AI reasoning |
| **Uvicorn** | ASGI server |
| **python-dotenv** | Env variable loading |

### Frontend
| Tech | Purpose |
|------|---------|
| **React 18** | UI library |
| **Vite** | Build tool |
| **Tailwind CSS** | Styling |
| **React Router** | Routing |
| **Axios** | HTTP client |
| **Recharts** | Charts |
| **React Leaflet** | Global map |
| **Lucide React** | Icons |

### Dev Tools
| Tool | Purpose |
|------|---------|
| Git | Version control |
| GitHub | Remote repo |
| VS Code | Editor |

---

## 📁 Project Structure

---

## 🗄️ Database Schema

### `factories`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| name | TEXT | Factory name |
| country | TEXT | |
| latitude | REAL | Map coordinate |
| longitude | REAL | Map coordinate |
| capacity | INTEGER | Units/day |
| status | TEXT | active/idle/maintenance |
| created_at | TIMESTAMP | |

### `products`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| name | TEXT | |
| sku | TEXT UNIQUE | |
| category | TEXT | |
| unit_cost | REAL | |

### `orders`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| product_id | INTEGER FK | |
| quantity | INTEGER | |
| destination | TEXT | |
| deadline | DATE | |
| status | TEXT | pending/producing/shipped/delivered |
| factory_id | INTEGER FK | |

### `shipments`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| order_id | INTEGER FK | |
| origin_factory_id | INTEGER FK | |
| destination | TEXT | |
| mode | TEXT | air/sea/road |
| cost | REAL | |
| eta_days | INTEGER | |
| status | TEXT | |

### `inventory`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| factory_id | INTEGER FK | |
| product_id | INTEGER FK | |
| quantity | INTEGER | |
| reorder_level | INTEGER | |

### `energy`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| factory_id | INTEGER FK | |
| kwh_used | REAL | |
| cost | REAL | |
| source | TEXT | grid/solar/wind |
| recorded_at | TIMESTAMP | |

### `procurement`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| material_name | TEXT | |
| quantity | REAL | |
| supplier | TEXT | |
| cost | REAL | |
| status | TEXT | ordered/received |

### `agent_logs`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| agent_name | TEXT | |
| action | TEXT | |
| input_data | TEXT | JSON |
| decision | TEXT | |
| gemini_response | TEXT | |
| created_at | TIMESTAMP | |

### `optimization_runs`
| Column | Type | Notes |
|--------|------|-------|
| id | INTEGER PK | |
| objective | TEXT | cost/time/energy |
| result_summary | TEXT | |
| improvement_pct | REAL | |
| ran_at | TIMESTAMP | |

---

## 🔌 API Endpoints

### Factory
- `GET    /api/factories` — list all
- `GET    /api/factories/{id}` — detail
- `POST   /api/factories` — create
- `PUT    /api/factories/{id}` — update
- `DELETE /api/factories/{id}` — delete

### Product
- `GET    /api/products`
- `POST   /api/products`
- `PUT    /api/products/{id}`
- `DELETE /api/products/{id}`

### Order
- `GET    /api/orders`
- `POST   /api/orders`
- `PUT    /api/orders/{id}`
- `DELETE /api/orders/{id}`
- `POST   /api/orders/{id}/assign` — trigger coordinator

### Shipment
- `GET    /api/shipments`
- `POST   /api/shipments`
- `PUT    /api/shipments/{id}`

### Inventory
- `GET    /api/inventory`
- `POST   /api/inventory`
- `GET    /api/inventory/alerts`

### Energy
- `GET    /api/energy`
- `POST   /api/energy`
- `GET    /api/energy/summary`

### Procurement
- `GET    /api/procurement`
- `POST   /api/procurement`

### Agent
- `GET    /api/agents` — list all agents + status
- `GET    /api/agents/logs` — all decision logs
- `POST   /api/agents/run/{agent_name}` — manually trigger

### Optimization
- `POST   /api/optimization/run` — run optimization
- `GET    /api/optimization/history`

### Dashboard
- `GET    /api/dashboard/kpis` — top-level KPIs
- `GET    /api/dashboard/activity` — recent agent feed
- `GET    /api/dashboard/digital-twin` — snapshot

> 📖 Full interactive docs at `http://localhost:8000/docs` (FastAPI Swagger UI)

---

## ⚙️ Installation & Setup

### Prerequisites
- Python 3.10+
- Node.js 18+
- Git
- Gemini API key ([Get one free](https://aistudio.google.com/app/apikey))

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/vishakha2121/ai-global-manufacturing-ecosystem.git
cd ai-global-manufacturing-ecosystem