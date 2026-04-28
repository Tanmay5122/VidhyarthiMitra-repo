# Project Structure

```
unnati-chatbot/
│
├── README.md                          # Main documentation
├── SETUP.md                           # Installation guide
├── CONTRIBUTING.md                    # Contribution guidelines
├── LICENSE                            # MIT License
│
├── Unnati_Chatbot.json               # Main workflow file
│                                      # (Import this into n8n)
│
├── .env.example                       # Environment variables template
├── .gitignore                         # Git ignore rules
│
├── .github/
│   └── workflows/
│       └── tests.yml                 # CI/CD automation
│
├── docs/                             # Additional documentation
│   ├── architecture.md               # System design
│   ├── api-reference.md              # API endpoints
│   ├── troubleshooting.md            # Common issues
│   └── deployment.md                 # Deployment guides
│
├── examples/                         # Usage examples
│   ├── curl-requests.md              # API call examples
│   ├── test-cases.md                 # Test scenarios
│   └── integration-samples.md        # Integration examples
│
└── CHANGELOG.md                      # Version history
```

---

## File Descriptions

### Core Files

| File | Purpose |
|------|---------|
| `Unnati_Chatbot.json` | Complete n8n workflow (IMPORT THIS) |
| `README.md` | Project overview, features, quick start |
| `SETUP.md` | Detailed installation & configuration |
| `CONTRIBUTING.md` | How to contribute to the project |
| `LICENSE` | MIT License |

### Configuration

| File | Purpose |
|------|---------|
| `.env.example` | Environment variables template |
| `.gitignore` | Files to ignore in Git |
| `.github/workflows/tests.yml` | CI/CD automation |

### Documentation

| File | Purpose |
|------|---------|
| `docs/architecture.md` | System design & flow |
| `docs/api-reference.md` | API endpoints & responses |
| `docs/troubleshooting.md` | Common issues & solutions |
| `docs/deployment.md` | Production deployment |

### Examples

| File | Purpose |
|------|---------|
| `examples/curl-requests.md` | Example API calls |
| `examples/test-cases.md` | Test scenarios |
| `examples/integration-samples.md` | Integration code |

---

## How to Use This Repository

### For Users
1. Read **README.md** for overview
2. Follow **SETUP.md** for installation
3. Check **docs/** for detailed guidance

### For Contributors
1. Read **CONTRIBUTING.md**
2. Fork repository
3. Make changes
4. Submit pull request

### For Deployment
1. Follow **SETUP.md**
2. Use **docs/deployment.md**
3. Check **examples/** for integration

---

## Adding New Files

When adding new documentation:

```
1. Create in appropriate folder (docs/ or examples/)
2. Add link in README.md
3. Update this structure file
4. Update .gitignore if needed
```

---

## File Size Limits

- Keep individual files < 100KB
- Split large docs into sections
- Link between related files

---

## Naming Conventions

- Use lowercase with hyphens: `api-reference.md`
- Be descriptive: `setup-mongodb.md` not `setup.md`
- Use `UPPERCASE.md` for root-level docs: `README.md`, `SETUP.md`
