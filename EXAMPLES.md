# Haiper Usage Examples

Real-world examples of Haiper in action across different domains.

---

## 📚 Example 1: Research & Fact-Checking

**User:** "Is it true that the Titanic wreck was found at a depth of 3,800 meters?"

**Haiper Response:**

Based on my knowledge, the Titanic wreck was found at approximately 3,843 meters (12,606 feet) depth in the North Atlantic. However, let me provide you with verification sources:

**Verification Links:**
- https://google.com/search?q=Titanic+wreck+depth+meters
- https://en.wikipedia.org/wiki/Sinking_of_the_Titanic
- https://oceanexplorer.noaa.gov/explorations/02quest/background/titanic/titanic.html

**Confidence Level:** 95% (This is well-documented historical information)

**Additional Context:**
- Discovery date: September 1, 1985
- Discovered by: Robert Ballard
- Location: South of Newfoundland

**For more learning:**
- https://youtube.com/results?search_query=Titanic+discovery+documentary
- https://github.com/search?q=Titanic+dataset

---

## 💻 Example 2: Programming & Code Review

**User:** "Create a simple REST API in Python with authentication"

**Haiper Response:**

I'll break this down into key components:

### Architecture Components:
1. **Framework** - Flask/FastAPI
2. **Authentication** - JWT tokens
3. **Database** - SQLite (for simplicity)
4. **Request validation** - Pydantic

### File Structure:
```
api/
├── main.py              # Application entry
├── auth.py              # Authentication logic
├── models.py            # Data models
├── requirements.txt     # Dependencies
└── tests/
    └── test_auth.py     # Unit tests
```

### Complete Code:

**requirements.txt:**
```
fastapi==0.104.1
uvicorn==0.24.0
pydantic==2.5.0
python-jose[cryptography]==3.3.0
passlib[bcrypt]==1.7.4
```

**main.py:**
```python
from fastapi import FastAPI, Depends, HTTPException, status
from pydantic import BaseModel
from datetime import datetime, timedelta
from typing import Optional
import jwt

app = FastAPI()

# Configuration
SECRET_KEY = "your-secret-key-change-this"
ALGORITHM = "HS256"

# Models
class User(BaseModel):
    username: str
    password: str

class Token(BaseModel):
    access_token: str
    token_type: str

# Authentication function
def create_access_token(data: dict, expires_delta: Optional[timedelta] = None):
    to_encode = data.copy()
    if expires_delta:
        expire = datetime.utcnow() + expires_delta
    else:
        expire = datetime.utcnow() + timedelta(hours=1)
    
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt

@app.post("/token", response_model=Token)
async def login(user: User):
    """
    Authenticate user and return JWT token
    """
    # In production, verify against database
    if user.username == "testuser" and user.password == "testpass":
        access_token = create_access_token(
            data={"sub": user.username},
            expires_delta=timedelta(hours=24)
        )
        return {"access_token": access_token, "token_type": "bearer"}
    
    raise HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="Invalid credentials"
    )

@app.get("/users/me")
async def get_current_user(token: str = Header(...)):
    """
    Protected endpoint - requires valid token
    """
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username = payload.get("sub")
        if username is None:
            raise HTTPException(status_code=401, detail="Invalid token")
    except jwt.InvalidTokenError:
        raise HTTPException(status_code=401, detail="Invalid token")
    
    return {"username": username}

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

### Learning Resources:
- https://fastapi.tiangolo.com/
- https://github.com/tiangolo/fastapi
- https://youtube.com/results?search_query=FastAPI+tutorial
- https://jwt.io/ (JWT explanation)

### How to Run:
```bash
pip install -r requirements.txt
python main.py
# API available at http://localhost:8000

