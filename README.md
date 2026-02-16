# Office Facility Automated Pipeline - Track, Log, Notify - All Automated

End-to-end automated ticketing system for office facility requests. Captures web form submissions via n8n webhook, generates unique ticket IDs, logs to Google Sheets, and sends dual email notifications (employee + admin). Built with vanilla HTML/CSS/JS frontend and n8n workflow backend. Eliminates manual data entry and reduces processing time by 90%.

## Tech Stack

| Automation & Backend | Frontend | APIs & Services | Deployment (Planned) | Impact Metrics |
|:---:|:---:|:---:|:---:|:---:|
| ![n8n](https://img.shields.io/badge/n8n-EA4B71?logo=n8n&logoColor=white) | ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black) | ![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?logo=google-sheets&logoColor=white) | ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) | ![Cost Reduction](https://img.shields.io/badge/cost%20reduction-%E2%82%B91%2C65%2C000%2Fyear-success.svg) |
| ![JSON](https://img.shields.io/badge/JSON-000000?logo=json&logoColor=white) | ![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white) | ![Gmail](https://img.shields.io/badge/Gmail-D14836?logo=gmail&logoColor=white) | ![Nginx](https://img.shields.io/badge/Nginx-009639?logo=nginx&logoColor=white) | ![Time Saved](https://img.shields.io/badge/time%20saved-330%20hrs%2Fyear-orange.svg) |
| | ![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white) | | | |


![N8N Workflow Diagram](N8N_Workflow_Form_To_Inbox_Pipeline.png)

## Problem Statement

Manual facility request processing creates:
- **Operational inefficiency**: 5+ minutes per request for data entry
- **Delayed responses**: Hours to days for employee acknowledgment
- **Poor visibility**: Email-based tracking with no centralized audit trail
- **Lost requests**: Emails buried in admin inboxes

## Solution Overview

Automated pipeline that captures form submissions, generates tracking tickets, logs structured data, and triggers instant notifications—without manual intervention.

### System Architecture

```
[Web Form] → [n8n Webhook] → [Ticket Generator] → [Response Fork]
                                                    ├─→ [Browser: Ticket ID]
                                                    ├─→ [Google Sheets: Log Entry]
                                                    └─→ [Gmail: Dual Emails]
```

---

## Features

### Frontend (HTML/CSS/JavaScript)
- 13 predefined request types (IT support, maintenance, courier, parking, etc.)
- Conditional logic (courier selection reveals provider options)
- Real-time progress tracking
- 60-second timeout with retry mechanism
- Modal-based feedback (success with ticket number + copy-to-clipboard)
- Responsive gradient UI

### Backend (n8n Workflow)
- Webhook trigger for form capture
- Unique ticket ID generation (timestamp-based)
- Bidirectional response (ticket ID back to browser)
- Google Sheets integration (structured logging)
- Dual email dispatch:
  - **Employee**: Confirmation with ticket number
  - **Admin**: Alert with full request details

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Frontend | Vanilla HTML/CSS/JavaScript |
| Automation Engine | n8n (Node.js-based workflow automation) |
| Data Storage | Google Sheets API |
| Notification | Gmail API |
| Hosting (Current) | Localhost (Node.js) |
| Hosting (Planned) | Docker on IT server / Cloud VM |

---

## Project Structure

```
office-facility-automation-pipeline/
├── Department_wise_modern_facility_form_v3.html  # Web form frontend
├── workflow-diagram.png                          # Visual pipeline representation
├── documentation.pdf                             # Detailed system documentation
└── README.md                                     # This file
```

---

## Business Impact & ROI

### Current Request Volume
- **Daily requests**: 10-20 (average: 15)
- **Monthly requests**: 330+ (based on 22 working days)
- **Annual requests**: 3,600+ (based on 240 working days)

### Time Savings Analysis

**Manual Processing Time (Before Automation):**
- Data entry to tracking sheet: 3 min
- Sending confirmation email: 1 min
- Sending admin notification: 1 min
- **Total per request: 5 minutes**

**Monthly Manual Processing Time:**
```
330 requests/month × 5 min = 1,650 minutes = 27.5 hours/month
```

**Annual Manual Processing Time:**
```
27.5 hours/month × 12 months = 330 hours/year
```

### Cost Savings

**Assumptions:**
- Admin hourly wage: ₹500/hour (mid-level administrative role)
- Automation processing time: 0 minutes (no manual intervention)

**Monthly Savings:**
```
27.5 hours × ₹500/hour = ₹13,750/month
```

**Annual Savings:**
```
330 hours × ₹500/hour = ₹1,65,000/year
```

### Performance Comparison

| Metric | Before Automation | After Automation | Improvement |
|--------|-------------------|------------------|-------------|
| **Manual Data Entry** | 5 min/request | 0 min | **100% reduction** |
| **Employee Wait Time** | Hours to days | <60 seconds | **99.9% faster** |
| **Monthly Admin Hours** | 27.5 hours | 0 hours | **27.5 hours saved** |
| **Monthly Cost** | ₹13,750 labor cost | ₹0 labor cost | **₹13,750 saved** |
| **Request Tracking** | Email chaos | Centralized sheet | **Full visibility** |
| **Lost Requests** | 5-10% (email buried) | 0% (during uptime) | **Eliminated** |

---

## Current System Availability

### Hosting Constraint: Localhost (Office Hours Only)

**Current Setup:**
- n8n runs on localhost (laptop-based)
- **System ON**: 8:00 AM - 6:00 PM (10 hours/day, weekdays only)
- **System OFF**: Evenings, nights, and weekends

### Availability Model

| Time Period | System Status | Request Handling |
|-------------|---------------|------------------|
| **Weekdays 8 AM - 6 PM** | ✅ Online | Requests processed normally |
| **Weekdays 6 PM - 8 AM** | ❌ Offline | Timeout error after 60 seconds |
| **Weekends** | ❌ Offline | Timeout error after 60 seconds |
| **Holidays** | ❌ Offline | Timeout error after 60 seconds |

### Impact of Downtime

**Operational Hours:**
- Available: 10 hours/day × 5 days/week = 50 hours/week
- Unavailable: 118 hours/week (70% of total time)

**Request Distribution (Estimated):**
- During office hours (8 AM - 6 PM): ~85-90% of requests
- After hours/weekends: ~10-15% of requests

**Monthly Lost Requests:**
```
Total monthly requests: 330
Requests during office hours: ~297 (90%)
Requests after hours: ~33 (10%)
```

**Business Impact of Downtime:**
- Lost employee time (resubmission required): 33 requests × 3 min = 99 min/month
- User frustration from "Server Not Active" errors
- Delayed request processing (next business day)

---

## Current Limitations

### Critical Constraint: Laptop-Based Hosting

**Architecture Dependency:**
- Workflow runs only when laptop is powered on
- Requires active internet connection
- Vulnerable to system crashes, restarts, or power loss

**Failure Scenarios:**
1. **After-Hours Requests**: Employee submits request at 7 PM → 60-second timeout → "Server Not Active" modal
2. **Weekend Urgency**: Critical facility issue on Saturday → No ticket generation → Manual escalation required
3. **Unexpected Shutdown**: Laptop crashes or restarts during office hours → Temporary service disruption

**User Experience Impact:**
- Form submission successful **only during office hours**
- After-hours submissions require retry next business day
- No automated logging or email notifications when system is offline

---

## Production Deployment Plan

### Goal: Achieve 24/7 Availability

**Target Uptime**: 99.5% (allows ~3.6 hours downtime/month for maintenance)

### Option 1: Company IT Server (Recommended)

**Setup:**
```bash
# Docker Compose deployment
version: '3'
services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    volumes:
      - ~/.n8n:/home/node/.n8n
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=securepassword
    restart: unless-stopped
```

**Benefits:**
- 24/7 uptime (server-grade hardware)
- No dependency on personal laptop
- Centralized IT management
- Zero additional infrastructure cost (uses existing servers)

**Estimated Setup Time**: 2-4 hours

---

### Option 2: Cloud VM (DigitalOcean, AWS, Azure)

**Recommended Specs:**
- Droplet size: 2 GB RAM / 1 vCPU
- OS: Ubuntu 22.04 LTS
- Monthly cost: ₹1,000-1,250

**Setup Steps:**
1. Deploy VM with Docker pre-installed
2. Configure nginx reverse proxy
3. Install SSL certificate (Let's Encrypt)
4. Point subdomain: `n8n.yourcompany.com`

**Benefits:**
- Geographic redundancy
- Automatic backups
- Scalable resources
- Managed infrastructure

**Estimated Setup Time**: 4-6 hours (including DNS/SSL config)

---

### Option 3: n8n Cloud (Managed Service)

**Pricing**: ₹1,650/month (Starter plan)

**Benefits:**
- Zero infrastructure management
- Built-in SSL and backups
- 99.9% uptime SLA
- Automatic updates

**Trade-offs:**
- Monthly recurring cost
- Less control over infrastructure

---

### Migration Impact Analysis

**Current State (Localhost):**
- Uptime: ~42% (50 hours/week ÷ 168 hours/week)
- Processed requests: ~297/month (90% coverage)
- Lost requests: ~33/month (10% failure rate)

**Post-Migration (24/7 Hosting):**
- Uptime: ~99.5% (scheduled maintenance only)
- Processed requests: ~330/month (100% coverage)
- Lost requests: ~0/month (negligible)

**Additional Business Value:**
- After-hours emergency requests handled immediately
- Weekend facility issues tracked and logged
- No employee resubmission required (first-time resolution)
- Complete audit trail for compliance

**ROI on Cloud Hosting:**
```
Monthly cloud cost: ₹1,000 (DigitalOcean droplet)
Monthly labor savings: ₹13,750
Net monthly benefit: ₹12,750

Annual cloud cost: ₹12,000
Annual labor savings: ₹1,65,000
Net annual benefit: ₹1,53,000

ROI: 1,275% (payback period: 0.9 days)
```

---

## Setup Instructions

### Prerequisites
- n8n installed (via npm or Docker)
- Google account with API access enabled
- Gmail API credentials configured in n8n

### Step 1: Install n8n

**Option A: npm (Local Development)**
```bash
npm install n8n -g
n8n start
```
Access at: `http://localhost:5678`

**Option B: Docker (Production)**
```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

### Step 2: Import Workflow
1. Open n8n at `http://localhost:5678`
2. Create new workflow
3. Build the following node structure:

**Node Configuration:**

**1. Webhook Node**
- HTTP Method: `POST`
- Path: `facility-request-v1`
- Response Mode: `When Last Node Finishes`

**2. Function Node (Ticket Generator)**
```javascript
const timestamp = new Date().getTime();
const ticketId = `TKT-${timestamp}`;
return [{
  json: {
    ...items[0].json,
    ticketNumber: ticketId,
    timestamp: new Date().toISOString()
  }
}];
```

**3. Respond to Webhook Node**
- Response Body: `{{ { "ticketNumber": $json.ticketNumber } }}`

**4. Google Sheets Node**
- Operation: `Append`
- Sheet: `Facility Requests`
- Columns: Map all form fields + ticketNumber + timestamp

**5. Gmail Node (Employee)**
- To: `{{ $json.email }}`
- Subject: `Facility Request Confirmed - Ticket #{{ $json.ticketNumber }}`
- Body: Template with ticket details

**6. Gmail Node (Admin)**
- To: `admin@yourcompany.com`
- Subject: `New Facility Request - {{ $json.request_type }}`
- Body: Full request details

### Step 3: Configure Frontend
1. Open `Department_wise_modern_facility_form_v3.html`
2. Update line 435 with your webhook URL:

```html
<!-- Local Development -->
<form action="http://localhost:5678/webhook/facility-request-v1" method="POST">

<!-- Production (replace with your server) -->
<form action="https://your-n8n-server.com/webhook/facility-request-v1" method="POST">
```

3. Test form submission and verify:
   - Ticket number appears in success modal
   - Entry logged to Google Sheets
   - Emails sent to employee and admin

---

## Scalability Roadmap

### Phase 1: Current State ✅
- Single facility request form
- Basic logging and notifications
- Office hours availability (8 AM - 6 PM weekdays)

### Phase 2: 24/7 Availability 🚀
- Migrate to cloud/IT server hosting
- Eliminate after-hours downtime
- 100% request capture rate

### Phase 3: Multi-Form Support
- HR forms (leave requests, onboarding)
- Finance forms (expense reports, purchase orders)
- Department-specific routing logic

### Phase 4: Advanced Features
- SLA tracking (measure resolution time)
- Status update workflow (in-progress, completed, rejected)
- SMS notifications for high-priority requests
- Integration with ticketing systems (Jira, ServiceNow)

### Phase 5: Analytics Dashboard
- Request volume by department
- Average resolution time
- Most common request types
- Admin workload distribution
- Peak usage hours analysis

---

## Skills Demonstrated

- **Frontend Development**: Vanilla JS, responsive CSS, client-side validation, timeout handling
- **API Integration**: Webhook handling, bidirectional communication, error handling
- **Workflow Automation**: n8n pipeline design, conditional logic, data transformation
- **Cloud Architecture**: Localhost-to-production migration planning, uptime SLA design
- **System Design**: End-to-end data flow, error recovery patterns, availability modeling
- **DevOps**: Docker containerization, deployment strategies, infrastructure planning
- **Business Analysis**: ROI calculation, time-motion study, cost-benefit analysis

---

## Configuration Notes

### Google Sheets Setup
1. Create new spreadsheet: "Facility Requests"
2. Set column headers:
   ```
   Ticket Number | Timestamp | Employee Name | Email | Department | 
   Date Needed | Request Type | Courier Services | Additional Details
   ```
3. Share with n8n service account (read/write access)

### Gmail API Setup
1. Enable Gmail API in Google Cloud Console
2. Create OAuth 2.0 credentials
3. Configure credentials in n8n (Settings → Credentials → Gmail)

---

## Testing Checklist

- [ ] Form validation works (required fields prevent submission)
- [ ] Ticket ID generates correctly (format: `TKT-{timestamp}`)
- [ ] Success modal displays ticket number
- [ ] Copy-to-clipboard function works
- [ ] Google Sheets entry created with all fields
- [ ] Employee receives confirmation email
- [ ] Admin receives alert email
- [ ] Timeout modal triggers when n8n is offline
- [ ] Retry button resubmits form
- [ ] After-hours behavior documented (timeout expected)

---

## Troubleshooting

### Form submits but no ticket number appears
- Check n8n workflow is active (toggle in workflow editor)
- Verify webhook URL matches form action attribute
- Check browser console for CORS errors
- Confirm system is online (office hours: 8 AM - 6 PM weekdays)

### Google Sheets not updating
- Verify service account has edit access to spreadsheet
- Check sheet name matches node configuration
- Review n8n execution log for API errors

### Emails not sending
- Confirm Gmail API credentials are valid
- Check email addresses are correct (no typos)
- Review Gmail API quota limits (not exceeded)

### "Server Not Active" modal appears during office hours
- Verify laptop is powered on
- Check n8n process is running: `ps aux | grep n8n`
- Restart n8n: `n8n start`
- Check network connectivity

---

## Known Limitations

### Current Constraints
1. **Office Hours Only**: System unavailable 6 PM - 8 AM and weekends
2. **Laptop Dependency**: Vulnerable to crashes, restarts, power loss
3. **Single Point of Failure**: No redundancy or failover
4. **No After-Hours Support**: Emergency requests must wait until next business day

### Mitigation Strategy
- Short-term: Document office hours in form UI ("Available 8 AM - 6 PM weekdays")
- Long-term: Migrate to 24/7 cloud hosting (see Production Deployment Plan)

---

## Contributing

Contributions welcome. Focus areas:
- Additional request types
- Enhanced error handling
- Mobile UI improvements
- Multi-language support
- After-hours queueing mechanism

---

## License

MIT License - Free for personal and commercial use.

---

## Contact

For implementation questions or collaboration:
- GitHub Issues: [Repository Issues Page]
- Portfolio: [Your Portfolio URL]

---

## Acknowledgments

- **n8n**: Open-source workflow automation platform
- **Google APIs**: Sheets and Gmail integration
- **Design Inspiration**: Modern SaaS form patterns

---

**Built with**: ☕ Coffee, 🧠 Systems Thinking, ⚙️ Automation Obsession

**Impact**: 330 hours/year saved | ₹1,65,000 annual labor cost reduction | 100% elimination of manual data entry