# Test authentication:
curl -X POST "http://localhost:8000/token" \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","password":"testpass"}'
```

### Next Steps to Extend:
1. Add database (PostgreSQL)
2. Add user registration
3. Add role-based access control
4. Add rate limiting
5. Add input validation

---

## 🔬 Example 3: Theoretical Problem Analysis

**User:** "Could we terraform Mars in 50 years?"

**Haiper Response:**

## Physical & Scientific Analysis

### Requirements for Terraforming Mars:

**1. Atmospheric Change**
- Current: 95% CO₂, 0.03 kPa pressure
- Target: Earth-like (21% O₂, 101 kPa)
- Challenge: Mars lost most atmosphere due to weak magnetic field

Resources:
- https://google.com/search?q=Mars+terraforming+atmosphere
- https://nasa.gov/vision/universe/solarsystem/how-to-terraform-mars.html
- https://youtube.com/results?search_query=terraforming+Mars+explained

**2. Temperature Increase**
- Current: -63°C average
- Target: +15°C
- Method: Greenhouse gases or orbital mirrors

Resources:
- https://google.com/search?q=Mars+climate+change+terraforming
- https://arxiv.org/search/?query=Mars+terraforming+temperature

**3. Water & Oceans**
- Mars has polar ice caps (~5M km³ water estimated)
- Need to melt ice and create hydrological cycle
- Process would take centuries minimum

Resources:
- https://google.com/search?q=Mars+water+ice+location
- https://usgs.gov/faqs/does-mars-have-water

### Timeline Reality:

| Stage | Timeframe | Status |
|-------|-----------|--------|
| Phase 1: Greenhouse warming | 20-30 years | Theoretical |
| Phase 2: Atmospheric buildup | 30-50 years | Very speculative |
| Phase 3: Water cycle establishment | 100+ years | Not achievable in 50 years |
| Phase 4: Biological seeding | 200-500 years | Way too long |

### Current Technology Gap:

- ❌ No method to reliably warm entire planet
- ❌ No method to regenerate magnetic field
- ❌ Technology to build orbital mirrors doesn't exist at scale
- ❌ Would require energy equivalent to decades of global consumption

### 50-Year Realistic Goal Instead:

- ✅ Establish human colonies (possible)
- ✅ Begin greenhouse gas injection (possible)
- ✅ Mine water ice (possible)
- ✅ Create biodomes with Earth-like conditions (possible)

**Confidence:** 5% for full terraforming in 50 years | 60% for habitable colonies

**Further Reading:**
- https://www.spacex.com/starship/ (colonization vehicle)
- https://youtube.com/results?search_query=Mars+colony+timeline
- https://arxiv.org/search/?query=Mars+habitability

---

## 🎨 Example 4: Creative & Visual

**User:** "Design a futuristic city layout"

**Haiper Response:**

## Visual Reference Search
- https://google.com/search?tbm=isch&q=futuristic+city+architecture
- https://pinterest.com/search/pins/?q=cyberpunk+city
- https://artstation.com/search?sort=relevance&query=futuristic+city

## City Layout Design

### Core Components:

**1. Vertical Architecture**
- Buildings 500-1000m tall
- Multiple sky-levels with connecting bridges
- Minimizes ground footprint

**2. Transportation**
- Elevated rail systems
- Autonomous vehicles only
- No street-level traffic

**3. Green Spaces**
- Vertical gardens on buildings
- Rooftop parks
- Underground water features

**4. Energy**
- Solar panel coverage on all surfaces
- Wind turbines in sky-level
- Geothermal underground

### Layout Diagram (Text-based):

```
    ☀️  [Wind Turbines]
    |
 [═══ Sky-Level Bridge ═══]
    |      |       |
   🏢    🏢     🏢    (1000m towers)
    |      |       |
 [═══ Mid-Level Transit ═══]
    |      |       |
   🏗️    🏗️     🏗️    (500m buildings)
    |      |       |
    🚗 -- 🚗 -- 🚗  (Vehicle Layer)
    |      |       |
   🌳 -- 🌳 -- 🌳  (Ground Parks)
    |      |       |
   ⛰️ Geothermal Core
```

### Python Visualization:

```python
import matplotlib.pyplot as plt
import numpy as np

fig, ax = plt.subplots(figsize=(12, 10))

# Draw towers
tower_heights = [1000, 950, 1100, 850, 920]
tower_x = np.arange(0, 5)

for i, height in enumerate(tower_heights):
    ax.bar(i, height, width=0.8, color='steelblue', edgecolor='black', linewidth=2)
    ax.text(i, height + 50, f'{height}m', ha='center', fontsize=10, fontweight='bold')

# Draw bridges
ax.hlines(800, 0, 4, colors='green', linestyles='solid', linewidth=3, label='Sky Level')
ax.hlines(500, 0, 4, colors='orange', linestyles='solid', linewidth=3, label='Mid Level')

# Ground level
ax.hlines(0, -1, 5, colors='brown', linestyles='solid', linewidth=5, label='Ground Parks')

ax.set_ylim(-100, 1200)
ax.set_xlim(-1, 5)
ax.set_xlabel('City Districts', fontsize=12, fontweight='bold')
ax.set_ylabel('Height (meters)', fontsize=12, fontweight='bold')
ax.set_title('Futuristic City Profile', fontsize=14, fontweight='bold')
ax.legend(loc='upper right')
ax.grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig('futuristic_city.png', dpi=300, bbox_inches='tight')
plt.show()

print("City layout visualization saved!")
```

### Design Features:

✅ Vertical maximization (less sprawl)
✅ Sustainable energy systems
✅ Automated transportation
✅ Integrated nature
✅ Climate controlled environments

### Architectural Inspiration:
- https://youtube.com/results?search_query=futuristic+city+architecture
- https://behance.net/search/projects/?search=futuristic+city
- https://archdaily.com/tag/futuristic

---

## 📊 Example 5: Data Analysis

**User:** "Analyze this dataset for trends"

**Haiper Response:**

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from scipy import stats

# Load data
data = pd.read_csv('sales_data.csv')

print("=== DATA OVERVIEW ===")
print(f"Rows: {len(data)}")
print(f"Columns: {list(data.columns)}")
print(f"\nFirst rows:\n{data.head()}")

# Statistical Analysis
print("\n=== STATISTICAL SUMMARY ===")
print(data.describe())

# Trend Analysis
data['date'] = pd.to_datetime(data['date'])
monthly_sales = data.groupby(data['date'].dt.to_period('M'))['sales'].sum()

# Linear regression for trend
x = np.arange(len(monthly_sales))
slope, intercept, r_value, p_value, std_err = stats.linregress(x, monthly_sales.values)

print(f"\nTrend Analysis:")
print(f"Slope: {slope:.2f} (sales/month)")
print(f"R-squared: {r_value**2:.4f}")
print(f"P-value: {p_value:.6f}")
print(f"Interpretation: {'Significant' if p_value < 0.05 else 'Not significant'} trend")

# Visualization
fig, axes = plt.subplots(2, 2, figsize=(14, 10))

# Plot 1: Sales over time
axes[0, 0].plot(monthly_sales.index.astype(str), monthly_sales.values, marker='o')
axes[0, 0].plot(x, slope*x + intercept, 'r--', label=f'Trend (slope={slope:.2f})')
axes[0, 0].set_title('Monthly Sales Trend')
axes[0, 0].set_xlabel('Month')
axes[0, 0].set_ylabel('Sales ($)')
axes[0, 0].legend()
axes[0, 0].grid(True, alpha=0.3)

# Plot 2: Distribution
axes[0, 1].hist(data['sales'], bins=30, edgecolor='black')
axes[0, 1].set_title('Sales Distribution')
axes[0, 1].set_xlabel('Sales Value')
axes[0, 1].set_ylabel('Frequency')

# Plot 3: By category
data.groupby('category')['sales'].sum().plot(kind='bar', ax=axes[1, 0], color='skyblue')
axes[1, 0].set_title('Sales by Category')
axes[1, 0].set_ylabel('Total Sales')

# Plot 4: Correlation heatmap
if len(data.select_dtypes(include=[np.number]).columns) > 1:
    corr_matrix = data.select_dtypes(include=[np.number]).corr()
    im = axes[1, 1].imshow(corr_matrix, cmap='coolwarm', vmin=-1, vmax=1)
    axes[1, 1].set_xticks(range(len(corr_matrix.columns)))
    axes[1, 1].set_yticks(range(len(corr_matrix.columns)))
    axes[1, 1].set_xticklabels(corr_matrix.columns, rotation=45)
    axes[1, 1].set_yticklabels(corr_matrix.columns)
    axes[1, 1].set_title('Correlation Heatmap')
    plt.colorbar(im, ax=axes[1, 1])

plt.tight_layout()
plt.savefig('analysis_report.png', dpi=300, bbox_inches='tight')
plt.show()

print("\nAnalysis visualization saved to 'analysis_report.png'")
```

### Key Findings Template:
1. **Trend**: [Direction and magnitude]
2. **Significance**: [Statistical confidence]
3. **Anomalies**: [Unusual data points]
4. **Recommendations**: [Actionable insights]

### Learning Resources:
- https://pandas.pydata.org/docs/
- https://scipy.org/
- https://matplotlib.org/
- https://youtube.com/results?search_query=pandas+data+analysis+tutorial

---

## 🔐 Example 6: Security & Ethical Review

**User:** "How do I improve my web application security?"

**Haiper Response:**

### Security Assessment Framework

**Layer 1 - Quick Security Check:**
✅ Using HTTPS?
✅ Input validation implemented?
✅ SQL injection prevention?
✅ CSRF tokens in forms?
✅ Authentication mechanism?

**Layer 2 - Detailed Analysis:**

**Authentication:**
- Use industry-standard libraries (Argon2, bcrypt)
- Never store plain passwords
- Implement rate limiting on login
- Use multi-factor authentication

Resources:
- https://owasp.org/www-community/attacks/authentication_cheat_sheet
- https://passlib.readthedocs.io/

**Authorization:**
- Implement role-based access control (RBAC)
- Check permissions on every protected endpoint
- Use principle of least privilege

Resources:
- https://owasp.org/www-project-authorization-cheat-sheet/

**Data Protection:**
- Encrypt sensitive data in transit (HTTPS)
- Encrypt sensitive data at rest
- Use secure headers (CSP, X-Frame-Options, etc.)

Resources:
- https://owasp.org/www-project-secure-headers/

**Input Validation:**
- Validate all user input
- Use parameterized queries (prevent SQL injection)
- Sanitize HTML output (prevent XSS)

Resources:
- https://owasp.org/www-community/attacks/xss/

**Layer 3 - Implementation Example:**

```python
from flask import Flask, request, jsonify
from werkzeug.security import check_password_hash, generate_password_hash
import re

app = Flask(__name__)

# Input validation functions
def is_valid_email(email):
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None

def is_valid_password(password):
    if len(password) < 12:
        return False, "Password must be at least 12 characters"
    if not any(char.isupper() for char in password):
        return False, "Password must contain uppercase letter"
    if not any(char.isdigit() for char in password):
        return False, "Password must contain digit"
    return True, "Valid"

# Secure endpoint
@app.route('/register', methods=['POST'])
def register():
    data = request.get_json()
    
    # Input validation
    if not is_valid_email(data.get('email')):
        return jsonify({"error": "Invalid email"}), 400
    
    is_valid, message = is_valid_password(data.get('password'))
    if not is_valid:
        return jsonify({"error": message}), 400
    
    # Hash password (never store plain)
    hashed_password = generate_password_hash(data['password'])
    
    # Store in database with parameterized query
    # db.execute("INSERT INTO users (email, password) VALUES (?, ?)", 
    #            (data['email'], hashed_password))
    
    return jsonify({"message": "User registered successfully"}), 201
```

### Security Audit Checklist:
- [ ] HTTPS enabled
- [ ] Passwords hashed with Argon2/bcrypt
- [ ] Input validation on all endpoints
- [ ] CSRF protection
- [ ] SQL injection prevention
- [ ] XSS protection
- [ ] Security headers set
- [ ] Authentication required for sensitive operations
- [ ] Rate limiting implemented
- [ ] Error messages don't leak info

### Official Resources:
- https://owasp.org/ (Security standards)
- https://cwe.mitre.org/ (Common weaknesses)
- https://github.com/OWASP/Top10 (Top 10 vulnerabilities)

---

## ✨ More Examples Available

These are just a few examples. Haiper can help with:
- ✅ Machine learning projects
- ✅ DevOps automation
- ✅ Mobile app development
- ✅ Database design
- ✅ UI/UX design
- ✅ Content writing
- ✅ Academic research
- ✅ Business strategy

**Try Haiper with your own questions!**
